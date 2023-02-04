<template>
  <div>
    <div id="title">
      <div class="button" v-on:click="toPrevMonth">&#10094;</div>
      <div class="button" v-on:click="toNextMonth">&#10095;</div>
      {{ year }}년 {{ month }}월
    </div>
    <div id="calendar">
      <div v-for="one in days" :key="one">{{ one }}</div>
      <div
        v-for="lastDates in lastDatesArray"
        :key="'last' + lastDates"
        id="notThisMonth"
      >
        {{ lastDates }}
      </div>
      <div v-for="thisDates in datesArray" :key="thisDates">
        {{ thisDates }}
      </div>
      <div
        v-for="nextDates in nextDatesArray"
        :key="'next' + nextDates"
        id="notThisMonth"
      >
        {{ nextDates }}
      </div>
    </div>
  </div>
</template>
<script>
import dayjs from "dayjs";
import "dayjs/locale/ko";
dayjs.locale("ko");

export default {
  created() {},
  data() {
    let today = dayjs();
    return {
      selected: today,
      year: today.year(),
      month: today.month() + 1,
      date: today.date(),
      firstday: today.set("date", 1).day(),
      lastDate: today.daysInMonth(),
      lastMonthLastDate: today.subtract(1, "month").daysInMonth(),
      lastDatesArray: "",
      datesArray: "",
      nextDatesArray: "",
      days: [
        "일요일",
        "월요일",
        "화요일",
        "수요일",
        "목요일",
        "금요일",
        "토요일",
      ],
    };
  },
  created() {
    this.setCalendar(this.selected);
  },
  methods: {
    setCalendar: function (up) {
      let updated = up;
      console.log("updated.month()::", updated.month());
      //다시 한번더 변수 할당 => 다르게 할 수 있을 것 같은데?
      this.year = updated.year();
      this.month = updated.month() + 1;
      this.date = updated.date();
      this.firstday = updated.set("date", 1).day();
      this.lastday = updated.set("date", updated.daysInMonth()).day();
      this.lastDate = updated.daysInMonth();
      this.lastMonthLastDate = updated.subtract(1, "month").daysInMonth();
      //현재 선택달에서 배열 다시 만들기
      this.datesArray = Array.from({ length: this.lastDate }, (v, i) => i + 1);
      this.lastDatesArray = Array.from(
        { length: this.firstday },
        (v, i) => this.lastMonthLastDate - this.firstday + i + 1
      );
      this.nextDatesArray = Array.from(
        { length: 6 - this.lastday },
        (v, i) => i + 1
      );
    },
    toPrevMonth: function () {
      if (this.selected.month() < 0) {
        this.selected = this.selected.subtract(1, "year").set("M", 11);
      } else {
        this.selected = this.selected.subtract(1, "month");
      }
      this.setCalendar(this.selected);
      return console.log(this.selected);
    },
    toNextMonth: function () {
      if (this.selected.month() > 11) {
        this.selected = this.selected.add(1, "year").set("M", 0);
      } else {
        this.selected = this.selected.add(1, "month");
      }
      this.setCalendar(this.selected);
    },
  },
};
</script>
<style scoped>
#calendar {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-template-rows: repeat(7, 100px);
}

#calendar div {
  border: 1px solid pink;
  text-align: center;
  padding-top: 10px;
}

#title {
  font-size: 40px;
  font-weight: bold;
  display: flex;
  align-items: center;
}

#title .button {
  font-size: 30px;
  line-height: 30px;
  margin: 10px 20px;
  padding: 5px 5px;
  cursor: pointer;
  width: 30px;
  height: 30px;

  text-align: center;
  border-radius: 100%;
}

#title .button:hover {
  background: lightgray;
}

#notThisMonth {
  color: lightgray;
}
</style>
