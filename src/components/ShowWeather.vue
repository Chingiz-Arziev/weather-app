<template>
  <div :class="weatherInfo">
      <entry-field
        @search-city="getData($event)"
        :error-message="errorMessage"
      />

    <div class="display-info">
      <h1 class="title">{{title}}</h1>
      <ul class="temp">
        <li class=" info current"> <img class="icon" src="../assets/img/Termometr.png">
          {{ currentLabel }}:  {{current}}
        </li>
        <li class=" info min"> <img class="icon" src="../assets/img/Termometr.png"> Минимальная:  {{min}}</li>
        <li class=" info max"> <img class="icon" src="../assets/img/Termometr.png"> Максимальная: {{max}}</li>
        <li class=" info feels"> <img class="icon" src="../assets/img/Dots.png"> Ощущаемая:  {{feels}}</li>
      </ul>

      <br>
      <hr>
      <br>

      <ul class="wind-info">
        <li class=" info humidity"> <img class="icon" src="../assets/img/Dry.png"> Влажность:   {{humidity}}</li>
        <li class=" info pressure"> <img class="icon" src="../assets/img/Barometr.png"> Давление:    {{pressure}}</li>
        <li class=" info speed"> <img class="icon" src="../assets/img/Wind.png"> Скорость ветра: {{speed}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  import EntryField from '../components/EntryField'
  import langData from '../lang.json';

  export default {
    props: ['theme', 'lang', 'degree'],

    data() {
      return {
        title: 'Название города',
        date: '',
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
      currentLabel: function() {
        return langData['min'][this.$props.lang];
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
          return;
        }

        if (data.weather.main === 'clear') {
          
        }

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
        this.min = Math.round((this.current - 32) / 1.8);
        this.max = Math.round((this.current - 32) / 1.8);
        this.feels = Math.round((this.current - 32) / 1.8);
      },

      fahrenheitToСelsius() {
        this.current = Math.round((this.current + 32) * 1.8);
        this.min = Math.round((this.current + 32) * 1.8);
        this.max = Math.round((this.current + 32) * 1.8);
        this.feels = Math.round((this.current + 32) * 1.8);
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
   font-size: 20px;
   border: 1px solid rgb(226, 226, 226);
   border-radius: 5px;
   padding: 10px;
 }

</style>