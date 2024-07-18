<script setup lang="ts">
  import StartTestButton from '@/components/StartTestButton.vue'
</script>

<template>
  <main>
    <div class="hero">
      <div class="content">
        <div class="center">
          <hgroup>
            <p>Пройдите точный и быстрый</p>
            <h1>тест на определение IQ</h1>
          </hgroup>
          <div class="brain">
            <img src="@/assets/brain.png" />
          </div>
          <div class="catch">
            <StartTestButton />
            <p class="description">
              <span class="accented">
                И получите рекомендации 
                по развитию своего интеллекта 
              </span>
              и улучшению финансового благосостояния и личной жизни
            </p>
          </div>
        </div>
        <div class="more">
          <img src="@/assets/arrow-up.svg" width="16" height="16" />
          <p>Подробнее</p>
        </div>
      </div>
    </div>
    <div class="quote">
      <div class="content">
        <img class="quote-mark top" src="@/assets/quote_open.svg" />
        <p>
          Профессиональный IQ-тест позволяет не только определить коэффициент вашего 
          интеллекта,  но и выработать список рекомендаций для повышения этого 
          показателя. 
        </p>
        <img class="quote-mark bottom" src="@/assets/quote_close.svg" />
      </div>
    </div>
    <div class="benefits">
      <div class="content">
        <p>
          Также по результатам теста
          <em>вы получите</em> подробные
          <em>советы</em> по определению наиболее перспективной
          <em>для вашего типа</em> <strong>интеллекта </strong>
          <em>сферы деятельности,</em>
          которая принесет вам скорейший финансовый результат.
        </p>
        <div class="btn-img">
          <img src="@/assets/intellect_types.png" />
          <StartTestButton class="button" />
        </div>
      </div>
    </div>
    <div class="benefits-2">
      <div class="content">
        <div class="text">
          <p>
            Прохождение теста займет у вас не более <em>12 минут</em>,
            а его <strong>результаты</strong>
            вы сможете <em>использовать всю жизнь.</em>
          </p>
          <div class="panel">
            Профессиональная интерпретация и детально
            <strong>проработанные рекомендации</strong>
            позволят вам качественно
            <strong>изменить все аспекты своей жизни:</strong>
            от финансового до любовного.      
          </div>
        </div>
        <StartTestButton class="button" theme="outlined" />
        <footer class="copyright">
          <img src="@/assets/copyright.svg" />
          2019
        </footer>
        <img class="decoration right" src="@/assets/lightning.png" />
        <img class="decoration left" src="@/assets/lightning.png" />
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  overflow-y: scroll;
  overflow-x: hidden;
}

.content {
  max-width: 65ch;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
}

.hero {
  height: calc(100vh - var(--navbar-height));

  padding-top: 1.5rem;
  padding-bottom: 1rem;

  background-image: url("@/assets/rain_bk2.png");
  background-repeat: repeat;
  background-size: contain;
  background-position: top;

  text-align: center;
  text-wrap: balance;

  position: relative;
  z-index: 0;
}

.hero .content {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  align-items: center;
}

.hero .center {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  align-items: center;
  justify-content: space-around;
  width: 100%;
  flex-grow: 1;
}

.hero hgroup {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
}

.hero h1 {
  color: var(--accent);
}

.hero .brain {
  min-height: 0;
  max-height: 200px;
  padding-top: 1rem;
  padding-bottom: 1rem;
  position: relative;
  z-index: -1;
}

.hero .brain img {
  display: block;
  object-fit: contain;
  height: 100%;
}

