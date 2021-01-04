<template>
  <div class="container">
    <div v-if="currentQuestion < quizData.length">
      <Questions
        :question="quizData[currentQuestion].question"
        :first="quizData[currentQuestion].a"
        :second="quizData[currentQuestion].b"
        :third="quizData[currentQuestion].c"
        @actionFoo="actionFoo"
        ref="Child"
      />
      <button
        @click="newQuestion"
        v-on:click="$refs.Child.selectItem()"
        class="button-next"
      >
        Next
      </button>
    </div>

    <div v-if="currentQuestion >= quizData.length">
      <p>You scored {{ trueAnswers }}/{{ quizData.length }}</p>
      <button @click="restart">Restart</button>
    </div>
  </div>
</template>

<script>
import Questions from "./Questions";

export default {
  name: "HelloWorld",
  components: {
    Questions,
  },
  data() {
    return {
      currentQuestion: 0,
      trueAnswers: 0,
      legal: false,
      quizData: [
        {
          question: "First?",
          a: "false",
          b: "false",
          c: "true",
          correct: "c",
        },
        {
          question: "Second?",
          a: "false",
          b: "true",
          c: "false",
          correct: "b",
        },
        {
          question: "Third?",
          a: "true",
          b: "false",
          c: "false",
          correct: "a",
        },
      ],
    };
  },
  methods: {
    newQuestion() {
      if (this.legal === true) {
        this.trueAnswers++;
        this.legal = false;
        this.currentQuestion++;
      } else {
        this.legal = false;
        this.currentQuestion++;
      }
    },
    actionFoo(e) {
      if (e === this.quizData[this.currentQuestion].correct) {
        this.legal = true;
      } else if (e !== this.quizData[this.currentQuestion].correct) {
        this.legal = false;
      }
    },
    restart() {
      this.currentQuestion = 0;
      this.trueAnswers = 0;
    },
  },
};
</script>

<style scoped>
.container {
  width: 100%;
}

.container div {
  width: 100%;
}
.button-next {
  display: flex;
  margin: 0 auto;
}
</style>
