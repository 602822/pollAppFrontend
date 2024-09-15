<script>
    import {onMount} from "svelte";
    import Poll from "./Poll.svelte";

    let result = null;
    let errorMessage = null;
    export let username

    async function fetchPolls() {
        try {
            const response = await fetch("http://localhost:8080/polls");
            if (!response.ok) throw new Error("Failed to fetch polls");
            const data = await response.json();
            result = Object.values(data);
        } catch (error) {
            errorMessage = error.message;
        }
    }

    onMount(() => {

        fetchPolls();


        const intervalId = setInterval(fetchPolls, 5000);

        return () => clearInterval(intervalId);
    });


</script>

<style>

</style>


{#if errorMessage}
    <p>Error: {errorMessage}</p>
{:else if !result}
    <p>Loading polls......</p>
{:else}
    <h1>Polls will update every 5 seconds</h1>
    {#each result as poll, index}
        <Poll {poll} {username} {index}/>
    {/each}
{/if}