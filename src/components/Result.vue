<template>

    <div class="result">
        <!-- Exibe o título do resultado correspondente -->
        <div class="title">{{ results[resultIndex].title }}</div>
        <!-- Exibe a descrição do resultado correspondente -->
        <div class="desc">{{ results[resultIndex].desc }}</div>
    </div>

</template>

<script>
export default {
    // Recebe os resultados possíveis e o total de acertos como props
    props: ["results", "totalCorrect"],
    computed: {
        // Computa o índice do resultado que corresponde ao total de acertos
        resultIndex() {
            let index = 0;
            
            // Percorre a lista de resultados e verifica em qual faixa o total se encaixa
            this.results.forEach((e,i) => {
                if (e.min <= this.totalCorrect && e.max >= this.totalCorrect) {
                    index = i; // Define o índice correspondente
                }
            });
            return index;
        }
    },
    
};
</script>
