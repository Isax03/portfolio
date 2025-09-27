<script lang="ts">
    import Badge from "$lib/components/ui/badge/badge.svelte";
    import * as Card from "$lib/components/ui/card";
    import { University, Calendar, Clock, MapPin } from "@lucide/svelte";
    import Separator from "../ui/separator/separator.svelte";

    export interface EducationCardProps {
        institution: string;
        degree: string;
        location: string;
        startDate: Date;
        endDate?: Date | null;
        institutionPic?: string;
        institutionPicClass?: string;
        summary?: string;
    }

    let {
        institution,
        degree,
        location,
        startDate,
        endDate,
        institutionPic,
        institutionPicClass,
        summary
    }: EducationCardProps = $props();

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
            {#if institutionPic}
                <div class="flex-shrink-0 h-max rounded-lg shadow-[0_0_15px_var(--accent)]">
                    <img
                        src={institutionPic}
                        alt="{institution} logo"
                        class="size-12 lg:size-16 rounded-lg object-contain {institutionPicClass}"
                    />
                </div>
            {/if}

            <div class="flex flex-col gap-3 flex-1">
                <Card.Title class="text-lg font-bold">{degree}</Card.Title>

                <div class="flex flex-wrap gap-2">
                    <Badge
                        variant="outline"
                        class="flex items-center gap-1.5 px-3 py-1"
                    >
                        <University class="size-3 text-accent" />
                        {institution}
                    </Badge>

                    <Badge
                        variant="outline"
                        class="flex items-center gap-1.5 px-3 py-1"
                    >
                        <MapPin class="size-3 text-accent" />
                        {location}
                    </Badge>
                </div>

                <Separator class="!h-[0.5px]" />

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
    {#if summary}
        <Separator class="-my-3 !w-[90%] self-center !h-[0.5px]" />
        <Card.Content>
            <p class="text-sm text-muted-foreground">{@html summary}</p>
        </Card.Content>
    {/if}
</Card.Root>
