<script lang="ts">
    import { page } from "$app/state";
    import { buttonVariants } from "$lib/components/ui/button/button.svelte";
    import * as Sheet from "$lib/components/ui/sheet";
    import * as Tooltip from "$lib/components/ui/tooltip/index";
    import {
        BriefcaseBusiness,
        CodeXml,
        FileUser,
        FolderOpen,
        GraduationCap,
        House,
        Menu,
    } from "@lucide/svelte";
    import { mode } from "mode-watcher";
    import DarkMode from "./DarkMode.svelte";

    const navItems = [
        { href: "/education", label: "Education", icon: GraduationCap },
        { href: "/experience", label: "Experience", icon: BriefcaseBusiness },
        { href: "/skills", label: "Skills", icon: CodeXml },
        { href: "/projects", label: "Projects", icon: FolderOpen },
        { href: "/resume", label: "Resume", icon: FileUser },
    ];

    const currentPath = $derived(page.url.pathname);

    function isActive(href: string) {
        if (href === "/") {
            return currentPath === href;
        }
        return currentPath.startsWith(href);
    }
</script>

<nav
    class="sticky top-0 z-99 w-full h-max py-4 flex items-center justify-between bg-background border-b border-border"
>
    <div class="w-full flex items-center justify-between mx-auto h-max px-4">
        <a href="/" class="flex items-center w-max">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 645.35 800"
                fill={mode.current === "dark" ? "white" : "black"}
                class="size-8 mr-2"
            >
                <polygon
                    points="645.35 275.36 513.92 323.94 339.24 388.51 188.55 444.2 0 513.89 107.92 390.7 107.92 390.68 236.29 363.15 371.22 334.18 535.89 298.85 645.35 275.36"
                />
                <polygon
                    points="450.18 0 256.29 329.18 139.92 354.15 450.18 0"
                />
                <polygon
                    points="475.5 367.8 96.87 800 316.91 426.42 316.91 426.4 475.5 367.8"
                />
            </svg>
            <span class="font-bold text-lg">Isaia Tonini</span>
        </a>

        <div class="items-center justify-between hidden lg:flex lg:w-auto">
            <ul class="flex flex-row space-x-8">
                {#each navItems as item}
                    <li>
                        <a
                            href={item.href}
                            class="flex items-center gap-2 py-2 transition-colors {isActive(
                                item.href
                            )
                                ? 'text-accent font-bold underline underline-offset-6'
                                : 'text-muted-foreground hover:text-primary'}"
                        >
                            <item.icon class="size-4 text-inherit" />
                            {item.label}
                        </a>
                    </li>
                {/each}
            </ul>
        </div>

        <div class="flex items-center justify-end gap-3">
            <DarkMode />

            <div class="block lg:hidden">
                <Sheet.Root>
                    <Sheet.Trigger
                        class={buttonVariants({
                            variant: "outline",
                            size: "icon",
                        })}
                    >
                        <Menu />
                    </Sheet.Trigger>
                    <Sheet.Content side="right" class="w-72 z-100">
                        <Sheet.Header />
                        <div class="flex flex-col gap-4 mx-2 items-start">
                            <Sheet.Close
                                class={buttonVariants({ variant: "link" })}
                            >
                                <a
                                    href="/"
                                    class="flex gap-3 text-lg items-center transition-colors {isActive(
                                        '/'
                                    )
                                        ? 'text-accent font-bold'
                                        : 'text-muted-foreground hover:text-primary'}"
                                >
                                    <House class="size-5 text-inherit" />
                                    Home
                                </a>
                            </Sheet.Close>
                            {#each navItems as item}
                                <Sheet.Close
                                    class={buttonVariants({ variant: "link" })}
                                >
                                    <a
                                        href={item.href}
                                        class="flex gap-3 text-lg items-center transition-colors {isActive(
                                            item.href
                                        )
                                            ? 'text-accent font-bold'
                                            : 'text-muted-foreground hover:text-primary'}"
                                    >
                                        <item.icon
                                            class="size-5 text-inherit"
                                        />
                                        {item.label}
                                    </a>
                                </Sheet.Close>
                            {/each}
                        </div>
                    </Sheet.Content>
                </Sheet.Root>
            </div>
        </div>
    </div>
</nav>
