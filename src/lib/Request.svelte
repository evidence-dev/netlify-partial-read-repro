<script>
    /** @type {string} */
    export let title;

    /** @type {string}*/
    export let subtitle = "";

    /** @type {Promise<Response>} */
    export let response;

    /** @type {number} */
    export let expectedContentLength = 0;

    export let open = false;
</script>

<section>
    <h2 class="text-xl font-bold mb-2">
        {title}
        {#if subtitle}
            <span class="block text-sm text-slate-500 uppercase font-semibold">
                {subtitle}
            </span>
        {/if}
    </h2>
    {#await response}
        Loading...
    {:then r}
        {@const contentLength = r.headers.get("content-length")}
        <div class="flex gap-4 items-start">
            <div class="flex flex-col gap-2">
                <button on:click={() => (open = !open)}>
                    {open ? "Hide" : "Show"} Headers
                </button>
                {#if expectedContentLength}
                    <span
                        class:text-green-500={contentLength ===
                            expectedContentLength.toString()}
                        class:text-red-500={contentLength !==
                            expectedContentLength.toString()}
                    >
                        Content Length: {contentLength}</span
                    >
                {:else}
                    <span>Content Length: {contentLength}</span>
                {/if}
            </div>
            {#await r.text()}
                Loading...
            {:then text}
                <div class="flex-1">
                    <pre class="bg-slate-100 p-2 max-h-fit">{text || "[[Empty Response]]"}</pre>
                </div>
            {/await}

            {#if open}
                <div class="text-xs flex-1">
                    <dl class="font-bold">
                        {#each r.headers as [k, v]}
                            <dt>{k}</dt>
                            <dd class="pl-8">{v}</dd>
                        {/each}
                    </dl>
                </div>
            {:else}
                <div class="flex-1"></div>
            {/if}
        </div>
    {/await}
</section>
