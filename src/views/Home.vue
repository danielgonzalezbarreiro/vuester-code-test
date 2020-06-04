<template>
  <div class="dialog">
    <p>{{speak}}</p>
    <button @click="changeDialog()" v-show="this.dialogs[this.dialog].game">Sigue</button>
    <button v-show="!this.dialogs[this.dialog].game">
      <router-link :to="{name: 'Game'}">Lucha</router-link>
    </button>
  </div>
</template>

<script>
// @ is an alias to /src
/* import HelloWorld from '@/components/HelloWorld.vue' */

export default {
  name: "Home",
  data() {
    return {
      dialog: 0,
      dialogs: [
        {
          text: "What are u doing here?",
          dialog: "0",
          game: true
        },
        {
          text: "You're died",
          dialog: "1",
          game: true
        },
        {
          text: "Ready to fight",
          dialog: "2",
          game: false
        }
      ]
    };
  },
  computed: {
    speak() {
      return this.dialogs[this.dialog].text;
    }
  },
  methods: {
    changeDialog() {
      this.dialog++;
    }
  }
};
</script>

<style scoped>
.dialog {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  margin-top: 10rem;
}
.dialog p {
  font-size: 40px;
}

.dialog button {
  display: flex;
  align-content: center;
  justify-content: center;
  padding: 1rem;
  width: 100px;
  align-self: center;
  color: #e4fde1;
  border: 3px solid #f45b69;
  background: #028090;
  font-weight: bold;
}

.dialog button:hover {
  color: #114b5f;
  border: 3px solid #f45b69;
  background: #e4fde1;
  font-weight: bold;
}
</style>