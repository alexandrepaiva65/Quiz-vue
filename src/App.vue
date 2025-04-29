<template>
    <div class="ctr">

    <!-- Transição com nome "fade" para trocar entre componentes com animação -->
    <transition name="fade" mode="out-in">
        
    <!-- Renderiza o componente "question" enquanto ainda há perguntas a serem respondidas -->
    <question 
        v-if="questionsAnswered < questions.length" 
        :questions = "questions" 
        :questionsAnswered = "questionsAnswered" 
        @question-answered="questionAnswered" 
    />

    <!-- Se todas as perguntas foram respondidas, exibe o componente "result" -->
    <result v-else :results = "results" :totalCorrect = "totalCorrect"/>
    </transition>
    

    <!-- Botão de reset só aparece quando todas as perguntas foram respondidas -->
    <button 
        type="button" 
        class="reset-btn" 
        @click.prevent="reset" 
        v-if="questionsAnswered === questions.length"
    >
        Reset
    </button>
</div>

</template>



<script>
import Question from './components/Question.vue' // Importa o componente de pergunta
import Result from './components/Result.vue' // Importa o componente de resultado

export default {
  name: 'App',
  components: {
    Question, // Declara o componente Question para uso neste componente
    Result // Declara o componente Result para uso neste componente
  },
  data() {
    return {
        questionsAnswered: 0, // Contador de perguntas respondidas
        totalCorrect: 0, // Contador de respostas corretas
        questions: [ // Lista de perguntas do quiz
            {
                q: 'What is 2 + 2?',  // Texto da pergunta
                answers: [ // Opções de resposta
                    {
                        text: '4', // Texto da resposta
                        is_correct: true // Marca se está correta
                    },
                    {
                        text: '3',
                        is_correct: false 
                    },
                    {
                        text: 'Fish',
                        is_correct: false 
                    },
                    {
                        text: '5',
                        is_correct: false 
                    }
                ] 
            },
            { 
                q: 'How many letters are in the word "Banana"?', 
                answers: [
                    {
                        text: '5',
                        is_correct: false
                    },
                    {
                        text: '7',
                        is_correct: false 
                    },
                    {
                        text: '6',
                        is_correct: true 
                    },
                    {
                        text: '12',
                        is_correct: false 
                    }
                ] 
            },
            { 
                q: 'Find the missing letter: C_ke', 
                answers: [
                    {
                        text: 'e',
                        is_correct: false
                    },
                    {
                        text: 'a',
                        is_correct: true 
                    },
                    {
                        text: 'i',
                        is_correct: false 
                    }
                ] 
            },
        ],
        results: [ // Faixas de resultados possíveis com base na pontuação
            {
                min: 0, // Valor mínimo de acertos para este resultado
                max: 2, // Valor máximo de acertos para este resultado
                title: "Try again!", // Título exibido
                desc: "Do a little more studying and you may succeed!" // Descrição exibida
            },
            {
                min: 3,
                max: 3,
                title: "Wow, you're a genius!",
                desc: "Studying has definitely paid off for you!"
            }
        ]
    }
  },
  methods: {
    questionAnswered(is_correct) {
        // Se a resposta estiver correta, incrementa o total de acertos
        if (is_correct) {
            this.totalCorrect++;
        }
        // Incrementa o contador de perguntas respondidas
        this.questionsAnswered++;
    },
    reset() {
        // Reseta os contadores para reiniciar o quiz
        this.questionsAnswered = 0;
        this.totalCorrect = 0;
    }
  },
}

</script>


<style>

</style>
