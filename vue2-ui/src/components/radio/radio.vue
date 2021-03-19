<template>
  <label
    class="v-radio flex"
    :class="[{ disable: disabled }]"
    :aria-disabled="disabled"
  >
    <span
      class="v-radio_input flex"
      :class="{
        disable: disabled,
        checked: model === label,
      }"
    >
      <span class="v-radio_inner"></span>
      <input
        ref="radio"
        class="v-radio_original"
        :name="name"
        :value="label"
        v-model="model"
        :disabled="disabled"
        :aria-disabled="disabled"
        @change="handleChange"
        type="radio"
      />
    </span>
    <span>
      <template v-if="!$slots.default">{{label}}</template>
      <slot></slot>
    </span>
  </label>
</template>
<script>
export default {
  data() {
    return {};
  },
  props: {
    value: {},
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
        this.$emit("input", val);
      },
    },
  },
  methods: {
    handleChange() {
      this.$nextTick(() => {
        this.$emit("change", this.model);
      });
    },
  },
};
</script>