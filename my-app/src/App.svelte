<script>
    import { Router, Link, Route } from "svelte-routing";
    import Jogar from "./routes/Jogar.svelte";
    import Sobre from "./routes/Sobre.svelte";
    import Ajuda from "./routes/Ajuda.svelte";
  
    export let url = "";
  </script>
  
  <Router url="{url}">
    <nav>
      <Link to="/">Jogar</Link>
      <Link to="sobre">Sobre</Link>
      <Link to="ajuda">Ajuda</Link>
    </nav>
    <div>
      <Route path="sobre"> <Sobre /></Route>
      <Route path="ajuda"> <Ajuda /></Route>
      <Route path="/"><Jogar /></Route>
    </div>
  </Router>