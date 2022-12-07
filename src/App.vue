<script>
import MainView from "./components/game/MainScreen.vue";
import InteractScreen from "./components/game/InteractScreen.vue";
import ResultScreen from "./components/game/ResultScreen.vue";
import CopyRight from "./components/game/CopyRightScreen.vue";
import { shuffled } from "./utils/array.js";
export default {
  name: "App",
  components: {
    MainView,
    InteractScreen,
    ResultScreen,
    CopyRight,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      time: 0,
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCard = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      // const secondCard = firstCard.map((firstCard)=>{
      //   return firstCard;
      // });
      const secondCard = [...firstCard];
      const Card = [...firstCard, ...secondCard];
      this.settings.cardContext = shuffled(shuffled(shuffled(Card)));
      this.settings.startedAt = new Date().getTime();
      // data is ready
      this.statusMatch = "match";
    },
    onGetResults() {
      console.log("hoan thanh");
      this.statusMatch = "finish";
      this.time = new Date().getTime() - this.settings.startedAt;
      return this.time;
    },
  },
};
</script>

<template>
  <main-view v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart" />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardContext="settings.cardContext"
    @onFinish="onGetResults"
  />
  <result-screen
    v-if="statusMatch === 'finish'"
    :time="time"
    @onstartAgain="statusMatch='default'"
  />
  <copy-right />
</template>

<style scoped></style>
