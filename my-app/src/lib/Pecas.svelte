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
    
/* --------------- Movimentação ------------------ */

    let linhaPecaEscolhida, colunaPecaEscolhida, pecaEscolhida;
    let vezJogador2 = true;
    let vezJogador1 = false;
    let comidasJogador1 = 0;
    let comidasJogador2 = 0;

    

    function escolher (x, y) {

        // Guardando linhaPecaEscolhida peça escolhida
            if(tabuleiro[x][y]){
                linhaPecaEscolhida = x;
                colunaPecaEscolhida = y;
                pecaEscolhida = tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida];
                return; 
            }
      
            if ((tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] == damaJogador2) && (vezJogador2)) {
                if (tabuleiro[x][y] == null){
                        moverDamaDirBaixoEsqCima(x, y, Jogador1,damaJogador1,Jogador2);
                        moverDamaEsqCimaDirBaixo(x, y, Jogador1,damaJogador1,Jogador2);
                        moverDamaEsqBaixoDirCima(x, y, Jogador1,damaJogador1,Jogador2);
                        moverDamaDirCimaEsqBaixo(x, y, Jogador1,damaJogador1,Jogador2);
                        return; 
                }
            }else{
                if ((tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] == damaJogador1) && (vezJogador1)) {
                    if (tabuleiro[x][y] == null){

                            moverDamaDirBaixoEsqCima(x, y, Jogador2,damaJogador2,Jogador1);
                            moverDamaEsqCimaDirBaixo(x, y, Jogador2,damaJogador2,Jogador1);
                            moverDamaEsqBaixoDirCima(x, y, Jogador2,damaJogador2,Jogador1);
                            moverDamaDirCimaEsqBaixo(x, y, Jogador2,damaJogador2,Jogador1);
                            return; 
                    }
                }     
            }    

             


      if ((tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] == Jogador2) && (vezJogador2)) {
            if (tabuleiro[x][y] == null){
                if ((x == linhaPecaEscolhida -1) && (y == colunaPecaEscolhida + 1 || y == colunaPecaEscolhida -1) ){
                    mover(x, y);
                    return; 
                }
            }

        
        
          comer(x, y, Jogador1);
          comer(x, y, damaJogador1);
        // 
        } 
            if ((vezJogador1) && (tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] == Jogador1)){
               if (tabuleiro[x][y] == null){
                    if ((x == linhaPecaEscolhida + 1) && (y == colunaPecaEscolhida + 1 || y == colunaPecaEscolhida -1)){
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
        linhaPecaEscolhida = null;
        colunaPecaEscolhida = null;
        pecaEscolhida = null;
    }

    // Mover peça
    function mover (x ,y) {

            tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] = null;
            tabuleiro[x][y] = pecaEscolhida;
            virarDama(x, y);
            resetar(); 
            mudarVez();
        
    }

    // Peças normais comendo peças normais
    function comer (x, y, alvo) {

       if (tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] == Jogador2){
            
                if (x == linhaPecaEscolhida - 2 && y == colunaPecaEscolhida - 2){
                    if (tabuleiro[linhaPecaEscolhida-1][colunaPecaEscolhida-1] == alvo){
                        tabuleiro[linhaPecaEscolhida-1][colunaPecaEscolhida-1] = null;
                        mover(x, y);
                        comidasJogador2++;
                        ganhador();
                        return;
                    }
                }

               if (x == linhaPecaEscolhida - 2 && y == colunaPecaEscolhida + 2){
                    if (tabuleiro[linhaPecaEscolhida-1][colunaPecaEscolhida+1] == alvo){
                        tabuleiro[linhaPecaEscolhida-1][colunaPecaEscolhida+1] = null;
                        mover(x, y);
                        comidasJogador2++;
                        ganhador();
                        return;
                    }
                } 
        }

       if (tabuleiro[linhaPecaEscolhida][colunaPecaEscolhida] == Jogador1){
          if (x == linhaPecaEscolhida + 2 && y == colunaPecaEscolhida - 2){
                if (tabuleiro[linhaPecaEscolhida+1][colunaPecaEscolhida-1] == alvo){
                    tabuleiro[linhaPecaEscolhida+1][colunaPecaEscolhida-1] = null;
                    mover(x, y);
                    comidasJogador1++;
                    ganhador();
                    return;
                }
            }  

                if (x == linhaPecaEscolhida + 2 && y == colunaPecaEscolhida + 2){
                    if (tabuleiro[linhaPecaEscolhida+1][colunaPecaEscolhida+1] == alvo){
                        tabuleiro[linhaPecaEscolhida+1][colunaPecaEscolhida+1] = null;
                        mover(x, y);
                        comidasJogador1++;
                        ganhador();
                        return;
                    }
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
            if (linhaPecaEscolhida < x && colunaPecaEscolhida < y){
                
                if (tabuleiro[linhaPecaEscolhida+i][colunaPecaEscolhida+j] == aliado) {
                    if (aliados == 1){
                        return;
                    }
                    aliados++
                    
                }

                if (tabuleiro[linhaPecaEscolhida+i][colunaPecaEscolhida+j] == inimigo || tabuleiro[linhaPecaEscolhida+i][colunaPecaEscolhida+j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = linhaPecaEscolhida+i;
                    colunaInimigo = colunaPecaEscolhida + j;
                    
                }


            if (aliados < 1 && inimigos <= 1) {
                if (linhaPecaEscolhida+i == x && colunaPecaEscolhida+j == y){
                   mover(x, y);
                   tabuleiro[linhaInimigo][colunaInimigo] = null;
                    if (tabuleiro[x][y] == damaJogador1){
                        comidasJogador1++
                        ganhador();
                    }else if (tabuleiro[x][y] == damaJogador2) {
                        comidasJogador2++
                        ganhador();
                    }
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

            if (linhaPecaEscolhida > x && colunaPecaEscolhida > y){
                if (tabuleiro[linhaPecaEscolhida-i][colunaPecaEscolhida-j] == aliado) {
                    if (aliados == 1) {
                        return;
                    }
                    aliados++
                }

                if (tabuleiro[linhaPecaEscolhida-i][colunaPecaEscolhida-j] == inimigo || tabuleiro[linhaPecaEscolhida-i][colunaPecaEscolhida-j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = linhaPecaEscolhida-i;
                    colunaInimigo = colunaPecaEscolhida - j;
                }

                if (aliados < 1 && inimigos <= 1) {
                   if (linhaPecaEscolhida-i == x && colunaPecaEscolhida-j == y){
                        mover(x, y);
                        tabuleiro[linhaInimigo][colunaInimigo] = null;
                        if (tabuleiro[x][y] == damaJogador1){
                            comidasJogador1++
                            ganhador();
                        }else if (tabuleiro[x][y] == damaJogador2) {
                            comidasJogador2++
                            ganhador();
                        }
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
  
            if (linhaPecaEscolhida < x && colunaPecaEscolhida > y){
                if (tabuleiro[linhaPecaEscolhida+i][colunaPecaEscolhida-j] == aliado) {
                    if (aliados == 1){
                        return;
                    }
                    aliados++
                }

                if (tabuleiro[linhaPecaEscolhida+i][colunaPecaEscolhida-j] == inimigo || tabuleiro[linhaPecaEscolhida+i][colunaPecaEscolhida-j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++;
                    linhaInimigo = linhaPecaEscolhida+i;
                    colunaInimigo = colunaPecaEscolhida - j;
                }

                if (aliados < 1 && inimigos <= 1) {
                    if (linhaPecaEscolhida+i == x && colunaPecaEscolhida-j == y){
                        mover(x, y);  
                        tabuleiro[linhaInimigo][colunaInimigo] = null;
                        if (tabuleiro[x][y] == damaJogador1){
                            comidasJogador1++
                            ganhador();
                        }else if (tabuleiro[x][y] == damaJogador2) {
                            comidasJogador2++
                            ganhador();
                        }
                        return;
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
  
            if (linhaPecaEscolhida > x && colunaPecaEscolhida < y){
                if (tabuleiro[linhaPecaEscolhida-i][colunaPecaEscolhida+j] == aliado) {
                    if (aliados == 1) {
                        return;
                    }
                    aliados++;
                }

                if (tabuleiro[linhaPecaEscolhida-i][colunaPecaEscolhida+j] == inimigo || tabuleiro[linhaPecaEscolhida-i][colunaPecaEscolhida+j] == damaInimigo) {
                    if (inimigos == 1) {
                        return;
                    }
                    inimigos++
                    linhaInimigo = linhaPecaEscolhida-i;
                    colunaInimigo = colunaPecaEscolhida + j;
                }

                if (aliados < 1 && inimigos <= 1) {
                    if (linhaPecaEscolhida-i == x && colunaPecaEscolhida+j == y){
                        mover(x, y);
                        tabuleiro[linhaInimigo][colunaInimigo] = null;
                        if (tabuleiro[x][y] == damaJogador1){
                            comidasJogador1++
                            ganhador();
                        }else if (tabuleiro[x][y] == damaJogador2) {
                            comidasJogador2++
                            ganhador();
                        }                 
                        return;
                    }
                }
                
            }

            i++;
            j++;
        }
    }
    
    function ganhador () {

        if (comidasJogador2 == 8) {
            setInterval(() => {
                alert("Reds venceu!!!");
                location.reload();
            }, 1000);
        }

        if (comidasJogador1 == 8) {
            setInterval(() => {
                alert("Blues venceu!!!");
                location.reload();
            }, 1000);
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