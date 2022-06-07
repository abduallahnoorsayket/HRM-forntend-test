<template>
  <div>
    <div class="long-title">
      <h3>Tasks for Employees </h3>
    </div>
    <DxScheduler
      :data-source="dataSource"
      :current-date="currentDate"
      :views="views"
      :height="500"
      :editing="false"
      :show-all-day-panel="false"
      :start-day-hour="7"
      start-date-expr="start.dateTime"
      end-date-expr="end.dateTime"
      text-expr="summary"
      time-zone="America/Los_Angeles"
      current-view="workWeek"
    />
  </div>
</template>
<script>
// import "whatwg-fetch";
import axios from "axios";
import DxScheduler from "devextreme-vue/scheduler";
import CustomStore from "devextreme/data/custom_store";

export default {
  name: "googleCal",
  components: {
    DxScheduler,
  },
  data() {
    return {
      views: ["day", "workWeek", "month"],
      currentDate: new Date(2022, 6, 1),
      dataSource: new CustomStore({
        load: (options) => this.getData(options, { showDeleted: false }),
      }),
    };
  },
  methods: {
    getData(_, requestOptions) {
      const PUBLIC_KEY = "AIzaSyB28zJFAcw4Nm6JpJKiXkUDmFaoCgZ6VzU";
      const CALENDAR_ID =
        "abdullahnoorsayket@gmail.com";
      const dataUrl = [
        "https://www.googleapis.com/calendar/v3/calendars/",
        CALENDAR_ID,
        "/events?key=",
        PUBLIC_KEY,
      ].join("");

      return axios
        .get(dataUrl, requestOptions)
        .then((response) => response.json())
        .then((data) => data.items);
    },
  },
};
</script>
<style>
.long-title h3 {
  font-family: "Segoe UI Light", "Helvetica Neue Light", "Segoe UI",
    "Helvetica Neue", "Trebuchet MS", Verdana;
  font-weight: 200;
  font-size: 28px;
  text-align: center;
  margin-bottom: 20px;
}
</style>
