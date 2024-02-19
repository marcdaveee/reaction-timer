<template>
  <div v-if="isPlaying" class="block" @click="getReactionTime">
    <p>Click Me!</p>
  </div>
</template>

<script>
export default {
  name: "Block",

  data() {
    return {
      // amount of ms the player can click the block right after it appears
      reactionTime: null,
      currentMs: 0,
      currentInterval: null,
      //   game ends after user clicks the block
      isPlaying: false,
    };
  },

  // A Lifecycle hook that will be called when the Block component is rendered
  // starts the timer
  mounted() {
    this.currentInterval = setInterval(() => (this.currentMs += 1), 1);
    this.isPlaying = true;
  },

  methods: {
    // Called when user clicked the block after it appears and get the reaction time in ms
    getReactionTime() {
      clearInterval(this.currentInterval);
      this.reactionTime = this.currentMs;
      this.endGame();
    },

    // Game ends and pass the reaction time data to the parent (App.vue)
    endGame() {
      this.isPlaying = false;
      this.$emit("end", this.reactionTime);
    },
  },
};
</script>

<style>
.block {
  width: 400px;
  background: lightblue;
  padding: 100px 0;
  margin: 40px auto;
  text-align: center;
  border-radius: 4px;
}
</style>
