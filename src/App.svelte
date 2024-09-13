<script>
    import CreateUserComponent from "./lib/CreateUserComponent.svelte";
    import {Router, Route, Link} from "svelte-routing";
    import CreatePollComponent from "./lib/CreatePollComponent.svelte";
</script>

<main>
  <Router>
    <nav>
        <ul>

            <li>
                <Link to="/users">Create User</Link>
            </li>
            <li>
                <Link to="/polls">Create Poll</Link>
            </li>
        </ul>
    </nav>
        <Route path="/users" component="{CreateUserComponent}"></Route>
        <Route path="/polls" component="{CreatePollComponent}"></Route>
    </Router>


</main>

<style>

</style>
