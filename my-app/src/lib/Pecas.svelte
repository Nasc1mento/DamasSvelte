<script>


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
    let tabuleiro = montarTabuleiro (propriedadesTabuleiro);

    function montarTabuleiro (propriedadesTabuleiro){

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
    
/* --------------- Lógica do jogo* ------------------ */

    let a,b, pecaEscolhida;

    function mover (x, y){
       if (pecaEscolhida == null){
        a = x
        b = y
        pecaEscolhida = tabuleiro[a][b]
        return
       }

        tabuleiro[a][b] = null;
        tabuleiro[x][y] = pecaEscolhida;

        pecaEscolhida = null
        a = null
        b = null

        
    }

</script>

<table>
    {#each tabuleiro as linha, i}
        <tr>
            {#each linha as item, j}
                <td style="background-color: {item};" class="{item != null ? 'ocupado' : 'desocupado'}" on:click={()=>mover(i, j)}></td>
            {/each}
        </tr>  
    {/each}
</table>
