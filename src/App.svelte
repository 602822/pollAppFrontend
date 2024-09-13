<script>
    import CreateUserComponent from "./lib/CreateUserComponent.svelte";
    import {Router, Route, Link} from "svelte-routing";
    import CreatePollComponent from "./lib/CreatePollComponent.svelte";
    import HomeComponent from "./lib/HomeComponent.svelte";
</script>

<main>
  <Router>
        <Route path="/users" component="{CreateUserComponent}"></Route>
        <Route path="/polls" component="{CreatePollComponent}"></Route>
        <Route path="/" component="{HomeComponent}"></Route>
    </Router>


</main>

<style>

</style>
