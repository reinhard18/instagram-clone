<script lang="ts">
    import Sibebar from "$lib/components/Sibebar.svelte";
    

    let { children} = $props();
</script>



        <Sibebar/>
       
    <div class="ml-[80px] py-8 md:ml-[244px]">{@render children()} </div>

