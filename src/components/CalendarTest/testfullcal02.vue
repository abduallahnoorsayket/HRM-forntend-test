<template>
  <Master>
    <template v-slot:content>
      <div class="app-main__inner">
        <full-calendar :config="config" :events="events" />
      </div>
    </template>
  </Master>
</template>

<script>
import Master from "../layouts/Master";

// import axios from "axios";
// import Swal from "sweetalert2";

import moment from "moment";
export default {
  name: "testfullcal02",
  components: { Master },
  data() {
    return {
      events: [
        {
          title: "test",
          allDay: true,
          start: moment(),
          end: moment().add(1, "d"),
        },
        {
          title: "another test",
          start: moment().add(2, "d"),
          end: moment().add(2, "d").add(2, "h"),
        },
      ],
      config: {
        defaultView: "month",
        eventRender: function (event, element) {
          console.log(event, element);
        },
      },
    };
  },
};
</script>

<style scoped></style>
