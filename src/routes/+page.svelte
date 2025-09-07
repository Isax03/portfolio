<script>
    import { Button } from "$lib/components/ui/button";
    import * as Tooltip from "$lib/components/ui/tooltip";
    import { AtSign, Github, Instagram, Linkedin } from "@lucide/svelte";

    const contacts = [
        {
            name: "GitHub",
            href: "https://github.com/Isax03",
            icon: Github,
        },
        {
            name: "LinkedIn",
            href: "https://www.linkedin.com/in/isaiatonini/",
            icon: Linkedin,
        },
        {
            name: "Gmail",
            href: "mailto:isaia.tonini@gmail.com",
            icon: AtSign,
        },
        {
            name: "Instagram",
            href: "https://www.instagram.com/isa.toni03/",
            icon: Instagram,
        },
    ];
</script>

<div class="flex flex-col w-full h-full items-center justify-center gap-4">
    <div class="flex gap-20 items-center">
        <img
            src="/profile.png"
            alt="Profile"
            class="profile size-60 rounded-full border-2 border-accent"
        />
        <div>
            <h1 class="text-3xl mb-5">
                <span class=" font-bold">Welcome!</span> I'm
                <span class="text-accent">Isaia</span> Tonini
            </h1>
            <p class="text-lg max-w-xl text-muted-foreground mb-3">
                A <span class="text-accent/50">full-stack</span> developer and
                technology enthusiast, passionate about
                <span class="text-accent/50">programming</span>
                and <span class="text-accent/50">software development</span>.
            </p>
            <p class="text-sm max-w-xl text-muted-foreground mb-5">
                Below you can find my contacts! For the rest, you can explore
                the website or download my resume in the resume section.
            </p>
            <div class="flex gap-2 items-center">
                {#each contacts as contact}
                    <Tooltip.Provider>
                        <Tooltip.Root>
                            <Tooltip.Trigger>
                                <Button
                                    variant="outline"
                                    size="icon"
                                    href={contact.href}
                                    target="_blank"
                                >
                                    <contact.icon class="size-4" />
                                </Button>
                            </Tooltip.Trigger>
                            <Tooltip.Content class="z-[99]">
                                <p>{contact.name}</p>
                            </Tooltip.Content>
                        </Tooltip.Root>
                    </Tooltip.Provider>
                {/each}
            </div>
        </div>
    </div>
</div>

<style>
    .profile {
        transition: transform 0.3s ease;
    }
    .profile:hover {
        transform: scale(1.3);
    }
</style>
