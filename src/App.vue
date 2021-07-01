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
          Start
        </button>
        <button class="countdown-app__btn" v-on:click="stopCountDown">
          Stop
        </button>
        <button class="countdown-app__btn" v-on:click="resetCountDown">
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
main {
  display: flex;
  justify-content: center;
  align-item: center;

  .countdown-app {
    width: 600px;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    &__btns {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 450px;
    }
    &__btn {
      width: 80px;
      height: 50px;
    }

    &__time {
      font-size: 60px;
    }
  }
}
</style>
