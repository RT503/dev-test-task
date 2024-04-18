<template>
  <main className="main">
    <div v-if="showQuestions">
      <div className="questionPage_wrapper">
        <h1 className="questionPage_heading">Тестирование</h1>
        <form className="questionPage_container">
          <fieldset className="questionPage_fieldset">
            <div>
              <h2>{{ currentQuestion.text }}</h2>
              <div class="questionPage_question" v-for="(option, index) in currentQuestion.options" :key="index">
                <input :id="'checkbox_' + index" type="checkbox" :checked="this.currentQuestion.isChecked"
                       @click="selectOption(option)">
                <label :for="'checkbox_' + index">{{ option }}</label>
              </div>
            </div>
          </fieldset>
        </form>
        <ProgressBar :total-questions="questions.length" :current-question="currentQuestionIndex"/>
      </div>
    </div>
    <div class="summary" v-else>
      <div v-if="correctAnswers === 10">
        <h2>Поздравляем</h2>
        <p>Вы правильно ответили на все вопросы.
          Вы действительно отлично разбираетесь в IT. </p>
      </div>

      <div v-if="correctAnswers > 0 && correctAnswers < 10 ">
        <h2>Хороший результат!</h2>
        <p>Вы ответили правильно на 5 вопросов.
          Так держать!</p>
      </div>

      <div v-if="correctAnswers === 0">
        <h2>Упс :(</h2>
        <p>Вы неправильно ответили на все вопросы.
          Нужно подучить теорию.</p>
      </div>
      <ul>
        <li v-for="(question, index) in questions" :key="index">
          <div :class="question.correct ? 'correct' : 'incorrect'">
            <h2>{{ question.text }}</h2>
            <p>{{ question.selectedAnswer }}</p>
          </div>
        </li>
      </ul>
    </div>
  </main>
</template>

<script>
import ProgressBar from "@/components/ProgressBar.vue";

export default {
  components: {ProgressBar},
  data() {
    return {
      showQuestions: true,
      currentQuestionIndex: 0,
      correctAnswers: 0,
      questions: [
        {
          text: 'Что такое операционная система?',
          options: ['Это просто программа на компьютере, как и другие - Word или Chrome', 'Это показатель того, какой процессор используется на компьютере. Например, 32-битный или 64-битный', 'Это набор взаимосвязанных программ, осуществляющих управление компьютером и взаимодействие с пользователем', 'Нет такого понятия, есть понятие "файловая система"'],
          correctAnswer: 'Это набор взаимосвязанных программ, осуществляющих управление компьютером и взаимодействие с пользователем',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Является ли Android операционной системой?',
          options: ['Да, это такая же ОС, как и другие, просто для мобильных девайсов', 'Нет, операционные системы бывают только для ПК', 'Нет, Android это программа, которая ставится на операционную систему девайса. ОС на разных девайсах разные', 'Это домашняя страничка в настройках вашего браузера'],
          correctAnswer: 'Да, это такая же ОС, как и другие, просто для мобильных девайсов',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Что такое процессор компьютера?',
          options: ['Это блок, внутри которого находится дисковод и много разъемов для монитора, клавиатуры и компьютерной мышки',
            'Это общее название всех комплектующих компьютера',
            'Это элемент компьютера, с помощью которого обрабатывается информация, находящаяся как в собственной памяти, так и в памяти других устройств',
            'Это суммарный показатель вычислительной мощности компьютера, например 2,7 ГГц'],
          correctAnswer: 'Это элемент компьютера, с помощью которого обрабатывается информация, находящаяся как в собственной памяти, так и в памяти других устройств',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Какие бывают разрядности у современных процессоров?',
          options: ['32 и 64 бита',
            '12 и 32 бита',
            '15 и 32 бита',
            '86 и 64 бита'],
          correctAnswer: '32 и 64 бита',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Какой тип процессора чаще всего используют мобильные девайсы?',
          options: ['iOS использует Intel, остальные используют AMD',
            'Чаще всего используют Intel',
            'Чаще всего используют AMD',
            'Чаще всего используют ARM'],
          correctAnswer: 'Чаще всего используют ARM',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Для чего компьютеру нужна RAM?',
          options: ['Для быстрого доступа к данным',
            'Для долгосрочного хранения данных',
            'Для правильной фрагментации памяти',
            'Для дефрагментации данных'],
          correctAnswer: 'Для быстрого доступа к данным',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Чем отличается HDD от SSD?',
          options: ['HDD - это твердотельный накопитель без подвижных частей. Более дешевый, чем SSD. HDD работает быстрее',
            'HDD - это твердотельный накопитель без подвижных частей. Более дорогой, чем SSD. HDD работает быстрее',
            'SSD - это твердотельный накопитель без подвижных частей. Более дешевый, чем HDD. SSD работает быстрееи',
            'SSD - это твердотельный накопитель без подвижных частей. Более дорогой, чем HDD. SSD работает быстрее'],
          correctAnswer: 'SSD - это твердотельный накопитель без подвижных частей. Более дорогой, чем HDD. SSD работает быстрее',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Как отличаются между собой USB?',
          options: ['Бывают только USB 2.0 и 3.2',
            'Бывают только micro-USB и mini-USB',
            'USB отличаются по пропускной способности (micro-USB, mini-USB, lightning и т.д.) и форме (USB 2.0, USB 3.2)',
            'USB отличаются по форме (micro-USB, mini-USB, lightning и т.д.) и пропускной способности (USB 2.0, USB 3.2)'],
          correctAnswer: 'USB отличаются по форме (micro-USB, mini-USB, lightning и т.д.) и пропускной способности (USB 2.0, USB 3.2)',
          selectedAnswer: null,
          isChecked: false
        },
        {
          text: 'Какой файловой системы не существует?',
          options: ['Fat',
            'NTFS',
            'APFS',
            'BolSFS'],
          correctAnswer: 'BolSFS',
          selectedAnswer: null,
          isChecked: false
        },
      ],
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex];
    },
  },
  methods: {
    selectOption(option) {
      setTimeout(() => {
        this.currentQuestion.selectedAnswer = option;
        this.currentQuestion.correct = (option === this.currentQuestion.correctAnswer);
        console.log(this.currentQuestion.isChecked)

        if (this.currentQuestion.correct) {
          this.correctAnswers++;
        }

        if (this.currentQuestionIndex < this.questions.length - 1) {
          this.currentQuestionIndex++;
        } else {
          this.showQuestions = false;
        }
      }, 20)
    },

  },
  mounted() {
    this.questions.sort(() => Math.random() - 0.5);
    this.questions.forEach(question => {
      question.options.sort(() => Math.random() - 0.5);
    });
  }

}
</script>


<style>

.summary {
  padding: 80px;
}

.correct {
  background-color: #E5F5E1;
}

.incorrect {
  background-color: #FFE0E0;
}
</style>
