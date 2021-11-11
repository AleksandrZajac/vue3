<template>
  <select v-model="modelValue">
    <option disabled value="">Выберите из списка</option>
    <option
      v-for="option in options"
      :key="option.value"
      :value="option.value"
    >
      Выберите из списка
    </option>
  </select>
</template>

<script>
  export default {
    name: 'my-select',
    props: {
      modelValue: {
        type: String
      },
      options: {
        type: Array,
        default: () => []
      }
    }
  }
</script>

<style scoped>

</style>
