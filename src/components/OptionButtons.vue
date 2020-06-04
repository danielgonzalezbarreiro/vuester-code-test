<template>
  <div>
    <div class="options">
      <button @click="attackEvent">ATTACK</button>
      <button @click="specialAttackEvent">SPECIAL ATTACK</button>
      <button @click="healEvent">HEAL</button>
      <button @click="giveUpEvent">GIVE UP</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "OptionButtons",
  props: {
    specialAttackCounter: Number,
    potionsCounter: Number
  },
  methods: {
    attackEvent() {
      this.$emit("attack");
    },
    healEvent() {
      this.$emit("heal");
    },
    specialAttackEvent() {
      this.$emit("specialAttack");
    },
    giveUpEvent() {
      this.$emit("giveUp");
    }
  }
};
</script>

<style scoped>
.options {
  width: 80%;
  padding: 1rem;
  margin: auto;
  margin-top: 1rem;
}
.options button {
  color: #e4fde1;
  border: 3px solid #f45b69;
  background: #028090;
  padding: 0.5rem 1rem;
  margin: 0.667rem;
  font-weight: bold;
}

.options button:hover {
  color: #114b5f;
  border: 3px solid #f45b69;
  background: #e4fde1;
  padding: 0.5rem 1rem;
  margin: 0.667rem;
  font-weight: bold;
}
</style>