<script lang="ts">
	import { Slides } from '$lib';
</script>

<svelte:head>
	<title>Presentation</title>
</svelte:head>

{#await import('@viz/muze') then { default: muze }}
	<Slides {muze} />
{/await}
