<script context="module">

    import Tabuleiro  from "../lib/Tabuleiro.svelte";
    import Pecas from '../lib/Pecas.svelte';


    export function mostrar (x, y, peca, valor){

        if (valor != null){
            console.log(peca[x][y])
        }
            
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




    



