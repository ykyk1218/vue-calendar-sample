<template>
  <td :class="{today: isToday()}">{{ viewDate }}</td>
</template>

<script>

export default {
  name: 'DateCell',
  props: ['viewDate'],
  data: () => {
    return {
      isToday: function() {
        const now = new Date()
        const year = now.getFullYear()
        const month = now.getMonth()+1
        const date = now.getDate()
        if(this.$parent.year == year &&
           this.$parent.month == month &&
           this.viewDate == date) {
          return true
        }else{
          return false
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .today {
    background-color: #ef9a9a;
    color: #fff;
    font-weight: bold;
    border-radius: 30px;
  }
</style>
