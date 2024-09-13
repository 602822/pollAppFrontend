<script>
    let username;
    let email;

    function createNewUser() {
        fetch("http://localhost:8080/users", {
            method: "POST",
            body: JSON.stringify(
                {username: username, email: email}
            ), headers: {
                "Content-Type": "application/json"
            }
        }).then((response) => {
            if (response.status === 201) {
                username = "";
                email = "";
            }
        }).catch((error) => {
            alert(error.message)
        })
    }

</script>

<style>
    input {
        padding: 8px;
        margin-top: 5px;
        margin-bottom: 25px;
        border: 2px solid black;
        border-radius: 5px;

    }

    button {
        background-color: blue;
        border-radius: 4px;
        color:white;
        border: none;
        font-size: 16px;
        font-family: Arial,serif;
        padding: 10px;

    }

    button:hover {
        background-color: dodgerblue;
        cursor: pointer;
    }

div {
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
    font-family: Arial,serif;

}

h1 {
    font-family: Arial,serif;
}
</style>

<div>
    <h1>Create User</h1>
<form on:submit|preventDefault={createNewUser}>
    <label>Username</label>
    <input type="text" name="name" id="username" placeholder="Your username" bind:value={username}>
    <label>Email</label>
    <input type="text" name="email" id="email" placeholder="Your email" bind:value={email}>

    <button type="submit">Create user</button>
</form>
</div>