<template>
  <div class="counter-container">
    <h1>{{ count }}</h1>
  </div>
</template>

<script>
export default {
  name: "CounterMoustique", // Nom multi-mots pour le composant
  data() {
    return {
      count: 42, // Remplace 42 par le nombre que tu veux afficher
    };
  },
};
</script>

<style scoped>
/* Ajoute tes styles ici, si besoin */
</style>
