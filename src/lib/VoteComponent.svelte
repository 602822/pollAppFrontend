<script>
    import {onMount} from "svelte";
    import Poll from "./Poll.svelte";
    let result = null;
    let errorMessage = null;


    onMount(async () => {
        try {
            const response = await fetch("http://localhost:8080/polls");
            if (!response.ok) throw new Error("Failed to fetch polls")
            const data = await response.json();
            result = Object.values(data);
        } catch (error) {
            errorMessage = error.message;
        }
    })


</script>

<style>

</style>

{#if errorMessage}
    <p>Error: {errorMessage}</p>
{:else if !result}
    <p>Loading polls......</p>
{:else}
    {#each result as poll}
        <Poll {poll}/>
    {/each}
{/if}