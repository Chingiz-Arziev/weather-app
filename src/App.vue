<template>
  <div class="app" :class="backgroundAspect">
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
      @change-aspect="changeAspect"
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
      backgroundAspect: '',
    }
  },

  methods: {
    changeAspect(aspect) {
      if (aspect === 'no-background') {
        this.backgroundAspect = '';
      }

      if (aspect === 'Snow') {
        this.backgroundAspect = 'weather-snow';
      }

      if (aspect === 'Rain') {
        this.backgroundAspect = 'weather-rain';
      }

      if (aspect === 'Clouds') {
        this.backgroundAspect = 'weather-clouds';
      }

      if (aspect === 'Clear') {
        this.backgroundAspect = 'weather-clear';
      }
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

.weather-clear {
  background-image: url('https://img4.goodfon.com/wallpaper/nbig/6/61/nebo-oblaka-iasnaia-pogoda-priroda.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}

.weather-snow {
  background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSehtRLjpMlxJErdzVJueff539-yWkysgiiCw&usqp=CAU');
  background-repeat: no-repeat;
  background-size: cover;
}

.weather-rain {
  background-image: url('https://i.pinimg.com/736x/66/f7/d5/66f7d5aaea8b44c6d10244dce9f36e7f.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}
.weather-clouds {
  background-image: url('https://images.unsplash.com/photo-1534088568595-a066f410bcda?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NHx8cmFpbiUyMGNsb3VkfGVufDB8fDB8fA%3D%3D&w=1000&q=80');
  background-repeat: no-repeat;
  background-size: cover;
}
</style>