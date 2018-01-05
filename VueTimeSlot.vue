<template lang="html">
  <div>
   <span class="arrow-block" v-on:click="addDate"> Add Date</span>
    <div class="vue-time-slot-container">
      <div class="vue-time-slot-table-row-header">
        <span class="vue-time-slot-column-header">Time</span>
        <span class="vue-time-slot-row-header" v-for="value in dateRange">
          {{value.label}} AM
        </span>
        <span class="vue-time-slot-row-header" v-for="value in dateRange">
          {{value.label}} PM
        </span>
      </div>
      <div class="vue-time-slot-calendar-table" id="vue-time-slot-calendar-table">
        <div class="vue-time-slot-day-header" v-for="day in dayIndex">
          <span class="vue-time-slot-column-header">{{day.label}}</span>
          <span class="vue-time-slot-cell" v-for="(value, key) in dateRange" v-on:click="slot($event, value, 'am', day)">
            {{value.label}} AM
          </span>
          <span class="vue-time-slot-cell" v-for="value in dateRange" v-on:click="slot($event, value, 'pm', day)">
            {{value.label}} PM
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    min: {
      type: Number,
      default: 3
    }
  },
  watch: {},
  data() {
    return {
      dateRange: [
        {
          label: "1 - 2",
          start_time: "01:00:00",
          end_time: "02:00:00"
        },
        {
          label: "2 - 3",
          start_time: "02:00:00",
          end_time: "03:00:00"
        },
        {
          label: "3 - 4",
          start_time: "03:00:00",
          end_time: "04:00:00"
        },
        {
          label: "4 - 5",
          start_time: "04:00:00",
          end_time: "05:00:00"
        },
        {
          label: "5 - 6",
          start_time: "05:00:00",
          end_time: "06:00:00"
        },
        {
          label: "6 - 7",
          start_time: "06:00:00",
          end_time: "07:00:00"
        },
        {
          label: "7 - 8",
          start_time: "07:00:00",
          end_time: "08:00:00"
        },
        {
          label: "8 - 9",
          start_time: "08:00:00",
          end_time: "09:00:00"
        },
        {
          label: "9 - 10",
          start_time: "09:00:00",
          end_time: "10:00:00"
        },
        {
          label: "10 - 11",
          start_time: "10:00:00",
          end_time: "11:00:00"
        },
        {
          label: "11 - 12",
          start_time: "11:00:00",
          end_time: "12:00:00"
        }
      ],
      dayIndex: [],
      todaysDate: this.formatDate(new Date(), "long"),
      dateIndex: 0
    };
  },
  mounted() {
    let todaysDate = new Date(new Date().getTime() + 0 * 24 * 60 * 60 * 1000);
    for (var index = 0; index < this.min; index++) {
      this.dayIndex.push(
        this.formatDate(this.nextDate(this.dateIndex), "short")
      );
      this.dateIndex++;
    }
  },
  methods: {
    formatDate(date, type) {
      let monthNames = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ];
      var day = date.getDate();
      var monthIndex = date.getMonth();
      var year = date.getFullYear();

      let month =
        type == "short"
          ? monthNames[monthIndex].slice(0, 3)
          : monthNames[monthIndex];

      return {
        label: day + ", " + month + " ",
        value: date
      };
    },
    addDate() {
      this.dayIndex.push(
        this.formatDate(this.nextDate(this.dateIndex), "short")
      );
      this.dateIndex++;
    },
    nextDate(index) {
      return new Date(new Date().getTime() + index * 24 * 60 * 60 * 1000);
    },
    slot(event, value, type, day) {
      event.target.classList.toggle("vue-time-slot-active-cell");
      value.mode = type;
      value.date = day.value;
      this.$emit("callback", value);
    }
  }
};
</script>

<style lang="css">
.vue-time-slot-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  font-size: 13px
}

.vue-time-slot-row-header {
  border: none !important;
  text-align: left;
  cursor: pointer;
  background-color: #ccc;
  font-size: 12px;
  padding: 7px;
  color: #000;
  width: 100%;
  height: 17px;
}

.vue-time-slot-column-header {
  border: none !important;
  text-align: center;
  cursor: pointer;
  background-color: #ccc;
  font-size: 12px;
  padding: 5px 0;
  color: #000;
}

.vue-time-slot-cell{
  padding: 7px;
  background-color: #fff;
  border-style: solid;
  border-color: #ccc;
  border-width: 1px 1px 0 0;
  text-align: center;
  cursor: pointer;
  color: #fff;
  font-size: 12px;
}
.vue-time-slot-cell:last-child{
  border-width: 1px 1px 1px 0;
}
.vue-time-slot-cell:hover{
  background-color: #fd8f91;
}

.vue-time-slot-active-cell {
  background-color: #ef4144;
  color: #fff;
}
.vue-time-slot-active-cell:hover{
  background-color: #ef4144;
}

.vue-time-slot-table-row-header {
  display: flex;
  flex-direction: column;
  width: 70px;
}
.vue-time-slot-day-header {
  display: flex;
  flex-direction: column;
  width: 70px;
}
.vue-time-slot-calendar-table {
  background-color: transparent;
  overflow: auto;
  white-space: nowrap;
  width: 85%;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

.vue-time-slot-calendar-table .vue-time-slot-day-header:first-child{
  border-style: solid;
  border-color: #ccc;
  border-width: 0 0 0 1px;
}

.arrow-block {
  font-size: 25px;
  font-weight: bolder;
  color: #ef4144;
  cursor: pointer;
  margin: -10px 15px;
}
</style>
