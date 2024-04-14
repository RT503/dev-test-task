<template>
  <div class="progress_numbers">
    <div>{{ currentQuestion  }} </div>
    <div>{{ totalQuestions }}</div>
  </div>
    <progress class="progress_bar" :value="currentQuestion + 1" :max="totalQuestions" ></progress>

</template>

<script>
export default {
  props: ['totalQuestions', 'currentQuestion']
};
</script>

<style scoped>
.progress_numbers{
  display: flex;
  justify-content: space-between;
}
.progress_bar{
  width: 100%;
}
</style>