<script>
    import { Router, Route } from "svelte-routing";
    import Home from "./routes/Home.svelte";
</script>

<Router>
    <Route path="/" component={Home} />
</Router>

<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
    }
</style>
