<script lang="ts">
  import type { Snippet } from "svelte";

  import Slide from "./slide.svelte";
  import Code from "./code.svelte";
  import Markdown from "./markdown.svelte";
  import Notes from "./notes.svelte";
  import superstoreData from "../data/superstore/data.json" with { type: "json" };
  import superstoreSchema from "../data/superstore/schema.json" with { type: "json" };
  import aaplData from "../data/aapl/data.json" with { type: "json" };
  import aaplSchema from "../data/aapl/schema.json" with { type: "json" };

  // Seeded random number generator
  function mulberry32(seed: number) {
    return function () {
      let t = (seed += 0x6d2b79f5);
      t = Math.imul(t ^ (t >>> 15), t | 1);
      t ^= t + Math.imul(t ^ (t >>> 7), t | 61);
      return ((t ^ (t >>> 14)) >>> 0) / 4294967296;
    };
  }

  // Function to get ordered random sample with seed
  function getSeededSample(
    array: typeof superstoreData | typeof aaplData,
    sampleSize: number,
    seed: number = 42,
  ) {
    const random = mulberry32(seed);

    // Create array of indices with random values
    const indices = array.map((_, index) => ({
      index,
      value: random(),
    }));

    // Sort by random value and take top n indices
    const selectedIndices = indices
      .sort((a, b) => a.value - b.value)
      .slice(0, sampleSize)
      .map((item) => item.index)
      .sort((a, b) => a - b); // Sort indices to maintain original order

    // Return items at selected indices
    return selectedIndices.map((index) => array[index]);
  }

  const sampledSuperstoreData = getSeededSample(superstoreData, 20, 0);
  const projectedSuperstoreSchema = superstoreSchema
    .filter(
      ({ name }) =>
        name === "Category" ||
        name === "Ship Mode" ||
        name === "Region" ||
        name === "Order Priority" ||
        name === "Sales" ||
        name === "Quantity",
    )
    .toSorted((a, b) => a.type.localeCompare(b.type));

  const sampledAaplData = getSeededSample(aaplData, 20, 0);
  const projectedAaplSchema = aaplSchema
    .filter(
      ({ name }) =>
        name === "Date" || name === "Open" || name === "High" || name === "Low" || name === "Close",
    )
    .toSorted((a, b) => a.type.localeCompare(b.type));
</script>

<Slide backgroundImage="bg.webp">
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <h1 class="!prose !prose-invert !text-9xl">Muze</h1>
    <h2 class="!prose !prose-invert !text-5xl">Concepts and Philosophies</h2>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <h1 class="!text-6xl">Muze in a nutshell</h1>
    <hr />
    <p class="fragment">Focused on speed</p>
    <p data-id="expressive" class="fragment">
      <span data-id="expressive-span">Simple, declarative and expressive API</span>
    </p>
    <p class="fragment">
      Built for the web
      <span class="fragment block">on JavaScript and WebAssembly</span>
    </p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p data-id="expressive">
      <span data-id="expressive-span" class="text-6xl">Simple, declarative and expressive API</span>
    </p>
    <p class="fragment"><span data-id="how">How?</span></p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span data-id="how" class="text-6xl">How?</span></p>
    <p class="fragment">By following a grammar</p>
  </div>
</Slide>

