<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card";
    import * as Select from "$lib/components/ui/select";
    import {
        Download,
        FileText,
        ExternalLink,
        Eye,
        Loader2
    } from "@lucide/svelte";

    let selected = $state<"Italian" | "English">("English");
    let isIta = $derived(selected === "Italian");
    let showPreview = $state(false);
    let isLoading = $state(false);

    const pdfUrl = $derived(
        `https://github.com/Isax03/curriculum-vitae/releases/download/CV-latest/Tonini_Isaia_CV_${isIta ? "it" : "en"}.pdf`
    );

    // Google Docs Viewer per mostrare il PDF senza download
    const previewUrl = $derived(
        `https://docs.google.com/viewer?url=${encodeURIComponent(pdfUrl)}&embedded=true`
    );

    // Apre il PDF in una nuova tab usando blob URL
    async function openInNewTab() {
        isLoading = true;
        try {
            const response = await fetch(pdfUrl);
            const blob = await response.blob();
            const blobUrl = URL.createObjectURL(blob);
            window.open(blobUrl, "_blank");
        } catch (error) {
            // Fallback: usa Google Docs Viewer
            window.open(previewUrl, "_blank");
        } finally {
            isLoading = false;
        }
    }
</script>

<div class="flex flex-col gap-8 items-center justify-center py-8 px-4 min-h-[calc(100vh-10rem)]">
    <!-- Download Section -->
    <Card.Root class="w-full max-w-2xl border-accent/30">
        <Card.Header class="text-center">
            <Card.Title class="flex items-center justify-center gap-2 text-2xl">
                <FileText class="size-6 text-accent" />
                Resume
            </Card.Title>
            <Card.Description>
                Download or preview my resume in your preferred language
            </Card.Description>
        </Card.Header>
        <Card.Content class="flex flex-col items-center gap-6">
            <!-- Language Selector -->
            <div class="flex flex-col sm:flex-row gap-4 items-center">
                <span class="text-sm text-muted-foreground">Select language:</span>
                <Select.Root type="single" name="resumeLanguage" bind:value={selected}>
                    <Select.Trigger class="w-40">
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

            <!-- Action Buttons -->
            <div class="flex flex-col sm:flex-row gap-3">
                <Button
                    size="lg"
                    href={pdfUrl}
                    class="text-base gap-2"
                    download
                >
                    <Download class="size-5" />
                    Download PDF
                </Button>
                <Button
                    size="lg"
                    variant="outline"
                    class="text-base gap-2"
                    onclick={() => (showPreview = !showPreview)}
                >
                    <Eye class="size-5" />
                    {showPreview ? "Hide Preview" : "Show Preview"}
                </Button>
                <Button
                    size="lg"
                    variant="ghost"
                    class="text-base gap-2"
                    onclick={openInNewTab}
                    disabled={isLoading}
                >
                    {#if isLoading}
                        <Loader2 class="size-5 animate-spin" />
                    {:else}
                        <ExternalLink class="size-5" />
                    {/if}
                    Open in New Tab
                </Button>
            </div>

            <!-- PDF Preview usando Google Docs Viewer -->
            {#if showPreview}
                <div class="w-full mt-4 rounded-lg overflow-hidden border bg-muted/20">
                    <iframe
                        src={previewUrl}
                        title="Resume Preview"
                        class="w-full h-150 lg:h-200"
                    ></iframe>
                </div>
            {/if}
        </Card.Content>
    </Card.Root>

    <!-- Additional Links -->
    <div class="text-center text-sm text-muted-foreground max-w-2xl">
        <p>
            Want to know more? Check out my
            <a href="/experience" class="text-accent hover:underline">experience</a>,
            <a href="/education" class="text-accent hover:underline">education</a>, or
            <a href="/projects" class="text-accent hover:underline">projects</a>
            for detailed information.
        </p>
    </div>
</div>
