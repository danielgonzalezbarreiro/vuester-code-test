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
  color: #e4fde1;
  text-align: center;
}
.bar {
  color: #f45b69;
  font-size: 1.5rem;
  background: greenyellow;
  margin: auto;
  border-radius: 20px;
  height: 40px;
}
</style>