<template>
  <div>
    <h2>{{ question.text }}</h2>
    <div v-for="option in shuffledOptions" :key="option" >
      <input type="checkbox" @click="selectAnswer(option)">
      <label>{{option}}</label>
    </div>
  </div>
</template>

<script>
export default {
  props: ['question'],
  data() {
    return {
      shuffledOptions: this.shuffle([...this.question.options])
    };
  },
  computed: {

  },
  methods: {
    selectAnswer(option) {
      if (option === this.question.correctAnswer) {
        this.$emit('answer');
      }
    },
    shuffle(array) {
      let currentIndex = array.length;
      let temporaryValue, randomIndex;
      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }
      return array;
    }
  }
};
</script>