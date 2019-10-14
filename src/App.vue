<template>
  <v-app>
    <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <QuestionBox 
      v-if="questions.length > 0"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
    />

    <v-footer app>
      <span>Jovenes Construyendo el Futuro - CCD</span>
    </v-footer>
    
  </v-app>
</template>

<script>
import Header from "./components/Header";
import QuestionBox from "./components/QuestionBox";

export default {
  components: {
    Header,
    QuestionBox
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=15&type=multiple', {
      method: 'GET'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) => {
      this.questions = jsonData.results
    })
  },
  props: {},
  data: () => ({
    questions: [],
    index: 0,
    numCorrect: 0,
    numTotal: 0
  }),
  methods: {
    next() {
      this.index++
    },
    increment(isCorrect) {
      if(isCorrect) {
        this.numCorrect++
      } 
      this.numTotal++
    }
  },
  created() {
    this.$vuetify.theme.dark = true;
  }
};
</script>
