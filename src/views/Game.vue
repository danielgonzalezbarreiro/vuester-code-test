<template>
  <div>
    <!--BARRAS DE VIDA -->
    <HealthBars :playerHp="playerHp" :enemyHp="enemyHp" :xp="xp"></HealthBars>
    <!--/BARRAS DE VIDA -->
    <!--OPCIONES DE JUEGO -->
    <OptionButtons
      v-on:attack="attack()"
      v-on:heal="heal()"
      v-on:specialAttack="specialAttack()"
      v-on:giveUp="giveUp()"
      :specialAttackCounter="specialAttackCount"
      :potionsCounter="potions"
    ></OptionButtons>
    <!--/OPCIONES DE JUEGO -->
    <p class="counters">Special Attack: {{specialAttackCount}} Potions: {{potions}} Level: {{level}}</p>
    <!-- LOGS -->
    <Logs :logs="logs"></Logs>
    <!-- /LOGS -->
  </div>
</template>

<script>
import HealthBars from "@/components/HealthBars.vue";
import OptionButtons from "@/components/OptionButtons.vue";
import Swal from "sweetalert2";
import Logs from "@/components/Logs.vue";

export default {
  name: "Game",
  components: {
    HealthBars,
    OptionButtons,
    Logs
  },
  data() {
    return {
      playerHp: 80,
      enemyHp: 80,
      potionHp: 20,
      specialAttackHp: 20,
      specialAttackCount: 0,
      potions: 0,
      logs: [],
      level: 1,
      xp: 0
    };
  },
  methods: {
    attack() {
      let damage = this.calculateDamage(3, 10);
      this.enemyHp -= damage;
      this.xp += 2;
      if (this.xp === 10) {
        this.xp = 0;
        this.level++;
        this.specialAttackCount++;
        this.potions++;
      }

      let log = { player: "You hit", damage: damage + " hp to enemy" };
      this.logs.splice(0);
      this.hpControll();
      this.enemyAttack();
      this.logs.unshift(log);
    },
    calculateDamage(min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    enemyAttack() {
      let damage = this.calculateDamage(5, 12);
      this.playerHp -= damage;

      let log = { player: "Enemy hits you", damage: damage + "hp" };
      this.logs.splice(1);
      this.logs.unshift(log);
      this.hpControll();
    },
    heal() {
      if (this.playerHp <= 40 && this.potions != 0) {
        this.potions--;
        this.playerHp += this.potionHp;

        let log = { health: "You heal " + this.potionHp + " hp" };
        this.enemyAttack();
        this.logs.unshift(log);
      }
    },
    specialAttack() {
      if (this.specialAttackCount > 0) {
        this.specialAttackCount--;
        this.enemyHp -= this.specialAttackHp;

        let log = {
          player: "Special Attack hits ",
          damage: this.specialAttackHp + " hp to enemy"
        };
        this.enemyAttack();
        this.logs.unshift(log);
      }
    },

    giveUp() {
      this.playerHp = 80;
      this.enemyHp = 80;
      this.specialAttackCount = 3;
      this.potions = 2;

      Swal.fire({
        title: "Surrender",
        text: "Nobody can defeat me",
        confirmButtonText: "Cry!"
      });
      this.goHome();
    },
    goHome() {
      this.$router.push("/");
    },
    hpControll() {
      if (this.playerHp <= 0) {
        this.playerHp = 0;

        Swal.fire({
          title: "Defeat",
          text: "If u try again, dead again",
          confirmButtonText: ":/"
        });
        this.goHome();
      }
      if (this.enemyHp <= 0) {
        this.enemyHp = 0;

        Swal.fire({
          title: "Win!",
          text: "Seriusly?",
          confirmButtonText: ":D"
        });
        this.goHome();
      }
    }
  }
};
</script>

<style scoped>
p.counters {
  color: #e4fde1;
}
</style>