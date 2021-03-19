<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <div class="flex">
      <v-radio
        v-for="(item, index) in relationArr"
        :key="item"
        v-model="radio"
        :disabled="disabled"
        :label="index"
        >{{ item }}</v-radio
      >
    </div>

    <!-- <router-view /> -->
  </div>
</template>
<script>
import VRadio from "../src/components/radio/radio";
export default {
  components: {
    VRadio,
  },
  data() {
    return {
      radio: 1,
      disabled: false,
      relationArr: ["学生", "家长", "老师"],
    };
  },
  created() {
    setTimeout(() => {
      console.log(this.radio);
    }, 3000);
  },
  methods: {
    radioChange(i) {
      console.log(i);
    },
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
