<template>
  <div class="clock">
    <div class="clock-face">
      <div
        :style="{ transform: `rotate(${hoursDegress}deg)` }"
        class="hand hour-hand"
      ></div>
      <div
        :style="{ transform: `rotate(${minsDegress}deg)` }"
        class="hand min-hand"
      ></div>
      <div
        :style="{ transform: `rotate(${secondsDegress}deg)` }"
        class="hand second-hand"
      ></div>
    </div>
  </div>
  <div>{{ hours }}:{{ mins }}:{{ seconds }}</div>
</template>
<script>
import dayjs from "dayjs";
import { reactive, inject, computed, readonly, toRefs, ref } from "vue";
export default {
  props: {
    dates: {
      type: String,
      default: "",
    },
  },
  // created: function () {
  //   this.moment = moment;
  // },
  setup(props) {
    const clock = ref(0);
    const seconds = ref(0);
    const mins = ref(0);
    const hours = ref(0);
    const secondsDegress = ref(0);
    const minsDegress = ref(0);
    const hoursDegress = ref(0);

    // const secondsDegress = ref(((seconds.value / 60) * 360))
    const { dates } = toRefs(props);
    const city = ref(dates.value.city);
    const region = ref(dates.value.region);
    const currentTime = () => {
      // console.log(dates.value.region);

      let locale = "en-US";
      let options_YYYY = {
        region,
        year: "numeric",
      };
      let options_HHMM = {
        timeZone: region.value,
        hour12: false,
        hour: "numeric",
        minute: "2-digit",
      };
      let options_MMDD = {
        region,
        month: "short",
        day: "numeric",
      };
      let options_SS = {
        region,
        month: "short",
        day: "numeric",
      };
      var options = {
        day: "numeric", //(e.g., 1)
        month: "short", //(e.g., Oct)
        year: "numeric", //(e.g., 2019)
        hour: "2-digit", //(e.g., 02)
        minute: "2-digit", //(e.g., 02)
        hour12: false, // 24 小時制
        timeZone: region.value, // 美國/紐約
      };
      // console.log(timezone);
      // console.log(dates);
      // console.log(region.value);
      clock.value = dayjs(new Date().toLocaleString(locale, options)).format(
        "hh:mm:ss"
      );
      hours.value = dayjs(new Date().toLocaleString(locale, options)).format(
        "hh"
      );
      mins.value = dayjs(new Date().toLocaleString(locale, options)).format(
        "mm"
      );
      seconds.value = new Date().getSeconds(locale, options);
      hoursDegress.value = (hours.value / 12) * 360;
      secondsDegress.value = (seconds.value / 60) * 360;
      minsDegress.value = (mins.value / 60) * 360;
    };

    setInterval(() => {
      currentTime();
    }, 1000);

    onMounted(() => {
      currentTime();
    });
    return {
      clock,
      city,
      region,
      hours,
      mins,
      seconds,
      secondsDegress,
      minsDegress,
      hoursDegress,
    };
  },
};
</script>
<style>
.clock {
  width: 30rem;
  height: 30rem;
  border: 20px solid white;
  border-radius: 50%;
  margin: 50px auto;
  position: relative;
  padding: 2rem;
  box-shadow: 0 0 0 4px rgba(0, 0, 0, 0.1), inset 0 0 0 3px #efefef,
    inset 0 0 10px black, 0 0 10px rgba(0, 0, 0, 0.2);
}

.clock-face {
  position: relative;
  width: 100%;
  height: 100%;
  transform: translateY(-3px); /* account for the height of the clock hands */
}

.clock-face:after {
  content: "";
  display: block;
  width: 30px;
  height: 30px;
  border-radius: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
}

.hand {
  position: absolute;
  width: 100%;
  height: 100%;
}

.second-hand:after {
  position: absolute;
  content: "";
  display: block;
  width: 5px;
  height: 50%;
  background-color: red;
  left: 50%;
  /* bottom: 50%; */
  transform: translate(-50%, 0%);
  /* transform: rotate(20deg); */
}

.min-hand:after {
  position: absolute;
  content: "";
  display: block;
  width: 10px;
  height: 40%;
  background-color: white;
  left: 50%;
  bottom: 50%;
  transform: translate(-50%, 0%);
}

.hour-hand:after {
  position: absolute;
  content: "";
  display: block;
  width: 15px;
  height: 20%;
  background-color: rgb(176, 6, 255);
  left: 50%;
  bottom: 50%;
  transform: translate(-50%, 0%);
}
</style>
