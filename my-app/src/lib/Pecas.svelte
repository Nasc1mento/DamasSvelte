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
    let damaJogador1 = 'aqua';
    let damaJogador2 = 'fuchsia';
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

    let vezJogador2 = true;
    let vezJogador1 = false;

    function escolher (x, y) {

        // Cancelar escolha da peça - clicando na mesma 2 vezes
        if (x == a && y == b){
            resetar();
            return;
        }

        // Guardando a peça escolhida
        if (pecaEscolhida == null) {
            if(tabuleiro[x][y])
            a = x
            b = y
            pecaEscolhida = tabuleiro[a][b]
            return;
        }

        // 
       if ((tabuleiro[a][b] == Jogador2 || tabuleiro[a][b] == damaJogador2) && (vezJogador2)) {
            if (tabuleiro[x][y] == null){
                if ((x == a -1) && (y == b + 1 || y == b -1) ){
                    mover(x, y);
                    return; 
                }
            }

        
        
          comer(x, y, Jogador1);
          comer(x, y, damaJogador1);
        // 
        } else {
            if (vezJogador1){
               if (tabuleiro[x][y] == null || tabuleiro[a][b] == damaJogador1){
                    if ((x == a + 1) && (y == b + 1 || y == b -1)){
                        mover(x, y);
                        return; 
                    }  
                }
                comer(x, y, Jogador2); 
                comer(x, y, damaJogador2);
            }
                
        }
    }

    function virarDama (x, y) {
        if (tabuleiro[x][y] == Jogador2) {
            if (x == 0){
                tabuleiro[x][y] = damaJogador2;
                return
            }
        }
        if (tabuleiro[x][y] == Jogador1) {
            if (x == 7){
                tabuleiro[x][y] = damaJogador1;
            }
        }
    }

            
    
    // Resetar peça escolhida depois do movimento
    function resetar () {
        a = null;
        b = null;
        pecaEscolhida = null;
    }

    // Mover peça
    function mover (x ,y) {
        tabuleiro[a][b] = null;
        tabuleiro[x][y] = pecaEscolhida;
        virarDama(x, y);
        resetar(); 
        mudarVez();
    }

    // Peças normais comendo peças normais
    function comer (x, y, alvo) {
        if (x == a - 2 && y == b - 2){
            console.log('entrei1')
            if (tabuleiro[a-1][b-1] == alvo){
                tabuleiro[a-1][b-1] = null;
                mover(x, y);
                return;
            }
        }

        if (x == a + 2 && y == b - 2){
            console.log('entrei2')
            if (tabuleiro[a+1][b-1] == alvo){
                tabuleiro[a+1][b-1] = null;
                mover(x, y);
                return;
            }
        }

        if (x == a - 2 && y == b + 2){
            console.log('entrei3')
            if (tabuleiro[a-1][b+1] == alvo){
            
                tabuleiro[a-1][b+1] = null;
                mover(x, y);
                return;
            }
        }

        if (x == a + 2 && y == b + 2){
            if (tabuleiro[a+1][b+1] == alvo){
            
                tabuleiro[a+1][b+1] = null;
                mover(x, y);
                return;
            }
        }
    }

    function mudarVez (){
        vezJogador1= !vezJogador1;
        vezJogador2 = !vezJogador2;
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

<h1>{vezJogador1 == true ? 'Blues':'Reds'}</h1>