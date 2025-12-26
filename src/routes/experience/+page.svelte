<script lang="ts">
    import ExperienceCard, { type ExperienceCardProps } from "$lib/components/portfolio/ExperienceCard.svelte";
    import { Squircle } from "@lucide/svelte";

    const experiences: ExperienceCardProps[] = [
        {
            title: "Full Stack Developer",
            company: "Würth Italia S.L.R.",
            location: "Egna (BZ), Italia",
            startDate: new Date("2025-07-21"),
            summary:
                "Development of internal web applications and software solutions for other departments within the company",
            companyPic: "/companies/wurth.png",
            skills: ["angular", "tailwindcss", "javascript", "typescript", "java", "spring", "oracle", "!static-flyway", "gitlab", "docker", "kubernetes", "argocd", "rancher"]
        },
        {
            title: "Software Engineer Intern",
            company: "Cherry Chain S.L.R.",
            location: "Povo (TN), Italia",
            startDate: new Date("2024-07-01"),
            endDate: new Date("2024-11-25"),
            summary:
                "Learned about TDD and DDD methodologies while working on real-world projects. Gained experience in both front-end and back-end development.",
            companyPic: "/companies/cherry_chain.png",
            skills: ["htmx", "tailwindcss", "javascript", "typescript", "kotlin", "!static-helidon", "postgresql", "!static-flyway", "docker", "gitlab"]
        },
    ];
</script>

<div class="flex flex-col gap-7 items-center py-5">
    <h1 class="text-4xl font-bold">Experience</h1>
    <p class="text-muted-foreground text-center max-w-2xl">
        Here are the experiences I've had so far in my career
    </p>

    <div
        class="flex flex-col w-full lg:max-w-275 lg:pb-10 gap-5 lg:gap-10 relative"
    >
        <div
            class="w-[0.5px] hidden lg:flex top-0 bottom-0 py-12.5 bg-neutral-700 absolute left-1/2 transform -translate-x-1/2 rounded"
        ></div>

        {#each experiences as experience, i}
            <div
                class="flex {i % 2 === 0
                    ? ''
                    : 'flex-row-reverse'} items-center"
            >
                <ExperienceCard
                    title={experience.title}
                    company={experience.company}
                    location={experience.location}
                    startDate={experience.startDate}
                    endDate={experience.endDate}
                    summary={experience.summary}
                    companyPic={experience.companyPic}
                    skills={experience.skills}
                />
                <div
                    class="p-6.5 z-20 bg-background relative hidden lg:block"
                >
                    <Squircle class="size-6 text-accent stroke-[1.5px]" />
                    <Squircle
                        class="size-3 text-accent stroke-[1.5px] absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2"
                    />
                </div>
            </div>
        {/each}
    </div>
</div>
