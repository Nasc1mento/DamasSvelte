<script>
    import {Item, montadora} from './Fabrica.svelte';

    var corClara = 'rgba(98, 49, 11, 1)'
    var corEscura = 'rgba(237, 180, 136, 1)';

    const propriedadesTabuleiro = new Item (8, 8);
    var tabuleiro = montadora (propriedadesTabuleiro);

</script>

<table class="tabuleiro">
        {#each tabuleiro as linha}
            <tr>
                {#each linha as item}
                    <td style="background-color: {item ? corEscura : corClara};"></td>
                {/each}
            </tr>  
        {/each}
</table>
   

