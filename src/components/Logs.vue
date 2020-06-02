<template>
  <div>
    <div class="logs" v-for="log in logs" :key="log.id">
      {{ log.player }}
      {{ log.damage }}
      {{log.health}}
    </div>
  </div>
</template>

<script>
export default {
  name: "Logs",
  props: {
    logs: Array
  }
};
</script>