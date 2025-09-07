<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import { Switch } from "$lib/components/ui/switch";
    import { Download } from "@lucide/svelte";

    let isIta = $state(false);
</script>

<div class="flex flex-col gap-2 items-center">
	<h1 class="text-4xl font-bold">Resume</h1>
	<div class="flex gap-2 items-center mt-4">
		<span class="text-lg {!isIta ? 'text-primary' : 'text-muted-foreground'}">English</span>
		<Switch bind:checked={isIta} />
		<span class="text-lg {isIta ? 'text-primary' : 'text-muted-foreground'}">Italian</span>
	</div>
	<p class="text-muted-foreground text-center max-w-2xl">
		Click the button below to download my resume in <span class="text-accent">{isIta ? "Italian" : "English"}</span>
	</p>
	<Button size="lg" href={`https://github.com/Isax03/curriculum-vitae/releases/download/CV-latest/Tonini_Isaia_CV_${isIta ? "it" : "en"}.pdf`} class="text-lg mt-6" download>
		<Download class="size-5" />
		Download Resume
	</Button>
</div>
