<script setup lang="ts">
import router from '@/router'
import { computed, ref, watch } from 'vue'

const colors = {
  red: '#F60100',
  grey: '#A8A8A8',
  blue: '#0000A9',
  green: '#00A701',
  yellow: '#FDFF19',
  brown: '#A95403',
  black: '#000000',
  magenta: '#850068',
  cyan: '#46B2AC',
}

const options = {
  sex: ['Мужчина', 'Женщина'],
  age: ['До 18', 'От 18 до 28', 'От 29 до 35', 'От 29 до 35', 'От 36'],
  extra: ["Дом", "Шалаш", "Бунгало", "Скамейка", "Хижина"],
  number: ['62', '48', '74', '57', '60', '77'],
  color: [
    colors.grey, colors.blue, colors.green,
    colors.red, colors.yellow, colors.brown,
    colors.black, colors.magenta, colors.cyan,
  ],
  colorAgain: [
    colors.grey, colors.cyan, colors.brown,
    colors.green, colors.black, colors.red,
    colors.magenta, colors.yellow, colors.blue,
  ],
  city: ['Вашингтон', 'Лондон', 'Париж', 'Нью-Йорк', 'Москва', 'Оттава'],
  figure: ['1', '2', '3', '4'],
  priority: [
    'Наслаждаться каждой минутой проведенного времени',
    'Быть устремленными мыслями в будущее',
    'Учитывать в ежедневной практике прошлый опыт',
  ],
  definition: [
    'Оно остроконечное',
    'Оно устойчиво',
    'Оно-находится в состоянии равновесия',
  ],
  star: ['34', '36', '53', '44', '66', '42'],
}

const currentQuestion = ref<number>(0)
const totalQuestions = Object.keys(options).length
const progressBarOffset = computed(() => {
  const percentage = currentQuestion.value / totalQuestions * 91
  return `${100 - (percentage + 8)}%`
})

const picked = defineModel<number | null>({ default: null })

const nextQuestion = () => {
  currentQuestion.value += 1
  picked.value = null
}

watch(currentQuestion, async (currentQuestion, _oldCurrentQuestion) => {
  if (currentQuestion > totalQuestions - 1) {
    setTimeout(() => router.push("/quiz/results"), 2000)
  }
})
</script>

