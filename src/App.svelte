<script>
    import CreateUserComponent from "./lib/CreateUserComponent.svelte";
    import {Router, Route} from "svelte-routing";
    import CreatePollComponent from "./lib/CreatePollComponent.svelte";
    import HomeComponent from "./lib/HomeComponent.svelte";
    import VoteComponent from "./lib/VoteComponent.svelte";
</script>

<main>
  <Router>
        <Route path="/users" component="{CreateUserComponent}"></Route>
        <Route path="/users" component="{CreatePollComponent}"></Route>
        <Route path="/" component="{HomeComponent}"></Route>
        <Route path="/votes" component="{VoteComponent}"></Route>
    </Router>


</main>

<style>

</style>
