<template>
  <div>
    <div class="hpbars">
      <div class="playerbar">
        <p>Player</p>
        <div class="bar" :style="{ width: enemyHp + '%'}">{{ playerHp }}</div>
      </div>
      <div class="enemybar">
        <p>Enemy</p>
        <div class="bar" :style="{ width: enemyHp + '%'}">{{ enemyHp }}</div>
      </div>
    </div>
    <div class="xpbar">
      <p>XP</p>
      <div class="barxp" :style="{ width: xp + '%' }">{{xp}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HealthBars",
  props: {
    playerHp: Number,
    enemyHp: Number,
    xp: Number
  }
};
</script>

<style scoped>
.hpbars {
  color: #e4fde1;
  text-align: center;
  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: center;
  margin: 0 auto;
  padding: 1rem;
}

.bar {
  color: green;
  border: 4px solid #f45b69;
  font-weight: bold;
  background: greenyellow;
  margin: auto;
  height: 40px;
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
}

.playerbar {
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
  flex-basis: 50%;
}
.enemybar {
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
  flex-basis: 50%;
}

.barxp {
  color: #028090;
  font-weight: bold;
  background: cyan;
  margin: auto;
  border-radius: 20px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
}
</style>