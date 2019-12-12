<template>
  <div>
    <b-jumbotron>
      <template v-slot:lead>{{ currentQuestion.question }}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in currentAnswers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="nextQuestion" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash';
export default {
  props: {
    currentQuestion: Object,
    nextQuestion: Function
  },
  data: () => ({
    selectedIndex: null, // No se pone cero para que no se marque por defecto la primera respuesta
    shuffleAnswers: []
  }),
  computed: {
    currentAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      console.table(answers);
      return answers;
    }
  },
  watch: {
    /* currentQuestion () {
      this.selectedIndex = null
      this.shuffleAnswers()
    } */
    currentQuestion: {
      inmediate: true,
      handler () {
        this.selectedIndex = null
        this.shuffleAnswers() 
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index
    },
    shuffleAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answers];
      this.shuffleAnswer = _.shuffle(answers)
    }
  },
  mounted() {
    this.shuffleAnswers();
    console.log(
      "%c%s",
      "color: blue; font-size: 14px",
      "currentQuestion",
      this.currentQuestion
    );
  }
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}

.list-group-item:hover {
  background-color: #eee;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background-color: lightblue;  
}

.correct {
  background-color: green;  
}

.incorrect {
  background-color: red;  
}
</style>