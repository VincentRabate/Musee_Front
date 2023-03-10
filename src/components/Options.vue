<template>
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
</template>

<script>
export default {
  props: [
    "question",
    "index",
    "getCurrentQuestion",
    "SetAnswer",
    "getCurrentImage",
  ],
};
</script>
