<template>
  <div>
    <h2>MQTT Client</h2>
    <p>Client connecté : {{ isConnected }}</p>
    <ul>
      <li v-for="(message, index) in messages" :key="index">{{ message }}</li>
    </ul>
  </div>
</template>

<script>
// Importer la bibliothèque Paho MQTT
import { Client } from 'paho-mqtt';

export default {
  data() {
    return {
      isConnected: false,
      client: null, // Initialiser le client
      messages: [],
    };
  },
  methods: {
    onConnect() {
      console.log("Connecté au serveur MQTT");
      this.isConnected = true;
      this.client.subscribe("#"); // S'abonner à tous les topics
    },
    onMessageArrived(message) {
      console.log("Message reçu:", message.payloadString);
      this.messages.push(message.payloadString); // Ajouter le message à la liste
      this.$emit('message-received', message.payloadString); // Émettre l'événement avec le message
    },
    onConnectionLost(responseObject) {
      if (responseObject.errorCode !== 0) {
        console.log("Connection lost:", responseObject.errorMessage);
      }
      this.isConnected = false; // Mettre à jour l'état de connexion
    },
  },
  mounted() {
    const location = {
      hostname: 'eu1.cloud.thethings.network',
      port: 8080, // Remplacer par le bon port
    };
    // Utiliser ws:// pour le WebSocket
    this.client = new Client(`ws://${location.hostname}:${location.port}`, 'clientId'); 
    this.client.onConnectionLost = this.onConnectionLost;
    this.client.onMessageArrived = this.onMessageArrived;

    // Connexion avec identifiants
    this.client.connect({
      onSuccess: this.onConnect,
      userName: 'your_username', // Remplacez par votre nom d'utilisateur
      password: 'your_password',  // Remplacez par votre mot de passe
    });
  },
};
</script>

<style scoped>
/* Ajoute tes styles ici */
</style>
