<template>
  <header class="header">
    <button @click="changeTheme">Theme change</button>
    <button @click="changeLanguage">Lang</button>
    <button @click="changeDegree">change degree</button>
  </header>
</template>

<script>
export default {
  props:['theme', 'lang', 'degree'],
  name: "Header",

  methods: {
    changeTheme() {
      const newTheme = this.$props.theme === 'light' ? 'dark' : 'light';
      this.$emit('change-theme', newTheme)
    },

    changeLanguage() {
      const newLang = this.$props.lang === 'ru' ? 'en' : 'ru';
      this.$emit('change-lang', newLang);
    },

    changeDegree() {
      const newDegree = this.$props.degree === 'celci' ? 'far' : 'celci';
      this.$emit('change-degree', newDegree);
    }
  }
}
</script>

<style scoped>
.header {
  background: white;
}
</style>