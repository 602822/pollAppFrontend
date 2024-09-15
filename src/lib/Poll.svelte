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

    button.upvote {
        background-color: green;
        color: white;
        border: solid black 2px;
        border-radius: 4px;
        font-size: 16px;
        font-family: Arial, serif;
    }

    button.downvote {
        background-color: red;
        color: white;
        border: solid black 2px;
        border-radius: 4px;
        font-size: 16px;
        font-family: Arial, serif;
    }

    span.voteText {
        font-family: Arial, serif;
        font-size: 16px;
        color: blue;
        font-weight: bold;

    }

    span.voteCaption {
        font-family: Arial, serif;
        font-size: 16px;
        font-weight: bold;
    }

    h2.pollQuestion {
        font-family: Arial, serif;
        font-size: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    li.vote {
        margin: 10px;
        padding: 5px;
    }


</style>

<div>

    <h2 class="pollQuestion">{poll.question}</h2>
    <ul>
        {#each poll.options as voteoption}
            <li class="vote">
               <span class="voteCaption"> {voteoption.caption} </span>
                <button class="upvote" on:click={() => upVote(voteoption, poll, index)}>Upvote</button>
                <button class="downvote" on:click={() => downVote(voteoption.presentationOrder, index, poll)}>Downvote</button>
              <span class="voteText"> Votes: {voteoption.numberOfVotes} </span>
            </li>
        {/each}
    </ul>
</div>