<Slide>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>A Grammar of Graphics</p>
    <img alt="The cover of a book called A Grammar of Graphics by Leland Wilkinson" src="gog.jpg" />
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>A <span data-id="grammar">Grammar</span></p>
    <p>gives us primitives</p>
    <p>to build more complex</p>
    <p>things</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p class="text-blue-400">The <span data-id="grammar">Grammar</span> of Graphics</p>
    <p>gives us primitives</p>
    <p>to build more complex</p>
    <p>things</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p class="text-blue-400">The Grammar of Graphics</p>
    <p data-id="primitives">gives us <span data-id="primitivess-span">primitives</span></p>
    <p>to build more complex</p>
    <p class="text-blue-400">visualizations</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p data-id="primitives">
      <span data-id="primitivess-span" class="text-bue-500 text-6xl">primitives</span>
    </p>
    <hr data-id="divider" />
    <p><span>Data</span></p>
    <p>Marks</p>
    <p>Encodings etc.</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-6xl">Data</span></p>
    <hr data-id="divider" />
    <p class="fragment">Ordinal</p>
    <p class="fragment">Nominal</p>
    <p class="fragment">Temporal</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-6xl">Data</span></p>
    <hr data-id="divider" />
    <p>Ordinal</p>
    <p>Nominal</p>
    <p>Temporal</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-6xl">Data</span></p>
    <hr data-id="divider" />
    <p>Attributes</p>
    <p>Nominal</p>
    <p>Temporal</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-6xl">Data</span></p>
    <hr data-id="divider" />
    <p>Attributes</p>
    <p>Measures</p>
    <p>Temporal</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-6xl">Data</span></p>
    <hr data-id="divider" />
    <p>Attributes</p>
    <p>Measures</p>
    <p>Dates</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <h1 class="!prose !prose-invert !font-sans !text-6xl">Marks</h1>
    <hr data-id="divider" />
    <p class="fragment">Bars</p>
    <p class="fragment">Points</p>
    <p class="fragment">Areas</p>
    <p class="fragment">Lines</p>
    <p class="fragment">Arcs</p>
    <p class="fragment">Ticks etc.</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <h1 class="!prose !prose-invert !font-sans !text-6xl">Encodings</h1>
    <hr data-id="divider" />
    <p class="fragment">Axes</p>
    <p class="fragment">Colors</p>
    <p class="fragment">Texts</p>
    <p class="fragment">Details</p>
    <p class="fragment">Shapes</p>
    <p class="fragment">Sizes</p>
    <p class="fragment">and more...</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <h1 class="!prose !prose-invert !text-6xl">Marks dictate the behaviour of encodings</h1>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Alright that's enough theory</p>
    <p class="fragment">Let's start building stuff.</p>
  </div>
</Slide>

