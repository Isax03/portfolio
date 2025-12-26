<script lang="ts">
    import EducationCard, { type EducationCardProps } from "$lib/components/portfolio/EducationCard.svelte";
    import { Squircle } from "@lucide/svelte";
    import { mode } from "mode-watcher";

    const experiences: EducationCardProps[] = [
        {
            institution: "University of Trento",
            degree: "Bachelor's Degree in Computer Science",
            location: "Trento, Italy",
            startDate: new Date("2022-09-01"),
            endDate: new Date("2025-07-01"),
            summary:
                "Basic notions in calculus, statistics, computer science. <br/> General: Networking, Cyber security, Databases, Computer Architectures, Software Engineering. <br/> Programming: C++, Java, Assembly, PolyML, SQL, Web Stack (HTML, CSS, JS/TS), Rust",
            institutionPic: "/education/unitn.png",
			institutionPicClass: `${mode.current === "dark" ? "invert" : ""} p-1`
        },
        {
            institution: "Galileo Galilei High School",
			degree: "Technical Institute Diploma, Informatics and Telecommunications",
            location: "Bolzano, Italy",
            startDate: new Date("2017-09-01"),
            endDate: new Date("2022-07-01"),
            summary:
                "Basics of computer science, programming and electronics. <br/> Programming: C++, Java, PHP, MySQL",
            institutionPic: "/education/galileo_galilei.png",
        },
    ];
</script>

<div class="flex flex-col gap-7 items-center py-5">
    <h1 class="text-4xl font-bold">Education</h1>
    <p class="text-muted-foreground text-center max-w-2xl">
        Here is my educational background and academic journey
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
                <EducationCard
					degree={experience.degree}
					institution={experience.institution}
					location={experience.location}
					startDate={experience.startDate}
					endDate={experience.endDate}
					summary={experience.summary}
					institutionPic={experience.institutionPic}
					institutionPicClass={experience.institutionPicClass}
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