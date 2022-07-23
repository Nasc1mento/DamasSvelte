<script context="module">

    export class Item{
        constructor (altura, largura){
            this.altura = altura;
            this.largura = largura;
        }
    }

    export function montadora (propriedadesItem){
        

        let item = Array(propriedadesItem.altura).fill().map(()=>Array(propriedadesItem.largura).fill());

        for (let i = 0; i < propriedadesItem.altura; i++){
            for (let j = 0; j < propriedadesItem.largura; j++){
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

