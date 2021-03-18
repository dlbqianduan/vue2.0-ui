<template>
  <label
    class="v-radio flex"
    :class="[
   {disable:disabled}
  ]"
    :aria-disabled="disabled"
    :tabindex="tabIndex"
  >
   <span class="v-radio_input flex">
     <span class="v-radio_inner">

     </span>
    <input
      :class="[{disable:disabled}]"
      class="v-radio_original"
      :name="name"
      v-model="model"
      :disabled="disabled"
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
        return this.isGroup ? this._radioGroup.value : this.value
      },
      set(val) {
        this.$emit('input', val)
        this.$refs.radio &&
          (this.$refs.radio.checked = this.model === this.label)
      },
    },
  },

  created() {},
  methods: {},
}
</script>
<style lang='less' scoped></style>