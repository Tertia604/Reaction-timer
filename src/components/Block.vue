<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Нажми на меня</div>
</template>

<script>
import { onUpdated, ref } from "@vue/runtime-core";
export default {
  props: {
    delay: {
      type: Number,
    },
  },
  setup(props, context) {
    const showBlock = ref(false);
    const timer = ref(null);
    const reactionTime = ref(0);

    setTimeout(() => {
      showBlock.value = true;
      startTimer();
    }, props.delay);

    onUpdated(() => console.log("updated"));

    const startTimer = () => {
      timer.value = setInterval(() => {
        reactionTime.value += 10;
      }, 10);
    };

    const stopTimer = () => {
      clearInterval(timer.value);

      context.emit("end", reactionTime.value);
    };

    return {
      showBlock,
      stopTimer,
    };
  },
};
</script>

<style lang="scss">
.block {
  width: 400px;
  border-radius: 20px;
  background: teal;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>