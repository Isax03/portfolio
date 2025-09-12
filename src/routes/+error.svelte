<script lang="ts">
    import { page } from "$app/state";
    import { Button } from "$lib/components/ui/button";
    import { House } from "@lucide/svelte";
</script>

<svelte:head>
    <title>Error {page.status} - Portfolio</title>
</svelte:head>

<div class="h-full w-full flex flex-col items-center justify-center gap-6 text-center p-4">
    <h1 class="text-4xl font-bold text-accent">Oops!😅</h1>
    
    <p class="text-xl text-muted-foreground max-w-[600px]">
        {#if page.status === 404}
            Looks like you got lost! <br /><br />
            This page doesn't exist, but don't worry<br/>
            You can safely return home 🏠
        {:else}
            An unexpected error has occurred. <br />
            Don't worry, I'm already working on fixing it.
        {/if}
    </p>

    <p class="text-sm text-accent/60 mb-4 italic">
        Error {page.status}
    </p>

    <div class="flex justify-center">
        <Button href="/" variant="default">
            <House class="w-4 h-4 mr-2" />
            Back to Home
        </Button>
    </div>
</div>
