<template>
  <div id="app">
    <CounterMoustique :initial-count="initialCount" />
  </div>
</template>

<script>
import CounterMoustique from './components/CounterMoustique.vue'; // PascalCase ou camelCase

export default {
  data() {
    return {
      initialCount: 10,
    };
  },
  components: {
    CounterMoustique, // Utilisation du nom correct
  },
};
</script>

<style src="./assets/reset.css"></style>
<style src="./assets/style.css"></style>
