<template>
  <div class="container">
    <div class="after"></div>
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
        NEXT
      </button>
      <div class="question-count">
        <h1 class="question-count-title">Question:</h1>
        <p class="question-count-info">
          {{ questionCount + 1 }}/{{ quizData.length }}
        </p>
      </div>
    </div>

    <div v-if="currentQuestion >= quizData.length" class="restart">
      <p class="restart-info">
        You scored {{ trueAnswers }}/{{ quizData.length }}
      </p>
      <button @click="restart" class="button-restart">
        Play Again
      </button>
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
      questionCount: 0,
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
        this.questionCount++;
      } else {
        this.legal = false;
        this.currentQuestion++;
        this.questionCount++;
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
      this.questionCount = 0;
    },
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
  background-image: url("../assets/images/photo.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  overflow: hidden;
}

.after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: block;
  background-color: rgba(48, 36, 211, 0.253);
}

.button-next {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, 140px);
  padding: 10px 30px;
  background-color: rgb(48, 36, 211);
  border: none;
  outline: none;
  color: #ffffff;
  font-family: "Poppins";
  letter-spacing: 1.5px;
  border-radius: 10px;
  font-weight: 700;
  font-size: 16px;
  cursor: pointer;
}

.question-count {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -220px);
}

.question-count-title {
  font-size: 26px;
  text-align: center;
  color: #ffee00;
}

.question-count-info {
  text-align: center;
  color: #ffffff;
  font-size: 22px;
  margin-top: 10px;
}

.restart {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100%;
  position: relative;
}

.restart-info {
  color: #ffee00;
  font-size: 30px;
  margin-bottom: 30px;
  font-weight: 700;
}

.button-restart {
  padding: 10px 30px;
  background-color: #01be01;
  border: none;
  outline: none;
  color: #ffffff;
  font-family: "Poppins";
  letter-spacing: 1.5px;
  border-radius: 10px;
  font-weight: 700;
  font-size: 16px;
  cursor: pointer;
  text-transform: uppercase;
}
</style>
