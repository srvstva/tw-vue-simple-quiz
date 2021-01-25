<template>
  <div id="app" class="h-screen w-full bg-blue-900 flex items-center justify-center text-gray-600">
    <quiz-app title="Vue Quiz Master"/>
  </div>
</template>

<script>
import QuizApp from './components/QuizApp.vue'

export default {
  name: 'App',
  components: {
    QuizApp
  }
}
</script>

<style>
</style>
