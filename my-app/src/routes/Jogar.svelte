<script context="module">

    import Tabuleiro  from "../lib/Tabuleiro.svelte";
    import Pecas, {tabuleiro} from '../lib/Pecas.svelte';


    export function mostrar (x, y){


        console.log(tabuleiro[x][y]);

            
    }
</script>


    <div class="mesa">
        <div class = "tabuleiro">
            <Tabuleiro/>
        </div>
        <div class="pecas">
            <Pecas/>   
        </div>
    </div> 




    



