<script>

/* --------------- Criação de peças* ------------------ */

    class Tabuleiro{
        constructor (altura, largura){
        this.altura = altura;
        this.largura = largura;
        }
    }
    
    const propriedadesTabuleiro = new Tabuleiro (8, 8);

    let Jogador1 = 'blue'
    let Jogador2 = 'red';
    let tabuleiro = montarTabuleiro (propriedadesTabuleiro);

    function montarTabuleiro (propriedadesTabuleiro){

        let pecas = Array(propriedadesTabuleiro.altura).fill().map(()=>Array(propriedadesTabuleiro.largura).fill());

        for (let i = 0; i < propriedadesTabuleiro.altura; i++){
            for (let j = 0; j < propriedadesTabuleiro.largura; j++){
                if ((i == 0 && j % 2 == 0) || (i == 1 && j % 2 == 1)){
                    pecas[i][j] = Jogador1;
                    continue;
                }
                if ((i == 6 && j % 2 == 0) || (i == 7 && j % 2 == 1)){
                    pecas[i][j] = Jogador2;
                    continue;
                }

                pecas[i][j] = null;
            }
        }
        return pecas;
    }
    
/* --------------- Lógica do jogo* ------------------ */

    let a, b, pecaEscolhida;

    function escolher (x, y) {
        if (pecaEscolhida == null) {
            a = x
            b = y
            pecaEscolhida = tabuleiro[a][b]
            return;
        }

       if (tabuleiro[a][b] == Jogador2) {
            if ((x == a -1) && (y == b + 1 || y == b -1) ){
                if (tabuleiro[x][y] == null){
                    mover(x, y);
                    resetar();
                    return; 
                }
                
            }
            comer(x, y);
            return;
        }

       if (tabuleiro[a][b] == Jogador1) {
            if ((x == a + 1) && (y == b + 1 || y == b -1)){
                if (tabuleiro[x][y] == null){
                    mover(x, y);
                    resetar(); 
                    return; 
                }
            }

            comer(x, y);
            return;
        }
      
    }

    function comer (x, y,) {
        
    }

    function resetar () {
        a = null;
        b = null;
        pecaEscolhida = null;
    }

    function mover (x ,y) {
        tabuleiro[a][b] = null;
        tabuleiro[x][y] = pecaEscolhida;
    }

</script>

<table>
    {#each tabuleiro as linha, i}
        <tr>
            {#each linha as item, j}
                <td style="background-color: {item};" class="{item != null ? 'ocupado' : 'desocupado'}" on:click={()=>escolher(i, j)}></td>
            {/each}
        </tr>  
    {/each}
</table>
