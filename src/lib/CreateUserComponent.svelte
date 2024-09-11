<script>
    let username;
    let email;

    function createNewUser() {
        fetch("http://localhost:8080/users", {
            method:"POST",
            body: JSON.stringify(
               {username: username, email: email}
            ), headers: {
                "Content-Type":"application/json"
            }
        }).then((response) => {
            if(response.status === 201) {
                alert("User created successfully");
                username = "";
                email = "";
            }
        }).catch((error) => {
            alert(error.message)
        })
    }

</script>

<style>

</style>

<form on:submit|preventDefault={createNewUser}>
    <div>
        <label>Username: </label>
        <input type="text" id="username" bind:value={username}>
    </div>
    <div>
        <label>Email: </label>
        <input type="text" id="email" bind:value={email}>
    </div>
    <button type="submit">Create user</button>
</form>