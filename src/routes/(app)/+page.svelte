<script lang="ts">
    import TweetCard from "$lib/components/TweetCard.svelte";

    import Stories from "$lib/components/Stories.svelte";
    import { CircleUser } from "lucide-svelte";
    // let { data } = $props();
</script>

<div class="flex gap-5">
    <div class="flex-1 flex-shrink">
        <div class="mx-auto w-full max-w-[630px]">
            <Stories />
            <div class="mt-5 space-y-5 px-10 md:px-20">
                <!-- {#each data.posts as post}
                    <TweetCard {...post} />
                {/each} -->
                <TweetCard />
            </div>
        </div>
    </div>

    <div class="mx-16 hidden w-[319px] px-3 text-sm xl:inline-block">
        <div class="flex items-center gap-3">
            <CircleUser class="size-11" />
            <div>
                <p class="font-medium">
                    <!--{data.user?.firstName} {data.user?.lastName}-->
                </p>
                <p class="text-muted-foreground"><!--{data.user?.email}--></p>
            </div>
        </div>
        <div class="mb-3 mt-8 flex items-center justify-between">
            <p class="capitalize text-muted-foreground">suggested for you</p>
            <a class="text-xs font-medium" href="/">See All</a>
        </div>
        <div class="space-y-4">
            {#each { length: 5 } as _}
                <div class="flex items-center gap-3">
                    <CircleUser class="size-11" />
                    <div>
                        <p class="font-medium">lawal_adebola</p>
                        <p class="text-muted-foreground">fawaz</p>
                    </div>
                    <a href="/" class="ml-auto text-xs text-blue-500">Follow</a>
                </div>
            {/each}
        </div>
    </div>
</div>
