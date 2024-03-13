<script setup>
import { ref, onBeforeMount, onUnmounted } from "vue";

const flipDate = ref(false);
const flipHour = ref(false);
const flipMinute = ref(false);
const flipSecond = ref(false);
const countDownDate = new Date("Jul 22, 2024 16:05:25").getTime();
let intervalId;
const now = ref(new Date().getTime());
const distance = ref(countDownDate - now.value);
const days = ref(Math.floor(distance.value / (1000 * 60 * 60 * 24)));
const hours = ref(
  Math.floor((distance.value % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
);
const minutes = ref(
  Math.floor((distance.value % (1000 * 60 * 60)) / (1000 * 60))
);
const seconds = ref(Math.floor((distance.value % (1000 * 60)) / 1000));

const formatCountdown = () => {
  const previousDays = days.value;
  const previousHours = hours.value;
  const previousMinutes = minutes.value;
  const previousSeconds = seconds.value;

  now.value = new Date().getTime();
  distance.value = countDownDate - now.value;
  days.value = Math.floor(distance.value / (1000 * 60 * 60 * 24));
  hours.value = Math.floor(
    (distance.value % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
  );
  minutes.value = Math.floor((distance.value % (1000 * 60 * 60)) / (1000 * 60));
  seconds.value = Math.floor((distance.value % (1000 * 60)) / 1000);
  if (days.value !== previousDays) {
    flipDate.value = !flipDate.value;
  }

  if (hours.value !== previousHours) {
    flipHour.value = !flipHour.value;
  }

  if (minutes.value !== previousMinutes) {
    flipMinute.value = !flipMinute.value;
  }

  if (seconds.value !== previousSeconds) {
    flipSecond.value = !flipSecond.value;
  }

  if (distance.value < 0) {
    clearInterval(intervalId);
    alert("Expired");
  }
};

onBeforeMount(() => {
  intervalId = setInterval(formatCountdown, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});
</script>

<template>
  <!-- <div> -->
  <div class="default-layout">
    <div class="header">WE'RE LUANCHING SOON</div>
    <div class="countdown-container">
      <div v-if="distance >= 0" class="countdown">
        <div>
          <div class="countdown-item days" :class="{ flip: flipDate }">
            <div class="textD">{{ days }}</div>
            <!-- <div>DAYS</div> -->
          </div>
          <div class="desc">DAYS</div>
        </div>
        <div>
          <div class="countdown-item hours" :class="{ flip: flipHour }">
            <div class="textH">{{ hours }}</div>
            <!-- <div>HOURS</div> -->
          </div>
          <div class="desc">HOURS</div>
        </div>
        <div>
          <div class="countdown-item minutes" :class="{ flip: flipMinute }">
            <div class="textMin">{{ minutes }}</div>
            <!-- <div>MINUTES</div> -->
          </div>
          <div class="desc">MINUTES</div>
        </div>
        <div>
          <div>
            <div class="countdown-item seconds" :class="{ flip: flipSecond }">
              <div class="textSec">{{ seconds }}</div>
              <!-- <div>SECONDS</div> -->
            </div>
            <div class="desc">SECONDS</div>
          </div>
        </div>
      </div>

      <div v-else class="expired">Expired</div>
    </div>
    <div class="footer">
      <div class="social">
        <nuxt-link to="https://www.facebook.com/"
          ><img
            src="../images/icon-facebook.svg"
            alt="facebook"
            class="facebook"
        /></nuxt-link>
        <nuxt-link to="https://www.pinterest.com/"
          ><img
            src="../images/icon-pinterest.svg"
            alt="pinterest"
            class="pinterest"
        /></nuxt-link>
        <nuxt-link to="https://www.instagram.com/"
          ><img
            src="../images/icon-instagram.svg"
            alt="instagram"
            class="instagram"
        /></nuxt-link>
      </div>
      <div class="descFooter">
        Challenge by
        <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
          >Frontend Mentor</a
        >. Coded by <a href="https://github.com/Preeyapornn">Preyapornn P</a>.
      </div>
    </div>
    <div>
      <div class="divHills">
        <img
          src="../images/pattern-hills.svg"
          class="hills"
          alt="pattern-hills"
        />
      </div>
      <img src="../images/bg-stars.svg" alt="bg-stars" class="bg-stars" />
    </div>
  </div>
  <!-- </div> -->
</template>

<style scoped>
@media screen and (max-width: 375px) {
  * {
    background-image: url("../images/bg-stars.svg");
  }
  .default-layout {
    padding: 10px 10px 0px 20px;
  }
  .header {
    font-size: 20px;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .hills {
    /* visibility: hidden; */
    width: 150%;
    bottom: 0;
    left: 0;
    position: absolute;
  }
  .bg-stars {
    visibility: hidden;
  }

  .footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    bottom: 0;
    left: 0;
    transform: translateY(100%);
    img:hover {
      cursor: pointer;
      transform: scale(1.2);
    }
  }
  .pinterest,
  .instagram,
  .facebook {
    margin-left: 10px;
  }
  .descFooter {
    font-size: 10px;
    margin-top: 10px;
  }
  .countdown {
    display: grid;
    grid-template-columns: repeat(4, 10px);
    margin-top: 30%;
    gap: 5em;
    font-size: 15px;
    /* align-items: center; */
  }
  .countdown-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    margin-bottom: 5em;
  }
  .desc {
    font-size: 10px;
    font-weight: bold;
    margin-top: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .textD:hover,
  .textH:hover,
  .textMin:hover,
  .textSec:hover {
    color: hsl(345, 82%, 52%);
  }
  .textD,
  .textH,
  .textMin,
  .textSec {
    /* font-size: 5em; */
    font-weight: 800;
    color: hsl(345, 95%, 68%);
    /* margin-bottom: 10px; */
    text-align: center;
    background: linear-gradient(
      to bottom,
      hsl(235, 16%, 14%) 50%,
      hsl(237, 17%, 21%) 50%
    );
    padding: 10px 10px 10px 10px;
    border: solid 1px hsl(237, 17%, 21%);
    border-radius: 10px;
    box-shadow: 2px 2px 4px 3px rgb(0, 0, 0, 0.377);
    z-index: 44;
    position: relative;
    /* transition: all 0.3s ease-in-out; */
    /* transform-style: preserve-3d; */
    cursor: pointer;
  }
  .textD::after,
  .textH::after,
  .textMin::after,
  .textSec::after {
    position: absolute;
    content: "";
    width: 10%;
    height: 10%;
    background-color: hsl(346, 26%, 7%);
    left: 0px;
    top: 44%;
    border-radius: 0 50% 50% 0;
  }

  .textD::before,
  .textH::before,
  .textMin::before,
  .textSec::before {
    position: absolute;
    content: "";
    width: 10%;
    height: 10%;
    background-color: hsl(346, 26%, 7%);
    right: 0px;
    top: 44%;
    border-radius: 50% 0 0 50%;
  }

  .days,
  .hours,
  .minutes,
  .seconds {
    display: flex;
    flex-direction: column;
    align-items: center;
    /* margin-right: 10px; */
  }
  a {
    text-decoration: none;
    color: hsl(237, 18%, 59%);
    font: 800 16px;
  }
  .expired {
    font-size: 1.2em;
    text-align: center;
  }

  .countdown-item {
    border-radius: 5px;

    perspective: 1000px;
  }

  .flip {
    animation: flip 0.6s ease-in-out forwards;
  }

  @keyframes flip {
    0% {
      transform: rotateX(0deg);
    }
    50% {
      transform: rotateX(90deg);
    }
    100% {
      transform: rotateX(0deg);
    }
  }
  .flip-card {
    background-color: transparent;
    perspective: 1000px;
  }
  .flipped .flip-card-inner {
    transform: rotateX(360deg);
  }
}

@media screen and (min-width: 768px) {
  .hills {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: -1;
    width: 100%;
    /* transform: translateY(50%); */
  }

  .bg-stars {
    position: absolute;
    right: 0;
    top: 0;
    z-index: -1;
  }

  /* .container {
    margin-top: 10%;
    font-family: "Red Hat Text", sans-serif;
  } */

  .footer {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: absolute;
    z-index: 99 !important;
    bottom: 0;
    left: 45vh;
    transform: translateY(-50%);
  }

  .social {
    display: flex;
    justify-content: space-between;
    width: 100px;
    margin-top: 1%;

    img {
      margin-bottom: 10px;
    }

    :hover {
      cursor: pointer;
      transform: scale(1.2);
    }
  }

  a {
    text-decoration: none;
    color: hsl(237, 18%, 59%);
    font: 800 16px;
  }

  .countdown-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }

  .header {
    display: flex;
    font-weight: bold;
    font-size: 150%;
    font-family: "Red Hat Text", sans-serif;
    color: white;
    letter-spacing: 8px;
    left: 50%;
    transform: translateX(30%);
  }

  .countdown {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    margin-top: 10%;
    gap: 5em;
  }
  .group {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1em;
  }
  .desc {
    /* margin-top: 1em; */
    display: flex;
    justify-content: center;
    align-items: center;

    /* margin-left: 9em; */
  }
  .textD,
  .textH,
  .textMin,
  .textSec {
    font-size: 5em;
    font-weight: 800;
    color: hsl(345, 95%, 68%);
    /* margin-bottom: 10px; */
    text-align: center;
    background: linear-gradient(
      to bottom,
      hsl(235, 16%, 14%) 50%,
      hsl(237, 17%, 21%) 50%
    );
    padding: 20px;
    border: solid 1px hsl(237, 17%, 21%);
    border-radius: 10px;
    box-shadow: 2px 2px 4px 3px rgb(0, 0, 0, 0.377);
    z-index: 44;
    position: relative;
    /* transition: all 0.3s ease-in-out; */
    /* transform-style: preserve-3d; */
    cursor: pointer;

    :active {
      /* transform: translate(360deg); */
    }
  }

  .textD:hover,
  .textH:hover,
  .textMin:hover,
  .textSec:hover {
    color: hsl(345, 82%, 52%);
  }

  .textD::after,
  .textH::after,
  .textMin::after,
  .textSec::after {
    position: absolute;
    content: "";
    width: 10%;
    height: 10%;
    background-color: hsl(346, 26%, 7%);
    left: 0px;
    top: 44%;
    border-radius: 0 50% 50% 0;
  }

  .textD::before,
  .textH::before,
  .textMin::before,
  .textSec::before {
    position: absolute;
    content: "";
    width: 10%;
    height: 10%;
    background-color: hsl(346, 26%, 7%);
    right: 0px;
    top: 44%;
    border-radius: 50% 0 0 50%;
  }

  .days,
  .hours,
  .minutes,
  .seconds {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-right: 10px;
  }

  .expired {
    font-size: 1.2em;
    text-align: center;
  }

  .countdown-item {
    border-radius: 5px;

    perspective: 1000px;
  }

  .flip {
    animation: flip 0.6s ease-in-out forwards;
  }

  @keyframes flip {
    0% {
      transform: rotateX(0deg);
    }
    50% {
      transform: rotateX(90deg);
    }
    100% {
      transform: rotateX(0deg);
    }
  }
  .flip-card {
    background-color: transparent;
    perspective: 1000px;
  }
  .flipped .flip-card-inner {
    transform: rotateX(360deg);
  }
}
</style>
