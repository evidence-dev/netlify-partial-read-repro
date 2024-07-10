<script>
</script>

<main>
  <h2>Response Headers</h2>
  {#await fetch("/my-file.txt", { method: "HEAD" }) then e}
    <dl>
      {#each e.headers as [k, v]}
        <dt>{k}</dt>
        <dd>{v}</dd>
      {/each}
    </dl>
  {/await}

  <h2>Full File Read</h2>
  {#await fetch("/my-file.txt", { method: "GET" }).then((r) => r.text()) then e}
    <pre>{e}</pre>
  {/await}

  <h2>Partial File Read // Display 0-9 // Bytes 0-18</h2>
  {#await fetch( "/my-file.txt", { method: "GET", headers: { Range: "bytes=0-18" } }, ).then( (r) => r.text(), ) then e}
    <pre>{e}</pre>
  {/await}

  <h2>Partial File Read // Display 10-19 // Bytes 19-28</h2>
  {#await fetch( "/my-file.txt", { method: "GET", headers: { Range: "bytes=19-49" } }, ).then( (r) => r.text(), ) then e}
    <pre>{e}</pre>
  {/await}
</main>
