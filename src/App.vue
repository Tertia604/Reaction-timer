<template>
  <h1>Таймер реакции</h1>
  <button @click="start" :disabled="isPlaying">Пуск</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <Results v-if="showResults" :score="score" />
</template>

<script>
import { ref } from "vue";
import Block from "@/components/Block.vue";
import Results from "@/components/Results.vue";

export default {
  name: "App",
  components: { Block, Results },
  setup() {
    const isPlaying = ref(false);
    // задержка
    const delay = ref(null);
    // счёт
    const score = ref(null);
    // результаты
    const showResults = ref(false);

    // начало игры
    const start = () => {
      delay.value = 2000 + Math.random() * 5000;
      isPlaying.value = true;
      showResults.value = false;
    };

    // конец игры
    const endGame = (reactionTime) => {
      score.value = reactionTime;
      isPlaying.value = false;
      showResults.value = true;
    };

    return {
      isPlaying,
      score,
      delay,
      showResults,

      start,
      endGame,
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
  background: teal;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
  &:disabled {
    opacity: 0.2;
    cursor: not-allowed;
  }
}
</style>
