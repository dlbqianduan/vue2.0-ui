<template>
  <label
    class="v-radio flex"
    :class="[
   {disable:disabled}
  ]"
    :aria-disabled="disabled"
  >
   <span class="v-radio_input flex"
   :class="{
        disable: disabled,
        checked: model === label
      }"
   >
     <span class="v-radio_inner">

     </span>
    <input
      ref="radio"
      class="v-radio_original"
      :name="name"
      v-model="model"
      :disabled="disabled"
      @change="handleChange"
      aria-hidden="true"
      type="radio"
    />
   </span>

    <span>
      <slot></slot>
    </span>
  </label>
</template>
<script>
export default {
  data() {
    return {}
  },
  props: {
    value:{},
    label: {},
    name: String,
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    model: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit('input', val)
        this.$refs.radio &&
          (this.$refs.radio.checked = this.model === this.label)
      },
    },
  },

  created() {},
  methods: {
     handleChange() {
        this.$nextTick(() => {
          this.$emit('change', this.model);
          console.log(1234455)
        });
      }
  },
}
</script>
<style lang='less' scoped></style>