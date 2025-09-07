<script lang="ts">
    import { page } from "$app/state";
    import Button, {
        buttonVariants,
    } from "$lib/components/ui/button/button.svelte";
    import * as Sheet from "$lib/components/ui/sheet";
    import * as Tooltip from "$lib/components/ui/tooltip/index";
    import { BriefcaseBusiness, CodeXml, FileUser, FolderOpen, Github, GraduationCap, Menu } from "@lucide/svelte";
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
            <img
                src={mode.current === "dark"
                    ? "/favicon-dark.svg"
                    : "/favicon-light.svg"}
                alt="Logo"
                class="size-8 mr-2"
            />
            <span class="font-bold text-lg">Isaia Tonini</span>
        </a>

        <div class="items-center justify-between hidden md:flex md:w-auto">
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
            <Tooltip.Provider>
                <Tooltip.Root>
                    <Tooltip.Trigger>
                        <DarkMode />
                    </Tooltip.Trigger>
                    <Tooltip.Content class="z-[99]">
                        <p>
                            {mode.current === "dark"
                                ? "Light Mode"
                                : "Dark Mode"}
                        </p>
                    </Tooltip.Content>
                </Tooltip.Root>
            </Tooltip.Provider>

            <div class="block md:hidden">
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
                        <Sheet.Header>
                            <Sheet.Title>Menu</Sheet.Title>
                        </Sheet.Header>
                        <div class="flex flex-col gap-4 mt-4 items-start">
                            {#each navItems as item}
                                <Sheet.Close
                                    class={buttonVariants({ variant: "link" })}
                                >
                                    <a
                                        href={item.href}
                                        class="flex gap-2 items-center py-2 transition-colors {isActive(
                                            item.href
                                        )
                                            ? 'text-accent font-bold underline underline-offset-6'
                                            : 'text-muted-foreground hover:text-primary'}"
                                    >
										<item.icon class="size-4 text-inherit" />
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
