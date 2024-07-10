<script>
  import "./app.css";
  import Request from "./lib/Request.svelte";
</script>

<main class="flex flex-col gap-4 px-8">
  <Request
    title="Head"
    expectedContentLength={312}
    response={fetch("/my-file.txt", { method: "HEAD" })}
    open
  />
  <Request
    title="Full File Read"
    expectedContentLength={312}
    response={fetch("/my-file.txt", { method: "GET" })}
  />
  <Request
    title="Partial Read"
    subtitle="Bytes 0-18"
    response={fetch("/my-file.txt", {
      method: "GET",
      headers: { Range: "bytes=0-18" },
    })}
    expectedContentLength={19}
  />
  <Request
    title="Partial Read"
    subtitle="Bytes 20-48"
    response={fetch("/my-file.txt", {
      method: "GET",
      headers: { Range: "bytes=20-48" },
    })}
    expectedContentLength={29}
  />
  <Request
    title="Partial Read"
    subtitle="Bytes 0-18"
    response={fetch("/my-file.txt", {
      method: "GET",
      headers: { Range: "bytes=0-18" },
    })}
    expectedContentLength={19}
  />
</main>
