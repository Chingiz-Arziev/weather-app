<template>
  <div class="app">
    <show-weather/>
  </div>
</template>

<script>

import EntryField from './components/EntryField'
import ShowWeather from './components/ShowWeather'

export default {
  components: {
    'entry-field': EntryField,
    'show-weather': ShowWeather
 },
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

