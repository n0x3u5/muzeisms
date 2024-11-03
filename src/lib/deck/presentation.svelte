<script lang="ts">
  import Slide from "./slide.svelte";
  import Code from "./code.svelte";
  import Markdown from "./markdown.svelte";
  import Notes from "./notes.svelte";
  import data from "../data/superstore/data.json" with { type: "json" };
  import schema from "../data/superstore/schema.json" with { type: "json" };

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
  function getSeededSample(array: typeof data, sampleSize: number, seed: number = 42) {
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

  const sampledData = getSeededSample(data, 15, 0);
  const projectedSchema = schema
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
  <p class="fragment text-3xl">Alright that's enough theory</p>
  <p class="fragment text-3xl">Let's start putting all this together...</p>
</Slide>

<Slide>
  <p class="fragment text-3xl">Using <span class="text-blue-500">Muze</span>, of course.</p>
</Slide>

<Slide animate>
  <p class="text-3xl">Let's first take a look at a sample of our data.</p>
  <table data-id="data-table" class="text-sm">
    <thead>
      <tr>
        {#each projectedSchema as { name, type, subtype }}
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
      {#each sampledData as row}
        <tr>
          {#each projectedSchema as { name, type, subtype }}
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
  <p class="text-3xl">Let's first take a look at a sample of our data.</p>
  <table data-id="data-table" class="text-sm">
    <thead>
      <tr>
        {#each projectedSchema as { name, type, subtype }}
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
      {#each sampledData as row}
        <tr>
          {#each projectedSchema as { name, type, subtype }}
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
  <p class="text-3xl">Let's start with an empty canvas and attach our data to it.</p>
  <Code classStr="fragment" id="code">
    {`canvas()
        .data(sampleData);
    `}
  </Code>
  <p class="fragment text-3xl">Not much to see here yet. I know.</p>
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
  <p>Note that Muze did a couple of things for us.</p>
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
  <p class="text-3xl">And there we have it! Just 2 lines to get a sensible bar chart.</p>
  <Code classStr="fragment" id="code" lines="3-4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p class="text-3xl">But... let's not overlook this line here.</p>
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
  <p class="fragment text-bold text-5xl text-emerald-500">DataModel</p>
  <p class="text-2xl">It's actually a super fast, in-memory relational algebra engine.</p>
  <Code classStr="fragment" id="code">
    {`const sampleData = new DataModel(rawData);`}
  </Code>
</Slide>

<Slide animate>
  <p class="text-bold text-5xl text-emerald-500">DataModel</p>
  <p>Powers all data operations performed by Muze.</p>
</Slide>

<Slide animate>
  <p class="text-3xl">Recall this table?</p>
  <p class="fragment text-2xl">
    The actual data file has <span class="text-amber-500">~8.5k rows</span> and
    <span class="text-purple-500">25 columns</span>.
  </p>
  <table data-id="data-table" class="text-sm">
    <thead>
      <tr>
        {#each projectedSchema as { name, type, subtype }}
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
      {#each sampledData as row}
        <tr>
          {#each projectedSchema as { name, type, subtype }}
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
  <p class="text-3xl">This is it now.</p>
  <p class="fragment text-2xl">Thanks to DataModel's relational algebra capabilities.</p>
  <table data-id="data-table" class="text-sm">
    <thead>
      <tr>
        <th>Ship Mode</th>
        <th>Sales</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Delivery Truck</td>
        <td>6,224,878.72</td>
      </tr>
      <tr>
        <td>Express Air</td>
        <td>1,184,418.9</td>
      </tr>
      <tr>
        <td>Regular Air</td>
        <td>7,506,303.21</td>
      </tr>
    </tbody>
  </table>
  <Code classStr="fragment" id="code" lines="3-4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales']);
    `}
  </Code>
</Slide>

<Slide animate>
  <p class="text-bold text-5xl text-emerald-500">DataModel</p>
  <p class="fragment text-2xl">Allows Muze to deal with raw, un-aggregated data.</p>
  <p class="fragment text-2xl">
    While keeping Muze capable of accepting pre-aggregated data as well.
  </p>
</Slide>

<Slide animate>
  <p class="text-bold text-5xl text-emerald-500">DataModel</p>
  <ul class="fragment text-2xl">
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
  <p class="fragment text-3xl">Now let's say we want to see another measure.</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales", "Quantity"]}>
  <p class="text-3xl">Okay.</p>
  <p class="fragment text-3xl">Hmm... let's dial that back to a single measure.</p>
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
  <p class="fragment text-3xl">Dual axis?</p>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={["Sales"]}>
  <p class="text-3xl">Sure!</p>
  <p class="fragment text-3xl">But now we'll need to start being explicit.</p>
  <Code id="code" lines="4">
    {`canvas()
        .data(sampleData)
        .columns(['Ship Mode'])
        .rows(['Sales', 'Quantity']);
    `}
  </Code>
</Slide>

<Slide animate hasMuze muzeColumns={["Ship Mode"]} muzeRows={[["Sales"], ["Profit"]]}>
  <p class="text-3xl">Sure!</p>
  <p class="text-3xl">But now we'll need to start being explicit.</p>
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
  <p class="text-3xl">Sure!</p>
  <p class="text-3xl">
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
  <p class="fragment text-3xl">Done!</p>
  <p class="fragment text-3xl">Okay... could we get Sales and Profit on the same axis?</p>
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
  <p class="fragment text-3xl">Yep!</p>
  <p class="fragment text-3xl">
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
  <p class="fragment text-3xl">Stacked bar?</p>
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
  <p class="fragment text-3xl">You got it!</p>
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
  <p class="fragment text-3xl">Break this down by another attribute?</p>
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
  <p class="fragment text-3xl">Boom!</p>
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
  <p class="fragment text-3xl">And another...?</p>
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
  <p class="fragment text-3xl">That's Muze for you.</p>
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
  <p class="fragment text-3xl">Placeholder for Muze live sample gallery</p>
</Slide>

<Slide>
  <p class="fragment text-3xl">Transition to 1DSxViz</p>
</Slide>

<Slide>
  <p class="fragment text-3xl">Fin! 💖</p>
</Slide>
