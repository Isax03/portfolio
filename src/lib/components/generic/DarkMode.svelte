<script lang="ts">
    import * as Tooltip from "$lib/components/ui/tooltip";
    import { Moon, Sun } from "@lucide/svelte";
    import { mode, toggleMode } from "mode-watcher";
    import { buttonVariants } from "../ui/button";
</script>

<Tooltip.Provider>
    <Tooltip.Root>
        <Tooltip.Trigger onclick={toggleMode} class="cursor-pointer {buttonVariants({ variant: "outline", size: "icon" })}">
            <Sun
                class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
            />
            <Moon
                class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
            />
            <span class="sr-only">Toggle theme</span>
        </Tooltip.Trigger>
        <Tooltip.Content class="z-99">
            <p>
                {mode.current === "dark" ? "Light Mode" : "Dark Mode"}
            </p>
        </Tooltip.Content>
    </Tooltip.Root>
</Tooltip.Provider>
