<script lang="ts">
	import Slide from './slide.svelte';
	import Code from './code.svelte';
	import Markdown from './markdown.svelte';
	import Notes from './notes.svelte';
</script>

<Slide backgroundImage="bg.webp">
	<p class="text-6xl">🚧 MUZE (W.I.P. 🔥) 🚧</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Muze in a nutshell</p>
	<hr />
	<p class="fragment text-3xl">Built on JavaScript and WASM</p>
	<p class="fragment text-3xl">Focused on speed</p>
	<p class="fragment text-3xl">Simple, expressive API</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Simple, expressive API</p>
	<p class="fragment text-3xl">How?</p>
</Slide>

<Slide animate>
	<p class="text-6xl">How?</p>
	<div class="fragment">
		<div>By following a grammar</div>
		<div class="flex justify-center">
			<img
				class="w-[342px]"
				alt="A High School English Grammar book by Wren and Martin"
				src="wren-and-martin.jpg"
			/>
		</div>
	</div>
</Slide>

<Slide animate>
	<div class="flex justify-center">
		<img
			class="w-[342px]"
			alt="A High School English Grammar book by Wren and Martin"
			src="wren-and-martin.jpg"
		/>
	</div>
	<p data-id="which-grammar">Well, not exactly that one</p>
</Slide>

<Slide animate>
	<p data-id="which-grammar">This one!</p>
</Slide>

<Slide animate>
	<p data-id="which-grammar">A Grammar of Graphics</p>
	<div class="flex justify-center">
		<img
			class="w-[342px]"
			alt="The cover of a book called A Grammar of Graphics by Leland Wilkinson"
			src="gog.jpg"
		/>
	</div>
</Slide>

<Slide animate>
	<p>A grammar</p>
	<p>gives us primitives</p>
	<p>to build more complex</p>
	<p>things</p>
</Slide>

<Slide animate>
	<p class="text-blue-400">The Grammar of Graphics</p>
	<p>gives us primitives</p>
	<p>to build more complex</p>
	<p>things</p>
</Slide>

<Slide animate>
	<p class="text-blue-400">The Grammar of Graphics</p>
	<p>gives us primitives</p>
	<p>to build more complex</p>
	<p class="fragment strike text-blue-400">graphics</p>
</Slide>

<Slide animate>
	<p class="text-blue-400">The Grammar of Graphics</p>
	<p>gives us primitives</p>
	<p>to build more complex</p>
	<p class="text-blue-200 line-through">graphics</p>
	<p class="fragment text-blue-400">visualizations</p>
</Slide>

<Slide animate>
	<p>A grammar</p>
	gives us
	<span class="fragment highlight-current-blue">primitives</span>
	<p>to build more complex</p>
	<p>things</p>
</Slide>

<Slide animate>
	<p class="text-6xl text-blue-400">primitives</p>
	<p class="fragment text-3xl">Letters</p>
	<p class="fragment text-3xl">Parts of Speech</p>
	<p data-id="words" class="fragment text-3xl">Words</p>
	<p class="fragment text-3xl">and more...</p>
</Slide>

<Slide animate>
	<p class="text-6xl text-blue-400">primitives</p>
	<p class="text-3xl">Data</p>
	<p class="text-3xl">Parts of Speech</p>
	<p data-id="words" class="text-3xl">Words</p>
	<p class="text-3xl">and more...</p>
</Slide>

<Slide animate>
	<p class="text-6xl text-blue-400">primitives</p>
	<p class="text-3xl">Data</p>
	<p class="text-3xl">Marks</p>
	<p class="text-3xl">Words</p>
	<p class="text-3xl">and more...</p>
</Slide>