.hero .brain::before {
  content: '';
  position: absolute;
  top: -60px;
  bottom: -60px;
  left: -60px;
  right: -60px;
  background: radial-gradient(#2950C299, #2950C211 60%, transparent 65%);
  z-index: -2;
}

h1 {
  text-transform: uppercase;
  font-size: 30px;
  line-height: 2.25rem;
  font-family: "Yeseva One", serif;
}

.hero .catch {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  align-items: center;
}

.hero .catch .accented {
  color: var(--accent);
}

.hero .catch .description,
.hero .catch .description > * {
  font-weight: bold;
  font-size: 15px;
  line-height: 18px;
}

.hero .more {
  font-size: 8px;
  line-height: 10px;

  display: flex;
  flex-direction: column;
  row-gap: 0.25rem;
  align-items: center;

  margin-top: auto;
}

.quote {
  padding: 2rem;

  background-image: url('@/assets/shine_bg.png');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;

  font-size: 18px;
  line-height: 1.75rem;
  font-family: "Yeseva One", serif;

  text-align: center;
  text-wrap: balance;

  position: relative;
  z-index: 0;
}

.quote .content {
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
}

.quote::before {
  display: block;
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: -1;
  background: radial-gradient(#2950C2, #265BC7F5 41%, transparent 85%);
}

.quote .quote-mark {
  flex-grow: 0;
}

.quote .quote-mark.top {
  align-self: flex-start;
}

.quote .quote-mark.bottom {
  align-self: flex-end;
}

.benefits {
  padding-top: 2.75rem;
  padding-bottom: 2.75rem;
  padding-left: 0.75rem;
  padding-right: 0.75rem;
  backgrond-color: #F3F3F2;
  color: #272727;

  font-size: 16px;
  line-height: 24px;
}

.benefits .content {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  row-gap: 2rem;
  column-gap: 2rem;
  align-items: center;
  justify-content: center;
  max-width: 100%;
}

.benefits .content > p {
  max-width: 40ch;
}

.benefits .content .btn-img {
  display: flex;
  flex-direction: column;
  row-gap: 2rem;
}

.benefits em {
  text-transform: uppercase;
  font-weight: bold;
}

.benefits strong {
  font-weight: bold;
}

.benefits img {
  align-self: center;
  object-fit: contain;
  min-height: 100px;
  max-height: 200px;
  max-width: 100%;
}

.benefits .button {
  align-self: center;
}

.benefits-2 {
  padding-top: 2.75rem;
  padding-left: 0.75rem;
  padding-right: 0.75rem;
  
  background-image: url('@/assets/rain_bk2.png');
  background-repeat: repeat;
  background-size: contain;
  background-position: center;

  font-family: "Merriweather", serif;
  font-size: 15px;
  line-height: 20px;

  position: relative;
  z-index: 0;
}

.benefits-2 .content {
  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
}

.benefits-2 em {
  font-weight: 900;
  color: var(--accent);
}

.benefits-2 strong {
  font-weight: 900;
}

.benefits-2 .text {
  display: flex;
  flex-wrap: wrap;
  row-gap: 1.5rem;
  column-gap: 1.5rem;
  align-items: center;
}

.benefits-2 .text > * {
  max-width: 30ch;
}

.benefits-2 .panel {
  border-radius: 20px;
  background-color: #F3F3F2CC;

  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
  padding-left: 0.75rem;
  padding-right: 0.75rem;

  color: #181818;
  font-size: 16px;
  line-height: 23px;
}

.benefits-2 .panel strong {
  font-weight: bold;
}

.benefits-2 .button {
  align-self: center;
}

.benefits-2 .copyright {
  align-self: center;
  color: #FFFFFF80;
  font-size: 10px;
  font-family: Roboto, sans-serif;
  display: flex;
  column-gap: 0.25rem;
  margin-top: 1rem;
  margin-bottom: 0.5rem;
}

.benefits-2 .decoration {
  position: absolute;
  width: 165px;
  height: 165px;
  z-index: -1;
}

.benefits-2 .decoration.left {
  bottom: 15%;
  left: -4rem;
  transform: rotate(-31.55deg);
}

.benefits-2 .decoration.right {
  top: 15%;
  right: -4rem;
  transform: rotate(19.42deg);
}
</style>
