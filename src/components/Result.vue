<template>
  <div class="result">
    <p>Reaction Time: {{ result }}ms</p>
    <p class="grade">{{ grade }}</p>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: ["result"],

  data() {
    return {
      grade: null,
    };
  },

  mounted() {
    if (this.result <= 100) {
      this.grade = "You got Ninja Reflexes!";
    } else if (this.result <= 200) {
      this.grade = "Fast enough";
    } else {
      this.grade = "Snail Pace...";
    }
  },
};
</script>

<style>
.result {
  margin: 50px auto;
  text-align: center;
}

.grade {
  font-weight: 700;
  color: darkblue;
  font-size: 25px;
}
</style>
