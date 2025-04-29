<template>
    <div class="questions-ctr">
        <!-- Barra de progresso mostrando porcentagem de perguntas respondidas -->
        <div class="progress">
            <!-- Largura da barra muda dinamicamente com base nas respostas -->
            <div class="bar" :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"></div>
            <!-- Texto exibindo quantas perguntas foram respondidas -->
            <div class="status">
                {{ questionsAnswered }} out of {{ questions.length }} questions answered
            </div>
        </div>

        <!-- Transição para animação entre perguntas -->
        <transition-group name="fade">
        <!-- Itera sobre todas as perguntas -->
        <div 
            class="single-question" 
            v-for="(question, qi) in questions"
            :key="question.q" 
            v-show="questionsAnswered === qi" 
        >
            <!-- Texto da pergunta -->
            <div class="question">{{ question.q }}</div>
            <div class="answers">
                <!-- Itera sobre as respostas da pergunta atual -->
                <div 
                    class="answer" 
                    v-for="answer in question.answers" 
                    :key="answer.text" 
                    @click.prevent="selectAnswer(answer.is_correct)" 
                >
                    {{ answer.text }} <!-- Texto da resposta -->
                </div>
            </div>
        </div>
        </transition-group>
    </div>
</template>

<script>
export default {
    // Recebe as perguntas e o número de perguntas já respondidas como props
    props: ["questions", "questionsAnswered"],
    // Declara que este componente emite o evento "question-answered"
    emits: ["question-answered"],
    methods: {
        // Emite o evento com valor booleano indicando se a resposta estava correta
        selectAnswer(is_correct) {
            this.$emit("question-answered", is_correct);
        }
    }
};
</script>
