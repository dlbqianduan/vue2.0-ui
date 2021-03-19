<template>
  <label class="v-checkbox flex" :class="[{ disable: isDisabled }]" :aria-disabled="isDisabled">
    <span
      class="v-checkbox_input flex"
      :class="{
        disable: isDisabled,
        checked: isChecked,
      }"
    >
      <span class="v-checkbox_inner"></span>
      <input
        v-if="trueLabel || falseLabel"
        ref="checkbox"
        class="v-checkbox_original"
        :name="name"
        :aria-hidden="indeterminate ? 'true' : 'false'"
        :true-value="trueLabel"
        :false-value="falseLabel"
        :value="label"
        :disabled="isDisabled"
        :aria-disabled="isDisabled"
        v-model="model"
        @change="handleChange"
        type="checkbox"
      />
      <input
        v-else
        ref="checkbox"
        class="v-checkbox_original"
        :aria-hidden="indeterminate ? 'true' : 'false'"
        :disabled="isDisabled"
        :value="label"
        :name="name"
        v-model="model"
        @change="handleChange"
        type="checkbox"
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
  props: {
    value: {},
    label: {},
    indeterminate: Boolean,
    name: String,
    disabled: {
      type: Boolean,
      default: false,
    },
    checked: Boolean, //当前是否勾选
    trueLabel: [String, Number],
    falseLabel: [String, Number],
  },
  data() {
    return {
      selfModel: false,
      isLimitExceeded: false, //是否超出限制（针对min,max)
    }
  },
  computed: {
    model: {
      get() {
        return this.$parent.value
      },
      set(val) {
        console.log(this.model)
        this.isLimitExceeded = false
        this.$parent.min !== undefined &&
          val.length < this.$parent.min &&
          (this.isLimitExceeded = true)

        this.$parent.max !== undefined &&
          val.length > this.$parent.max &&
          (this.isLimitExceeded = true)

        this.isLimitExceeded === false &&
          this.dispatch('VCheckboxGroup', 'input', [val])
        console.log(this.model)
      },
    },
    isChecked() {
      if ({}.toString.call(this.model) === '[object Boolean]') {
        return this.model
      } else if (Array.isArray(this.model)) {
        return this.model.indexOf(this.label) > -1
      } else {
        return false
      }
    },

    isDisabled() {
      return this.$parent.disabled || this.disabled || {}.disabled
    },
  },
  created() {
    this.checked && this.addToStore()
  },
  methods: {
    addToStore() {
      if (Array.isArray(this.model) && this.model.indexOf(this.label) === -1) {
        this.model.push(this.label)
      } else {
        this.model = this.trueLabel || true
      }
    },
    handleChange(ev) {
      if (this.isLimitExceeded) return
      let value
      if (ev.target.checked) {
        value = this.trueLabel === undefined ? true : this.trueLabel
      } else {
        value = this.falseLabel === undefined ? false : this.falseLabel
      }
      this.$emit('change', value, ev)
      this.$nextTick(() => {
        this.dispatch('VCheckboxGroup', 'change', [this.$parent.value])
      })
      console.log(this.model)
    },
    dispatch(componentName, eventName, params) {
      var parent = this.$parent || this.$root
      var name = parent.$options.componentName

      while (parent && (!name || name !== componentName)) {
        parent = parent.$parent

        if (parent) {
          name = parent.$options.componentName
        }
      }
      if (parent) {
        parent.$emit.apply(parent, [eventName].concat(params))
      }
    },
  },
}
</script>