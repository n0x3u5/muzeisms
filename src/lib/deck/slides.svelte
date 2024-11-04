<script lang="ts">
  import { onMount } from "svelte";

  import Reveal from "reveal.js";
  import Highlight from "reveal.js/plugin/highlight/highlight";
  import Markdown from "reveal.js/plugin/markdown/markdown";
  import Notes from "reveal.js/plugin/notes/notes";

  import "reveal.js/dist/reveal.css";
  // import "reveal.js/dist/theme/dracula.css";
  import "reveal.js/dist/theme/white.css";
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
      { mark: "bar", encoding: { color: { value: () => "#FFFFB3" } } },
    ];
    const color = slide.__attributes["data-muze-color"];
    const config = slide.__attributes["data-muze-config"];

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
            : superstoreDM,
      )
      .layers(layers)
      .columns(columns)
      .rows(isShared ? [muze.Operators.share(...rows)] : rows)
      .color(color)
      .config(
        config == null
          ? {
              axes: {
                y: datasetName === "aapl" ? { name: "Price" } : {},
              },
              legend: {
                show: false,
                color: {
                  range:
                    datasetName === "aapl"
                      ? ["#ff7b7b", "#73fc96"]
                      : [
                          "#8DD3C7",
                          "#FFFFB3",
                          "#BEBADA",
                          "#FB8072",
                          "#80B1D3",
                          "#FDB462",
                          "#B3DE69",
                          "#FCCDE5",
                          "#D9D9D9",
                          "#BC80BD",
                          "#CCEBC5",
                          "#FFED6F",
                        ],
                },
              },
              tooltip: {
                fields: ["Open", "High", "Low", "Close"],
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

    if (hasMuze && canvas.mount() == null) {
      canvas.mount(viz);
    }
  });

  onMount(async () => {
    deck = new Reveal({
      hash: true,
      plugins: [Markdown, Highlight, Notes],
    });

    await deck.initialize();

    isDeckInitialized = true;

    deck.on("slidechanged", (e) => {
      const currentSlide = e.currentSlide;

      const hasMuze = currentSlide.__attributes["data-has-muze"];

      if (hasMuze) {
        if (canvas == null || canvas._disposed) {
          canvas = env.canvas();
        }
        useCanvas(currentSlide, canvas);
        if (canvas.mount() == null) {
          canvas.mount(viz);
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
<div class="absolute left-0 top-0 size-96" bind:this={viz}></div>
