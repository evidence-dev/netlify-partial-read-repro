<script>
  import "./app.css";
  import Request from "./lib/Request.svelte";
</script>

<main class="px-8 flex">
  <div class="flex flex-col gap-4">
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
  </div>
  <div class="flex flex-col gap-4">
    <Request
      title="Head"
      expectedContentLength={139582656}
      response={fetch("/my-very-large-file.txt", { method: "HEAD" })}
      open
    />
    <Request
      title="Partial Read"
      subtitle="Bytes 0-18"
      response={fetch("/my-very-large-file.txt", {
        method: "GET",
        headers: { Range: "bytes=0-18" },
      })}
      expectedContentLength={19}
    />
    <Request
      title="Partial Read"
      subtitle="Bytes 0-18"
      response={fetch("/my-very-large-file.txt", {
        method: "GET",
        headers: { Range: "bytes=0-18" },
      })}
      expectedContentLength={19}
    />
    <Request
      title="Partial Read"
      subtitle="Bytes 2000-3000"
      response={fetch("/my-very-large-file.txt", {
        method: "GET",
        headers: { Range: "bytes=2000-3000" },
      })}
      expectedContentLength={1001}
    />
    <Request
      title="Partial Read"
      subtitle="Bytes 2000-3000"
      response={fetch("/my-very-large-file.txt", {
        method: "GET",
        headers: { Range: "bytes=2000-3000" },
      })}
      expectedContentLength={1001}
    />
    <Request
      title="Partial Read"
      subtitle="Bytes 20000-30000"
      response={fetch("/my-very-large-file.txt", {
        method: "GET",
        headers: { Range: "bytes=20000-30000" },
      })}
      expectedContentLength={10001}
    />
    <Request
      title="Partial Read"
      subtitle="Bytes 20000-30000"
      response={fetch("/my-very-large-file.txt", {
        method: "GET",
        headers: { Range: "bytes=20000-30000" },
      })}
      expectedContentLength={10001}
    />
  </div>
</main>
