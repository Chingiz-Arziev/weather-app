<template>
  <div >
    <form :class="weatherInfo" @submit.prevent="input">
      <input
        class="input"
        :class="this.inputColor"
        placeholder="Веддите название города"
        v-model="city"
      >
      <div
        class="error-message" 
        v-if="errorMessage"
        >
        Город не найден
      </div>

      <button
        class="btn"
      >
        Узнать погоду
      </button>
    </form>
  </div>
</template>

<script>
  export default {
    props: ['errorMessage', 'theme'],
    data() {
      return {
        city: '',
      }
    },
    methods: {
      input() {
        this.$emit('search-city', this.city)
      }
    },
    computed: {
      inputColor: function () {
        return this.$props.errorMessage ? 'error' : 'complete';
      },
      weatherInfo: function () {
        return this.$props.theme === 'light' ? 'light-info' : 'dark-info';
      },
    }
  }

</script>

<style scoped>
  .input {
    width: 300px;
    height: 50px;
    border: none;
    border: 1px solid rgb(13, 92, 251);
    padding: 0px 10px;
    font-size: 14px;
    border-radius: 5px;
  }

  input:focus {
    outline: none;
  }

 .btn {
    width: 300px;
    height: 50px;
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

  .error {
    border: 1px solid red;
  }

  .complete {
    border-bottom: 1px solid green;
  }


  .error-message {
    background-color: red;
    padding: 15px;
    color: #fff;
    text-align: center;
    border-radius: 5px;
  }


  .dark-info .btn{
    background-color: rgb(30, 51, 93);
  }

  .dark-info .btn:hover{
    background-color: rgb(24, 81, 187);
  }

  .dark-info .input{
    background-color: rgb(39, 44, 54);
    color: #fff;
  }
  .dark-info .input::-webkit-input-placeholder {
    color: #fff;
  }

  .dark-info .complete {
    border: 1px solid rgb(13, 92, 251);
  }





   .light-info .btn{
    background-color: rgb(13, 92, 251);
  }

  .light-info .btn:hover{
    background-color: rgb(57, 107, 207);
  }

  .light-info .input{
    background-color: rgb(255, 255, 255);
    color: rgb(0, 0, 0);
  }
  .light-info .input::-webkit-input-placeholder {
    color: rgb(36, 36, 36);
  }

  .light-info .complete {
    border-bottom: 1px solid rgb(13, 92, 251);
  }
</style>