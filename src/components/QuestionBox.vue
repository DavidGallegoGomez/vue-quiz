<template>
  <div>
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <p>
        Answers
      </p>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>