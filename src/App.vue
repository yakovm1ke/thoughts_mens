<script setup lang="ts">
import {computed, ref} from 'vue'
import axios from 'axios'
import loader from './assets/loader.svg'

const SHEET_URL = 'https://sheetdb.io/api/v1/ie1y4wektzefc'

const loading = ref(false)
const touched = ref(false)
const wasSucceed = ref(false)
const wasFailed = ref(false)
const profession1 = ref('')
const profession2 = ref('')

const isFormValid = computed(() => {
  if (!touched.value) return true

  return profession1.value.trim().length > 0
    && profession2.value.trim().length > 0
})

async function handleSubmit() {
  loading.value = true
  touched.value = true
  if (!isFormValid.value) return

  const body = {
    profession1: profession1.value,
    profession2: profession2.value,
  }

  try {
    await axios.post(SHEET_URL, body)
    wasSucceed.value = true
  } catch(e) {
    wasFailed.value = true
  } finally {
    loading.value = false
  }
}

function resetForm() {
  touched.value = false
  profession1.value = ''
  profession2.value = ''
  wasSucceed.value = false
  wasFailed.value = false
}
</script>

<template>
  <div
    :class='$style.container'
    v-if='wasFailed'
  >
    <div :class='$style.pageTitle'>
      паблик мужские мысли
    </div>
    <div :class='[$style.error, $style.formTitle]'>
      что-то пошло не так
    </div>
    <button
      @click='resetForm'
      :class='$style.button'
    >
      попробовать снова
    </button>
  </div>
  <div
    :class='$style.container'
    v-else-if='wasSucceed'
  >
    <div :class='$style.pageTitle'>
      паблик мужские мысли
    </div>
    <div :class='[$style.success, $style.formTitle]'>
      ваша мысль успешно записана
    </div>
    <button
      @click='resetForm'
      :class='$style.button'
    >
      отправить новую мысль
    </button>
  </div>
  <div
    :class='$style.container'
    v-else
  >
    <div :class='$style.pageTitle'>
      паблик мужские мысли
    </div>
    <img
      :class='$style.image'
      src='/logo.jpg'
    >
    <div :class='$style.formTitle'>
      симбиоз профессий
    </div>
    <div :class='$style.fields'>
      <input
        :value='profession1'
        :class='$style.field'
        placeholder='Профессия 1'
        @input='profession1 = ($event.target as HTMLInputElement).value'
      >
      <div :class='$style.formTitle'>
        И
      </div>
      <input
        :value='profession2'
        :class='$style.field'
        placeholder='Профессия 2'
        @input='profession2 = ($event.target as HTMLInputElement).value'
      >
    </div>
    <button
      @click='handleSubmit'
      :class='$style.button'
    >
      отправить
    </button>
    <div
      :class='$style.error'
      v-if='touched && !isFormValid'
    >
      заполните обязательные поля!
    </div>
    <div>
      телеграм канал
      <a
        :class='$style.link'
        href='https://t.me/thoughts_mens'
        target='_blank'
        rel='noopener noreferrer'
      >
        паблик мужские мысли
      </a>
    </div>
  </div>
  <div
    v-if='loading'
    :class='$style.loadingWrapper'
  >
    <img :src='loader'/>
  </div>
</template>

<style module>
@import url('https://fonts.googleapis.com/css2?family=Manrope:wght@200;300;400;500;600;700;800&display=swap');

body {
  margin: 0;
  font-family: 'Manrope', sans-serif;
  font-size: 15px;
}
.container {
  box-sizing: border-box;
  padding: 20px;
  overflow: hidden;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
.pageTitle {
  text-align: center;
  font-size: 32px;
  font-weight: 800;
}
.image {
  display: flex;
  max-width: 150px;
  width: 100%;
}
.formTitle {
  text-align: center;
  font-size: 24px;
  font-weight: 800;
}
.fields {
  width: 100%;
  overflow: hidden;
  display: grid;
  gap: 10px;
  grid-template-columns: minmax(150px, 1fr) auto minmax(150px, 1fr);
  align-items: center;
}
.field {
  width: 100%;
  box-sizing: border-box;
  background: transparent;
  border: 1px solid black;
  border-radius: 4px;
  font-family: inherit;
  padding: 8px;
  font-size: inherit;
}
.button {
  font-family: inherit;
  font-size: 15px;
  background: black;
  color: white;
  font-weight: 800;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
}
.button:hover {
  cursor: pointer;
}
.button:active {
  transform: translateY(2px);
}
.link {
  color: rgba(82, 110, 211, 1);
  text-decoration: none;
}
.link:visited {
  color: rgba(82, 110, 211, 1);
}
.link:hover {
  color: rgba(108, 134, 226, 1);
}
.error {
  color: rgba(221, 76, 30, 1);
}
.success {
  color: rgba(74, 201, 155, 1)
}
.loadingWrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(27, 31, 59, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}
@media screen and (max-width: 400px) {
  .fields {
    justify-items: center;
    grid-template-columns: 1fr;
  }
}
</style>
