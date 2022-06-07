<template>
  <div class="header-nav">
    <button class="btn btn-control" @click="changeTheme">Theme</button>
    <button class="btn btn-control" @click="changeLanguage">Language</button>
    <button class="btn btn-control" @click="changeDegree">Degree</button>
  </div>
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
      const newDegree = this.$props.degree === 'celsius' ? 'far' : 'celsius';
      this.$emit('change-degree', newDegree);
    }
  }
}
</script>

<style scoped>

.header-nav {
  width: 370px;
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #fff;
  box-shadow: 0 4px 16px #ccc;
}
.btn-control {
  padding: 13px 24px;
  background-color: rgb(13, 92, 251);
  color: #fff;
  font-size: 14px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn-control:hover {
  background-color: rgb(57, 107, 207);
}
</style>