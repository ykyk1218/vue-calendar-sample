<template>
  <div id="calendar">
    <p>{{ year }}年{{ month }}月</p>
    <Button :fullDate="fullDate"/>
    <table>
      <tr>
        <td v-for="w in week">{{ w }}</td>
      </tr>
      <tr>
        <DateCell v-for="(w, i) in week" :viewDate="viewDate(i, 1)" />
      </tr>
      <tr>
        <DateCell v-for="(w, i) in week" :viewDate="viewDate(i, 2)" />
      </tr>
      <tr>
        <DateCell v-for="(w, i) in week" :viewDate="viewDate(i, 3)" />
      </tr>
      <tr>
        <DateCell v-for="(w, i) in week" :viewDate="viewDate(i, 4)" />
      </tr>
      <tr>
        <DateCell v-for="(w, i) in week" :viewDate="viewDate(i, 5)" />
      </tr>
      <tr>
        <DateCell v-for="(w, i) in week" :viewDate="viewDate(i, 6)" />
      </tr>
    </table>
  </div>
</template>

<script>
import DateCell from './DateCell'
import Button from './Button'

const d = new Date()
const year = d.getFullYear()
const month = d.getMonth()+1

export default {
  name: 'Calendar',
  components: {
    DateCell,
    Button
  },
  data: function() {
    return {
      week: ["日","月","火","水","木","金","土"],
      year: year,
      month: month,
      viewDate: function(weekIndex, row) {
        let startDateWeek = new Date(this.year, this.month-1, 1).getDay()
        let endMonthDate = new Date(this.year, this.month, 0).getDate()
        if(row === 1 && weekIndex < startDateWeek ) {
          console.log(startDateWeek)
          return ""
        }else if(this.date >= endMonthDate) {
          return ""
        }
        this.setDate()
        return this.date
      },
      fullDate: d,
      i:0
    }
  },
  methods: {
    setDate: function() {
      if(this.date == undefined || this.date === 0) {
        this.date = 1
      }else{
        this.date += 1
      }
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 #calendar {
   color: #666;
   font-size: 2em;
   width: 400px;
   margin: auto;
 }

 table {
   border: 1px solid #ef9a9a;
 }

 table td {
   padding: 10px;
 }


</style>
