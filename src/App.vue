<template>
  <div class="app">
    <header-nav
      :theme="theme"
      :lang="lang"
      :degree="degree"
      @change-lang="lang = $event"
      @change-theme="theme = $event"
      @change-degree="degree = $event"
    />

    <show-weather
      :theme="theme"
      :lang="lang"
      :degree="degree"
    />
  </div>
</template>

<script>
import ShowWeather from './components/ShowWeather'
import HeaderNav from "./components/HeaderNav";

export default {
  components: {
    'header-nav': HeaderNav,
    'show-weather': ShowWeather
 },
  data() {
    return {
      theme: 'light',
      lang: 'ru',
      degree: 'celsius',

      bgImga: ''
    }
  }
}

</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

.app {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgb(255, 255, 255);
}

</style>