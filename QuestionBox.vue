<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:header>Vue.js with Bootstrap</template>

      <template v-slot:lead>{{ currentQuestion.question }}</template>

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          v-on:click="selectAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >{{ answer }}</b-list-group-item>
      </b-list-group>

      <b-button variant="primary" v-on:click="submitAnswers">Submit</b-button>
      <b-button v-on:click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answers);
      return answers;
    }
  },
  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: []
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
      console.log(index);
    },
    
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect);
    }
  },

  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswers();
      }
    }
  }
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: black;
  background-color: transparent;
  color: black;
}
.btn {
  margin: 0 5px;
}
.selected {
  background-color: lightblue;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: red;
}
</style>