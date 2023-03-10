<template>
  <h2 class="end-screen">Vous avez finis le quizz!</h2>
  <p class="end-screen">
    Votre score est de {{ score }}/{{ questions.length }}
  </p>
  <div v-if="score >= 5"><p>Bien joué 😃</p></div>
  <div v-else><p>Essaie encore 😉</p></div>
</template>

<script>
export default {
  props: ["score", "question"],
};
</script>
