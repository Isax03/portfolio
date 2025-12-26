<script lang="ts">
    import { page } from "$app/state";
    import Badge from "$lib/components/ui/badge/badge.svelte";
    import { Button } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card";
    import Separator from "$lib/components/ui/separator/separator.svelte";
    import {
        ArrowLeft,
        Github,
        ExternalLink,
        Calendar,
        Users,
    } from "@lucide/svelte";

    interface ProjectDetail {
        title: string;
        slug: string;
        description: string;
        fullDescription: string;
        bannerImage: string;
        detailImage: string;
        githubUrl: string;
        liveUrl?: string;
        technologies: string[];
        features: string[];
        developers: { name: string; github: string }[];
        year: string;
    }

    const projectsData: Record<string, ProjectDetail> = {
        fdp: {
            title: "Festa di Primavera",
            slug: "fdp",
            description: "A ticket management system for the spring festival",
            fullDescription:
                "A comprehensive ticket management software developed for the 'Festa di Primavera' organized by the Salesiano University Dormitory 'Piergiorgio Frassati' in Trento. First used in 2024 and continuously maintained and improved, the system handles ticket generation, sales, check-in, and food order management with role-based access control. The project is designed to be passed on to future dormitory residents to ensure its continued use in upcoming editions.",
            bannerImage: "/projects/fdp/banner.svg",
            detailImage: "/projects/fdp/detail.svg",
            githubUrl: "https://github.com/Festa-di-Primavera/fdp-app",
            liveUrl: "https://fdp-app.vercel.app",
            technologies: [
                "SvelteKit",
                "TypeScript",
                "Firebase",
                "Firestore",
                "Lucia Auth",
                "TailwindCSS",
                "Flowbite",
                "Vercel",
                "ReSend",
            ],
            features: [
                "User authentication via email/password or Google SSO with email verification",
                "Role-based access control with granular permissions",
                "Ticket generation (parametric or CSV upload) and batch assignment to sellers",
                "QR code ticket sales with seller tracking and earnings management",
                "Check-in system with QR code scanning for event entry",
                "Real-time dashboard with sales statistics and analytics",
                "Cashier system for food orders linked to tickets",
                "Queue checkpoint system to manage order flow to kitchen",
                "Kitchen display for order preparation and tracking",
                "Staff orders system for personnel without nominal tickets",
            ],
            developers: [
                { name: "Isaia Tonini", github: "https://github.com/Isax03" },
                {
                    name: "Riccardo Benevelli",
                    github: "https://github.com/RickyBenevelli",
                },
            ],
            year: "2024 - Present",
        },
        "lfc-playground": {
            title: "LFC Playground",
            slug: "lfc-playground",
            description:
                "A web playground for validating formal languages exercises",
            fullDescription:
                "A web application created to help students studying Formal Languages and Compilers at the University of Trento. It provides an interactive environment to verify the correctness of exercises, especially the 'mechanical' ones, and experiment with grammars and parsing tables.",
            bannerImage: "/projects/lfc-playground/banner.svg",
            detailImage: "/projects/lfc-playground/detail.svg",
            githubUrl: "https://github.com/Isax03/lfc-playground",
            liveUrl: "https://lfc-playground.vercel.app",
            technologies: [
                "SvelteKit",
                "TypeScript",
                "TailwindCSS",
                "shadcn-svelte",
                "Vercel",
            ],
            features: [
                "FIRST and FOLLOW set calculation",
                "LL(1) parsing table construction",
                "String parsing with LL(1) and parse tree visualization",
                "Left recursion removal",
                "Grammar factorization",
                "Chomsky Normal Form conversion",
                "SLR(1) parsing table construction",
                "SLR(1) characteristic automaton construction",
                "Shift/reduce parsing with SLR(1)",
            ],
            developers: [
                { name: "Isaia Tonini", github: "https://github.com/Isax03" },
            ],
            year: "2024",
        },
        "ptz-vision": {
            title: "PTZ Vision",
            slug: "ptz-vision",
            description: "Android app for remote PTZ camera control",
            fullDescription:
                "An Android application developed for the Mobile Programming course at the University of Trento. PTZ Vision allows users to remotely control PTZ cameras using the VISCA protocol over IP, with real-time RTSP video streaming. The app features a modern Material Design 3 interface with adaptive layouts for both portrait and landscape orientations.",
            bannerImage: "/projects/ptz-vision/banner.svg",
            detailImage: "/projects/ptz-vision/detail.svg",
            githubUrl: "https://github.com/PTZ-Vision/PTZ-Vision-Android",
            technologies: [
                "Kotlin",
                "Jetpack Compose",
                "Room",
                "ExoPlayer (Media3)",
                "Material Design 3",
                "VISCA Protocol",
                "Coroutines",
            ],
            features: [
                "Full PTZ Control via virtual joystick",
                "RTSP video streaming with real-time preview",
                "Multi-camera support with quick selection",
                "Auto Focus & AI Tracking support",
                "Adaptive layout for Portrait and Landscape",
                "Local database with Room for camera configurations",
                "Haptic feedback during joystick usage",
                "Scene presets for saved positions",
            ],
            developers: [
                { name: "Isaia Tonini", github: "https://github.com/Isax03" },
                { name: "Kevin Delugan", github: "https://github.com/BisUmTo" },
            ],
            year: "2024",
        },
    };

    const slug = $derived(page.params.slug);
    const project = $derived(
        slug && slug in projectsData ? projectsData[slug] : undefined
    );
