<script lang="ts">
  import type { Snippet } from "svelte";

  let {
    children,
    classStr = "",
    id,
    lines = true,
    lineOffset = 1,
    noescape = true,
  }: {
    children?: Snippet;
    classStr?: string;
    id?: string;
    lines?: string | boolean;
    lineOffset?: number;
    noescape?: boolean;
  } = $props();
</script>

<pre class={classStr} data-id={id || null}>
  <code
    data-trim
    data-line-numbers={lines}
    data-ln-start-from={`${lineOffset}`}
    data-noescape={noescape}>
    {@render children?.()}
  </code>
</pre>
