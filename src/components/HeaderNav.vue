<template>
  <div class="header-nav" :class="headerTheme">
    <div>
      <button
        class="btn-control-theme"
        :class="buttonTheme"
        @click="changeTheme"
      > 1
      </button>

      <button
        class="btn-control-lang"
        @click="changeLanguage"
      >
        {{ changeTitleLang }}
      </button>

      <button
        class="btn-control-deg"
        @click="changeDegree"
      >
        {{ changeTitleDeg }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props:['theme', 'lang', 'degree'],

  data() {
    return {
      titleLang : true,
      titleDeg  : true,
    }
  },

  computed: {
    changeTitleLang() {
      return this.titleLang ? 'ENG' : 'RUS'
    },

    changeTitleDeg() {
      return this.titleDeg ? ' F° ' : ' C° '
    },

    headerTheme() {
      return this.$props.theme === 'light' ? 'header-light' : 'header-dark'
    },

    buttonTheme() {
      return this.$props.theme === 'light' ? 'light-btn' : 'dark-btn';
    }
  },

  methods: {
    changeTheme() {
      const newTheme = this.$props.theme === 'light' ? 'dark' : 'light';
      this.$emit('change-theme', newTheme);
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

.btn-control-lang, .btn-control-deg {
  padding: 15px 45px;
  background-color: rgb(13, 92, 251);
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  text-align: center;
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

.light-btn {
  padding: 15px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  color: #fff;
  background-image: url('../assets/img/moon.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-color: rgb(13, 92, 251);
}

.dark-btn {
  padding: 15px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  color: #fff;
  background-image: url('../assets/img/sun.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-color: rgb(13, 92, 251);
}
</style>