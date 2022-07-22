<script>
    import { Router, Link, Route } from "svelte-routing";
    import Menu from "./routes/Menu.svelte";
    import Sobre from "./routes/Sobre.svelte";
    import Jogar from "./routes/Jogar.svelte";
  
    export let url = "";
  </script>
  
  <Router url="{url}">
    <nav>
      <Link to="/">Menu</Link>
      <Link to="sobre">Sobre</Link>
      <Link to="jogar">Jogar</Link>
    </nav>
    <div>
      <Route path="/" component="{Menu}" />
      <Route path="jogar" component="{Jogar}" />
      <Route path="sobre" component="{Sobre}" />
      <Route path="/"><Menu /></Route>
    </div>
  </Router>