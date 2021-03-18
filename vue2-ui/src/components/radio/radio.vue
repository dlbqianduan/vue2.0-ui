<template>
  <div class="el-radio-group" role="radiogroup" @keydown="handleKeydown">
    <slot></slot>
  </div>
</template>
<script>
export default {
  data() {
    return {
      
    }
  },
  computed: {
    elTag() {
      return (this.$vnode.data || {}).tag || 'div'
    },
  },
  methods: {
    handleKeydown() {
      // 左右上下按键 可以在radio组内切换不同选项
    },
  },
  created() {
    console.log(this.$vnode, this.$vnode.tag);
  },
}
</script>
<style lang="less" scoped>
</style>