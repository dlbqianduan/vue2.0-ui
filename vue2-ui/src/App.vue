<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>-->
    <section>
      <h2>单选框 radio</h2>
      <div class="flex padding">
        <v-radio v-model="radio" :label="1"></v-radio>
        <v-radio v-model="radio" :label="2"></v-radio>
        <v-radio v-model="radio" :label="3"></v-radio>
      </div>
      <div class="flex padding">
        <v-radio
          @change="radioChange"
          v-for="(item, index) in relationArr"
          :key="item"
          v-model="radio1"
          :disabled="index == 2"
          :label="index"
        >
          <span>{{ item }}</span>
        </v-radio>
      </div>
    </section>
    <section>
      <h2>多选框 checkBox</h2>
      <div class="flex padding">
        <v-check-box-group v-model="checkBoxArr" :max="4">
          <v-check-box label="广州"></v-check-box>
          <v-check-box label="上海"></v-check-box>
          <v-check-box label="北京"></v-check-box>
          <v-check-box label="深圳"></v-check-box>
        </v-check-box-group>
      </div>
    </section>
    <!-- <router-view /> -->
  </div>
</template>
<script>
import VRadio from '../src/components/radio/radio'
import VCheckBoxGroup from '../src/components/checkBox/checkbox-group'
import VCheckBox from '../src/components/checkBox/checkbox'
export default {
  components: {
    VRadio,
    VCheckBox,
    VCheckBoxGroup
  },
  data() {
    return {
      radio: 1,
      radio1: 1,
      relationArr: ['学生啊', '家长啊', '老师啊'],
      checkBoxArr: ['北京'],
    }
  },
  created() {},
  methods: {
    radioChange(c) {
      console.log(c)
      alert(JSON.stringify(c))
    },
  },
}
</script>
<style lang="less" scoped>
#app {
  width: 800px;
  margin: 0 auto;
  padding: 30px;
  section {
    margin-bottom: 50px;
  }
}
</style>
