<template>
  <div class="header-nav" :class="headerTheme">
    <div class="btns">
      <button 
        class="btn btn-control" 
        @click="changeTheme"
        >{{ changeTitleTheme }}
      </button>

      <button 
        class="btn btn-control" 
        @click="changeLanguage"
        >{{ changeTitleLang }}
      </button>

      <button 
        class="btn btn-control" 
        @click="changeDegree"
        > {{ changeTitleDeg }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props:['theme', 'lang', 'degree'],

  data() {
    return {
      titleTheme: true,
      titleLang : true,
      titleDeg  : true,
      theme: 'light'
    }
  },

  computed: {
    changeTitleTheme() {
      return this.titleTheme ? 'Темнная тема' : 'Светлая тема'
    },
    changeTitleLang() {
      return this.titleLang ? 'ENG' : 'RUS'
    },
    changeTitleDeg() {
      return this.titleDeg ? 'Фар' : 'Цел'
    },
    headerTheme() {
      return this.$props.theme === 'light' ? 'header-light' : 'header-dark'
    }
  },

  methods: {
    changeTheme() {
      const newTheme = this.$props.theme === 'light' ? 'dark' : 'light';
      this.$emit('change-theme', newTheme)
      this.titleTheme = !this.titleTheme
    },

    changeLanguage() {
      const newLang = this.$props.lang === 'ru' ? 'en' : 'ru';
      this.$emit('change-lang', newLang);
      this.titleLang = !this.titleLang
    },

    changeDegree() {
      const newDegree = this.$props.degree === 'celsius' ? 'far' : 'celsius';
      this.$emit('change-degree', newDegree);
      this.titleDeg = !this.titleDeg
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
  background-color: rgb(255, 255, 255);
  box-shadow: 0 4px 16px #ccc;
  margin-bottom: 5px;
  border-radius: 5px;
}

.btn-control {
  padding: 13px 23px;
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

.header-dark {
  background-color: #000a1a;
}

.header-dark .btn-control {
  background-color: rgb(30, 51, 93);
}

.header-dark .btn-control:hover {
  background-color: rgb(57, 107, 207);
}

.header-lights {
  background-color: rgb(255, 255, 255);
}
</style>