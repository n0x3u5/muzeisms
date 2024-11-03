<script lang="ts">
  export let id: string | null = null;
  export let animate = false;
  export let restart = false;
  export let grammar: any = null;
  export let hasMuze: boolean = false;
  export let muzeColumns: Array<string> = [];
  export let muzeRows: Array<string> = [];
  export let muzeLayers: Array<{ mark: "bar" | "line" }> = null;
  export let muzeColor: string | null = null;
  export let isShared: boolean = false;
  export let backgroundImage: string | null = null;
</script>

<section
  data-has-muze={hasMuze}
  data-is-shared={isShared}
  data-muze-columns={muzeColumns}
  data-muze-rows={muzeRows}
  data-muze-layers={muzeLayers}
  data-muze-color={muzeColor}
  data-grammar={grammar || null}
  data-auto-animate-id={id}
  data-auto-animate={animate || null}
  data-auto-animate-restart={restart || null}
  data-background-image={backgroundImage || null}
  data-background-opacity={backgroundImage ? "0.3" : "0"}
>
  <slot />
</section>