<template>
  <div class="quiz">
    <Teleport to="#navbar-title">
      <div class="title">
        <img src="@/assets/brain.png" />
        <p>Тест на определение IQ</p>
      </div>
    </Teleport>
    <div class="progress-bar" />
    <div class="question" v-if="currentQuestion == 0">
      <h1>Ваш пол:</h1>
      <div class="options">
        <label
          v-for="(sex, index) in options.sex"
          :for="'sex-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'sex-' + index"
            name="sex" :value="index" v-model="picked"
          />
          <p>{{ sex }}</p>
        </label>
      </div>
    </div>
    <div class="question" v-else-if="currentQuestion == 1">
      <h1>Укажите ваш возраст:</h1>
      <div class="options">
        <label
          v-for="(age, index) in options.age"
          :for="'age-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'age-' + index"
            name="age" :value="index" v-model="picked"
          />
          <p>{{ age }}</p>
        </label>
      </div>
    </div>
    <div class="question" v-else-if="currentQuestion == 2">
      <h1>Выберите лишнее:</h1>
      <div class="options">
        <label
          v-for="(extra, index) in options.extra"
          :for="'extra-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'extra-' + index"
            name="extra" :value="index" v-model="picked"
          />
          <p>{{ extra }}</p>
        </label>
      </div>
    </div>
    <div class="question number-seq" v-else-if="currentQuestion == 3">
      <hgroup>
        <h1>Продолжите числовой ряд:</h1>
        <div class="numbers">
          <p>18</p>
          <p>20</p>
          <p>24</p>
          <p>32</p>
        </div>
      </hgroup>
      <div class="options">
        <label
          v-for="(number, index) in options.number"
          :for="'numbers-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'numbers-' + index"
            name="number" :value="index" v-model="picked"
          />
          <p>{{ number }}</p>
        </label>
      </div>
    </div>
    <div class="question" v-else-if="currentQuestion == 4">
      <h1>Выберите цвет, который сейчас наиболее вам приятен:</h1>
      <div class="color-grid">
        <input
          v-for="(color, index) in options.color"
          :style="{ 'background-color': color }"
          :class="{highlight: (index === picked)}"
          class="color-radio"
          type="radio" name="color" :value="index" v-model="picked"
        />
      </div>
    </div>
    <div class="question" v-else-if="currentQuestion == 5">
      <h1>
        Отдохните пару секунд, еще раз Выберите цвет,
        который сейчас наиболее Вам приятен:
      </h1>
      <div class="color-grid">
        <input
          v-for="(color, index) in options.colorAgain"
          :style="{ 'background-color': color }"
          :class="{highlight: (index === picked)}"
          class="color-radio"
          type="radio" name="color" :value="index" v-model="picked"
        />
      </div>
    </div>
    <div class="question" v-else-if="currentQuestion == 6">
      <h1>Какой из городов лишний?</h1>
      <div class="options">
        <label
          v-for="(city, index) in options.city"
          :for="'city-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'city-' + index"
            name="city" :value="index" v-model="picked"
          />
          <p>{{ city }}</p>
        </label>
      </div>
    </div>
    <div class="question figures" v-else-if="currentQuestion == 7">
      <h1>Выберите правильную фигуру из четырёх пронумерованных.</h1>
      <img src="@/assets/figures.png" />
      <div class="number-row">
        <div
          v-for="(figure, index) in options.figure"
          :class="{highlight: (index === picked)}"
        >
          <label :for="'figure-' + index">
            {{ figure }}
          </label>
          <input
            type="radio" name="figure" :id="'figure-' + index"
            :value="index" v-model="picked"
          />
        </div>
      </div>
    </div>
    <div class="question" v-else-if="currentQuestion == 8">
      <h1>Вам привычнее и важнее:</h1>
      <div class="options">
        <label
          v-for="(priority, index) in options.priority"
          :for="'priority-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'priority-' + index"
            name="extra" :value="index" v-model="picked"
          />
          <p>{{ priority }}</p>
        </label>
      </div>
    </div>
    <div class="question pyramid" v-else-if="currentQuestion == 9">
      <h1>
        Какое определение, по-вашему, больше подходит
        к этому геометрическому изображению:
      </h1>
      <img src="@/assets/pyramid.png" />
      <div class="options">
        <label
          v-for="(definition, index) in options.definition"
          :for="'definition-' + index"
          :class="{highlight: (index === picked)}"
        >
          <input
            class="radio" type="radio"
            :id="'definition-' + index"
            name="extra" :value="index" v-model="picked"
          />
          <p>{{ definition }}</p>
        </label>
      </div>
    </div>
    <div class="question star" v-else-if="currentQuestion == 10">
      <h1>Вставьте подходящее число</h1>
      <img src="@/assets/star.png" />
      <hr />
      <div class="number-row">
        <div
          v-for="(num, index) in options.star"
          :class="{highlight: (index === picked)}"
        >
          <label :for="'star-' + index">
            {{ num }}
          </label>
          <input
            type="radio" name="star" :id="'star-' + index"
            :value="index" v-model="picked"
          />
        </div>
      </div>
    </div>
    <div class="result-loading" v-else-if="currentQuestion == 11">
      <h1>Обработка результатов</h1>
      <img
        class="load-icon"
        src="@/assets/load_icon.svg"
        width="65" height="68"
      />
      <p>
        Определение стиля мышления........... .... ...................................................
      </p>
    </div>
    <template v-if="currentQuestion < totalQuestions">
      <button v-if="picked !== null" @click="nextQuestion">далее</button>
      <button v-else class="disabled">далее</button>
    </template>
    <template v-else>
      <div />
    </template>
  </div>
</template>

<style scoped>
.quiz {
  height: calc(100vh - var(--navbar-height));
  overflow: hidden;

  padding-top: 1rem;
  padding-bottom: 1.5rem;
  padding-left: 1rem;
  padding-right: 1rem;

  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  align-items: center;
  justify-content: space-between;

  background-image: url("@/assets/rain_bk2.png");
  background-repeat: repeat;
  background-size: contain;
  background-position: center;

  position: relative;
  z-index: 0;
}

.quiz::before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #0D0C11BA;
  z-index: -1;
}

.title {
  display: flex;
  column-gap: 0.5rem;
  height: 100%;
  align-items: center;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}

.title img {
  object-fit: contain;
  min-height: 0;
  max-height: 100%;
}

