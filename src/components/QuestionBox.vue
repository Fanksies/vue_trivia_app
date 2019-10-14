<template>
  <v-content>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col class="">
          <v-card class="mx-auto px-7" max-width="500" tile light>
            <v-list
              rounded
            >
              <p class="title mb-4 mt-3 mx-3" v-html="currentQuestion.question">
                
              </p>
              <v-list-item-group 
                color="primary"
                >
              <!-- <v-list-item-group color="primary"> -->
                <v-list-item
                 v-for="(answer, index) in shuffledAnswers" 
                :key="index" 
                @click.prevent="selectAnswer(index)"
                :class="[ 
                        answered && correctIndex === index ? 'success' : 
                        answered && selectedIndex === index && correctIndex !== index ? 'error' : ''
                      ]"
                >
                  <v-list-item-icon>
                    <v-icon>mdi-xbox-controller</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title 
                      v-html="answer"
                      
                    ></v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                
              </v-list-item-group>
              <div class="text-center my-6 d-flex justify-space-between mx-4">
                <v-btn class="deep-purple accent-4" 
                  large 
                  dark
                  :disabled = "selectedIndex === null || answered"
                  @click="submitAnswer"
                >
                  Submit Answer
                </v-btn>
                <v-btn class="primary accent-4" 
                  large 
                  dark
                  @click="next"
                >Next Question</v-btn>
              </div>
            </v-list>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-content>
</template>

<style scoped>
  .v-application .success {
    color:white;
  }
   .v-application .error {
    color:white;
  }
  
</style>
  
<script>
import _ from 'lodash'

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data: () => ({
    selectedIndex: null,
    correctIndex: null,
    shuffledAnswers: [],
    answered: false
  }),
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.answered = false
        this.shuffleAnswers()
      }
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

      this.answered = true

      this.increment(isCorrect)
    },
    shuffleAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    }
    
  },
}
</script>
