<template>
  <button :type="type" :disabled="disabled_btn" @click="callFn">
    <span
        v-if="spinning"
        class="spinner-border spinner-border-sm"
        style="margin-bottom: 2px; margin-left: -2px;"
        role="status"
        aria-hidden="true"
    />
    <i v-else-if="!!icon" :class="icon"></i>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'btn-loading',

  props: {
    fn: {
      type: Function,
      require: true,
    },
    icon: {
      type: String,
      require: false,
      default: null,
    },
    disabled: {
      type: Boolean,
      require: false,
      default: false,
    },
    type: {
      type: String,
      require: false,
      default: 'button',
    },
    stopSpin: {
      type: Boolean,
      require: false,
      default: false,
    }
  },

  data () {
    return {
      spinning: false,
      disabled_btn: this.disabled || typeof this.fn !== 'function',
    }
  },

  methods: {
    callFn () {
      this.spinning = true
      this.disabled_btn = true

      this.fn()
          .then(() => {
            this.stopLoading()
          })
          .catch(() => this.stopLoading(false))
    },

    stopLoading (success = true) {
      if (this.stopSpin) {
        this.spinning = false
        this.disabled_btn = false
      }

      this.$emit('success', success)

      if (!success) {
        this.$emit('fail')
      }
    },
  },

  watch: {
    disabled (disabled) {
      this.disabled_btn = disabled
    },
  },
}
</script>
