<template>
  <v-form v-model="valid">
    <v-container v-if="!ready">
      <v-layout>
        <v-flex xs12 md4>
          <h1>How many questions do you want?</h1>
          <v-text-field
            v-model="quizLength"
            label="Number of questions"
            required
          ></v-text-field>
          <v-btn @click="assignQuizLength" @keyup.enter="assignQuizLength"
            >Start!</v-btn
          >
        </v-flex>
      </v-layout>
    </v-container>
    <v-container v-if="ready">
      <v-layout v-if="isComplete === true">
        Well done!
        <h4>You got {{ correctAnswers }}/{{ quizLength }} right!</h4>
        <v-btn @click="startAgain">Try again?</v-btn>
      </v-layout>
      <v-layout v-if="isComplete === false">
        <v-flex xs12 md4>
          <h1>{{ value1 }} + {{ value2 }} =</h1>
          <v-text-field
            v-model="userAnswer"
            label="Your answer"
            required
          ></v-text-field>
          <v-btn @click="submit" @keyup.enter="submit">Check your answer</v-btn>
          <v-btn @click="nextQuestion" :disabled="userResult == null"
            >Next question</v-btn
          >

          <h2 class="text-danger" v-if="userResult">
            You got it: {{ userResult }}
          </h2>
          <h3>Your score: {{ correctAnswers }}/{{ quizLength }}</h3>
        </v-flex>
      </v-layout>
    </v-container>
  </v-form>
</template>

<script>
export default {
  name: 'MathQuiz',
  data() {
    return {
      valid: false,
      ready: false,
      userAnswer: null,
      userResult: null,
      quizLength: null,
      correctAnswers: 0,
      totalAnsweredQuestions: 0,
    };
  },
  methods: {
    getValue() {
      return Math.floor(Math.random() * 100 + 1);
    },
    assignValues() {
      this.value1 = this.getValue();
      this.value2 = this.getValue();
    },
    getResult() {
      return this.value1 + this.value2;
    },
    submit() {
      if (this.getResult() === Number(this.userAnswer)) {
        this.userResult = 'Right!';
        this.correctAnswers++;
      } else {
        this.userResult = 'Wrong :(';
      }
      this.totalAnsweredQuestions++;
    },
    assignQuizLength() {
      this.ready = true;
    },
    nextQuestion() {
      this.userAnswer = null;
      this.userResult = null;
      this.valid = false;
      this.assignValues();
    },
    startAgain() {
      this.userAnswer = null;
      this.userResult = null;
      this.valid = false;
      this.correctAnswers = 0;
      this.totalAnsweredQuestions = 0;
      this.quizLength = null;
      this.ready = false;
    },
  },
  mounted() {
    this.assignValues();
  },
  computed: {
    isComplete() {
      if (this.totalAnsweredQuestions >= this.quizLength) {
        return true;
      }
      return false;
    },
  },
};
</script>

<style scoped>
.text-danger {
  color: #f84f4f;
}
</style>
