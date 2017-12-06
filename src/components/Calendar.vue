<template>
  <div id="calendar">
    <p>{{ currentYear }}年{{ currentMonth }}月</p>
    <div class="button-wrapper">
      <v-button class="button-left"  @click="setPrevMonth(currentYear, currentMonth)">&lt; 前</v-button>
      <v-button class="button-right" @click="setNextMonth(currentYear, currentMonth)">次 &gt;</v-button>
    </div>
    <table>
      <tr>
        <th v-for="week in jpWeekNames">{{ week }}</th>
      </tr>
      <tr v-for="weekRowNumber in 6">
        <td v-for="weekNumber in 7" v-if="dateTimeFrom(weekRowNumber - 1, weekNumber - 1) != null">
          <date-cell :currentDateTime="dateTimeFrom(weekRowNumber - 1, weekNumber - 1)"/>
        </td>
        <td v-else></td>
      </tr>
    </table>
  </div>
</template>

<script>
import DateCell from '@/components/DateCell'
import Button from '@/components/Button'

export default {
  name: 'Calendar',
  components: {
    DateCell,
    VButton: Button
  },
  data () {
    return {
      jpWeekNames: ['日', '月', '火', '水', '木', '金', '土'],
      currentYear: new Date().getFullYear(),
      currentMonth: new Date().getMonth() + 1
    }
  },
  computed: {
    beginningOfMonth () {
      return new Date(this.currentYear, this.currentMonth - 1)
    },
    endOfMonth () {
      return new Date(this.currentYear, this.currentMonth, 0)
    }
  },
  methods: {
    dateTimeFrom (weekRowIndex, weekIndex) {
      let dateIndex = weekRowIndex * 7 + weekIndex - this.beginningOfMonth.getDay()
      let date = dateIndex + 1
      if (date < 1 || this.endOfMonth.getDate() < date) {
        return null
      }
      return new Date(this.currentYear, this.currentMonth - 1, date)
    },
    setNextMonth () {
      let nextMonth = new Date(this.currentYear, this.currentMonth)
      this.currentYear = nextMonth.getFullYear()
      this.currentMonth = nextMonth.getMonth() + 1
    },
    setPrevMonth () {
      let prevMonth = new Date(this.currentYear, this.currentMonth - 2)
      this.currentYear = prevMonth.getFullYear()
      this.currentMonth = prevMonth.getMonth() + 1
    }
  }
}
</script>

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

table th {
  padding: 10px;
}

.button-wrapper {
  overflow: hidden;
}

.button-left {
  float: left;
}

.button-right {
  float: right;
}
</style>
