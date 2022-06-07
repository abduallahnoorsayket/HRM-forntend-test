<template>
  <Master>
    <template v-slot:content>
      <div class="app-main__inner">
        <!-- <div class="app-page-title">
          <div class="page-title-wrapper">
            <div class="page-title-heading">
              <div class="page-title-icon">
                <i class="fas fa fa-cog icon-gradient bg-tempting-azure"></i>
              </div>
              Test calendar
            </div>
          </div>
        </div> -->
        <!-- <full-calendar :events="events"></full-calendar> -->
        <FullCalendar :options="calendarOptions" />
      </div>
    </template>
  </Master>
</template>

<script>
import "@fullcalendar/core/vdom"; // solves problem with Vite
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";
//
import Master from "../layouts/Master";
// import { FullCalendar } from "vue-full-calendar";
// import 'fullcalendar/dist/fullcalendar.css'
// import "@fullcalendar/core/vdom"; // solves problem with Vite
// import FullCalendar from "@fullcalendar/vue";
// import dayGridPlugin from "@fullcalendar/daygrid";
// import interactionPlugin from "@fullcalendar/interaction";
// import axios from "axios";
// import Swal from "sweetalert2";

export default {
  name: "testfullcal",
  components: { Master, FullCalendar },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
        dateClick: this.handleDateClick,
        events: [
          { title: "event 1", date: "2022-05-11" },
          { title: "event 2", date: "2022-05-08" },
        ],
      },
    };
  },

  methods: {
    handleDateClick: function (arg) {
      alert("date click! " + arg.dateStr);
    },
  },

  created() {},

  computed: {},
};
</script>

<style scoped></style>
