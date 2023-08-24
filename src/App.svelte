<script>
  import Router from "svelte-spa-router";
  import Home from "./Home.svelte";
  import Show from "./Show.svelte";
  import Edit from "./Edit.svelte";
  import New from "./New.svelte";
  import Login from "./Login.svelte";
  const routes = {
    // Exact path
    "/": Home,
    "/show/:id": Show,
    "/edit/:id": Edit,
    "/new": New,
    "/login": Login,
  };
</script>

<main>
  <Router {routes} />
</main>
