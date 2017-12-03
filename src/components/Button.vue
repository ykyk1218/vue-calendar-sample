<template>
  <div class="button-wrapper">
    <button class="button-left" v-on:click="handleCalendar('-1', fullDate)">&lt; 前</button>
    <button class="button-right" v-on:click="handleCalendar('1', fullDate)">次 &gt;</button>
  </div>
</template>

<script>
  export default {
    name: 'Button',
    props: ['fullDate'],
    methods: {
      handleCalendar: function(page, fullDate) {
        const tmpMonth = fullDate.getMonth() + 1 + parseInt(page)
        fullDate.setMonth(tmpMonth-1)
        this.$parent.year  = fullDate.getFullYear()
        this.$parent.month = fullDate.getMonth()+1
        this.$parent.date = 0
      }
    }
  }
</script>

<style scoped>
  .button-wrapper {
    overflow: hidden;
  }
  button {
    margin-bottom: 5px;
    padding: 8px;
    background-color: #ef9a9a;
    color: #fff;
  }
  .button-left {
    float: left;
  }
  .button-right {
    float: right;
  }
</style>
