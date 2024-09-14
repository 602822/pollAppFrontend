<script>
    export let poll;

</script>

<style>


</style>

<div>

    <h2>{poll.question}</h2>

    <ul>
        {#each poll.options as voteoption}
            <li>
                {voteoption.caption}
                <button>Upvote</button>
                <button>Downvote</button>
            </li>
        {/each}
    </ul>
</div>