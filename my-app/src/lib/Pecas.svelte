<script>
    import { corEscura } from "./Tabuleiro.svelte";
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


        // Guardando a peça escolhida
            if(tabuleiro[x][y]){
                a = x
                b = y
                pecaEscolhida = tabuleiro[a][b]
                return; 
            }
      
            if ((tabuleiro[a][b] == damaJogador2) && (vezJogador2)) {
                if (tabuleiro[x][y] == null){
                        moverDamaDirBaixoEsqCima(x, y, Jogador1,damaJogador1,Jogador2);
                        moverDamaEsqCimaDirBaixo(x, y, Jogador1,damaJogador1,Jogador2);
                        moverDamaEsqBaixoDirCima(x, y, Jogador1,damaJogador1,Jogador2);
                        moverDamaDirCimaEsqBaixo(x, y, Jogador1,damaJogador1,Jogador2);
                        return; 
                }
            }else{
                if ((tabuleiro[a][b] == damaJogador1) && (vezJogador1)) {
                    if (tabuleiro[x][y] == null){

                            moverDamaDirBaixoEsqCima(x, y, Jogador2,damaJogador2,Jogador1);
                            moverDamaEsqCimaDirBaixo(x, y, Jogador2,damaJogador2,Jogador1);
                            moverDamaEsqBaixoDirCima(x, y, Jogador2,damaJogador2,Jogador1);
                            moverDamaDirCimaEsqBaixo(x, y, Jogador2,damaJogador2,Jogador1);
                            return; 
                    }
                }     
            }    

             


      if ((tabuleiro[a][b] == Jogador2) && (vezJogador2)) {
            if (tabuleiro[x][y] == null){
                if ((x == a -1) && (y == b + 1 || y == b -1) ){
                    mover(x, y);
                    return; 
                }
            }

        
        
          comer(x, y, Jogador1);
          comer(x, y, damaJogador1);
        // 
        } 
            if ((vezJogador1) && (tabuleiro[a][b] == Jogador1)){
               if (tabuleiro[x][y] == null){
                    if ((x == a + 1) && (y == b + 1 || y == b -1)){
                        mover(x, y);
                        return; 
                    }  
                }
                comer(x, y, Jogador2); 
                comer(x, y, damaJogador2);
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
    
    function moverDamaEsqCimaDirBaixo (x, y, inimigo, damaInimigo, aliado) {
        
        let i = 1;
        let j = 1;
        let aliados = 0;
        let inimigos = 0;
        let linhaInimigo;
        let colunaInimigo;

        while  (i <= 7 && j <= 7) {
            if (a < x && b < y){
                
                if (tabuleiro[a+i][b+j] == aliado) {
                    if (aliados == 1){
                        return;
                    }
                    aliados++
                    
                }

                if (tabuleiro[a+i][b+j] == inimigo || tabuleiro[a+i][b+j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = a+i;
                    colunaInimigo = b + j;
                    
                }


            if (aliados < 1 && inimigos <= 1) {
                if (a+i == x && b+j == y){
                   mover(x, y);
                   tabuleiro[linhaInimigo][colunaInimigo] = null;
                   console.log([aliados,inimigos])

                    return; 
                }
            }
                
                    
            }

            i++;
            j++;

        }

    }
    
    function moverDamaDirBaixoEsqCima (x, y, inimigo, damaInimigo, aliado) {

        let i = 1;
        let j = 1;
        let aliados = 0;
        let inimigos = 0;
        let linhaInimigo;
        let colunaInimigo;

        while  (i <= 7 && j <=7) {

            if (a > x && b > y){
                if (tabuleiro[a-i][b-j] == aliado) {
                    if (aliados == 1) {
                        return;
                    }
                    aliados++
                }

                if (tabuleiro[a-i][b-j] == inimigo || tabuleiro[a-i][b-j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = a-i;
                    colunaInimigo = b - j;
                }

                if (aliados < 1 && inimigos <= 1) {
                   if (a-i == x && b-j == y){
                        mover(x, y);
                        tabuleiro[linhaInimigo][colunaInimigo] = null;
                        
                        return;
                    } 
                }
                
            }

            i++;
            j++;
        }
        
    }


    function moverDamaEsqBaixoDirCima (x, y, inimigo, damaInimigo, aliado) {
        let i = 1;
        let j = 1;
        let aliados = 0;
        let inimigos = 0;
        let linhaInimigo;
        let colunaInimigo;

        while  (i <= 7 && j <=7) {
  
            if (a < x && b > y){
                if (tabuleiro[a+i][b-j] == aliado) {
                    if (aliados == 1){
                        return;
                    }
                    aliados++
                }

                if (tabuleiro[a+i][b-j] == inimigo || tabuleiro[a+i][b-j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = a+i;
                    colunaInimigo = b - j;
                }

                if (aliados < 1 && inimigos <= 1) {
                    if (a+i == x && b-j == y){
                        mover(x, y);  
                        tabuleiro[linhaInimigo][colunaInimigo] = null;
                   
                    return
                }
                }
                
            }

            i++;
            j++;
        }
    }

    function moverDamaDirCimaEsqBaixo (x, y, inimigo, damaInimigo, aliado) {
        let i = 1;
        let j = 1;
        let aliados = 0;
        let inimigos = 0;
        let linhaInimigo;
        let colunaInimigo;

        while  (i <= 7 && j <=7) {
  
            if (a > x && b < y){
                if (tabuleiro[a-i][b+j] == aliado) {
                    if (aliados == 1) {
                        return;
                    }
                    aliados++
                }

                if (tabuleiro[a-i][b+j] == inimigo || tabuleiro[a-i][b+j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = a-i;
                    colunaInimigo = b + j;
                }

                if (aliados < 1 && inimigos <= 1) {
                    if (a-i == x && b+j == y){
                        mover(x, y);
                        tabuleiro[linhaInimigo][colunaInimigo] = null;
                    
                    return
                }
                }
                
            }

            i++;
            j++;
        }
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