<template>
  <div class="weather-info">
      <entry-field
      v-model="title"
    />
    <button class="btn" @click="getData">Узнать погоду</button>

    <div class="display-info">
      <h1 class="title">{{title}}</h1>
      <ul class="temp">
        <li class=" info current"> <img class="icon" src="../assets/img/Termometr.png"> Текущая:  {{current}}</li>
        <li class=" info min"> <img class="icon" src="../assets/img/Termometr.png"> Минимальная:  {{min}}</li>
        <li class=" info max"> <img class="icon" src="../assets/img/Termometr.png"> Максимальная: {{max}}</li>
        <li class=" info feels"> <img class="icon" src="../assets/img/Dots.png"> Ощущаемая:  {{feels}}</li>
      </ul>

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
  
  export default {
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
        speed: ''
      }
    },

    methods: {
      async getData() {
        const KEY = '9eb904ebd5ce5f85a7d9a4204c298d91'
        const API = `https://api.openweathermap.org/data/2.5/weather?q=${this.title}&appid=${KEY}&units=metric`

        const response = await fetch(API)
        const data = await response.json()

        console.log(data);

        this.current = Math.floor(data.main.temp) 
        this.min = Math.floor(data.main.temp_min)
        this.max = Math.floor(data.main.temp_max)
        this.feels = Math.floor(data.main.feels_like)

        this.humidity = Math.floor(data.main.humidity)
        this.pressure = Math.floor(data.main.pressure)
        this.speed = Math.floor(data.wind.speed)
      }
    },

    components: {
      'entry-field': EntryField
    }
  }

</script>

<style scoped>
.weather-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 370px;
  padding: 35px;
  border-radius: 5px;
  box-shadow: 0 4px 16px #ccc;
}
 .btn {
   width: 300px;
   height: 40px;
   border: none;
   border-radius: 5px;
   cursor: pointer;
   margin: 20px 0;
   background-color: rgb(13, 92, 251);
   color: #fff;
   font-size: 14px;
 }
 .btn:hover {
   background-color: rgb(57, 107, 207);
   color: #fff;
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