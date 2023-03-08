<script setup>
import { ref, computed } from "vue";

const questions = ref([
  {
    question: "Qui a paint ce tableau?",
    painture:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_25745-1.jpg?itok=Qrqw80MA",
    answer: 1,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    Selected: null,
  },
  {
    question: "Qui a paint ce tableau?",
    answer: 2,
    painture:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_25745-1.jpg?itok=Qrqw80MA",
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    Selected: null,
  },
  {
    question: "Qui a paint ce tableau?",
    painture:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_25745-1.jpg?itok=Qrqw80MA",
    answer: 3,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    Selected: null,
  },
  {
    question: "Qui a paint ce tableau?",
    painture:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_25745-1.jpg?itok=Qrqw80MA",
    answer: 4,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    Selected: null,
  },
]);

const quizzCompleted = ref(false);
const currentQuestion = ref(0);
const score = computed(() => {
  let value = 0;
  questions.value.map((q) => {
    if (q.selected == q.answer) {
      value++;
    }
  });
  return value;
});

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value];
  question.index = currentQuestion.value;
  return question;
});

const setAnswer = (evt) => {
  questions.value[currentQuestion.value].selected = evt.target.value;
};

const nextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
  } else {
    quizzCompleted.value = true;
  }
};
</script>

<template>
  <main class="app">
    <h1>Le quizz des musées</h1>
    <section class="quiz">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion.question }}</span>
      </div>
      <img
        src="https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_25745-1.jpg?itok=Qrqw80MA"
        alt="tableau"
      />
      <div class="button-container">
        <button>{{ getCurrentQuestion.options[0] }}</button>
        <button>{{ getCurrentQuestion.options[1] }}</button>
        <button>{{ getCurrentQuestion.options[2] }}</button>
        <button>{{ getCurrentQuestion.options[3] }}</button>
      </div>
    </section>
  </main>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
body {
  background-color: #fff;
  color: black;
}
</style>
