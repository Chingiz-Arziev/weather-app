<template>
  <div>
    <form @submit.prevent="input">
      <input
        class="input"
        :class="this.inputColor"
        placeholder="Веддите название города"
        v-model="city"
      >

      <button class="btn" @click="input">Узнать погоду</button>
    </form>
  </div>
</template>

<script>
  export default {
    props: ['errorMessage'],
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
      }
    }
  }

</script>

<style scoped>
  .input {
    width: 300px;
    height: 50px;
    border: none;
    border-bottom: 1px solid rgb(13, 92, 251);
    padding: 0px 10px;
    font-size: 16px;
  }

  input:focus {
    outline: none;
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

  .error {
    border: 1px solid red;
  }

  .complete {
    border: 1px solid green;
  }
</style>