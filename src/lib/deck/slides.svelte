<script lang="ts">
  import { onMount } from "svelte";

  import Reveal from "reveal.js";
  import Highlight from "reveal.js/plugin/highlight/highlight";
  import Markdown from "reveal.js/plugin/markdown/markdown";
  import Notes from "reveal.js/plugin/notes/notes";

  import "reveal.js/dist/reveal.css";
  import "reveal.js/dist/theme/dracula.css";
  // import 'reveal.js/dist/theme/white.css';
  import "../highlight/night-owl.css";

  import Presentation from "./presentation.svelte";

  import data from "../data/superstore/data.json" with { type: "json" };
  import schema from "../data/superstore/schema.json" with { type: "json" };

  type Muze = typeof import("@viz/muze").default;

  let {
    muze,
  }: {
    muze: Muze;
  } = $props();

  const DataModel = $derived(muze.DataModel);
  const loadedData = $derived(DataModel.loadDataSync(data, schema));
  const dm = $derived(new DataModel(loadedData));

  const env = $derived(muze());

  let viz: HTMLDivElement | null = $state(null);

  let canvas: Muze["Canvas"] = $state(null);

  let deck: Reveal.Api | null = $state(null);
  let isDeckInitialized = $state(false);

  const useCanvas = (slide, canvas) => {
    const columns = slide.__attributes["data-muze-columns"];
    const rows = slide.__attributes["data-muze-rows"];
    const isShared = slide.__attributes["data-is-shared"];
    const layers = slide.__attributes["data-muze-layers"] ?? [
      { mark: "bar", encoding: { color: { value: () => "#FFFFB3" } } },
    ];
    const color = slide.__attributes["data-muze-color"];

    canvas
      .data(dm)
      .layers(layers)
      .columns(columns)
      .rows(isShared ? [muze.Operators.share(...rows)] : rows)
      .color(color)
      .config({
        legend: {
          show: false,
          color: {
            range: [
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
      });
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