.title p {
  text-transform: uppercase;
  font-family: 'Yeseva One', serif;
  font-size: 12px;
  color: var(--accent);
}

.progress-bar {
  height: 0.75rem;
  width: 100%;
  max-width: 28rem;
  margin-left: 2rem;
  margin-right: 2rem;

  background-color: #F2F3F399;
  border-radius: 9999px;

  flex-shrink: 0;

  position: relative;
}

.progress-bar::before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: v-bind('progressBarOffset');
  background-color: #3BDE7C;
  border-radius: 9999px;
}

.question {
  width: 100%;
  min-height: 0;
  flex-grow: 1;
  overflow-y: scroll;
  overflow-x: visible;
  max-width: 65ch;

  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
  align-items: center;
  justify-content: center;
}

.question h1 {
  font-size: 20px;
  line-height: 24px;
  text-align: center;
  text-wrap: balance;
}

.question img {
  display: block;
  min-height: 100px;
  max-height: 300px;
  max-width: 100%;
  object-fit: contain;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  flex-shrink: 0;
  flex-grow: 1;
  flex-basis: 0;
}

.question .options {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  row-gap: 0.5rem;

  width: 100%;
  min-height: 0;
  flex-shrink: 1;
  flex-grow: 0;
}

.question .options > * {
  flex-basis: 3.5rem;
  flex-shrink: 1;
  min-height: auto;
  padding-left: 2rem;
  padding-right: 2rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;

  background-color: #F2F3F326;

  font-size: 18px;
  line-height: 1.2em;

  display: flex;
  column-gap: 1rem;
  align-items: center;
}

.question .options > .highlight {
  background-color: var(--accent);
  color: #272727;
}

.question .options .radio {
  appearance: none;
  background-color: transparent;
  border-radius: 9999px;
  width: 20px;
  height: 20px;
  border: 1px solid #FFF;
  flex-shrink: 0;
}

.question .options .radio:checked {
  background-color: #2950C2;
  border-color: #272727;
}

.question.number-seq hgroup {
  display: flex;
  flex-direction: column;
  row-gap: 0.5rem;
  align-items: center;
}

.question.number-seq .numbers {
  display: flex;
  column-gap: 1rem;
}

.question .color-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  row-gap: 1rem;
  column-gap: 1rem;
}

.question .color-grid .color-radio {
  width: 75px;
  height: 75px;
  appearance: none;
}

.question .color-grid .color-radio.highlight {
  border: 6px solid var(--accent);
}

.question .number-row {
  display: flex;
}

.question .number-row > * {
  background-color: #fff;
  color: #0D0C11;
  font-size: 20px;
  width: 40px;
  height: 40px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.question .number-row > *.highlight {
  border: 6px solid var(--accent);
}

.question .number-row > * > input {
  appearance: none;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
}

.question.figures .number-row {
  column-gap: 2rem;
}

.question.pyramid h1 {
  font-size: 16px;
  line-height: 1.2em;
}

.question.star {
  width: auto;
  max-width: none;
}

.question.star > * {
  max-width: 65ch;
}

.question.star img {
  max-width: 100%;
  padding-left: 2.5rem;
  padding-right: 2.5rem;
}

.question.star hr {
  height: 4px;
  width: 100vw;
  max-width: none;
  border: none;
  background-color: #F2F3F326;
  margin-bottom: -0.5rem;
}

.question.star .number-row {
  column-gap: 0.5rem;
}

.result-loading {
  display: flex;
  flex-direction: column;
  row-gap: 3rem;
  align-items: center;

  padding-left: 1rem;
  padding-right: 1rem;

  font-size: 14px;
  line-height: 1.2em;

  margin-bottom: 4rem;
}

.result-loading h1 {
  font-size: 23px;
  line-height: 30px;
  text-align: center;
  padding-left: 3rem;
  padding-right: 3rem;
}

.result-loading .load-icon {
  animation: rotate-full 1s steps(12, end) infinite;
}

@keyframes rotate-full {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(-360deg);
  }
}

button {
  background-color: var(--accent);
  border-radius: 9999px;

  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  width: 12rem;

  text-transform: uppercase;
  font-family: "Merriweather", serif;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 0.0625rem;
}

button.disabled {
  background-color: #DADADA;
  box-shadow: inset 0 4px 10px rgb(0 0 0 / 0.25);
  color: #8E8E8E;
}
</style>
