<script lang="ts">
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
  <h1 class="!prose !prose-invert !text-9xl">Muze</h1>
  <h2 class="!prose !prose-invert !text-5xl">Next Gen DataViz</h2>
</Slide>

<Slide animate>
  <h1 class="!text-6xl">Muze in a nutshell</h1>
  <hr />
  <p class="fragment">Built on JavaScript and WASM</p>
  <p class="fragment">Focused on speed</p>
  <p class="fragment">Simple, declarative and expressive API</p>
</Slide>

<Slide animate>
  <p class="text-6xl">Simple, declarative and expressive API</p>
  <p class="fragment"><span data-id="how">How?</span></p>
</Slide>

<Slide animate>
  <p><span data-id="how" class="text-6xl">How?</span></p>
  <p class="fragment">By following a grammar</p>
</Slide>

<Slide animate>
  <p>A Grammar of Graphics</p>
  <div class="flex justify-center">
    <img alt="The cover of a book called A Grammar of Graphics by Leland Wilkinson" src="gog.jpg" />
  </div>
</Slide>

<Slide animate>
  <p>A <span data-id="grammar">Grammar</span></p>
  <p>gives us primitives</p>
  <p>to build more complex</p>
  <p>things</p>
</Slide>

<Slide animate>
  <p class="text-blue-400">The <span data-id="grammar">Grammar</span> of Graphics</p>
  <p>gives us primitives</p>
  <p>to build more complex</p>
  <p>things</p>
</Slide>

<Slide animate>
  <p class="text-blue-400">The Grammar of Graphics</p>
  <p data-id="primitives">gives us <span data-id="primitivess-span">primitives</span></p>
  <p>to build more complex</p>
  <p class="text-blue-400">visualizations</p>
</Slide>

<Slide animate>
  <p data-id="primitives">
    <span data-id="primitivess-span" class="text-bue-500 text-6xl">primitives</span>
  </p>
  <hr data-id="divider" />
  <p>Data</p>
  <p>Parts of Speech</p>
  <p data-id="words">Syntax etc.</p>
</Slide>

<Slide animate>
  <p data-id="primitives">
    <span data-id="primitivess-span" class="text-bue-500 text-6xl">primitives</span>
  </p>
  <hr data-id="divider" />
  <p>Data</p>
  <p>Marks</p>
  <p>Syntax etc.</p>
</Slide>

<Slide animate>
  <p data-id="primitives">
    <span data-id="primitivess-span" class="text-bue-500 text-6xl">primitives</span>
  </p>
  <hr data-id="divider" />
  <p><span>Data</span></p>
  <p>Marks</p>
  <p>Encodings etc.</p>
</Slide>

<Slide animate>
  <p><span class="text-6xl">Data</span></p>
  <hr data-id="divider" />
  <p class="fragment">Ordinal</p>
  <p class="fragment">Nominal</p>
  <p class="fragment">Temporal</p>
</Slide>

<Slide animate>
  <p><span class="text-6xl">Data</span></p>
  <hr data-id="divider" />
  <p>Ordinal</p>
  <p>Nominal</p>
  <p>Temporal</p>
</Slide>

<Slide animate>
  <p><span class="text-6xl">Data</span></p>
  <hr data-id="divider" />
  <p>Attributes</p>
  <p>Nominal</p>
  <p>Temporal</p>
</Slide>

<Slide animate>
  <p><span class="text-6xl">Data</span></p>
  <hr data-id="divider" />
  <p>Attributes</p>
  <p>Measures</p>
  <p>Temporal</p>
</Slide>

<Slide animate>
  <p><span class="text-6xl">Data</span></p>
  <hr data-id="divider" />
  <p>Attributes</p>
  <p>Measures</p>
  <p>Dates</p>
</Slide>

<Slide animate>
  <h1 class="!prose !prose-invert !font-sans !text-6xl">Marks</h1>
  <hr data-id="divider" />
  <p class="fragment">Bars</p>
  <p class="fragment">Points</p>
  <p class="fragment">Areas</p>
  <p class="fragment">Lines</p>
  <p class="fragment">Arcs</p>
  <p class="fragment">Ticks etc.</p>
</Slide>

<Slide animate>
  <h1 class="!prose !prose-invert !font-sans !text-6xl">Encodings</h1>
  <hr data-id="divider" />
  <p class="fragment">Axes</p>
  <p class="fragment">Colors</p>
  <p class="fragment">Texts</p>
  <p class="fragment">Details</p>
  <p class="fragment">Shapes</p>
  <p class="fragment">Sizes</p>
  <p class="fragment">and more...</p>
</Slide>

<Slide animate>
  <h1 class="!prose !prose-invert !text-6xl">Marks dictate the behaviour of encodings</h1>
