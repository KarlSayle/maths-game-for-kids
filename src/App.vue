<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Maths</span>
        <span class="font-weight-light">Quiz</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <MathQuiz/>
    </v-content>
  </v-app>
</template>

<script>
import MathQuiz from './components/MathQuiz';

export default {
  name: 'App',
  components: {
    MathQuiz,
  },
  data() {
    return {
      //
    };
  },
};
</script>
