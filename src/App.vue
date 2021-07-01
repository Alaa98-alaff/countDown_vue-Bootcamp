<template>
  <main>
    <div class="countdown-app">
      <h1 class="countdown-app__time">
        {{ time <= 59 ? "0:" + time : oneMin }}
      </h1>
      <section class="countdown-app__btns">
        <button
          class="countdown-app__btn"
          v-on:click="countDown"
          :disabled="isActive"
        >
          <img class="btn__icon" src="./assets/start.png" alt="start" />
          Start
        </button>
        <button class="countdown-app__btn" v-on:click="stopCountDown">
          <img class="btn__icon" src="./assets/stop.png" alt="stop" />
          Stop
        </button>
        <button class="countdown-app__btn" v-on:click="resetCountDown">
          <img class="btn__icon" src="./assets/reset.png" alt="reset" />
          Reset
        </button>
      </section>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    let stoped = false;
    let time = ref(60);
    let isActive = ref(false);
    let oneMin = ref("1:00");

    function countDown() {
      if (stoped === false && time.value > 0) {
        time.value -= 1;
        isActive.value = true;

        setTimeout(() => {
          countDown();
        }, 1000);
      }
    }

    function stopCountDown() {
      stoped = true;
      setTimeout(() => {
        stoped = false;
        isActive.value = false;
      }, 800);
    }

    function resetCountDown() {
      stopCountDown();
      time.value = 60;
    }
    return {
      countDown,
      time,
      stopCountDown,
      resetCountDown,
      stoped,
      isActive,
      oneMin,
    };
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Luckiest+Guy&display=swap");
main {
  font-family: "Luckiest Guy", cursive;
  display: flex;
  justify-content: center;
  align-item: center;

  .countdown-app {
    margin-top: 50px;
    width: 600px;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: grey;
    border-radius: 20px;

    &__btns {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 450px;
    }
    &__btn {
      font-family: "Luckiest Guy", cursive;
      letter-spacing: 2px;
      width: 150px;
      height: 80px;
      border: none;
      margin: 10px;
      cursor: pointer;
      border-radius: 20px;
      display: flex;
      justify-content: space-evenly;
      align-items: center;
      // background-color: grey;
    }

    &__time {
      font-size: 60px;
    }

    .btn__icon {
      width: 40px;
      height: 40px;
    }
  }
}
</style>
