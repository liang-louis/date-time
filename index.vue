<template>
  <el-date-picker
    v-model="defaultValue"
    type="date"
    :placeholder="placeholder"
    :disabled="disabled"
    :clearable="clearable"
    @change="changeVal"
  />
</template>

<script>
export default {
  name: 'DateTimePicker',
  props: {
    value: {
      type: [String, Date],
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      default: ''
    },
    clearable: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {}
  },
  computed: {
    defaultValue: {
      get() {
        return this.value
      },
      set(val) {
        if (!val || val === 'Invalid Date') {
          this.$emit('input', '')
          return false
        }
        const date = `${this.$dayJs(val).format('YYYY-MM-DD')} ${this.$dayJs().hour()}:${this.$dayJs().minute()}:${this.$dayJs().second()}`
        this.$emit('input', this.$dayJs(date).format('YYYY-MM-DD HH:mm:ss'))
      }
    }
  },
  methods: {
    changeVal(val) {
      const date = `${this.$dayJs(val).format('YYYY-MM-DD')} ${this.$dayJs().hour()}:${this.$dayJs().minute()}:${this.$dayJs().second()}`
      this.$emit('change', this.$dayJs(date).format('YYYY-MM-DD HH:mm:ss'))
    }
  }
}
</script>

<style scoped>

</style>
