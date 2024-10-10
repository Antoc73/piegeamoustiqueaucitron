<template>
  <div id="app">
    <CounterMoustique :initial-count="initialCount" />
    <MqttClient />
  </div>
</template>

<script>
import MqttClient from './components/MqttClient.vue'; // Utilisation du nom correct
import CounterMoustique from './components/CounterMoustique.vue'; // PascalCase ou camelCase

export default {
  data() {
    return {
      initialCount: 10,
    };
  },
  components: {
    MqttClient,
    CounterMoustique, // Utilisation du nom correct
  },
};
</script>

<style src="./assets/reset.css"></style>
<style src="./assets/style.css"></style>
