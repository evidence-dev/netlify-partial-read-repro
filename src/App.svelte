<script>
  import "./app.css";
</script>

<main class="max-w-prose flex flex-col gap-4 px-8">
  <section>
    <h2>Response Headers</h2>
    {#await fetch("/my-file.txt", { method: "HEAD" }) then e}
      <dl>
        {#each e.headers as [k, v]}
          <dt>{k}</dt>
          <dd>{v}</dd>
        {/each}
      </dl>
    {/await}
  </section>

  <section>
    <h2>Full File Read</h2>
    {#await fetch("/my-file.txt", { method: "GET" }) then r}
      <div class="flex justify-between gap-4">
        <div>
          {#await r.text()}
            Loading...
          {:then text}
            <pre>{text}</pre>
          {/await}
        </div>
        <div>
          <dl>
            {#each r.headers as [k, v]}
              <dt>{k}</dt>
              <dd>{v}</dd>
            {/each}
          </dl>
        </div>
      </div>
    {/await}
  </section>

  <section>
    <h2>Partial File Read // Display 0-9 // Bytes 0-18</h2>

    {#await fetch( "/my-file.txt", { method: "GET", headers: { Range: "bytes=0-18" } }, ) then r}
      <div class="flex justify-between gap-4">
        <div>
          {#await r.text()}
            Loading...
          {:then text}
            <pre>{text}</pre>
          {/await}
        </div>
        <div>
          <dl>
            {#each r.headers as [k, v]}
              <dt>{k}</dt>
              <dd>{v}</dd>
            {/each}
          </dl>
        </div>
      </div>
    {/await}
  </section>
  <section>
    <h2>Partial File Read // Display 10-19 // Bytes 20-48</h2>
    {#await fetch( "/my-file.txt", { method: "GET", headers: { Range: "bytes=20-48" } }, ) then r}
      <div class="flex justify-between gap-4">
        <div>
          {#await r.text()}
            Loading...
          {:then text}
            <pre>{text}</pre>
          {/await}
        </div>
        <div>
          <dl>
            {#each r.headers as [k, v]}
              <dt>{k}</dt>
              <dd>{v}</dd>
            {/each}
          </dl>
        </div>
      </div>
    {/await}
  </section>
</main>

<style lang="postcss">
  dl {
  }
  dt {
    @apply font-bold;
  }
  dd {
    @apply pl-8;
  }
  h2 {
    @apply text-xl font-bold mb-2;
  }
</style>
