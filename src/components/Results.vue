<template>
  <p>Таймер реакции - {{ score }} ms</p>
  <p class="rank">{{ rank }}</p>
</template>

<script>
import { ref } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";
export default {
  props: {
    score: {
      type: Number,
    },
  },
  setup(props) {
    const rank = ref(null);

    onMounted(() => {
      if (props.score < 250) {
        rank.value = "Самый быстрый палец на всём диком западе";
      } else if (props.score < 400) {
        rank.value = "Быстрый";
      } else {
        rank.value = "Тренируйся больше";
      }
    });

    return {
      rank,
    };
  },
};
</script>

<style lang="scss">
.rank {
  font-size: 1.4em;
  color: teal;
  font-weight: bold;
}
</style>