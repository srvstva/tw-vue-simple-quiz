<template>
  <div class="w-6/12">
    <div class="text-center">
      <h3
        class="text-5xl text-transparent font-bold bg-gradient-to-tr from-blue-300 to-purple-100 bg-clip-text"
      >
        {{title}}
      </h3>
    </div>
    <div class="card bg-white border shadow p-10 rounded mt-8">
      <div class="mt-4" v-if="!quizCompleted">
        <h4 class="font-semibold">
          {{ questions[index].question }}
        </h4>
        <div
          v-for="(choice, id) in questions[index].choices"
          :key="id + '' + index"
        >
          <label
            :for="id"
            class="block border py-4 px-6 mt-2 rounded"
            :class="{
              'hover:bg-gray-50 cursor-pointer': selectedIndex == '',
              'bg-red-400':
                selectedIndex != '' &&
                selectedIndex == id &&
                id != questions[index].correctIndex,
              'bg-green-400':
                id == questions[index].correctIndex && selectedIndex != '',
            }"
          >
            <input
              type="radio"
              :id="id"
              class="hidden"
              :value="id"
              @change="answered($event)"
              :disabled="selectedIndex != ''"
            />
            {{ choice }}
          </label>
        </div>
        <div class="text-right">
          <button
            v-show="selectedIndex != '' && index < total - 1"
            @click="nextQuestion"
            class="px-4 py-2 mt-4 border rounded bg-blue-600 text-white focus:outline-none hover:bg-blue-700"
          >
            Next
          </button>
          <button
            v-show="selectedIndex != '' && index == total - 1"
            class="px-4 py-2 mt-4 border rounded bg-blue-600 text-white focus:outline-none hover:bg-blue-700"
            @click="showResults"
          >
            Finish
          </button>
        </div>
      </div>
      <div v-else>
        <h2 class="text-bold text-3xl">Results</h2>
        <div class="flex justify-start space-x-4">
          <p>
            Correct Answers:
            <span class="text-2xl text-green-500 font-semibold">{{
              correctAnswers
            }}</span>
          </p>
          <p>
            Wrong Answers:
            <span class="text-2xl text-red-500 font-semibold">{{
              wrongAnswers
            }}</span>
          </p>
        </div>
        <button
          @click="resetQuiz"
          class="px-4 py-2 mt-4 border rounded bg-blue-600 text-white focus:outline-none hover:bg-blue-700"
        >
          Play Again
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "QuizApp",
  props: {
    title: String,
  },
  data() {
    return {
      index: 0,
      questions: [
        {
          question:
            "Grand Central Terminal, Park Avenue, New York is the world's",
          choices: [
            "largest railway station",
            "highest railway station",
            "longest railway station",
            "None of the above",
          ],
          correctIndex: 0,
        },
        {
          question: "Entomology is the science that studies",
          choices: [
            "Behavior of human beings",
            "Insects",
            "The origin and history of technical and scientific terms",
            "The formation of rocks",
          ],
          correctIndex: 1,
        },
        {
          question: "Garampani sanctuary is located at",
          choices: [
            "Junagarh, Gujarat",
            "Diphu, Assam",
            "Kohima, Nagaland",
            "Gangtok, Sikkim",
          ],
          correctIndex: 1,
        },
      ],
      correctAnswers: 0,
      wrongAnswers: 0,
      score: 0,
      total: 3,
      selected: false,
      selectedIndex: "",
      quizCompleted: false,
    };
  },
  methods: {
    nextQuestion: function () {
      this.index++;
      this.selectedIndex = "";
    },
    answered: function (event) {
      this.selectedIndex = event.target.value;
      if (this.selectedIndex == this.questions[this.index].correctIndex)
        this.correctAnswers++;
      else this.wrongAnswers++;
    },
    showResults: function () {
      this.quizCompleted = true;
    },
    resetQuiz: function () {
      this.index = 0;
      this.selectedIndex = 0;
      this.correctAnswers = 0;
      this.wrongAnswers = 0;
      this.quizCompleted = false;
    },
  },
};
</script>

<style scoped>
</style>
