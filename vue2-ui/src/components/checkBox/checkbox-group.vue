<template>
  <div class="v-checkbox-group flex" role="group" aria-label="checkbox-group">
    <label
      v-if="startAll"
      class="v-checkbox-all flex"
      :class="[max && max !== startAllArr.length ? 'disabled' : '']"
    >
      <span
        class="v-all_inner"
        :class="[
          checked ? 'checked' : '',
          max && max != startAllArr.length ? 'disabled' : '',
        ]"
      ></span>
      <span>全选</span>
      <input
        class="v-all_input hidden"
        type="checkbox"
        :disabled="isDisabled"
        v-model="model"
      />
    </label>
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: "VCheckboxGroup",
  componentName: "VCheckboxGroup",
  data() {
    return {
      checked: false,
      startAllArr: [],
    };
  },
  props: {
    value: {},
    disabled: Boolean,
    max: Number,
    startAll: Boolean, //是否开启全选功能
  },
  computed: {
    model: {
      get() {
        return this.checked;
      },
      set() {
        let startAllArr = [];
        this.checked = !this.checked;
        this.checked && (startAllArr = this.startAllArr);
        this.$emit("input", startAllArr);
      },
    },
    isDisabled() {
      return this.max && this.max !== this.startAllArr.length;
    },
  },
  created() {
    this.startAll &&
      this.$slots.default.forEach((ele) => {
        this.startAllArr.push(ele.componentOptions.propsData.label);
      });
  },
};
</script>
<style lang='less' scoped>
</style>