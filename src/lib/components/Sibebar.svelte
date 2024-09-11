<script lang="ts">
    import {
        ActivitySquare,
        CircleUser,
        Instagram,
        Menu,
        Moon,
        Settings,
        Sun,
    } from "lucide-svelte";
    import Logo from "./icons/Logo.svelte";
    import Home from "./icons/Home.svelte";
    import Search from "./icons/Search.svelte";
    import Explore from "./icons/Explore.svelte";
    import Notifications from "./icons/Notifications.svelte";
    import { text } from "@sveltejs/kit";
    import NewPost from "./icons/NewPost.svelte";
    import { cn } from "$lib/utils";
    import * as Dialog from "$lib/components/ui/dialog";
    import Media from "./icons/media.svelte";
    import { Button } from "$lib/components/ui/button";
    import * as Form from "$lib/components/ui/form";
    import * as DropdownMenu from "$lib/components/ui/dropdown-menu";
    import Save from "./icons/Save.svelte";
    import { mode, toggleMode } from "mode-watcher";
    const sidebarItems = [
        {
            text: "home",
            icon: Home,
            href: "/",
        },
        {
            text: "search",
            icon: Search,
        },
        {
            text: "explore",
            icon: Explore,
        },
        {
            text: "messages",
            icon: Notifications,
        },
        {
            text: "create",
            icon: NewPost,
            href: "/",
        },
        {
            text: "profile",
            icon: CircleUser,
            href: "/",
        },
    ];

    let openModal = $state(false);
</script>

<aside
    class="fixed flex h-full min-h-screen w-fit flex-col border-r bg-background p-3 md:w[224]"
>
    <div class="my-8 pl-3">
        <div class="hidden w-fit md:inline-block">
            <Logo />
        </div>

        <Instagram class="md:hidden" />
    </div>

    <div class="flex flex-1 flex-col gap-2">
        {#each sidebarItems as { text, icon, href }}
            <svelte:element
                this={href ? "a" : text === "create" ? "button" : "div"}
                {href}
                role="none"
                class="flex cursor-pointer items-center gap-1 rounded-md p-3 text-sm capitalize hover:bg-muted"
                onclick={() => {
                    if (text === "create") {
                        openModal = true;
                    }
                }}
            >
                <!-- svelte-ignore svelte_component_deprecated -->
                <svelte:component this={icon} />
                <div
                    class={cn("ml-4 hidden md:inline-block", {
                        "font-bold": text === "home",
                    })}
                >
                    {text}
                </div>
            </svelte:element>
        {/each}
    </div>

    <DropdownMenu.Root>
        <DropdownMenu.Trigger
            class="flex cursor-pointer items-center gap-1 rounded-md p-3 text-sm capitalize hover:bg-muted"
            ><Menu />
            <div class="ml-4 hidden md:inline-block">
                more
            </div></DropdownMenu.Trigger
        >
        <DropdownMenu.Content class="w-[300px] rounded-xl p-3 shadow-lg">
            <DropdownMenu.Group>
                <DropdownMenu.Label>My Account</DropdownMenu.Label>
                <DropdownMenu.Separator />
                <DropdownMenu.Item
                    href="/"
                    class="felx cursor-pointer items-center gap-2 p-3"
                >
                    <Settings /> Settings
                </DropdownMenu.Item>
                <DropdownMenu.Item
                    href="/"
                    class="felx cursor-pointer items-center gap-2 p-3"
                >
                    <ActivitySquare /> Your Activity
                </DropdownMenu.Item>
                <DropdownMenu.Item
                    href="/"
                    class="felx cursor-pointer items-center gap-2 p-3"
                >
                    <Save /> Saved
                </DropdownMenu.Item>

                <DropdownMenu.Item
                    class="flex cursor-pointer items-center gap-2 p-3"
                    onclick={toggleMode}
                >
                    {#if $mode === "dark"}
                        <Sun />
                        Light
                    {:else if $mode === "light"}
                        <Moon />
                        Dark Mode
                    {/if}
                </DropdownMenu.Item>

                <DropdownMenu.Item
                    href="/login"
                    class="felx cursor-pointer items-center gap-2 p-3"
                >
                    Logout
                </DropdownMenu.Item>
            </DropdownMenu.Group>
        </DropdownMenu.Content>
    </DropdownMenu.Root>
</aside>

<Dialog.Root bind:open={openModal}>
    <Dialog.Content class="max-w-[450px]">
        <Dialog.Header>
            <Dialog.Title>Create a new post</Dialog.Title>

            <form action="/?/createPost" enctype="multipart/form-data">
                <div class="grid h-fit place-items-center">
                    <div class="absolute space-y-3 text-center">
                        <div class="mx-auto w-fit">
                            <Media />
                        </div>
                        <p>Drag Photos and Videos here</p>
                        <Button size="sm" class="bg-blue-500"
                            >Select from computer</Button
                        >
                    </div>
                    <input
                        class="h-[350px] w-full bg-transparent text-transparent file:hidden"
                        type="file"
                        accept="image/png, image/jpeg"
                        id=""
                        name="imageUrl"
                    />
                </div>
                <!-- error -->

                <!-- <Form.Field {form} name="field">
                    <Form.Control let:attrs>
                      <Form.Label>Label</Form.Label>
                      <input {...attrs} bind:value="{formData.field}" />
                    </Form.Control>
                    <Form.Description>Description</Form.Description>
                    <Form.FieldErrors />
                  </Form.Field>  -->
                <Form.Button class="bg-blue-500">Submit</Form.Button>
            </form>
        </Dialog.Header>
    </Dialog.Content>
</Dialog.Root>
