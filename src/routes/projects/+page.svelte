<script lang="ts">
    import ProjectCard, { type ProjectCardProps } from "$lib/components/portfolio/ProjectCard.svelte";

    const projects: ProjectCardProps[] = [
        {
            title: "Festa di Primavera",
            slug: "fdp",
            description: "A ticket management system for the spring festival organized by the Salesiano University Dormitory 'Piergiorgio Frassati' in Trento. Continuously maintained since 2024.",
            bannerImage: "/projects/fdp/banner.svg",
            githubUrl: "https://github.com/Festa-di-Primavera/fdp-app",
            technologies: ["SvelteKit", "TypeScript", "Firebase", "TailwindCSS", "Vercel"]
        },
        {
            title: "LFC Playground",
            slug: "lfc-playground",
            description: "A web playground for validating exercises for the Formal Languages and Compilers course at University of Trento. Features include FIRST/FOLLOW calculation, LL(1) and SLR(1) parsing tables.",
            bannerImage: "/projects/lfc-playground/banner.svg",
            githubUrl: "https://github.com/Isax03/lfc-playground",
            technologies: ["SvelteKit", "TypeScript", "TailwindCSS", "Vercel"]
        },
        {
            title: "PTZ Vision",
            slug: "ptz-vision",
            description: "An Android application for remotely controlling PTZ cameras with VISCA protocol and RTSP video streaming. Developed for the Mobile Programming course at University of Trento.",
            bannerImage: "/projects/ptz-vision/banner.svg",
            githubUrl: "https://github.com/PTZ-Vision/PTZ-Vision-Android",
            technologies: ["Kotlin", "Jetpack Compose", "Room", "ExoPlayer", "VISCA"]
        }
    ];
</script>

<div class="flex flex-col gap-7 items-center py-5">
    <h1 class="text-4xl font-bold">Projects</h1>
    <p class="text-muted-foreground text-center max-w-2xl">
        Here are some of the projects I've worked on. Click on any project to see more details.
    </p>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 w-full max-w-6xl px-4">
        {#each projects as project}
            <ProjectCard
                title={project.title}
                slug={project.slug}
                description={project.description}
                bannerImage={project.bannerImage}
                githubUrl={project.githubUrl}
                technologies={project.technologies}
            />
        {/each}
    </div>
</div>
