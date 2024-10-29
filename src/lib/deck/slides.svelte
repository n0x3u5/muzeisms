<script lang="ts">
	import { onMount } from 'svelte';

	import Reveal from 'reveal.js';
	import Highlight from 'reveal.js/plugin/highlight/highlight';
	import Markdown from 'reveal.js/plugin/markdown/markdown';
	import Notes from 'reveal.js/plugin/notes/notes';

	import 'reveal.js/dist/reveal.css';
	import 'reveal.js/dist/theme/dracula.css';
	// import 'reveal.js/dist/theme/white.css';
	import 'reveal.js/plugin/highlight/monokai.css';

	import Presentation from './presentation.svelte';

	type Muze = typeof import('@viz/muze').default;

	let {
		muze
	}: {
		muze: Muze;
	} = $props();

	const DataModel = $derived(muze.DataModel);
	const loadedData = $derived(
		DataModel.loadDataSync(
			[
				{ a: 'A', b: 28, c: 14 },
				{ a: 'B', b: 55, c: 11 },
				{ a: 'C', b: 43, c: 19 },
				{ a: 'D', b: 91, c: 27 },
				{ a: 'E', b: 81, c: 17 },
				{ a: 'F', b: 53, c: 15 },
				{ a: 'G', b: 19, c: 20 },
				{ a: 'H', b: 87, c: 22 },
				{ a: 'I', b: 52, c: 25 }
			],
			[
				{ name: 'a', type: 'dimension' },
				{ name: 'b', type: 'measure' },
				{ name: 'c', type: 'measure' }
			]
		)
	);
	const dm = $derived(new DataModel(loadedData));

	const env = $derived(muze());

	let viz: HTMLDivElement | null = $state(null);

	let canvas: Muze['Canvas'] = $state(null);

	onMount(() => {
		Reveal.initialize({
			plugins: [Markdown, Highlight, Notes]
		}).then(() => {
			const onSlideChanged = (event: Event) => {
				const hasMuze = event.currentSlide.__attributes['data-has-muze'];
				if (!hasMuze) {
					if (canvas != null) canvas.dispose();
					return;
				}

				const columns = event.currentSlide.__attributes['data-muze-columns'];
				const rows = event.currentSlide.__attributes['data-muze-rows'];
				const color = event.currentSlide.__attributes['data-muze-color'];

				if (canvas == null || canvas._disposed) {
					canvas = env.canvas();
				}

				canvas
					.data(dm)
					.layers({ mark: 'bar' })
					.columns(columns)
					.rows(rows)
					.color(color)
					.config({
						legend: {
							color: {
								range: [
									'#8DD3C7',
									'#FFFFB3',
									'#BEBADA',
									'#FB8072',
									'#80B1D3',
									'#FDB462',
									'#B3DE69',
									'#FCCDE5',
									'#D9D9D9',
									'#BC80BD',
									'#CCEBC5',
									'#FFED6F'
								]
							}
						}
					});

				if (canvas.mount() == null) {
					canvas.mount(viz);
				}
			};
			Reveal.on('slidechanged', onSlideChanged);
		});
	});
</script>

<div class="reveal">
	<div class="slides">
		<Presentation />
	</div>
</div>
<div class="absolute left-0 top-0 size-96" bind:this={viz}></div>