</Slide>

<Slide animate>
  <p class="fragment">Alright that's enough theory</p>
  <p class="fragment">Let's start building stuff.</p>
</Slide>

<Slide>
  <p class="fragment">Using <span class="text-blue-500">Muze</span>, of course.</p>
</Slide>

<Slide animate>
  <p>Let's first take a look at a sample of our data.</p>
  <table data-id="data-table" class="text-sm">
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
</Slide>

<Slide animate>
  <p>Let's first take a look at a sample of our data.</p>
  <table data-id="data-table" class="text-sm">
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
</Slide>

<Slide animate>
  <p>Let's start with an empty canvas and attach our data to it.</p>
  <Code classStr="fragment" id="code">
    {`canvas()
        .data(sampleData);
    `}
  </Code>
  <p class="fragment">Not much to see here yet. I know.</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <p>Now we tell Muze what to plot along columns.</p>
  <Code classStr="fragment" id="code" lines="3">
    {`canvas()
      .data(sampleData)
      .columns(['Ship Mode']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <p>Note that Muze did a few things for us.</p>
  <Code classStr="fragment" id="code" lines="3">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <p>First, it automatically infers an appropriate mark.</p>
  <Code classStr="fragment" id="code" lines="3">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <p>Second, it automatically assigns the default X-axis encoding.</p>
  <Code classStr="fragment" id="code" lines="3">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <p>A more explicit way of specifying the same thing is as follows.</p>
  <Code classStr="fragment" id="code" lines="4-7">
    {`canvas()
      .data(sampleData)
      .columns(['Ship Mode'])
      .layers([{
        mark: 'bar',
        encoding: { x: 'Ship Mode' }
      }]);
  `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]}>
  <p>But for now, let's stick with the terse version.</p>
  <Code classStr="fragment" id="code">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p>Next, let's specify the rows.</p>
  <Code classStr="fragment" id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p>Again, Muze auto infers the Y encoding for the bars.</p>
  <Code classStr="fragment" id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p>And there we have it! Just 2 lines to get a sensible bar chart.</p>
  <Code classStr="fragment" id="code" lines="3-4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
</Slide>

<Slide hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p>Muze provides sensible defaults.</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p>Now... let's not overlook this line here.</p>
  <Code classStr="fragment" id="code" lines="2">
    {`canvas()
        .data(sampleData)
        // ...;
    `}
  </Code>
</Slide>

<Slide animate>
  <p class="text-2xl"><code class="text-xl">sampleData</code> isn't just a simple list of rows.</p>
  <Code classStr="fragment" id="code" lines="2">
    {`canvas()
        .data(sampleData)
        // ...;
    `}
  </Code>
</Slide>

<Slide animate>
  <h1 class="fragment !text-6xl">DataModel</h1>
  <p class="text-2xl">It's actually a super fast, in-memory relational algebra engine.</p>
  <Code classStr="fragment" id="code">
    {`const sampleData = new DataModel(rawData);`}
  </Code>
</Slide>

<Slide animate>
  <h1 class="!text-6xl">DataModel</h1>
  <hr data-id="divider" />
  <p>Powers all data operations performed by Muze.</p>
  <p class="fragment">Allows Muze to deal with raw, un-aggregated data.</p>
</Slide>

<Slide animate>
  <h1 class="!text-6xl">DataModel</h1>
  <hr data-id="divider" />
  <ul class="fragment !mt-4 text-2xl">
    <li>Relational algebra (SELECT, WHERE, GROUP BY, HAVING etc)</li>
    <li>
      <p>Fast 🏎️</p>
      <ul>
        <li>Powered by Rust and WebAssembly</li>
        <li>Zero-copy data access</li>
      </ul>
    </li>
    <li class="mt-4">Works in the browser</li>
    <li class="mt-4">Lightweight</li>
  </ul>
</Slide>

<Slide>
  <p>Alright, tangent over!</p>
  <p class="fragment">Back to Muze.</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <Code id="code">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
  <p class="fragment">Now let's say we want to see another measure.</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales", "Quantity"]}>
  <p>Okay.</p>
  <p class="fragment">Hmm... let's dial that back to a single measure.</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales', 'Quantity']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <Code id="code">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
  <p class="fragment">Dual axis?</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p>Sure!</p>
  <p class="fragment">But now we'll need to start being explicit.</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales', 'Quantity']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={[["Sales"], ["Profit"]]}>
  <p>Sure!</p>
  <p>But now we'll need to start being explicit.</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows([['Sales'], ['Profit']]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={[["Sales"], ["Profit"]]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p>Sure!</p>
  <p>
    But now we'll need to start a <span class="font-bold italic">bit</span> more explicit.
  </p>
  <Code id="code" lines="4-8">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows([['Sales'], ['Profit']])
        .layers([
          { mark: 'bar', encoding: { y: 'Sales' } },
          { mark: 'line', encoding: { y: 'Profit' } }
        ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={[["Sales"], ["Profit"]]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p class="fragment">Done!</p>
  <p class="fragment">Okay... could we get Sales and Profit on the same axis?</p>
  <Code id="code" lines="4-8">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows([['Sales'], ['Profit']])
        .layers([
          { mark: 'bar', encoding: { y: 'Sales' } },
          { mark: 'line', encoding: { y: 'Profit' } }
        ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p class="fragment">Yep!</p>
  <p class="fragment">
    Just use the <code class="text-2xl">share</code> operator provided by Muze.
  </p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows([share('Sales', 'Profit')])
        .layers([
          { mark: 'bar', encoding: { y: 'Sales' } },
          { mark: 'line', encoding: { y: 'Profit' } }
        ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p>This capability allows Muze to compose marks together.</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows([share('Sales', 'Profit')])
        .layers([
          { mark: 'bar', encoding: { y: 'Sales' } },
          { mark: 'line', encoding: { y: 'Profit' } }
        ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p>We'll dive deeper into composition a little later.</p>
  <p class="fragment">For now, let's explore rows and columns a little further.</p>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p class="fragment">How about a stacked bar?</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows([share('Sales', 'Profit')])
        .layers([
          { mark: 'bar', encoding: { y: 'Sales' } },
          { mark: 'line', encoding: { y: 'Profit' } }
        ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[{ mark: "bar", encoding: { y: "Sales", color: "Region" } }]}
>
  <p class="fragment">You got it!</p>
  <Code id="code" lines="5">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales'])
        .color('Region');
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: "Region" }, transform: { type: "group" } },
  ]}
>
  <p>Let's make that grouped.</p>
  <Code id="code" lines="8">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales'])
        .color('Region')
        .layers([{
          mark: "bar",
          transform: { type: "group" }
        }]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[{ mark: "bar", encoding: { y: "Sales", color: "Region" } }]}
>
  <p>Okay, now back to stacked.</p>
  <Code id="code" lines="5">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales'])
        .color('Region');
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[{ mark: "bar", encoding: { y: "Sales", color: "Region" } }]}
>
  <p class="fragment">Break this down by another attribute?</p>
  <Code id="code" lines="5">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales'])
        .color('Region');
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Order Priority", "Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[{ mark: "bar", encoding: { y: "Sales", color: "Region" } }]}
>
  <p class="fragment">Boom! Facets!</p>
  <Code id="code" lines="3">
    {`canvas()
        .data(sampleData)
        .columns(['Order Priority', 'Ship Mode'])
        .rows(['Sales'])
        .color('Region');
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Order Priority", "Ship Mode"]}
  muzeRows={["Sales"]}
  muzeLayers={[{ mark: "bar", encoding: { y: "Sales", color: "Region" } }]}
>
  <p class="fragment">And another attribute?</p>
  <Code id="code" lines="3">
    {`canvas()
        .data(sampleData)
        .columns(['Order Priority', 'Ship Mode'])
        .rows(['Sales'])
        .color('Region');
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Order Priority", "Ship Mode"]}
  muzeRows={["Segment", "Sales"]}
  muzeLayers={[{ mark: "bar", encoding: { y: "Sales", color: "Region" } }]}
>
  <p class="fragment">Sure. We've got row facets for that.</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Order Priority', 'Ship Mode'])
        .rows(['Segment', 'Sales'])
        .color('Region');
    `}
  </Code>
</Slide>

<Slide>
  <p>Phew!</p>
  <p class="fragment">Okay. Let's go back again to the bar-line combo chart.</p>
  <p class="fragment">Its time for...</p>
</Slide>

<Slide>
  <h1 class="!text-6xl">Composition</h1>
  <hr data-id="divider" />
  <p class="fragment">A powerful by-product of using the Grammar of Graphics</p>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p>Here we are composing a line and a bar together.</p>
  <Code id="code" lines="2-5">
    {`...
      .rows([share('Sales', 'Profit')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Profit' } }
      ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p>We map bar's Y to Sales</p>
  <Code id="code" lines="4">
    {`...
      .rows([share('Sales', 'Profit')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Profit' } }
      ]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y: "Sales", color: { value: () => "#FFFFB3" } } },
    { mark: "line", encoding: { y: "Profit", color: { value: () => "#8DD3C7" } } },
  ]}
