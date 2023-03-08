<script setup>
import { ref, computed } from "vue";

const questions = ref([
  {
    answer: 0,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_25745-1.jpg?itok=Qrqw80MA",
    selected: null,
  },
  {
    answer: 1,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/COG/25917-20.jpg?itok=YLWhV4Vr",
    selected: null,
  },
  {
    answer: 0,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_88075-6.jpg?itok=j0Htx44M",
    selected: null,
  },
  {
    answer: 2,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_72167-1.jpg?itok=V4AS1Q3M",
    selected: null,
  },
  {
    answer: 3,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_48739-2.jpg?itok=xqwsMCVY",
    selected: null,
  },
  {
    answer: 1,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/CAR/lpdp_33933-6.jpg?itok=PS62G2Pr",
    selected: null,
  },
  {
    answer: 3,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_26313-17.jpg?itok=elP5-sDx",
    selected: null,
  },
  {
    answer: 2,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_24769-9.jpg?itok=Xb3mTdd4",
    selected: null,
  },
  {
    answer: 0,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_82935-14.jpg?itok=Q4ciNVQv",
    selected: null,
  },
  {
    answer: 3,
    options: [
      "Gustave Courbet",
      "Élisabeth Vigée Le Brun",
      "Paul Cézanne",
      "Mary Cassat",
    ],
    image:
      "https://apicollections.parismusees.paris.fr/sites/default/files/styles/thumbnail/collections/atoms/images/PPA/lpdp_33870-1.jpg?itok=qpJlcUbx",
    selected: null,
  },
]);

const quizCompleted = ref(false);
const currentQuestion = ref(0);
const score = computed(() => {
  let value = 0;
  questions.value.map((q) => {
    if (q.selected != null && q.answer == q.selected) {
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

const getCurrentImage = computed(() => {
  return questions.value[currentQuestion.value].image;
});

const SetAnswer = (e) => {
  questions.value[currentQuestion.value].selected = e.target.value;
  e.target.value = null;
};

const NextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
    return;
  }

  quizCompleted.value = true;
};
</script>

<template>
  <main class="app">
    <section class="quiz" v-if="!quizCompleted">
      <div class="quiz-info">
        <span class="score">Quizz ({{ score }}/{{ questions.length }})</span>
        <span class="question">Qui a paint cette œuvre ?</span>
      </div>

      <div class="options">
        <img :src="getCurrentImage" class="image" />
        <label
          v-for="(option, index) in getCurrentQuestion.options"
          :key="'option' + index"
          :class="`option ${
            getCurrentQuestion.selected == index
              ? index == getCurrentQuestion.answer
                ? 'correct'
                : 'wrong'
              : ''
          } ${
            getCurrentQuestion.selected != null &&
            index != getCurrentQuestion.selected
              ? 'disabled'
              : ''
          }`"
        >
          <input
            type="radio"
            class="reponses"
            :id="'option' + index"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="SetAnswer"
          />
          <span>{{ option }}</span>
        </label>
      </div>

      <button @click="NextQuestion" :disabled="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length
            ? "Finish"
            : getCurrentQuestion.selected == null
            ? "choisissez une réponse"
            : "question suivante"
        }}
      </button>
    </section>

    <section v-else>
      <h2 class="end-screen">Vous avez finis le quizz!</h2>
      <p class="end-screen">
        Votre score est de {{ score }}/{{ questions.length }}
      </p>
      <div v-if="score >= 6"><p>Pas mal bien joué</p></div>
      <div v-else><p>essaie encore</p></div>
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
  width: 400px;
  height: 872px;
  background-color: #fff;
  color: black;
  background-image: url(./assets/background_app_musee.svg);
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}

.score {
  position: relative;
  top: -16px;
  color: #fff;
  font-size: 1rem;
}

.image {
  height: 100%;
  object-fit: cover;
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  height: 100vh;
}

h1 {
  font-size: 2rem;
  margin-bottom: 2rem;
}

.quiz {
  padding: 1rem;
  width: 100%;
  max-width: 640px;
}

.quiz-info {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.quiz-info .question {
  display: flex;
  color: #fff;
  font-size: 1.25rem;
}

.quiz-info.score {
  color: #fff;
  font-size: 1.25rem;
}

.options {
  margin-bottom: 1rem;
}

.option {
  padding: 0.6rem;
  display: block;
  background-color: #e6e6e6;
  margin-bottom: 0.5rem;
  cursor: pointer;
  font-weight: 600;
}

.option:hover {
  background-color: #c9c7c7;
}

.option.correct {
  border: solid 4px #0aa607;
}

.option.wrong {
  border: solid 4px #a52853;
}

.option:last-of-type {
  margin-bottom: 0;
}

.option.disabled {
  opacity: 0.5;
}

.option input {
  display: none;
}

.end-screen {
  color: #fff;
}

button {
  appearance: none;
  outline: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem 1rem;
  background-color: #15245a;
  color: #fff;
  font-weight: 500;
  text-transform: uppercase;
  font-size: 1.2rem;
}

button:disabled {
  opacity: 0.5;
}

h2 {
  font-size: 2rem;
  margin-bottom: 2rem;
  text-align: center;
}

p {
  color: #8f8f8f;
  font-size: 1.5rem;
  text-align: center;
}
</style>