<Slide>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p class="fragment">
      <span class="text-4xl">
        Using
        <span class="px-2 text-6xl text-blue-500">Muze</span>, of course.
      </span>
    </p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-4xl">Let's first take a look at a sample of our data.</span></p>
    <table data-id="data-table" class="!m-4 text-base">
      <thead>
        <tr>
          {#each projectedSuperstoreSchema as { name, type, subtype }}
            <th
              class={type === "measure" || (type === "dimension" && subtype === "temporal")
                ? "!text-right"
                : "!text-left"}
            >
              {name}
            </th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each sampledSuperstoreData as row}
          <tr>
            {#each projectedSuperstoreSchema as { name, type, subtype }}
              <td
                class={type === "measure" || (type === "dimension" && subtype === "temporal")
                  ? "!text-right"
                  : "!text-left"}
              >
                {row[name as keyof typeof row]}
              </td>
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p><span class="text-4xl">Let's first take a look at a sample of our data.</span></p>
    <table data-id="data-table" class="!m-4 text-base">
      <thead>
        <tr>
          {#each projectedSuperstoreSchema as { name, type, subtype }}
            <th
              class={type === "measure" || (type === "dimension" && subtype === "temporal")
                ? "bg-emerald-700 !text-right"
                : "bg-sky-600 !text-left"}
            >
              {name}
            </th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each sampledSuperstoreData as row}
          <tr>
            {#each projectedSuperstoreSchema as { name, type, subtype }}
              <td
                class={type === "measure" || (type === "dimension" && subtype === "temporal")
                  ? "!text-right"
                  : "!text-left"}
              >
                {row[name as keyof typeof row]}
              </td>
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>
      Let's start with an empty <span class="px-1 text-4xl text-blue-500">Muze</span> canvas
    </p>
    <Code classStr="fragment" id="code">
      {`muze.canvas()`}
    </Code>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>And attach our data to it.</p>
    <Code classStr="fragment" lines="2" id="code">
      {`muze.canvas()
        .data(sampleData)
      `}
    </Code>
    <p class="fragment">Not much to see here yet. I know.</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Now, we tell Muze what to plot along columns.</p>
    <Code classStr="fragment" id="code" lines="3">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Now, we tell Muze what to plot along columns.</p>
    <Code classStr="fragment" id="code" lines="3">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Note that Muze did a few things for us.</p>
    <Code id="code" lines="3">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>First, it automatically inferred an appropriate mark.</p>
    <Code id="code" lines="3">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Second, it automatically assigned the default X-axis encoding.</p>
    <Code id="code" lines="3">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>A more explicit way of specifying the same thing is as follows.</p>
    <Code id="code" lines="4-7">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .layers([{
        mark: 'bar',
        encoding: { x: 'Ship Mode' }
      }])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>But for now, let's stick with the terse version.</p>
    <Code id="code" lines="3">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Next, let's specify the rows.</p>
    <Code id="code" lines="4">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Next, let's specify the rows.</p>
    <Code id="code" lines="4">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Here, Muze auto-infers the Y encoding for the bars.</p>
    <Code id="code" lines="4">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>And there we have it! Just 2 lines to get a sensible bar chart.</p>
    <Code id="code" lines="3-4">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Muze provides sensible defaults.</p>
    <Code classStr="opacity-0" id="code" lines="3-4">
      {`muze.canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Now... let's not overlook this line here.</p>
    <Code id="code" lines="2">
      {`muze.canvas()
      .data(sampleData)
      // ...
    `}
    </Code>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p class="text-2xl">
      <code class="text-xl">sampleData</code> isn't just a simple list of rows.
    </p>
    <Code id="code" lines="2">
      {`muze.canvas()
    .data(sampleData)
    // ...
  `}
    </Code>
  </div></Slide
>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <div class="fragment w-full">
      <h1 class="!text-6xl">DataModel</h1>
      <hr data-id="divider" />
    </div>
    <p class="text-2xl">
      It's actually a <span class="italic">super fast</span>,
      <span class="font-bold">in-memory</span> relational algebra engine.
    </p>
    <Code id="code" lines="2">
      {`muze.canvas()
    .data(sampleData)
    // ...
  `}
    </Code>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <div class="w-full">
      <h1 class="!text-6xl">DataModel</h1>
      <hr data-id="divider" />
    </div>
    <p>Powers all data operations performed by Muze.</p>
    <p class="fragment">Allows Muze to deal with raw, un-aggregated data.</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <div class="w-full">
      <h1 class="!text-6xl">DataModel</h1>
      <hr data-id="divider" />
    </div>
    <ul class="!mt-4 text-2xl">
      <li class="fragment">Relational algebra (SELECT, WHERE, GROUP BY, HAVING etc)</li>
      <li class="fragment">
        <p><span class="text-2xl">Fast 🏎️</span></p>
        <ul>
          <li>Powered by Rust and WebAssembly</li>
          <li>Zero-copy data access</li>
        </ul>
      </li>
      <li class="fragment mt-4">Works in the browser</li>
      <li class="fragment mt-4">Lightweight</li>
    </ul>
  </div>
</Slide>

<Slide>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Alright, tangent over!</p>
    <p class="fragment">Back to Muze.</p>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Here's where we'd left off.</p>
    <Code id="code">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>What if we wanted to see another measure now?</p>
    <Code id="code">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Chuck it in rows. See what happens.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales', 'Quantity'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales", "Quantity"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>That happens.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales', 'Quantity'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales", "Quantity"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>No. Give dual axis.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales', 'Quantity'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales", "Quantity"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Fine... but now we'll need to start being explicit.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales', 'Quantity'])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales", "Quantity"]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Fine... but now we'll need to start being explicit.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Ship Mode'])
      .rows([['Sales'], ['Quantity']])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={[["Sales"], ["Quantity"]]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Fine... but now we'll need to start being explicit.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Ship Mode'])
      .rows([['Sales'], ['Quantity']])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={[["Sales"], ["Quantity"]]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>And now we'll need to disambiguate.</p>
    <Code id="code" lines="4">
      {`//...
      .rows([['Sales'], ['Quantity']])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Quantity' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={[["Sales"], ["Quantity"]]}>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>And now we'll need to disambiguate.</p>
    <Code id="code" lines="5">
      {`//...
      .rows([['Sales'], ['Quantity']])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Quantity' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={[["Sales"], ["Quantity"]]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    {
      mark: "line",
      encoding: { y: "Quantity", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Done!</p>
    <Code id="code" lines="2-6">
      {`//...
      .rows([['Sales'], ['Quantity']])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Quantity' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={[["Sales"], ["Target Sales"]]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    {
      mark: "line",
      encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>But... what about now?</p>
    <Code id="code" lines="2-6">
      {`//...
      .rows([['Sales'], ['Target Sales']])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={[["Sales"], ["Target Sales"]]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    {
      mark: "line",
      encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>We need multiple measures on the same axis.</p>
    <Code id="code" lines="2-6">
      {`//...
      .rows([['Sales'], ['Target Sales']])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={[["Sales"], ["Target Sales"]]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    {
      mark: "line",
      encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>All we need to do is use Muze's <code>share</code> operator</p>
    <Code id="code" lines="2">
      {`//...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    {
      mark: "line",
      encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>All we need to do is use Muze's <code>share</code> operator</p>
    <Code id="code" lines="2">
      {`//...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    {
      mark: "line",
      encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>An accurate representation... but...</p>
    <Code id="code" lines="2">
      {`//...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  muzeLayers={[
    {
      mark: "line",
      encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" }, size: { value: () => 0 } },
    },
    {
      mark: "bar",
      encoding: { y: "Sales", color: { value: () => "#FFFFB3" } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Could we show this same information in another way?</p>
    <Code id="code" lines="2">
      {`//...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: {
        y: "Target Sales",
        color: { value: () => "#8DD3C7" },
        opacity: { value: () => 0.5 },
        size: { value: () => 1 },
      },
    },
    {
      mark: "bar",
      encoding: { y: "Sales", color: { value: () => "#FFFFB3" }, size: { value: () => 0.9 } },
    },
  ]}
  muzeConfig={{
    legend: {
      show: false,
      size: {
        range: [0, 150],
      },
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
  }}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Of course!</p>
    <Code id="code" lines="4-5">
      {`//...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales', size: 0.9 } },
        { mark: 'bar', encoding: { y: 'Target Sales', opacity: 0.5 } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  isRerendered
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "Target Sales",
        color: { value: () => "#FFFFFF" },
        size: { value: () => 0.01 },
      },
      transition: { disabled: true },
    },
    {
      mark: "bar",
      encoding: { y: "Sales", color: { value: () => "#FFFFB3" }, size: { value: () => 0.5 } },
    },
  ]}
  muzeConfig={{
    legend: {
      show: false,
      size: {
        range: [0, 150],
      },
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
  }}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Or maybe one prefers a more minimal aesthetic?</p>
    <Code id="code" lines="4-5">
      {`//...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales', size: 0.5 } },
        { mark: 'tick', encoding: { y: 'Target Sales' } }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "Target Sales",
        color: { value: () => "#FFFFFF" },
        size: { value: () => 0.01 },
      },
      transition: { disabled: true },
    },
    {
      mark: "bar",
      encoding: { y: "Sales", color: { value: () => "#FFFFB3" }, size: { value: () => 0.5 } },
    },
  ]}
  muzeConfig={{
    legend: {
      show: false,
      size: {
        range: [0, 150],
      },
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
  }}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>We call this technique composition.</p>
    <p class="fragment">And we'll dive a bit deeper into it a little later.</p>
    <Code classStr="opacity-0" id="code" lines="4-5">
      {`//...`}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y: "Sales", color: { value: () => "#FFFFB3" } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Right now though, let's see how we'd stack bars.</p>
    <Code id="code">
      {`//...
      .layers([
        {
          mark: 'bar',
          encoding: {
            y: 'Sales'
          }
        }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y: "Sales", color: { value: () => "#FFFFB3" } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Right now though, let's see how we'd stack bars.</p>
    <Code id="code" lines="7">
      {`//...
      .layers([
        {
          mark: 'bar',
          encoding: {
            y: 'Sales'
            color: 'Region'
          }
        }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y: "Sales", color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>That's it. Just the one line.</p>
    <Code id="code" lines="7">
      {`//...
      .layers([
        {
          mark: 'bar',
          encoding: {
            y: 'Sales'
            color: 'Region'
          }
        }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y: "Sales", color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Grouped?</p>
    <Code id="code" lines="7">
      {`//...
      .layers([
        {
          mark: 'bar',
          encoding: {
            y: 'Sales'
            color: 'Region'
          }
        }
      ])
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y: "Sales", color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>You got it.</p>
    <Code id="code" lines="6">
      {`//...
        encoding: {
        y: 'Sales'
        color: 'Region'
      },
      transform: { type: "group" }
    }
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y: "Sales", color: "Region" },
      transform: { type: "group" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>That's... nice. Let's get back to stacks.</p>
    <Code id="code" lines="6">
      {`//...
        encoding: {
        y: 'Sales'
        color: 'Region'
      },
      transform: { type: "group" }
    }
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>That's... nice. Let's get back to stacks.</p>
    <Code id="code">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales'])
      .layers([{
        mark: 'bar',
        encoding: { color: 'Region' }
      }])
      `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Can we break this down by another attribute?</p>
    <Code id="code">
      {`//...
      .columns(['Ship Mode'])
      .rows(['Sales'])
      .layers([{
        mark: 'bar',
        encoding: { color: 'Region' }
      }])
      `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Yes! By creating column facets.</p>
    <Code id="code" lines="2">
      {`//...
      .columns(['Segment', 'Ship Mode'])
      .rows(['Sales'])
      .layers([{
        mark: 'bar',
        encoding: { color: 'Region' }
      }])
      `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Segment", "Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Yes! By creating column facets.</p>
    <Code id="code" lines="2">
      {`//...
      .columns(['Segment', 'Ship Mode'])
      .rows(['Sales'])
      .layers([{
        mark: 'bar',
        encoding: { color: 'Region' }
      }])
      `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Segment", "Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>And another attribute?</p>
    <Code id="code" lines="2">
      {`//...
      .columns(['Segment', 'Ship Mode'])
      .rows(['Sales'])
      .layers([{
        mark: 'bar',
        encoding: { color: 'Region' }
      }])
      `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Segment", "Ship Mode"]}
  muzeRows={["Category", "Sales"]}
  muzeLayers={[
    {
      mark: "bar",
      encoding: { color: "Region" },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Go for it! We've got row facets too.</p>
    <Code id="code" lines="3">
      {`//...
      .columns(['Segment', 'Ship Mode'])
      .rows(['Category', 'Sales'])
      .layers([{
        mark: 'bar',
        encoding: { color: 'Region' }
      }])
      `}
    </Code>
  </div>
</Slide>

<Slide>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Phew!</p>
    <p class="fragment">Okay. Let's go back again to the bar-line combo chart.</p>
    <p class="fragment">Its time for...</p>
  </div>
</Slide>

<Slide>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <h1 class="!text-6xl">Composition</h1>
    <hr data-id="divider" />
    <p class="fragment">A powerful by-product of using the Grammar of Graphics</p>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Here we are composing a line and a bar together.</p>
    <Code id="code">
      {`...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ]);
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>We map bar's Y to Sales</p>
    <Code id="code" lines="4">
      {`...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ]);
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Target Sales", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>We map bar's Y to Sales</p>
    <p>And line's Y to Target Sales</p>
    <Code id="code" lines="5">
      {`...
      .rows([share('Sales', 'Target Sales')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Target Sales' } }
      ]);
    `}
    </Code>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>That's simple enough but...</p>
    <p class="fragment">A bar has a top side and a bottom side.</p>
    <p class="fragment">Could we encode data to those sides individually?</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Yes we can!</p>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Target Sales"]}
  isShared
  muzeLayers={[
    {
      mark: "bar",
      encoding: { y0: "Target Sales", y: "Sales", color: { value: () => "#FFFFB3" } },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>
      <span class="fragment"><span class="fragment strike">Hanging bars!</span></span>
      <span class="fragment"><span class="fragment strike">Waterfalls!</span></span>
      <span class="fragment"><span>Range bars?!</span></span>
    </p>
    <p class="fragment">🤷</p>
    <Code id="code" lines="5">
      {`...
      .rows([share('Sales', 'Target Sales')])
      .layers([{
          mark: 'bar',
          encoding: { y0: 'Sales', y: 'Target Sales' }
      }]);
    `}
    </Code>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>But the ride doesn't stop there!</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>We can actually compose multiple marks</p>
    <p class="fragment font-bold italic">and</p>
    <p class="fragment">multiple encodings for each mark!</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>But...</p>
    <p class="fragment">...why?</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Because...</p>
    <p class="fragment">of plots like these.</p>
    <div class="fragment flex justify-center">
      <img class="w-[400px]" alt="A candlestick" src="candlestick.svg" />
    </div>
    <p class="fragment">Let's build it!</p>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>Let's start with the data.</p>
    <table data-id="data-table" class="!m-4 text-base">
      <thead>
        <tr>
          {#each projectedAaplSchema as { name, type }}
            <th class={type === "measure" ? "!text-right" : "!text-left"}>
              {name}
            </th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each sampledAaplData as row}
          <tr>
            {#each projectedAaplSchema as { name, type }}
              <td class={type === "measure" ? "!text-right" : "!text-left"}>
                {#if name === "Date"}
                  {row[name as keyof typeof row]}
                {:else}
                  {row[name as keyof typeof row].toFixed(2)}
                {/if}
              </td>
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</Slide>

<Slide animate>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-16 pt-4">
    <p>First, let's create the shared field.</p>
    <Code id="code">
      {`// ...
      .rows([share('Open', 'High', 'Low', 'Close')])
    // ...
    `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  dataset={"aapl"}
  muzeColumns={["Date"]}
  muzeRows={["Open", "High", "Low", "Close"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "High",
        size: { value: () => 0 },
        color: { value: () => "#f8f8f2" },
      },
      transition: { disabled: true },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Now, let's create the tick layer.</p>
    <Code id="code" lines="4-5">
      {`// ...
    .layers([
      {
        mark: "tick",
        encoding: { y: "High" },
      },
    ])
  // ...
  `}
    </Code>
    <p class="fragment">Great! Now we have ticks marking the High positions!</p>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  dataset={"aapl"}
  muzeColumns={["Date"]}
  muzeRows={["Open", "High", "Low", "Close"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "High",
        y0: "Low",
        size: { value: () => 0 },
        color: { value: () => "#f8f8f2" },
      },
      transition: { disabled: true },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Now, let's create the tick layer.</p>
    <Code id="code" lines="5">
      {`// ...
    .layers([
      {
        mark: "tick",
        encoding: { y: "High", y0: "Low" },
      },
    ])
  // ...
  `}
    </Code>
    <p class="fragment">Sweet! Now we have ticks spanning from Low to High!</p>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  dataset={"aapl"}
  muzeColumns={["Date"]}
  muzeRows={["Open", "High", "Low", "Close"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "High",
        y0: "Low",
        size: { value: () => 0 },
        color: { value: () => "#f8f8f2" },
      },
      transition: { disabled: true },
    },
    {
      mark: "bar",
      encoding: {
        y: "Open",
        y0: "Close",
        color: { value: () => "#f8f8f2" },
      },
      transition: { disabled: true },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Similarly, we create the bar layer.</p>
    <Code id="code">
      {`// ...
    .layers([
      {
        mark: "bar",
        encoding: { y: "Open", y0: "Close" },
      },
    ])
  // ...
  `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  dataset={"aapl"}
  muzeColumns={["Date"]}
  muzeRows={["Open", "High", "Low", "Close"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "High",
        y0: "Low",
        size: { value: () => 0 },
        color: { value: () => "#f8f8f2" },
      },
      transition: { disabled: true },
    },
    {
      mark: "bar",
      encoding: {
        y: "Open",
        y0: "Close",
        color: "Direction",
      },
      transition: { disabled: true },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-16 pt-4">
    <p>Now we color only the bar layer, keeping the tick layer as is.</p>
    <Code id="code" lines="6">
      {`// ...
      {
        mark: "bar",
        encoding: {
          // ...
          color: "Direction"
        },
      },
  // ...
  `}
    </Code>
  </div>
</Slide>

<Slide
  animate
  hasMuze
  isShared
  dataset={"aapl"}
  muzeColumns={["Date"]}
  muzeRows={["Open", "High", "Low", "Close"]}
  muzeLayers={[
    {
      mark: "tick",
      encoding: {
        y: "High",
        y0: "Low",
        size: { value: () => 0 },
        color: { value: () => "#f8f8f2" },
      },
      transition: { disabled: true },
    },
    {
      mark: "bar",
      encoding: { y: "Open", y0: "Close", color: "Direction" },
      transition: { disabled: true },
    },
  ]}
>
  <div class="flex size-full flex-col items-center justify-end px-4 pb-56 pt-4">
    <p>And there we have it! A traditional candlestick chart.</p>
  </div>
</Slide>

<Slide>
  <div class="flex size-full flex-col items-center justify-center px-4 pb-56 pt-4">
    <p>Thanks for your attention! 💖</p>
  </div>
</Slide>

<style lang="postcss">
  p {
    @apply !text-3xl;
  }

  hr {
    @apply w-full border border-neutral-200;
  }
</style>