>
  <p>We map bar's Y to Sales</p>
  <p>And line's Y to Profit</p>
  <Code id="code" lines="5">
    {`...
      .rows([share('Sales', 'Profit')])
      .layers([
        { mark: 'bar', encoding: { y: 'Sales' } },
        { mark: 'line', encoding: { y: 'Profit' } }
      ]);
    `}
  </Code>
</Slide>

<Slide animate>
  <p>That's simple enough but...</p>
  <p>A bar has a top side and a bottom side.</p>
  <p>Could we encode data to those sides individually?</p>
</Slide>

<Slide animate>
  <p>Yes we can!</p>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y0: "Profit", y: "Sales", color: { value: () => "#FFFFB3" } } },
  ]}
>
  <p class="fragment"><span class="fragment strike">Hanging bars!</span></p>
  <p class="fragment"><span class="fragment strike">Waterfalls!</span></p>
  <p class="fragment">Range bars?!</p>
  <p class="fragment">🤷</p>
  <Code id="code" lines="5">
    {`...
      .rows([share('Sales', 'Profit')])
      .layers([{
          mark: 'bar',
          encoding: { y0: 'Profit', y: 'Sales' }
      }]);
    `}
  </Code>
</Slide>

<Slide
  animate
  hasMuze
  muzeColumns={["Ship Mode"]}
  muzeRows={["Sales", "Profit"]}
  isShared
  muzeLayers={[
    { mark: "bar", encoding: { y0: "Profit", y: "Sales", color: { value: () => "#FFFFB3" } } },
  ]}
