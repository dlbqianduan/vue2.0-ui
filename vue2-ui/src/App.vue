<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <v-radio v-model="radio">
      <v-radio-item :disabled="true" :label="1">选项一</v-radio-item>
      <v-radio-item :label="2">选项二</v-radio-item>
    </v-radio>
    <!-- <router-view /> -->
  </div>
</template>
<script>
import VRadio from  "../src/components/radio/radio";
import VRadioItem from  "../src/components/radio/radio-item";
export default {
  components:{
    VRadio,
    VRadioItem
  },
  data(){
    return {
      radio:1,
    }
  },
}
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