<Slide animate>
	<p class="text-6xl text-blue-400">primitives</p>
	<p class="text-3xl">Data</p>
	<p class="text-3xl">Marks</p>
	<p class="text-3xl">Encodings</p>
	<p class="text-3xl">and more...</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Data</p>
	<hr data-id="divider" />
	<p class="fragment text-3xl">Ordinal</p>
	<p class="fragment text-3xl">Nominal</p>
	<p class="fragment text-3xl">Temporal</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Data</p>
	<hr data-id="divider" />
	<p class="text-3xl">Ordinal</p>
	<p class="text-3xl">Nominal</p>
	<p class="text-3xl">Temporal</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Data</p>
	<hr data-id="divider" />
	<p class="text-3xl">Attributes</p>
	<p class="text-3xl">Nominal</p>
	<p class="text-3xl">Temporal</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Data</p>
	<hr data-id="divider" />
	<p class="text-3xl">Attributes</p>
	<p class="text-3xl">Measures</p>
	<p class="text-3xl">Temporal</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Data</p>
	<hr data-id="divider" />
	<p class="text-3xl">Attributes</p>
	<p class="text-3xl">Measures</p>
	<p class="text-3xl">Dates</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Marks</p>
	<hr data-id="divider" />
	<p class="fragment text-3xl">Bars</p>
	<p class="fragment text-3xl">Points</p>
	<p class="fragment text-3xl">Areas</p>
	<p class="fragment text-3xl">and more...</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Encodings</p>
	<hr data-id="divider" />
	<p class="fragment text-3xl">Details</p>
	<p class="fragment text-3xl">Axes</p>
	<p class="fragment text-3xl">Colors</p>
	<p class="fragment text-3xl">and more...</p>
</Slide>

<Slide animate>
	<p class="text-6xl">Let's put all this together now</p>
</Slide>

<Slide hasMuze>
	<p class="capitalize">Bar Mark</p>
</Slide>

<Slide hasMuze muzeColumns={['a']}>
	<p class="capitalize">Add X</p>
</Slide>

<Slide hasMuze muzeColumns={['a']} muzeRows={['b']}>
	<p class="capitalize">Add Y</p>
</Slide>

<Slide hasMuze muzeColumns={['a']} muzeRows={['b']} muzeColor={'a'}>
	<p class="capitalize">Add Color</p>
</Slide>

<Slide>
	<p class="capitalize">Code Blocks</p>
</Slide>

<Slide animate>
	<Code id="code" lines="1|3">
		{`
			<Slide animate>
				<!-- .. -->
			</Slide>
		`}
	</Code>
</Slide>

<Slide animate>
	<Code id="code" lines="2|4">
		{`
			<Slide animate>
				<Code lines>
					<!-- ... -->
				</Code>
			</Slide>
		`}
	</Code>
</Slide>

<Slide animate>
	<Code id="code" lines="3-5|1-7">
		{`
			<Slide animate>
				<Code lines>
					{code\`
						...
					\`}
				</Code>
			</Slide>
		`}
	</Code>
</Slide>

<Slide id="boxes" animate>
	<p class="capitalize">Cool transitions</p>
	<div class="flex place-content-center gap-2">
		<div data-id="box-1" class="h-[100px] w-[100px] bg-gray-400"></div>
		<div data-id="box-2" class="h-[100px] w-[100px] bg-gray-400"></div>
		<div data-id="box-3" class="h-[100px] w-[100px] bg-gray-400"></div>
	</div>
</Slide>

<Slide id="boxes" animate>
	<p class="capitalize">Moving boxes</p>
	<div class="flex place-content-center gap-2">
		<div data-id="box-1" class="h-[200px] w-[200px] bg-red-400"></div>
		<div data-id="box-2" class="h-[200px] w-[200px] bg-green-400"></div>
		<div data-id="box-3" class="h-[200px] w-[200px] bg-blue-400"></div>
	</div>
	<p class="capitalize">Cool transitions</p>
</Slide>

<Slide id="boxes" animate>
	<p>Moving boxes</p>
	<div class="flex place-content-center gap-2">
		<div data-id="box-1" class="h-[200px] w-[200px] bg-gray-400"></div>
		<img src="https://i.giphy.com/media/ToMjGpnXBTw7vnokxhu/giphy.webp" alt="Whoa" />
		<div data-id="box-3" class="h-[200px] w-[200px] bg-gray-400"></div>
	</div>
	<p>Whoa!</p>
</Slide>

<!-- <Markdown>
	{`
		## Markdown ❤️
		You can use **HTML** or **Markdown** for slides.
	`}
</Markdown>

<Markdown name="example.md" external />

<Slide>
	<p class="capitalize">Get started 😎</p>
</Slide> -->
