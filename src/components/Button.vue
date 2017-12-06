<template>
  <button @click="event => $emit('click', event.target)"><slot/></button>
</template>

<script>
export default {
  name: 'Button'
}
</script>

<style scoped>
button {
  margin-bottom: 5px;
  padding: 8px;
  background-color: #ef9a9a;
  color: #fff;
  outline: none;
}
</style>
