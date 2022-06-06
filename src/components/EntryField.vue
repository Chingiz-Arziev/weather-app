<template>
  <div>
      <input  class="input" 
              placeholder="Веддите название города"
              @input="input"
      >
  </div>
</template>

<script>
  export default {
    porps: {
      value: {
        type: String,
        default: ''
      },
    },
    methods: {
      input(e) {
        let value = e.target.value
        this.$emit('input', value)
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
</style>