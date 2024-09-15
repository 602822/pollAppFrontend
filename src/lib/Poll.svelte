<script>
    export let poll;
    export let username;
    export let index;

    function upVote(voteoption, poll, pollId) {
        fetch(`http://localhost:8080/users/${username}/votes`, {
            method: "POST",
            body: JSON.stringify(
                {
                    option: {caption: voteoption.caption, presentationOrder: voteoption.presentationOrder},
                    pollId: index,
                    voteOptionId: voteoption.presentationOrder
                }
            ), headers: {
                "Content-Type": "application/json"
            }
        }).then((response) => {
            if (response.ok) {
                alert("successfully voted on " + voteoption.caption)
            }
        }).catch((error) => {
            alert(error.message)
        })


        fetch(`http://localhost:8080/polls/${pollId}/${voteoption.presentationOrder}/increase`, {
            method: "PUT",
            body: JSON.stringify(poll), headers: {
                "Content-Type": "application/json"
            }
        }).then((response) => {
            if (response.ok) {
                alert("Vote successfully increased");
            }
        }).catch((error) => {
            alert(error.message)
        })
    }

    function downVote(voteOptionId, pollId, poll) {
        fetch(`http://localhost:8080/users/${username}/votes/${pollId}/${voteOptionId}`, {
            method: "DELETE",
        }).then((response) => {
            if (response.ok) {
                alert("successfully deleted vote");
            }
        }).catch((error) => {
            alert(error.message)
        })

        fetch(`http://localhost:8080/polls/${pollId}/${voteOptionId}/decrease`, {
            method: "PUT",
            body: JSON.stringify(poll), headers: {
                "Content-Type": "application/json"
            }
        }).then((response) => {
            if (response.ok) {
                alert("Vote successfully decreased");
            }
        }).catch((error) => {
            alert(error.message)
        })
    }




</script>

<style>


</style>

<div>

    <h2>{poll.question}</h2>

    <ul>
        {#each poll.options as voteoption}
            <li>
                {voteoption.caption}
                <button on:click={() => upVote(voteoption, poll, index)}>Upvote</button>
                <button on:click={() => downVote(voteoption.presentationOrder, index, poll)}>Downvote</button>
                Votes: {voteoption.numberOfVotes}
            </li>
        {/each}
    </ul>
</div>