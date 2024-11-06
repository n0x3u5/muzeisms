<script lang="ts">
  import { onMount } from "svelte";

  import Reveal from "reveal.js";
  import Highlight from "reveal.js/plugin/highlight/highlight";
  import Markdown from "reveal.js/plugin/markdown/markdown";
  import Notes from "reveal.js/plugin/notes/notes";

  import "reveal.js/dist/reveal.css";
  import "reveal.js/dist/theme/dracula.css";
  // import "reveal.js/dist/theme/white.css";
  import "../highlight/night-owl.css";

  import Presentation from "./presentation.svelte";

  import superstoreData from "../data/superstore/data.json" with { type: "json" };
  import superstoreSchema from "../data/superstore/schema.json" with { type: "json" };

  import aaplData from "../data/aapl/data.json" with { type: "json" };
  import aaplSchema from "../data/aapl/schema.json" with { type: "json" };

  import splomData from "../data/splom/data.json" with { type: "json" };
  import splomSchema from "../data/splom/schema.json" with { type: "json" };

  type Muze = typeof import("@viz/muze").default;

  let {
    muze,
  }: {
    muze: Muze;
  } = $props();

  const DataModel = $derived(muze.DataModel);
  const loadedSuperstoreData = $derived(DataModel.loadDataSync(superstoreData, superstoreSchema));
  const superstoreDM = $derived(new DataModel(loadedSuperstoreData));

  const loadedAaplData = $derived(DataModel.loadDataSync(aaplData, aaplSchema));
  const aaplDM = $derived(new DataModel(loadedAaplData));

  const loadedSplomData = $derived(DataModel.loadDataSync(splomData, splomSchema));
  const splomDM = $derived(new DataModel(loadedSplomData));

  const env = $derived(muze());

  let viz: HTMLDivElement | null = $state(null);

  let canvas: Muze["Canvas"] = $state(null);

  let deck: Reveal.Api | null = $state(null);
  let isDeckInitialized = $state(false);

  const useCanvas = (slide, canvas) => {
    const datasetName = slide.__attributes["data-dataset"];
    const columns = slide.__attributes["data-muze-columns"];
    const rows = slide.__attributes["data-muze-rows"];
    const isShared = slide.__attributes["data-is-shared"];
    const layers = slide.__attributes["data-muze-layers"] ?? [
      { mark: "bar", encoding: { color: { value: () => "#FFCE57" } } },
    ];
    const color = slide.__attributes["data-muze-color"];
    const config = slide.__attributes["data-muze-config"];
    const showColumnFacetHeader = slide.__attributes["data-show-column-facet-header"];

    canvas
      .data(
        datasetName === "aapl"
          ? aaplDM
              .select({
                operator: "and",
                conditions: [
                  { field: "Date", operator: "gte", value: +new Date(2017, 4, 30) },
                  { field: "Date", operator: "lte", value: +new Date(2017, 5, 30) },
                ],
              })
              .calculateVariable(
                { name: "Direction", type: "dimension" },
                ["Open", "Close"],
                (open: number, close: number) => (open > close ? "up" : "down"),
              )
          : datasetName === "splom"
            ? splomDM
            : superstoreDM.calculateVariable(
                { name: "Target Sales", type: "measure" },
                ["Sales"],
                (sales: number) => sales * 2,
              ),
      )
      .layers(layers)
      .columns(columns)
      .rows(isShared ? [muze.Operators.share(...rows)] : rows)
      .color(color)
      .config(
        config == null
          ? {
              theme: {
                name: "custom",
                className: "custom-theme",
                font: {
                  fontSize: "18px",
                  components: {
                    axis: {
                      name: {
                        fontSize: "20px",
                      },
                    },
                    facets: {
                      fontSize: "20px",
                    },
                  },
                },
              },
              columns: {
                headers: {
                  show: showColumnFacetHeader,
                },
                fields: {
                  "Ship Mode": {
                    headers: {
                      show: showColumnFacetHeader,
                    },
                  },
                },
              },
              axes: {
                x: {
                  showAxisName: !showColumnFacetHeader,
                },
                y:
                  datasetName === "aapl"
                    ? { name: "Price", transition: { disabled: true } }
                    : { transition: { disabled: true } },
              },
              legend: {
                show: false,
                color: {
                  range:
                    datasetName === "aapl"
                      ? ["#ff7b7b", "#73fc96"]
                      : ["#FFCE57", "#37A3EB", "#FE1A67", "#4CC0C0", "#8042FF"],
                },
              },
            }
          : config,
      );
  };

  $effect(() => {
    if (deck == null || !isDeckInitialized) return;

    const hasMuze = deck.getCurrentSlide().__attributes["data-has-muze"];

    if (hasMuze && (canvas == null || canvas._disposed)) {
      canvas = env.canvas();
    }
  });

  $effect(() => {
    if (deck == null || !isDeckInitialized || canvas == null || canvas._disposed) return;

    useCanvas(deck.getCurrentSlide(), canvas);
  });

  $effect(() => {
    if (deck == null || !isDeckInitialized || canvas == null || canvas._disposed) return;

    const hasMuze = deck.getCurrentSlide().__attributes["data-has-muze"];

    const muzeWidth = deck.getCurrentSlide().__attributes["data-muze-width"];

    if (muzeWidth != null) {
      canvas.width(muzeWidth);
      if (viz != null) viz.style.transform = `translateX(${-muzeWidth / 6}px)`;
    }

    if (hasMuze && canvas.mount() == null) {
      canvas.mount(viz);

      // canvas.on("afterRendered", () => {
      //   [...document.querySelectorAll(".muze-axis-grid-lines-y path")].forEach(
      //     (el) => (el.style.opacity = 0.3),
      //   );
      // });
    }
  });

  onMount(async () => {
    deck = new Reveal({
      hash: true,
      plugins: [Markdown, Highlight, Notes],
    });

    await deck.initialize({ disableLayout: true });

    isDeckInitialized = true;

    deck.on("slidechanged", (e) => {
      const currentSlide = e.currentSlide;

      const hasMuze = currentSlide.__attributes["data-has-muze"];
      const isRerendered = currentSlide.__attributes["data-is-rerendered"];

      if (isRerendered) {
        canvas.dispose();
      }

      if (hasMuze) {
        if (canvas == null || canvas._disposed) {
          canvas = env.canvas();
        }

        const muzeWidth = currentSlide.__attributes["data-muze-width"];

        if (muzeWidth != null) {
          canvas.width(muzeWidth);
          if (viz != null) viz.style.transform = `translateX(${-muzeWidth / 6}px)`;
        }

        useCanvas(currentSlide, canvas);
        if (canvas.mount() == null) {
          canvas.mount(viz);

          // canvas.on("afterRendered", () => {
          //   [...document.querySelectorAll(".muze-axis-grid-lines-y path")].forEach(
          //     (el) => (el.style.opacity = 0.3),
          //   );
          // });
        }
      } else {
        if (canvas != null) canvas.dispose();
      }
    });
  });
</script>

<div class="reveal">
  <div class="slides">
    <Presentation />
  </div>
</div>
<div class="absolute left-1/4 top-4 h-[55%] w-1/2" bind:this={viz}></div>

<style lang="postcss">
  :global(.muze-axis-name) {
    fill: #ffffff !important;
  }

  :global(.muze-columnHeader-cell) {
    font-size: 20px !important;
    color: #ffffff !important;
  }

  :global(.muze-axis-grid-lines-y) {
    opacity: 0.6 !important;
  }

  :global(.muze-grid-td-geom) {
    border-color: rgba(214, 214, 214, 0.4) !important;
  }

  :global(.muze-grid-td-axis) {
    border-color: rgba(214, 214, 214, 0.6) !important;
  }

  :global(.muze-grid-td-facet) {
    border-color: rgba(214, 214, 214, 0.6) !important;
  }

  :global(.muze-axis-container-left .muze-ticks:nth-child(2) .muze-tick-lines) {
    opacity: 0 !important;
  }
</style>
