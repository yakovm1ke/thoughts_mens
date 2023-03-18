<script setup lang="ts">
</script>

<template>
  <div :class='$style.container'>
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
        :class='$style.field'
        placeholder='Профессия 1'
      >
      <div :class='$style.formTitle'>
        И
      </div>
      <input
        :class='$style.field'
        placeholder='Профессия 2'
      >
    </div>
    <button :class='$style.button'>
      Отправить
    </button>

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
  font-size: 32px;
  font-weight: 800;
}
.image {
  display: flex;
  max-width: 150px;
  width: 100%;
}
.formTitle {
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
@media screen and (max-width: 400px) {
  .fields {
    justify-items: center;
    grid-template-columns: 1fr;
  }
}
</style>
