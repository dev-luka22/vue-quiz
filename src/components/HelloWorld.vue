<template>
  <div class="container">
    <div class="after"></div>
    <div v-if="currentQuestion < quizData.length">
      <Questions
        :question="quizData[currentQuestion].question"
        :first="quizData[currentQuestion].a"
        :second="quizData[currentQuestion].b"
        :third="quizData[currentQuestion].c"
        :fourth="quizData[currentQuestion].d"
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
          question: "Which of following is NOT JavaScript Data type?",
          a: "Number",
          b: "Boolean",
          c: "Undefined",
          d: "Float",
          correct: "d",
        },
        {
          question: "Who invented JavaScript?",
          a: "Dennis Ritchie",
          b: "James Gosling",
          c: "Brendan Eich",
          d: "Bjarne Stroustrup",
          correct: "c",
        },
        {
          question: "What is Vue?",
          a: "JavaScript framework",
          b: "CSS preprocessor",
          c: "Code editor",
          d: "Game engine",
          correct: "a",
        },
        {
          question:
            "Which symbol is used for multi-line comment in JavaScript?",
          a: "#",
          b: "<!-- -->",
          c: "/* */",
          d: "===",
          correct: "c",
        },
        {
          question: "Which of these is NOT JavaScript variable?",
          a: "var",
          b: "let",
          c: "const",
          d: "new",
          correct: "d",
        },
        {
          question: "What can we achieve with pop() method?",
          a: "Add new item to an array",
          b: "Remove the last element of an array",
          c: "Reverse the order of the elements in an array",
          d: "Fill all the array elements with a static value",
          correct: "b",
        },
        {
          question: "Which method do we use to add a new item in array?",
          a: "splice()",
          b: "fill()",
          c: "push()",
          d: "some()",
          correct: "c",
        },
        {
          question: "{state: true, range: 500} is:",
          a: "Array",
          b: "Object",
          c: "Hash Table",
          d: "Linked List",
          correct: "b",
        },
        {
          question: "What is API?",
          a: "Arranged programming input",
          b: "Assigned processor image",
          c: "Application programming interface",
          d: "Add previous input",
          correct: "c",
        },

        {
          question: "What is DOM?",
          a: "Document object model",
          b: "Documentation of methods",
          c: "Distribution of modals",
          d: "Delivery optimized model",
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
  height: 100vh;
  display: block;
  background-color: rgba(48, 36, 211, 0.253);
}

.button-next {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, 165px);
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
  transform: translate(-50%, -260px);
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

@media only screen and (max-width: 500px) {
  .button-next {
    transform: translate(-50%, 210px);
  }
}
</style>
