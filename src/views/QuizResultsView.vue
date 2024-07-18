<script setup lang="ts">
import { Teleport } from 'vue'
import { ref } from 'vue'

const countdown = ref<number>(10 * 60)

const doCountdown = () => {
  setTimeout(() => {
    if (countdown.value > 0) {
      countdown.value -= 1
      doCountdown()
    }
  }, 1000)
}

doCountdown()

interface Data {
  name: string,
  height: string,
  mass: string,
  hair_color: string,
  skin_color: string,
  eye_color: string,
  birth_year: string,
  gender: string,
}
const data = ref<Data | null>(null)
const call = async () => {
  data.value = null
  const response = await fetch('https://swapi.dev/api/people/1/')
  data.value = await response.json() as Data
}
</script>

<template>
  <div class="results-page">
    <Teleport to="#navbar-title">
      <div class="title">
        <img src="@/assets/brain.png" />
        <p>Готово!</p>
      </div>
    </Teleport>
    <div class="content">
      <h1>Ваш результат рассчитан:</h1>
      <p class="result">
        <em>Вы относитесь к 3%</em> респондентов, чей уровень
        интеллекта более чем на 
        15 пунктов отличается от среднего в большую или меньшую сторону! 
      </p>
      <p class="callout">Скорее получите свой результат!</p>
      <div class="info">
        В целях защиты персональных 
        данных результат теста, их подробная интерпретация и рекомендации
        доступны в виде голосового сообщения по звонку с
        вашего мобильного телефона
      </div>
      <div class="call">
        Звоните скорее, запись доступна всего
        <span class="timer">
          {{
            Math.floor(countdown / 60)
          }}:{{
            `${countdown % 60}`.padStart(2, '0')
          }}
        </span>
        минут
      </div>
      <button class="call-button" @click="call()">
        <img src="@/assets/call.svg" width="29" height="29" />
        <p>Позвонить и прослушать результат</p>
      </button>
      <div
        v-if="data !== null"
        class="call-response-modal"
        @click="data = null"
      >
        <table>
          <tr>
            <th>Имя</th>
            <td>{{ data.name }}</td>
          </tr>
          <tr>
            <th>Рост</th>
            <td>{{ data.height }}</td>
          </tr>
          <tr>
            <th>Вес</th>
            <td>{{ data.mass }}</td>
          </tr>
          <tr>
            <th>Цвет волос</th>
            <td>{{ data.hair_color }}</td>
          </tr>
          <tr>
            <th>Цвет кожи</th>
            <td>{{ data.skin_color }}</td>
          </tr>
          <tr>
            <th>Цвет глаз</th>
            <td>{{ data.eye_color }}</td>
          </tr>
          <tr>
            <th>Год рождения</th>
            <td>{{ data.birth_year }}</td>
          </tr>
          <tr>
            <th>Пол</th>
            <td>{{ data.gender }}</td>
          </tr>
        </table>
      </div>
      <footer>
        TERMENI SI CONDITII: ACESTA ESTE UN SERVICIU DE DIVERTISMENT.
        PRIN FOLOSIREA LUI DECLARATI CA AVETI 18 ANI IMPLINITI,
      </footer>
      <img class="decoration right" src="@/assets/lightning.png" />
      <img class="decoration left" src="@/assets/lightning.png" />
    </div>
  </div>
</template>

<style scoped>
.results-page {
  height: calc(100vh - var(--navbar-height));
  overflow-x: hidden;
  overflow-y: scroll;

  padding-top: 1.5rem;
  padding-left: 1.5rem;
  padding-right: 1.5rem;

  background-image: url("@/assets/rain_bk2.png");
  background-repeat: repeat;
  background-size: contain;
  background-position: center;

  text-align: center;
  text-wrap: balance;

  position: relative;
  z-index: 0;
}

.results-ready::before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #0D0C11BA;
  z-index: -1;
}

.results-page .decoration {
  position: absolute;
  width: 165px;
  height: 165px;
  z-index: -1;
  transform: rotate(-53.15deg);
}

.results-page .decoration.left {
  bottom: 20%;
  left: -5.5rem;
}

.results-page .decoration.right {
  bottom: 10%;
  right: -7rem;
}

.content {
  display: flex;
  flex-direction: column;
  row-gap: 0.75rem;
  align-items: center;

  max-width: 65ch;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
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
  font-size: 20px;
  letter-spacing: 2px;
  color: var(--accent);
}

h1 {
  text-transform: uppercase;
  font-size: 16px;
  font-weight: bold;
  letter-spacing: 2px;
}

.result {
  font-size: 14px;
  line-height: 18px;
}

.result em {
  text-decoration: underline;
}

.callout {
  color: #3BDE7C;
  text-transform: uppercase;
  font-size: 18px;
  font-weight: bold;
  letter-spacing: 1px;
  line-height: 22px;
}

.info {
  background-color: #1C2741;
  border-radius: 6px;
  padding: 1rem;
  margin-left: 1rem;
  margin-right: 1rem;

  font-family: 'Roboto', sans-serif;
  font-size: 8px;
  font-weight: 500;
  letter-spacing: 2px;
  line-height: 14px;
  text-transform: uppercase;
}

.call {
  color: #3BDE7C;
  font-size: 11px;
  letter-spacing: 1px;
}

.call .timer {
  font-size: 20px;
}

.call-button {
  background-color: #EB1B00;
  border-radius: 5px;

  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
  padding-left: 1rem;
  padding-right: 1rem;

  display: flex;
  column-gap: 1rem;
  align-items: center;
}

.call-button > p {
  font-family: 'Roboto', sans-serif;
  font-weight: 900;
  font-size: 15px;
  color: #fff;
  text-align: start;
}

footer {
  margin-top: auto;
  margin-bottom: calc(-9px - 1rem);
  padding-top: 1rem;
  padding-bottom: 1rem;
  max-width: 285px;

  font-family: Roboto, sans-serif;
  font-size: 7px;
  line-height: 9px;
  letter-spacing: 3px;
  color: #FFFFFF88;
}

.call-response-modal {
  color: #000;
  font-family: Roboto, sans-serif;
  font-size: 14px;
  line-height: 18px;

  background-color: #F3F3F2;
  border-radius: 6px;
  padding: 1rem;

  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  align-items: center;
}

.call-response-modal table {
  border-collapse: collapse;
  table-layout: auto;
}

.call-response-modal th,
.call-response-modal td {
  border: 1px solid #000;
  padding: 0.5rem;
}

.call-response-modal th {
  text-align: left;
}
</style>
