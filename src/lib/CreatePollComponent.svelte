<script>
    let question;
    let hoursValid;
    let voteOption;
    let voteOptions = [];
    let presentationOrder = 1;



    function addVoteOption() {
        voteOptions.push({caption: voteOption, presentationOrder: presentationOrder++});
        alert("VoteOption: " + voteOption + " added at " + presentationOrder)
        voteOption = "";
    }

    function createNewPoll() {
        fetch("http://localhost:8080/polls", {
            method: "POST",
            body: JSON.stringify(
                {question: question, hoursValid: hoursValid, options: voteOptions}
            ), headers: {
                "Content-Type": "application/json"
            }
        }).then((response) => {
            if (response.status === 201) {
                question = "";
                hoursValid = "";
            }
        }).catch((error) => {
            alert(error.message)
        })
    }


</script>

<style>

    input.input {
        padding: 8px;
        margin-top: 5px;
        margin-bottom: 25px;
        border: 2px solid black;
        border-radius: 5px;

    }

    button.submit-button {
        background-color: blue;
        border-radius: 4px;
        color: white;
        border: none;
        font-size: 16px;
        font-family: Arial, serif;
        padding: 10px;

    }

    button:hover {
        background-color: dodgerblue;
        cursor: pointer;
    }

    div.container {
        display: flex;
        flex-direction: column;
        justify-content: center; /* horizontally centers items*/
        align-items: center; /* vertically centers items */
        height: 100vh;

    }

    form {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    label {
        font-size: 15px;
        font-family: Arial, serif;
        margin-bottom: 5px;

    }

    h1 {
        font-family: Arial, serif;
    }

    div.vote-option {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;

    }

    button.add-button {
        background-color: blue;
        border-radius: 4px;
        color: white;
        border: none;
        font-size: 15px;
        font-family: Arial, serif;
        padding: 5px;
        margin-left: 10px;
        height: 32px;
    }

    input[name="voteinput"] {
        flex-grow: 1;
        margin-right: 10px;
        padding: 8px;
        border: 2px solid black;
        border-radius: 5px;
    }

</style>

<div class="container">
    <h1>Create Poll</h1>
    <form on:submit|preventDefault={createNewPoll}>
        <label>Question</label>
        <input class="input" type="text" name="name" id="username" placeholder="Favourite Food?" bind:value={question}>
        <label>Hours Valid</label>
        <input class="input" type="text" name="email" id="email" placeholder="1" bind:value={hoursValid}>
        <label>Vote Options (minimum 2)</label>
        <div class="vote-option">
            <input type="text" name="voteinput" placeholder="pizza" bind:value={voteOption}>
            <button class="add-button" type="button" on:click={addVoteOption}>Add</button>
        </div>
        <button class="submit-button" type="submit">Create Poll</button>
    </form>
</div>