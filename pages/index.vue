<template>
  <div class="wrapper">
    <!-- 時鐘 -->
    <div v-for="(item, index) in dates" :key="index" class="box">
      <!-- <ComponentsClock> -->
      <!-- {{item}} -->
      <Clock :dates="item" />
    </div>
    <!-- 墊子時鐘 -->
    <div class="time">
      <p>
        <span>{{ minText }}</span
        >:<span>{{ secondsText }}</span
        >:<span>{{ hour }}</span>
      </p>
    </div>
    <!-- <div v-for="(item, index) in dates" :key="index">{{item}}</div> -->
  </div>
</template>
<script>
// import dayjs from 'dayjs'

import { reactive, inject, computed, readonly } from "vue";
import clock from "~~/components/clock.vue";
export default {
  components: { clock },
  setup() {
    const minText = ref(0);

    const secondsText = ref(0);

    const hour = ref(0);

    const startTimer = () => {};

    onMounted(() => {
      startTimer();
    });

    const dates = reactive([
      { city: "Honolulu", region: "Pacific/Honolulu" },
      // { city: "Anchorage", region: "America/Anchorage" },
      { city: "Los Angeles", region: "America/Los_Angeles" },
      // { city: "San Francisco", region: "America/Los_Angeles" },
      // { city: "Vancouver", region: "America/Vancouver" },
      { city: "Phoenix", region: "America/Phoenix" },
      // { city: "Denver", region: "America/Denver" },
      { city: "Costa Rica", region: "America/Costa_Rica" },
      // { city: "Chicago", region: "America/Chicago" },
      { city: "Cancun", region: "America/Cancun" },
      // { city: "Jamaica", region: "America/Jamaica" },
      // { city: "Toronto", region: "America/Toronto" },
      { city: "Puerto Rico", region: "America/Puerto_Rico" },
      { city: "Dublin", region: "Europe/Dublin" },
      { city: "London", region: "Europe/London" },
      { city: "Rome", region: "Europe/Rome" },
      { city: "Vatican", region: "Europe/Vatican" },
      // { city: "Berlin", region: "Europe/Berlin" },
      // { city: "Prague", region: "Europe/Prague" },
      // { city: "Madrid", region: "Europe/Madrid" },
      // { city: "Paris", region: "Europe/Paris" },
      // { city: "Warsaw", region: "Europe/Warsaw" },
      // { city: "Algiers", region: "Africa/Algiers" },
      // { city: "Athens", region: "Europe/Athens" },
      // { city: "Cairo", region: "Africa/Cairo" },
      // { city: "Johannesburg", region: "Africa/Johannesburg" },
      // { city: "Istanbul", region: "Europe/Istanbul" },
      // { city: "Jerusalem", region: "Asia/Jerusalem" },
      // { city: "Baghdad", region: "Asia/Baghdad" },
      // { city: "Kuwait", region: "Asia/Kuwait" },
      // { city: "Addis Ababa", region: "Africa/Addis_Ababa" },
      // { city: "Tehran", region: "Asia/Tehran" },
      // { city: "Moscow", region: "Europe/Moscow" },
      // { city: "Katmandu", region: "Asia/Katmandu" },
      // { city: "Hong Kong", region: "Asia/Hong_Kong" },
      // { city: "Kuala Lumpur", region: "Asia/Kuala_Lumpur" },
      // { city: "Singapore", region: "Asia/Singapore" },
      // { city: "Perth", region: "Australia/Perth" },
      // { city: "Tokyo", region: "Asia/Tokyo" },
      // { city: "Melbourne", region: "Australia/Melbourne" }
    ]);
    return {
      minText,
      secondsText,
      hour,
      dates,
      startTimer,
    };
  },
};
</script>

<style>
.wrapper {
  background-color: #ddd;
  height: auto;
}

.box {
  border: 1px solid blue;
  min-width: 200px;
  height: fit-content;
}
</style>
