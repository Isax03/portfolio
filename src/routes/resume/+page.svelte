<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card";
    import {
        Download,
        FileText,
        ExternalLink
    } from "@lucide/svelte";

    const pdfUrlEn = "https://github.com/Isax03/curriculum-vitae/releases/download/CV-latest/Tonini_Isaia_CV_en.pdf";
    const pdfUrlIt = "https://github.com/Isax03/curriculum-vitae/releases/download/CV-latest/Tonini_Isaia_CV_it.pdf";

    const previewUrlEn = `https://docs.google.com/viewer?url=${encodeURIComponent(pdfUrlEn)}&embedded=true`;
    const previewUrlIt = `https://docs.google.com/viewer?url=${encodeURIComponent(pdfUrlIt)}&embedded=true`;

    function openInNewTab(isItalian: boolean) {
        const previewUrl = isItalian ? previewUrlIt : previewUrlEn;
        window.open(previewUrl, "_blank");
    }
</script>

<div class="flex flex-col w-full h-full items-center py-8 px-4">
    <div class="max-w-4xl w-full">
        <div class="text-center mb-10">
            <h1 class="text-4xl font-bold mb-4">
                <FileText class="inline-block size-10 mr-3 text-accent" />
                Resume
            </h1>
            <p class="text-lg text-muted-foreground max-w-2xl mx-auto">
                Download or preview my resume in your preferred language.
                Available in both English and Italian versions.
            </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- English Resume Card -->
            <Card.Root class="h-full transition-all duration-300 hover:border-accent hover:shadow-lg hover:shadow-accent/10">
                <Card.Header class="flex flex-row items-center gap-4">
                    <div class="p-3 rounded-lg bg-accent/10 text-accent font-bold text-xl">
                        EN
                    </div>
                    <div class="flex-1">
                        <Card.Title>English Version</Card.Title>
                        <Card.Description>Resume in English</Card.Description>
                    </div>
                </Card.Header>
                <Card.Content class="flex flex-col gap-3">
                    <Button
                        href={pdfUrlEn}
                        class="w-full gap-2"
                        download
                    >
                        <Download class="size-4" />
                        Download PDF
                    </Button>
                    <Button
                        variant="outline"
                        class="w-full gap-2"
                        onclick={() => openInNewTab(false)}
                    >
                        <ExternalLink class="size-4" />
                        Open in New Tab
                    </Button>
                </Card.Content>
            </Card.Root>

            <!-- Italian Resume Card -->
            <Card.Root class="h-full transition-all duration-300 hover:border-accent hover:shadow-lg hover:shadow-accent/10">
                <Card.Header class="flex flex-row items-center gap-4">
                    <div class="p-3 rounded-lg bg-accent/10 text-accent font-bold text-xl">
                        IT
                    </div>
                    <div class="flex-1">
                        <Card.Title>Italian Version</Card.Title>
                        <Card.Description>Curriculum in Italiano</Card.Description>
                    </div>
                </Card.Header>
                <Card.Content class="flex flex-col gap-3">
                    <Button
                        href={pdfUrlIt}
                        class="w-full gap-2"
                        download
                    >
                        <Download class="size-4" />
                        Download PDF
                    </Button>
                    <Button
                        variant="outline"
                        class="w-full gap-2"
                        onclick={() => openInNewTab(true)}
                    >
                        <ExternalLink class="size-4" />
                        Open in New Tab
                    </Button>
                </Card.Content>
            </Card.Root>
        </div>

        <div class="mt-10 text-center text-sm text-muted-foreground">
            <p>
                Want to know more? Check out my
                <a href="/experience" class="text-accent hover:underline">experience</a>,
                <a href="/education" class="text-accent hover:underline">education</a>, or
                <a href="/projects" class="text-accent hover:underline">projects</a>
                for detailed information.
            </p>
        </div>
    </div>
</div>
