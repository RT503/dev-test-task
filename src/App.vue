<template>
  <main className="main">
    <div className="questionPage_wrapper">
      <h1 className="questionPage_heading">Тестирование</h1>
      <form className="questionPage_container">
        <fieldset className="questionPage_fieldset">
          <Question :question="currentQuestion" @answer="updateProgress" />
        </fieldset>
      </form>
        <ProgressBar :current-question="currentQuestionIndex" :total-questions="questions.length"/>
    </div>
  </main>
</template>

<script>
import ProgressBar from "@/components/ProgressBar.vue";
import Question from "@/components/Question.vue";
export default {
  components: {ProgressBar, Question},
  data() {
    return {
      questions: [
        {
          text: 'Что такое операционная система?',
          options: ['Это просто программа на компьютере, как и другие - Word или Chrome', 'Это показатель того, какой процессор используется на компьютере. Например, 32-битный или 64-битный', 'Это набор взаимосвязанных программ, осуществляющих управление компьютером и взаимодействие с пользователем', 'Нет такого понятия, есть понятие "файловая система"'],
          correctAnswer: 'Это набор взаимосвязанных программ, осуществляющих управление компьютером и взаимодействие с пользователем'
        },
        {
          text: 'Является ли Android операционной системой?',
          options: ['Да, это такая же ОС, как и другие, просто для мобильных девайсов', 'Нет, операционные системы бывают только для ПК', 'Нет, Android это программа, которая ставится на операционную систему девайса. ОС на разных девайсах разные', 'Это домашняя страничка в настройках вашего браузера'],
          correctAnswer: 'Да, это такая же ОС, как и другие, просто для мобильных девайсов'
        }

      ],
      currentQuestionIndex: 0
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex];

    },

  },
  methods: {
    updateProgress() {
      this.currentQuestionIndex++;
    }
  }

}
</script>


<style>

</style>
