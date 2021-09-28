<script>
  import { Router, Route, Link } from "svelte-navigator";
  import User from "./User.svelte";
  import Vaccine from "./Vaccine.svelte";
</script>

<Router>
  <header>
    <nav class="flex flex-row justify-center items-center gap-2 bg-gray-300">
      <Link to="/"
        ><h3 class="text-lg text-gray-800 hover:underline">User</h3></Link
      >
      <Link to="vaccine"
        ><h3 class="text-lg text-gray-800 hover:underline">Vaccine</h3></Link
      >
    </nav>
  </header>

  <main>
    <Route path="/">
      <User />
    </Route>

    <Route path="/vaccine">
      <Vaccine />
    </Route>
  </main>
</Router>
