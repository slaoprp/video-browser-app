<template>
  <div>
    <input @input="onInput" type="text" placeholder="Search">
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    onInput(event) {
      this.$emit('termChange', event.target.value)
    }
  }
}
</script>

<style>
  
</style>