<script context="module">

    import {mostrar} from "../routes/Jogar.svelte";

    class Tabuleiro{
        constructor (altura, largura){
        this.altura = altura;
        this.largura = largura;
        }
    }
    
    const propriedadesTabuleiro = new Tabuleiro (8, 8);

    let corJogador1 = 'blue'
    let corJogador2 = 'red';
    let pecas;
    export let tabuleiro = montarTabuleiro (propriedadesTabuleiro);

    export function montarTabuleiro (propriedadesTabuleiro){

        pecas = Array(propriedadesTabuleiro.altura).fill().map(()=>Array(propriedadesTabuleiro.largura).fill());

        for (let i = 0; i < propriedadesTabuleiro.altura; i++){
            for (let j = 0; j < propriedadesTabuleiro.largura; j++){
                if ((i == 0 && j % 2 == 0) || (i == 1 && j % 2 == 1)){
                    pecas[i][j] = corJogador1;
                    continue;
                }
                if ((i == 6 && j % 2 == 0) || (i == 7 && j % 2 == 1)){
                    pecas[i][j] = corJogador2;
                    continue;
                }

                pecas[i][j] = null;
            }
        }
        return pecas;
    }


</script>

<table>
    {#each tabuleiro as linha, i}
        <tr>
            {#each linha as item, j}
                <td style="background-color: {item};" class="{item != null ? 'ocupado' : 'desocupado'}" on:click={()=>mostrar(i, j)}></td>
            {/each}
        </tr>  
    {/each}
</table>
