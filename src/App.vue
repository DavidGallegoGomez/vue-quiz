<template>
  <div id="app">
    <Header />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <question-box 
            :currentQuestion="questions[indexQuestion]" 
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox
  },
  data: () => ({
    questions: [],
    indexQuestion: 0
  }),
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=15&type=multiple', {
      method: 'get'
    })
      .then(response => { return(response.json()) })
      .catch(error => console.log(error))
      .then(jsonData => this.questions = jsonData.results )
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
