<script>
    import { Button } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card";
    import { AtSign, Github, Instagram, Linkedin, Mail, ArrowUpRight } from "@lucide/svelte";

    const contacts = [
        {
            name: "GitHub",
            description: "Check out my projects and contributions",
            href: "https://github.com/Isax03",
            icon: Github,
            username: "@Isax03",
        },
        {
            name: "LinkedIn",
            description: "Connect with me professionally",
            href: "https://www.linkedin.com/in/isaiatonini/",
            icon: Linkedin,
            username: "Isaia Tonini",
        },
        {
            name: "Gmail",
            description: "Send me an email",
            href: "mailto:isaia.tonini@gmail.com",
            icon: AtSign,
            username: "isaia.tonini@gmail.com",
        },
        {
            name: "Instagram",
            description: "Follow me on Instagram",
            href: "https://www.instagram.com/isa.toni03/",
            icon: Instagram,
            username: "@isa.toni03",
        },
    ];
</script>

<div class="flex flex-col w-full h-full items-center py-8 px-4">
    <div class="max-w-4xl w-full">
        <div class="text-center mb-10">
            <h1 class="text-4xl font-bold mb-4">
                <Mail class="inline-block size-10 mr-3 text-accent" />
                Contacts
            </h1>
            <p class="text-lg text-muted-foreground max-w-2xl mx-auto">
                Feel free to reach out to me through any of the following platforms. 
                I'm always open to new opportunities, collaborations, or just a friendly chat!
            </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            {#each contacts as contact}
                <a href={contact.href} target="_blank" rel="noopener noreferrer" class="group">
                    <Card.Root class="h-full transition-all duration-300 hover:border-accent hover:shadow-lg hover:shadow-accent/10">
                        <Card.Header class="flex flex-row items-center gap-4">
                            <div class="p-3 rounded-lg bg-accent/10 text-accent">
                                <contact.icon class="size-6" />
                            </div>
                            <div class="flex-1">
                                <Card.Title class="flex items-center gap-2">
                                    {contact.name}
                                    <ArrowUpRight class="size-4 opacity-0 -translate-y-1 translate-x-1 transition-all group-hover:opacity-100 group-hover:translate-y-0 group-hover:translate-x-0" />
                                </Card.Title>
                                <Card.Description>{contact.username}</Card.Description>
                            </div>
                        </Card.Header>
                        <Card.Content>
                            <p class="text-muted-foreground">{contact.description}</p>
                        </Card.Content>
                    </Card.Root>
                </a>
            {/each}
        </div>
    </div>
</div>
