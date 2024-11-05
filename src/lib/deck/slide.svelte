<script lang="ts">
  export let id: string | null = null;
  export let animate = false;
  export let restart = false;
  export let isRerendered = false;
  export let dataset: "aapl" | "superstore" | "splom" = "superstore";
  export let hasMuze: boolean = false;
  export let muzeColumns: Array<string> = [];
  export let muzeRows: Array<string> = [];
  export let muzeLayers: Array<{ mark: "bar" | "line" | "point" | "tick" }> | null = null;
  export let muzeColor: string | null = null;
  export let isShared: boolean = false;
  export let backgroundImage: string | null = null;
  export let muzeConfig: Record<string, unknown> | null = null;
</script>

<section
  class="!pointer-events-none size-full"
  data-dataset={dataset}
  data-is-rerendered={isRerendered}
  data-has-muze={hasMuze}
  data-is-shared={isShared}
  data-muze-columns={muzeColumns}
  data-muze-rows={muzeRows}
  data-muze-layers={muzeLayers}
  data-muze-color={muzeColor}
  data-muze-config={muzeConfig}
  data-auto-animate-id={id}
  data-auto-animate={animate || null}
  data-auto-animate-restart={restart || null}
  data-background-image={backgroundImage || null}
  data-background-opacity={backgroundImage ? "0.15" : "0"}
>
  <slot />
</section>
