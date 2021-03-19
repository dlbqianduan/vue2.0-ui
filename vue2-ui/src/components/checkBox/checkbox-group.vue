<template>
  <div class="v-checkbox-group flex" role="group" aria-label="checkbox-group">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: 'VCheckboxGroup',
  componentName: 'VCheckboxGroup',
  data() {
    return {
    }
  },
  props: {
     value: {},
      disabled: Boolean,
      min: Number,
      max: Number,
  },
  created() {
    setTimeout(() => {
      console.log(this.value)
    }, 1000)
  },
  methods: {},
}
</script>
<style lang='less' scoped></style>