</script>

{#if project}
    <div class="flex flex-col gap-8 items-center py-5 px-4">
        <div class="w-full max-w-4xl">
            <a
                href="/projects"
                class="inline-flex items-center gap-2 text-muted-foreground hover:text-accent transition-colors mb-6"
            >
                <ArrowLeft class="size-4" />
                <span>Back to Projects</span>
            </a>

            <div
                class="relative w-full h-48 md:h-64 lg:h-80 rounded-xl overflow-hidden mb-8"
            >
                <img
                    src={project.detailImage}
                    alt="{project.title} detail"
                    class="w-full h-full object-cover"
                />
                <div
                    class="absolute inset-0 bg-linear-to-t from-background via-background/20 to-transparent"
                ></div>
                <div class="absolute bottom-0 left-0 right-0 p-6">
                    <h1 class="text-3xl md:text-4xl font-bold text-foreground">
                        {project.title}
                    </h1>
                </div>
            </div>

            <div class="flex flex-wrap gap-4 mb-6">
                <a
                    href={project.githubUrl}
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    <Button variant="outline" class="flex items-center gap-2">
                        <Github class="size-4" />
                        View on GitHub
                    </Button>
                </a>
                {#if project.liveUrl}
                    <a
                        href={project.liveUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                    >
                        <Button
                            variant="default"
                            class="flex items-center gap-2"
                        >
                            <ExternalLink class="size-4" />
                            Live Demo
                        </Button>
                    </a>
                {/if}
            </div>

            <div
                class="flex flex-wrap gap-4 mb-6 text-sm text-muted-foreground"
            >
                <div class="flex items-center gap-2">
                    <Calendar class="size-4 text-accent" />
                    <span>{project.year}</span>
                </div>
                <div class="flex items-center gap-2">
                    <Users class="size-4 text-accent" />
                    <span>
                        {#each project.developers as dev, i}
                            <a
                                href={dev.github}
                                target="_blank"
                                rel="noopener noreferrer"
                                class="hover:text-accent transition-colors"
                            >
                                {dev.name}
                            </a>{#if i < project.developers.length - 1},&nbsp;{/if}
                        {/each}
                    </span>
                </div>
            </div>

            <Separator class="mb-6" />

            <Card.Root class="mb-8">
                <Card.Header>
                    <Card.Title>About</Card.Title>
                </Card.Header>
                <Card.Content>
                    <p class="text-muted-foreground leading-relaxed">
                        {project.fullDescription}
                    </p>
                </Card.Content>
            </Card.Root>

            <Card.Root class="mb-8">
                <Card.Header>
                    <Card.Title>Technologies</Card.Title>
                </Card.Header>
                <Card.Content>
                    <div class="flex flex-wrap gap-2">
                        {#each project.technologies as tech}
                            <Badge variant="secondary" class="px-3 py-1">
                                {tech}
                            </Badge>
                        {/each}
                    </div>
                </Card.Content>
            </Card.Root>

            <Card.Root>
                <Card.Header>
                    <Card.Title>Features</Card.Title>
                </Card.Header>
                <Card.Content>
                    <ul
                        class="list-disc list-inside space-y-2 text-muted-foreground"
                    >
                        {#each project.features as feature}
                            <li>{feature}</li>
                        {/each}
                    </ul>
                </Card.Content>
            </Card.Root>
        </div>
    </div>
{:else}
    <div class="flex flex-col gap-4 items-center justify-center h-full py-20">
        <p class="text-xl text-muted-foreground">
            <span class="text-accent">Project not found!</span>
        </p>
        <a href="/projects" class="text-accent underline underline-offset-2">
            Back to Projects
        </a>
    </div>
{/if}
