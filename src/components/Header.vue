<template>
    <v-app-bar
      app
      clipped-left
    >
      <v-toolbar-title><b>Trivia App</b></v-toolbar-title>
      <v-toolbar-title class="ml-auto">Score: {{ numCorrect }}/{{ numTotal }} </v-toolbar-title>

    </v-app-bar>
</template>

<script>
  export default {
    props: [
      'numCorrect',
      'numTotal'
    ]
  }
</script>
