<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import * as Select from "$lib/components/ui/select";
    import { Download } from "@lucide/svelte";

    let selected = $state<"Italian" | "English">("English");
    let isIta = $derived(selected === "Italian");
</script>

<div class="flex flex-col gap-2 items-center py-5">
    <h1 class="text-4xl font-bold">Resume</h1>
    <div class="flex gap-2 items-center mt-4">
        <Select.Root type="single" name="favoriteFruit" bind:value={selected}>
            <Select.Trigger class="w-[180px]">
                {selected}
            </Select.Trigger>
            <Select.Content>
                <Select.Group>
                    <Select.Label>Resume Language</Select.Label>
                    <Select.Item value="Italian" label="Italian">
                        Italian
                    </Select.Item>
                    <Select.Item value="English" label="English">
                        English
                    </Select.Item>
                </Select.Group>
            </Select.Content>
        </Select.Root>
    </div>
    <p class="text-muted-foreground text-center max-w-2xl">
        Click the button below to download my resume in <span
            class="text-accent">{isIta ? "Italian" : "English"}</span
        >
    </p>
    <Button
        size="lg"
        href={`https://github.com/Isax03/curriculum-vitae/releases/download/CV-latest/Tonini_Isaia_CV_${isIta ? "it" : "en"}.pdf`}
        class="text-lg mt-6"
        download
    >
        <Download class="size-5" />
        Download Resume
    </Button>
</div>
