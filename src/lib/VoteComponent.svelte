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

    div.container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
    }

    h2.info {
        font-family: Arial, serif;
        font-size: 15px;
        font-weight: bold;

    }


</style>


{#if errorMessage}
    <p>Error: {errorMessage}</p>
{:else if !result}
    <p>Loading polls......</p>
{:else}
    <div class="container">
    <h2 class="info">Polls will update every 5 seconds</h2>
    {#each result as poll, index}
        <Poll {poll} {username} {index}/>
    {/each}
    </div>
{/if}