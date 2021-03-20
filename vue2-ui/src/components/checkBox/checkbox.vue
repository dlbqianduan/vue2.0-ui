<template>
  <label
    class="v-checkbox flex"
    :class="[{ disable: isDisabled }]"
    :aria-disabled="isDisabled"
    :id="id"
  >
    <span
      class="v-checkbox_input flex"
      :class="{
        disable: isDisabled,
        checked: isChecked,
      }"
    >
      <span class="v-checkbox_inner"></span>
      <input
        ref="checkbox"
        class="v-checkbox_original"
        :disabled="isDisabled"
        :value="label"
        :name="name"
        v-model="model"
        type="checkbox"
        @change="handleChange"
      />
    </span>
    <span>
      <template v-if="!$slots.default">{{ label }}</template>
      <slot></slot>
    </span>
  </label>
</template>
<script>
export default {
  props: {
    value: {},
    label: {},
    name: String,
    disabled: {
      type: Boolean,
      default: false,
    },
    id: String,
    trueLabel: [String, Number],
    falseLabel: [String, Number],
  },
  data() {
    return {
      selfModel: false,
      isLimitExceeded: false, //是否超出限制（针对min,max)
    };
  },
  computed: {
    model: {
      get() {
        return this.$parent.value;
      },
      set(val) {
        this.isLimitExceeded = false;
        this.$parent.max !== undefined &&
          val.length > this.$parent.max &&
          (this.isLimitExceeded = true);

        this.isLimitExceeded === false &&
          this.dispatch("VCheckboxGroup", "input", [val]);
      },
    },
    isChecked() {
      if (Array.isArray(this.model)) {
        return this.model.indexOf(this.label) > -1;
      } else if (this.model !== null && this.model !== undefined) {
        return this.model === this.trueLabel;
      } else {
        return false;
      }
    },

    isDisabled() {
      return this.$parent.disabled || this.disabled || {}.disabled;
    },
  },
  methods: {
    handleChange(ev) {
      if (this.isLimitExceeded) return;
      let value;
      if (ev.target.checked) {
        value = this.trueLabel === undefined ? true : this.trueLabel;
      } else {
        value = this.falseLabel === undefined ? false : this.falseLabel;
      }
      this.$emit("change", value, ev);
      this.$nextTick(() => {
        this.dispatch("VCheckboxGroup", "change", [this.$parent.value]);
      });
    },
    dispatch(componentName, eventName, params) {
      var parent = this.$parent || this.$root;
      var name = parent.$options.componentName;

      while (parent && (!name || name !== componentName)) {
        parent = parent.$parent;

        if (parent) {
          name = parent.$options.componentName;
        }
      }
      if (parent) {
        parent.$emit.apply(parent, [eventName].concat(params));
      }
    },
  },
};
</script>