<template>
  <div class="questions-container">
    <b-jumbotron class="container">
      <template #lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item 
          v-for="(answer, index) in mixedAnswers" 
          :key="index" 
          @click="selectAnswer(index)"  
          :class="answerClass(index)"
        >
        {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <!-- submit button has to be disabled if no answer has been selected or 1 answer has been selected -->
      <b-button 
        class="submit-btn"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
      >
        Validez
      </b-button>

      <b-button class="next-btn" 
        @click="next"
        :disabled="selectedIndex === null"
      >
        Suivante
      </b-button>
    </b-jumbotron>
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
    // ---------------------------------------------------------------------------
    // Shuffle each next question but not on the first one : 2 ways to resolve this
    // 1- I can call SuffleAnswers() in this mounted() section
    // 2- Or it's easier tu use watch's functionnality as describing it as an object with immediate & handler properties
    // *** immediate **** prop, instead of running the watch function when currentQuestion updates, it 's going to also
    // run when currentQuestion first gets passes as props
    // ---------------------------------------------------------------------------
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

    // Good place to console.log received data from the parent
    mounted() {
      console.log('the received question from the parent is : ' + this.currentQuestion.question)
    }
  }
</script>

<style lang="scss" scoped>

.container {
  background-color: rgb(190, 178, 178);
  box-shadow: 10px 23px 48px 6px rgba(0,0,0,0.75);
  -webkit-box-shadow: 10px 23px 48px 6px rgba(0,0,0,0.75);
  -moz-box-shadow: 10px 23px 48px 6px rgba(0,0,0,0.75);
  border-radius: 1rem;
}
.list-group {
  margin-bottom: 2.5rem;
  
  &-item {
    font-weight: bold;
    &:hover {
      background: #3db5da;
      cursor: pointer;
    }
  }
}

.btn {
  margin: 0 .5rem;
}

.next-btn {
  background-color: #C87944;
}

.submit-btn {
  background-color: #DA5877;
}

.selected {
  background: #3db5da;
}

.correct {
  background: rgb(101, 160, 101);
}

.incorrect {
  background: rgb(194, 68, 68);
}



</style>