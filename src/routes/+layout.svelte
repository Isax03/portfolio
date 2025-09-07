<script lang="ts">
    import NavBar from "$lib/components/generic/NavBar.svelte";
    import { ModeWatcher } from "mode-watcher";
    import "../app.css";
	import { page } from '$app/state';
	const slug = $derived(page.url.pathname);
	const title = $derived(slug !== '/' ? `${slug.slice(1,2).toUpperCase()}${slug.slice(2)} - Isaia Tonini` : 'Home - Isaia Tonini');

    let { children } = $props();
</script>

<svelte:head>
<title>{title}</title>
</svelte:head>

<ModeWatcher />
<div class="min-h-[100svh] flex flex-col overflow-x-hidden">
    <NavBar />
    <section class="w-full p-4 h-full flex grow">
        <div class="w-full max-w-full overflow-x-hidden">
            {@render children?.()}
        </div>
    </section>
</div>
