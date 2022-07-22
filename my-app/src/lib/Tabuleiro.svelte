<script context="module">

    class Tabuleiro{
        constructor (altura, largura){
            this.altura = altura;
            this.largura = largura;
        }
    }

    let corbranca = 'white';
    let corPreta = 'black';

    const propriedadesTabuleiro = new Tabuleiro (8, 8);
    var tabuleiro = montarTabuleiro (propriedadesTabuleiro);

    export function montarTabuleiro (propriedadesTabuleiro){

        let tabuleiroCriado = Array(propriedadesTabuleiro.largura).fill().map(()=>Array(propriedadesTabuleiro.altura).fill());

        for (let i = 0; i < propriedadesTabuleiro.altura; i++){
            for (let j = 0; j < propriedadesTabuleiro.largura; j++){
                if (i % 2 == 0) {
                    j % 2 == 0 ? tabuleiroCriado[i][j] = true : tabuleiroCriado[i][j] = false;
                    continue;
                }
                j % 2 == 1 ? tabuleiroCriado[i][j] = true : tabuleiroCriado[i][j] = false;
            }
        }
        return tabuleiroCriado;
    }

</script>

<table style="postion:absolute">
        {#each tabuleiro as linha}
            <tr style="postion:absolute">
                {#each linha as item}
                    <td style="background-color: {item ? corPreta : corbranca};"></td>
                {/each}
            </tr>  
        {/each}
</table>
   

