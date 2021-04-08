<template>
  <div id="app"
    :style="{ backgroundImage: 'url(' + require('@/assets/img/background.jpg') + ')' }"
  >
    <AppHeader 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <!-- Bootstrap's grid system -->
    <b-container class="bv-example-row" >
      <b-row>
        <!-- Bootstrap gives me 12 verticals columns !! 6 means width's half-->
        <b-col sm="6" offset="3">
          <AppQuestions 
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    <!-- Bootstrap's grid system -->
    </b-container>
    
  </div>
</template>

<script>
  import AppHeader from '@/components/AppHeader.vue';
  import AppQuestions from '@/components/AppQuestions.vue';

  export default {
    components: {
      AppQuestions,
      AppHeader
    },

    data() {
      return {
        questions: [],
        index: 0, // index to navigate through all array's questions by clicking the next button
        numCorrect: 0,
        numTotal: 0
      }
    },

    methods: {
      next() {
        this.index++;
      },
      increment(isCorrect) {
        if(isCorrect) {
          this.numCorrect++
        }
        this.numTotal++
      }
    },

    // Sarah Drasner prefers calling APIs in created() lifecycle hook
    mounted: function () {
      fetch('https://opentdb.com/api.php?amount=10&category=29', {
        method: 'get'
      })
        .then((response) => {
          return response.json()
        })
        .then ((jsonData) => {
          this.questions = jsonData.results
        })
    }
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    width: 100%;
    height: 100vh; 
    overflow: hidden;
    background-size: cover !important;
    background: radial-gradient(ellipse at center, rgba(0,0,0,0) 0%, rgba(0,0,0,0) 37%, rgba(0,0,0,0.65) 100%), 
  }
</style>
