<template>
  <h1>Let's see how fast your reflexes is</h1>
  <button
    @click="startGame"
    :disabled="hasStarted"
    :class="{ disabled: hasStarted }"
  >
    Click to Start
  </button>
  <Block v-if="isPlaying" @end="showResult" />
  <Result v-if="hasEnded" :result="reactionTime" />
</template>

<script>
import Block from "./components/Block.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Block,
    Result,
  },
  data() {
    return {
      // track whether player is playing
      isPlaying: false,
      // track whether the game has ended or started
      hasStarted: false,
      hasEnded: false,
      // amount of delay before the block shows
      delay: null,
      // amount of milliseconds the user can click the box
      reactionTime: null,
    };
  },

  methods: {
    // called when user click the play button
    startGame() {
      this.hasStarted = true;
      this.hasEnded = false;
      // generate random secs of delay before the block appears
      this.delay = Math.floor(Math.random() * 5000 + 2000);
      setTimeout(() => (this.isPlaying = true), this.delay);
    },

    // called after the block has been clicked, triggered after listening to custom (end) emit events
    // Reaction time will be displayed
    showResult(reactionTime) {
      this.reactionTime = reactionTime;
      this.hasEnded = true;
      this.isPlaying = false;
      this.hasStarted = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  background: darkcyan;
  color: #fff;
  letter-spacing: 1.1px;
  font-size: 16px;
  text-transform: uppercase;
  font-weight: 600;
  cursor: pointer;
}

.disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
