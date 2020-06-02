<template>
  <div>
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
          text: "Hola, que tal?",
          dialog: "0",
          game: true
        },
        {
          text: "Has llegado muy lejos?",
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
