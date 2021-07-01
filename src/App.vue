<template>
  <main>
    <div class="countdown-app">
      <h1 class="countdown-app__time">{{ time }}</h1>
      <section class="countdown-app__btns">
        <button class="countdown-app__btn" v-on:click="countDown">Start</button>
        <button class="countdown-app__btn">Stop</button>
      </section>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    let time = ref(60);
    function countDown() {
      if (time.value > 0) {
        time.value -= 1;
      }

      setInterval(() => {
        if (time.value > 0) {
          time.value -= 1;
        }
      }, 1000);

      console.log("TEST");
    }
    return { countDown, time };
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
      width: 300px;
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