>
  <Code id="code" lines="5">
    {`...
      .rows([share('Sales', 'Profit')])
      .layers([{
          mark: 'bar',
          encoding: { y0: 'Profit', y: 'Sales' }
      }]);
    `}
  </Code>
</Slide>

<Slide animate>
  <p>But the ride doesn't stop there!</p>
</Slide>

<Slide animate>
  <p>We can actually compose multiple marks</p>
  <p class="fragment font-bold italic">and</p>
  <p class="fragment">multiple encodings for each mark!</p>
</Slide>

<Slide animate>
  <p>But...</p>
  <p class="fragment">...why?</p>
</Slide>

<Slide animate>
  <p>Because...</p>
  <p class="fragment">of plots like these.</p>
  <div class="fragment flex justify-center">
    <img class="w-[400px]" alt="A candlestick" src="candlestick.svg" />
  </div>
  <p class="fragment">Let's build it!</p>
</Slide>

<Slide animate>
  <p>Let's start with the data.</p>
  <table data-id="data-table" class="text-sm">
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
</Slide>

<Slide animate>
  <p>First, let's create the shared field.</p>
  <Code id="code">
    {`// ...
      .rows([share('Open', 'High', 'Low', 'Close')])
    // ...
    `}
  </Code>
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
  <p>Similarly, we create the bar layer.</p>
  <Code id="code" lines="5-6">
    {`// ...
    .layers([
      // ...
      {
        mark: "bar",
        encoding: { y: "Open", y0: "Close" },
      },
    ])
  // ...
  `}
  </Code>
  <p class="fragment">Bars done! Well, almost.</p>
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
  <p>Now we only color the bar layer, keeping the tick layer as is.</p>
  <Code id="code" lines="8">
    {`// ...
    .layers([
      // ...
      {
        mark: "bar",
        encoding: {
          // ...
          color: "Direction"
        },
      },
    ])
  // ...
  `}
  </Code>
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
  <p>And there we have it! A traditional candlestick chart.</p>
</Slide>

<Slide
  hasMuze
  dataset={"splom"}
  muzeColumns={["Miles_per_Gallon", "Acceleration", "Horsepower"]}
  muzeRows={["Miles_per_Gallon", "Acceleration", "Horsepower"].toReversed()}
  muzeLayers={[
    {
      mark: "point",
      encoding: {
        color: "Origin",
      },
    },
  ]}
  muzeConfig={{
    autoGroupBy: {
      disabled: true,
    },
    axes: {
      x: {
        numberOfTicks: 5,
      },
      y: {
        numberOfTicks: 5,
      },
    },
    gridLines: {
      y: {
        show: true,
      },
      x: {
        show: true,
      },
      zeroLineColor: "#FFFFFF",
    },
    legend: {
      color: {
        range: ["#BC80BD", "#CCEBC5", "#FFED6F"],
      },
    },
  }}
>
  <p>And there we have it! A traditional candlestick chart.</p>
</Slide>

<Slide>
  <p>Placeholder for Muze live sample gallery</p>
</Slide>

<Slide>
  <p>Transition to 1DSxViz</p>
</Slide>

<Slide>
  <p>Fin! 💖</p>
</Slide>

<style lang="postcss">
  p {
    @apply !text-3xl;
  }
</style>
