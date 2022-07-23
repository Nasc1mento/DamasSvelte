<script>
    import {Item, montadora} from './Fabrica.svelte';


   let corPadrao = 'black';

    const quantidadePecas = new Item (3, 8);
    let pecas = montadora (quantidadePecas);

</script>

<table class="pecas">
        {#each pecas as linha}
            <tr>
                {#each linha as item}
                    <td style="background-color: {item ? corPadrao : ''};"></td>
                {/each}
            </tr>  
        {/each}
</table>
   
