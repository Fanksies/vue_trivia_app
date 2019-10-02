<template>
  <v-app>
    <Header />
    <QuestionBox />

    <v-footer app>
      <span>Trivia App Nonsense</span>
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
  props: {},
  data: () => ({}),
  created() {
    this.$vuetify.theme.dark = true;
  }
};
</script>
