<template>
  <div>
    <div class="hpbars">
      <p>Player (you)</p>
      <div class="bar" :style="{ width: playerHp + '%'}">{{ playerHp }}</div>
      <p>Enemy</p>
      <div class="bar" :style="{ width: enemyHp + '%'}">{{ enemyHp }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HealthBars",
  props: {
    playerHp: Number,
    enemyHp: Number
  }
};
</script>

<style scoped>
.hpbars {
  text-align: center;
}
.bar {
  background: greenyellow;
  margin: auto;
  border-radius: 20px;
  height: 40px;
}
</style>