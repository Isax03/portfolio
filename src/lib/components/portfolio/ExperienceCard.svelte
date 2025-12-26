<script lang="ts">
    import Badge from "$lib/components/ui/badge/badge.svelte";
    import * as Card from "$lib/components/ui/card";
    import * as Tooltip from "$lib/components/ui/tooltip";
    import { Building2, Calendar, Clock, MapPin } from "@lucide/svelte";
    import { buttonVariants } from "../ui/button/button.svelte";
    import Separator from "../ui/separator/separator.svelte";

    export interface ExperienceCardProps {
        title: string;
        company: string;
        location: string;
        startDate: Date;
        endDate?: Date | null;
        summary: string;
        companyPic?: string;
        skills?: string[];
    }

    let {
        title,
        company,
        location,
        startDate,
        endDate,
        summary,
        companyPic,
        skills
    }: ExperienceCardProps = $props();

    // Format date for display
    function formatDate(date: Date): string {
        return date.toLocaleDateString("en-US", {
            year: "numeric",
            month: "short",
        });
    }

    // Calculate duration with dynamic formatting
    function calculateDuration(start: Date, end?: Date | null): string {
        const startTime = start.getTime();
        const currentTime = end == null ? Date.now() : end!.getTime();

        const diffMs = currentTime - startTime;
        const totalDays = Math.floor(diffMs / (1000 * 60 * 60 * 24));

        const years = Math.floor(totalDays / 365);
        const months = Math.floor((totalDays % 365) / 30.44);
        const weeks = Math.floor(((totalDays % 365) % 30.44) / 7);

        const parts: string[] = [];

        if (years > 0) parts.push(`${years} ${years === 1 ? "year" : "years"}`);
        if (months > 0)
            parts.push(`${months} ${months === 1 ? "month" : "months"}`);
        if (weeks > 0 && years === 0)
            parts.push(`${weeks} ${weeks === 1 ? "week" : "weeks"}`);

        return parts.join(", ");
    }
</script>

<Card.Root class="w-full lg:max-w-lg">
    <Card.Header>
        <div class="flex gap-4">
            {#if companyPic}
                <div class="shrink-0">
                    <img
                        src={companyPic}
                        alt="{company} logo"
                        class="size-12 lg:size-16 rounded-lg object-contain shadow-[0_0_15px_var(--accent)]"
                    />
                </div>
            {/if}

            <div class="flex flex-col gap-3 flex-1">
                <Card.Title class="text-lg font-bold">{title}</Card.Title>

                <div class="flex flex-wrap gap-2">
                    <Badge
                        variant="outline"
                        class="flex items-center gap-1.5 px-3 py-1"
                    >
                        <Building2 class="size-3 text-accent" />
                        {company}
                    </Badge>

                    <Badge
                        variant="outline"
                        class="flex items-center gap-1.5 px-3 py-1"
                    >
                        <MapPin class="size-3 text-accent" />
                        {location}
                    </Badge>
                </div>

                <Separator class="h-[0.5px]!" />

                <div class="space-y-1">
                    <div
                        class="flex items-center gap-2 text-sm text-muted-foreground"
                    >
                        <Calendar class="size-3 text-accent" />
                        {formatDate(startDate)} - {endDate == null
                            ? "Present"
                            : formatDate(endDate!)}
                    </div>

                    <div
                        class="flex items-center gap-2 text-sm text-muted-foreground"
                    >
                        <Clock class="size-3 text-accent" />
                        {calculateDuration(startDate, endDate)}
                    </div>
                </div>
            </div>
        </div>
    </Card.Header>
    <Separator class="-my-3 w-[90%]! self-center h-[0.5px]!" />
    <Card.Content>
        <p class="text-sm text-muted-foreground">{summary}</p>
    </Card.Content>
    {#if skills && skills.length > 0}
        <Separator class="-my-3 w-[90%]! self-center h-[0.5px]!" />
        <Card.Footer class="flex flex-wrap gap-2">
            {#each skills as skill}
                <Tooltip.Provider>
                    <Tooltip.Root>
                        <Tooltip.Trigger>
                            <div
                                class={buttonVariants({
                                    variant: "outline",
                                    size: "icon",
                                    class: "dark:hover:bg-input/30 hover:bg-background",
                                })}
                            >
                                {#if skill.startsWith('!static-')}
                                    <img
                                        src="/icons/{skill.replace('!static-', '')}.svg"
                                        alt={skill.replace('!static-', '')}
                                        class="size-6 rounded-[4px]"
                                    />
                                {:else}
                                    <img
                                        src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/{skill}/{skill}-original.svg"
                                        alt={skill}
                                        class="size-6 rounded-[4px]"
                                    />
                                {/if}
                            </div>
                        </Tooltip.Trigger>

                        <Tooltip.Content class="z-99">
                            <p class="capitalize">{skill.startsWith('!static-') ? skill.replace('!static-', '') : skill}</p>
                        </Tooltip.Content>
                    </Tooltip.Root>
                </Tooltip.Provider>
            {/each}
        </Card.Footer>
    {/if}
</Card.Root>
