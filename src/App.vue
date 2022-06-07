<template>
  <div class="app">
    <Header
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
import Header from "./components/Header";

export default {
  components: {
    Header,
    'show-weather': ShowWeather
 },
  data() {
    return {
      theme: 'light',
      lang: 'ru',
      degree: 'celci'
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
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(255, 255, 255);
}

</style>