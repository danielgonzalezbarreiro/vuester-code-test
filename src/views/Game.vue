<template>
  <div>
    <!--BARRAS DE VIDA -->
    <HealthBars :playerHp="playerHp" :enemyHp="enemyHp"></HealthBars>
    <!--/BARRAS DE VIDA -->
    <!--OPCIONES DE JUEGO -->
    <OptionButtons
      v-show="this.end"
      v-on:attack="attack()"
      v-on:heal="heal()"
      v-on:specialAttack="specialAttack()"
      v-on:giveUp="giveUp()"
      :specialAttackCounter="specialAttackCount"
      :potionsCounter="potions"
    ></OptionButtons>
    <!--/OPCIONES DE JUEGO -->
    <p v-show="this.winner">Ganaches!</p>
    <p v-show="this.looser">Perdiches!</p>
    <p class="counters">Special Attack: {{specialAttackCount}} Potions: {{potions}}</p>
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
      specialAttackCount: 3,
      potions: 2,
      logs: [],
      winner: false,
      looser: false,
      end: true
    };
  },
  methods: {
    attack() {
      let damage = this.calculateDamage(3, 10);
      this.enemyHp -= damage;
      this.hpControll();

      let log = { player: "Quitacheslle", damage: damage + " hp o inemigo" };
      this.logs.splice(0);
      this.enemyAttack();
      this.logs.unshift(log);
    },
    calculateDamage(min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    enemyAttack() {
      this.hpControll();
      let damage = this.calculateDamage(5, 12);
      this.playerHp -= damage;

      let log = { player: "O inimigo quitouche", damage: damage + "hp" };
      this.logs.splice(1);
      this.logs.unshift(log);
    },
    heal() {
      //CURAR SOLO PUEDE UTILIZARSE SI EL PLAYER ESTA A MENOS
      //DEL 50% DE VIDA,
      //CUANDO EL PLAYER SU CURA, EL ENEMIGO ATACA IGUALMENTE

      if (this.playerHp <= 40 && this.potions != 0) {
        this.potions--;
        this.playerHp += this.potionHp;

        let log = { health: "Curacheste " + this.potionHp + " hp" };
        this.enemyAttack();
        this.logs.unshift(log);
      }
    },
    specialAttack() {
      //solo se puede usar x veces (2 o 3)
      //numero bajo
      if (this.specialAttackCount > 0) {
        this.specialAttackCount--;
        this.enemyHp -= this.specialAttackHp;

        let log = {
          player: "O teu ataque especial quitoulle ",
          damage: this.specialAttackHp + " hp o inimigo"
        };
        this.enemyAttack();
        this.logs.unshift(log);
      }
    },

    giveUp() {
      //restaura todos los valores
      this.playerHp = 80;
      this.enemyHp = 80;
      this.specialAttackCount = 3;
      this.potions = 2;

      Swal.fire({
        title: "Te rendiste",
        text: "Pues vaya",
        confirmButtonText: ":("
      });
      this.goHome();
    },
    goHome() {
      this.$router.push("/");
    },
    hpControll() {
      if (this.playerHp <= 0) {
        this.playerHp = 0;
        this.looser = true;
        this.end = false;
        Swal.fire({
          title: "Perdiches",
          text: "Intentao de novo",
          confirmButtonText: ":/"
        });
      }
      if (this.enemyHp <= 0) {
        this.enemyHp = 0;
        this.winner = true;
        this.end = false;
        Swal.fire({
          title: "Ganaches",
          text: "Noraboa",
          confirmButtonText: ":)"
        });
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