<template>
  <div class="container">
    <div class="quiz">
      <div class="quiz-question">
        <span v-html="currentQuestion.question"></span>
      </div>
      <ul class="quiz-answers">
        <li 
          class="quiz-answers__answer" 
          v-for="(answer, index) in mixedAnswers" 
          :key="index"
          @click="selectAnswer(index)"  
          :class="answerClass(index)"
          >
          <span v-html="answer"></span>
        </li>
      </ul>
      <div class="quiz-button">
        <button 
          class="btn submit-btn"
          @click="submitAnswer"
          :disabled="selectedIndex === null || answered"
          >
        Submit
        </button>
        <button 
          class="btn next-btn"
          @click="next"
          :disabled="selectedIndex === null || !answered"  
        >
        Next
        </button>
      </div>
    </div>

  </div>
</template>

<script>
  import _ from 'lodash'

  export default {
    props: {
      currentQuestion: Object,
      next: Function,
      increment: Function
    },

    data() {
      return {
        // user selects an answer
        selectedIndex: null,
        // index of the correct answer
        correctIndex: null,
        // shuffled array of the answers
        mixedAnswers: [],
        // user selects an answer and submit it
        answered: false
      }
    },
    // A watcher is needed here in order to shuffle the right answer among the wrong answers
    // We want the correct answer mixed into the array of all the answers, otherwise it will appear
    // each time at the same place for the user
    // This watcher is called everytime the question is changed. 
    // Instead of making watch a function, it is possible to make it as an objet with a handler
    // immediate => when current question first get passed as prop, it is also running ! nice
    watch: {
      currentQuestion: {
        immediate: true,
        handler() {
          this.selectedIndex = null
          this.shuffleAnswers()
          this.answered = false
        }
      }
    },
    
    computed: {
      answers() {
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
        return answers
      }
    },    

    methods: {
      selectAnswer(index) {
        this.selectedIndex = index
      },

      submitAnswer() {
        let isCorrect = false
        if (this.selectedIndex === this.correctIndex) {
          isCorrect = true
        }
        // One answer has been selected
        this.answered = true
        this.increment(isCorrect)
      },

      // used to shuffle tab's answers in order to avoid to have the right answer always in the same position
      shuffleAnswers() {
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      // using lodash's shuffle
        this.mixedAnswers = _.shuffle(answers)
      // Saving the correct answer from the shuffle array
        this.correctIndex = this.mixedAnswers.indexOf(this.currentQuestion.correct_answer)
      },

      answerClass(index) {
        let answerClass = ''
        if (!this.answered && this.selectedIndex === index) {
          answerClass = 'selected'
        }
        else if (this.answered && this.correctIndex === index) {
          answerClass = 'correct'
        }
        else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
          answerClass = 'incorrect'
        }
        return answerClass
      }
           
    },

    mounted() {
      console.log('the received question from the parent is : ' + this.currentQuestion.question)
    }
  }
</script>

<style lang="scss" scoped>

.container {
  width: 92%;
  margin: 0 auto;
}

.quiz {
  padding: 1rem;
  margin-top: .5rem;
  background-color: rgb(153, 143, 143);
  box-shadow: 10px 23px 48px 6px rgba(0,0,0,0.75);
  -webkit-box-shadow: 10px 23px 48px 6px rgba(0,0,0,0.75);
  -moz-box-shadow: 10px 23px 48px 6px rgba(0,0,0,0.75);
   border-radius: 1rem;
}

.quiz-question {
  font-size: 1.3rem;
  font-weight: bold;
}

.quiz-answers {
  margin-top: 1.5rem;
  list-style-type: none;
  padding-left: 0;
  background: rgb(85, 84, 84);
  color: black;
  font-weight: bold;
  &__answer {
    padding: .5rem 0 .5rem 0;
    margin: .1rem 0 .1rem 0;
    border: 1px solid grey;
    a {
      text-decoration: none;
      color: black;
    }
    &:hover {
      background: #3db5da;
      cursor: pointer;   
    }
  }
}

.quiz-button {
  margin-top: 1.5rem;
}

.btn {
  margin: 0 .5em;
  padding: .6em 1em .6em 1em;
  font-weight: bold;
  font-size: .9em;
  transition: 0.3s;
  &:hover {
    cursor: pointer;

  }
}

button:disabled,
button[disabled]{
  border: 1px solid #999999;
  background-color: #cccccc;
  color: #666666;
}


.next-btn {
  background-color: #C87944;
}

.submit-btn {
  background-color: #80263b;
  color: black;
}

.selected {
  background: #2c89a5;
}

.correct {
  background: rgb(101, 160, 101);
}

.incorrect {
  background: rgb(194, 68, 68);
}

@media only screen and (min-width: 500px) {

  .container {
    width: 60%
  }

  .quiz {
    padding:2rem;
  }

  .quiz-question {
    font-size: 1.6rem;
  }

}


</style>