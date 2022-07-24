<script context="module">


    class Tabuleiro{
        constructor (altura, largura){
        this.altura = altura;
        this.largura = largura;
    }
}
    const propriedadesTabuleiro = new Tabuleiro (8, 8);

    let corClara = 'rgba(98, 49, 11, 1)'
    let corEscura = 'rgba(237, 180, 136, 1)';

    let tabuleiro = montarTabuleiro (propriedadesTabuleiro);

    function montarTabuleiro (propriedadesTabuleiro){
    
        let item = Array(propriedadesTabuleiro.altura).fill().map(()=>Array(propriedadesTabuleiro.largura).fill());

        for (let i = 0; i < propriedadesTabuleiro.altura; i++){
            for (let j = 0; j < propriedadesTabuleiro.largura; j++){
                if (i % 2 == 0) {
                    j % 2 == 0 ? item[i][j] = true : item[i][j] = false;
                    continue;
                }
                j % 2 == 1 ? item[i][j] = true : item[i][j] = false;
            }
        }
        return item;
    }


</script>

<table>
        {#each tabuleiro as linha, i}
            <tr>
                {#each linha as item, j}
                    <td style="background-color: {item ? corEscura : corClara};"></td>
                {/each}
            </tr>  
        {/each}
</table>
   
