<template>
  <span :class="{ today: isToday() }">{{ currentDate }}</span>
</template>

<script>
export default {
  name: 'DateCell',
  props: ['currentDateTime'],
  computed: {
    currentDate () {
      return this.currentDateTime.getDate()
    }
  },
  methods: {
    isToday () {
      let now = new Date()
      return (
        now.getDate() === this.currentDateTime.getDate() &&
        now.getMonth() === this.currentDateTime.getMonth() &&
        now.getFullYear() === this.currentDateTime.getFullYear()
      )
    }
  }
}
</script>

<style scoped>
span {
  display: inline-block;
  width: 100%;
  height: 100%;
}
.today {
  background-color: #ef9a9a;
  color: #fff;
  font-weight: bold;
  border-radius: 30px;
}
</style>
