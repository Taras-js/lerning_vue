<template>
  <select v-model="modelValue" @change="changeOption">
    <option disabled value="">Select from list</option>
    <option
        v-for="option in options"
        :value="option.value"
        key="option.value">
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: "my-select",
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      console.log(event)
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>

</style>