<script>
    import { Button } from "$lib/components/ui/button";
    import { ArrowRight, Mail } from "@lucide/svelte";
</script>

<div class="flex flex-col w-full h-full items-center justify-center gap-4">
    <div class="flex flex-col lg:flex-row gap-12 items-center">
        <img
            src="/profile.png"
            alt="Profile"
            class="profile size-40 lg:size-60 rounded-full mt-10 lg:mt-0"
        />
        <div class="text-center lg:text-left px-4 pb-5">
            <h1 class="text-3xl mb-5">
                <span class=" font-bold">Welcome!</span> I'm
                <span class="text-accent">Isaia</span> Tonini
            </h1>
            <p class="text-lg max-w-xl text-muted-foreground mb-3">
                A <span class="dark:text-accent/50 text-accent">full-stack</span> developer and
                technology enthusiast, passionate about
                <span class="dark:text-accent/50 text-accent">programming</span>
                and <span class="dark:text-accent/50 text-accent">software development</span>.
            </p>
            <p class="text-sm max-w-xl text-muted-foreground mb-5">
                Feel free to explore the website, download my resume, or get in touch with me!
            </p>
            <div class="flex gap-3 items-center justify-center lg:justify-start flex-wrap">
                <Button href="/contacts" class="gap-2">
                    <Mail class="size-4" />
                    Contact me
                </Button>
                <Button href="/resume" variant="outline" class="gap-2">
                    View Resume
                </Button>
            </div>
        </div>
    </div>
</div>

<style>
    .profile {
        transition: transform 0.3s ease;
		box-shadow: 0 0 15px var(--accent);
    }
    .profile:hover {
        transform: scale(1.3);
    }
</style>
