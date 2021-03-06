<template>
  <div :class="weatherInfo">
      <entry-field
        @search-city="getData($event)"
        :error-message="errorMessage"
      />
      <div class="display-info">
        <ul class="temp">
          <li class=" info current"> 
            <img class="icon" src="../assets/img/Termometr.png">
            {{ currentLabel }}:  {{current}}
          </li>

          <li class=" info min"> 
            <img class="icon" src="../assets/img/Termometr.png"> 
            {{ minLabel }}:  {{min}}
          </li>

          <li class=" info max"> 
            <img class="icon" src="../assets/img/Termometr.png"> 
            {{ maxLabel }}: {{max}}
          </li>

          <li class=" info feels"> 
            <img class="icon" src="../assets/img/Dots.png"> 
            {{ feelsLabel }}:  {{feels}}
          </li>
        </ul>

        <br>
        <hr>
        <br>

        <ul class="wind-info">
          <li class=" info humidity"> 
            <img class="icon" src="../assets/img/Dry.png"> 
            {{ humidityLabel }}:   {{humidity}}
          </li>

          <li class=" info pressure"> 
            <img class="icon" src="../assets/img/Barometr.png"> 
            {{ pressureLabel }}:    {{pressure}}
          </li>

          <li class=" info speed"> 
            <img class="icon" src="../assets/img/Wind.png"> 
            {{ speedLabel }}: {{speed}}
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
  import EntryField from '../components/EntryField'
  import langData from '../lang.json';

  export default {
    props: ['theme', 'lang', 'degree', 'aspect'],

    data() {
      return {
        current: '',
        min: '',
        max: '',
        feels: '',

        humidity: '',
        pressure: '',
        speed: '',

        errorMessage: '',
      }
    },

    watch: {
      degree: function(degree) {
        degree === 'celsius' ? this.celsiusToFaringate() : this.fahrenheitToСelsius();
      }
    },

    computed: {
      weatherInfo: function () {
        return this.$props.theme === 'light' ? 'light-info' : 'dark-info';
      },
      currentLabel: function () {
        return langData['current'][this.$props.lang];
      },
      minLabel() {
        return langData['min'][this.$props.lang];
      },
       maxLabel() {
        return langData['max'][this.$props.lang];
      },
        feelsLabel() {
        return langData['feels'][this.$props.lang];
      },
        humidityLabel() {
        return langData['humidity'][this.$props.lang];
      },
        pressureLabel() {
        return langData['pressure'][this.$props.lang];
      },
        speedLabel() {
        return langData['speed'][this.$props.lang];
      }
    },

    methods: {
      async getData(city) {
        this.errorMessage = '';

        const KEY = '9eb904ebd5ce5f85a7d9a4204c298d91'
        const API = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${KEY}&units=metric`

        const response = await fetch(API)
        const data = await response.json()

        if (data.cod >= 400) {
          this.errorMessage = data.message;
          this.$emit('change-aspect', 'no-background');
          return;
        }

        if (!data.weather[0].main) {
          this.$emit('change-aspect', 'no-background');
        }

        this.$emit('change-aspect', data.weather[0].main);

        this.current = Math.floor(data.main.temp)
        this.min = Math.floor(data.main.temp_min)
        this.max = Math.floor(data.main.temp_max)
        this.feels = Math.floor(data.main.feels_like)

        this.humidity = Math.floor(data.main.humidity)
        this.pressure = Math.floor(data.main.pressure)
        this.speed = Math.floor(data.wind.speed)
      },

      celsiusToFaringate() {
        this.current = Math.round((this.current - 32) / 1.8);
        this.min = Math.round((this.min - 32) / 1.8);
        this.max = Math.round((this.max - 32) / 1.8);
        this.feels = Math.round((this.feels - 32) / 1.8);
      },

      fahrenheitToСelsius() {
        this.current = Math.round((this.current + 32) * 1.8);
        this.min = Math.round((this.min + 32) * 1.8);
        this.max = Math.round((this.max + 32) * 1.8);
        this.feels = Math.round((this.feels + 32) * 1.8);
      }
    },

    components: {
      'entry-field': EntryField
    }
  }

</script>

<style scoped>
.light-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 370px;
  padding: 35px;
  border-radius: 5px;
  box-shadow: 0 4px 16px #ccc;
  background-color: #fff;
  opacity: 0.9;
}

.dark-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 370px;
  padding: 35px;
  border-radius: 5px;
  box-shadow: 0 4px 16px #000a1a;
  background-color: #000a1a;
}

.dark-info h1{
  color: rgb(255, 255, 255);
}

.dark-info li{
  color: rgb(255, 255, 255);
}

.dark-info img{
  color: rgb(255, 255, 255);
}

.info {
  margin: 6px 0 0 0;
  display: flex;
  justify-content: space-between;
  flex-direction: row-reverse;
 }

 li {
  list-style-type: none;
  font-size: 18px;
  border-radius: 5px;
  padding: 10px;
 }


 .weather-clear {
   background-image: url('https://img4.goodfon.com/wallpaper/nbig/6/61/nebo-oblaka-iasnaia-pogoda-priroda.jpg');
 }

 .weather-snow {
   background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSehtRLjpMlxJErdzVJueff539-yWkysgiiCw&usqp=CAU');
 }

 .weather-rain {
   background-image: url('https://i.pinimg.com/736x/66/f7/d5/66f7d5aaea8b44c6d10244dce9f36e7f.jpg');
 }
 .weather-clouds {
   background-image: url('https://images.unsplash.com/photo-1534088568595-a066f410bcda?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NHx8cmFpbiUyMGNsb3VkfGVufDB8fDB8fA%3D%3D&w=1000&q=80');
 }
</style>