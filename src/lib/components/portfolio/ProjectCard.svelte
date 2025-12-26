<script lang="ts">
    import Badge from "$lib/components/ui/badge/badge.svelte";
    import * as Card from "$lib/components/ui/card";
    import { Github, ExternalLink } from "@lucide/svelte";

    export interface ProjectCardProps {
        title: string;
        slug: string;
        description: string;
        bannerImage: string;
        githubUrl: string;
        technologies?: string[];
    }

    let {
        title,
        slug,
        description,
        bannerImage,
        githubUrl,
        technologies
    }: ProjectCardProps = $props();
</script>

<a href="/projects/{slug}" class="block w-full lg:max-w-lg group">
    <Card.Root class="w-full overflow-hidden transition-all duration-300 hover:shadow-[0_0_25px_var(--accent)] hover:border-accent/50">
        <div class="relative w-full h-40 overflow-hidden">
            <img
                src={bannerImage}
                alt="{title} banner"
                class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-105"
            />
            <div class="absolute inset-0 bg-linear-to-t from-background/80 to-transparent"></div>
        </div>
        
        <Card.Header class="pt-4">
            <div class="flex flex-col gap-3">
                <div class="flex items-center justify-between">
                    <Card.Title class="text-lg font-bold">{title}</Card.Title>
                    <a
                        href={githubUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="flex items-center gap-1.5 text-sm text-muted-foreground hover:text-accent transition-colors"
                        onclick={(e) => e.stopPropagation()}
                    >
                        <Github class="size-4" />
                        <span class="hidden sm:inline">GitHub</span>
                    </a>
                </div>
                
                <Card.Description class="text-sm text-muted-foreground line-clamp-2">
                    {description}
                </Card.Description>

                {#if technologies && technologies.length > 0}
                    <div class="flex flex-wrap gap-2 mt-2">
                        {#each technologies.slice(0, 4) as tech}
                            <Badge variant="secondary" class="text-xs px-2 py-0.5">
                                {tech}
                            </Badge>
                        {/each}
                        {#if technologies.length > 4}
                            <Badge variant="outline" class="text-xs px-2 py-0.5">
                                +{technologies.length - 4}
                            </Badge>
                        {/if}
                    </div>
                {/if}

                <div class="flex items-center gap-1 text-xs text-accent mt-2">
                    <ExternalLink class="size-3" />
                    <span>View Details</span>
                </div>
            </div>
        </Card.Header>
    </Card.Root>
</a>