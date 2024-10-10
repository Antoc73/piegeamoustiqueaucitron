<script>
// Create a client instance
location.hostname = eu1.cloud.thethings.network;
location.port = 1883;
client = new Paho.MQTT.Client(location.hostname, Number(location.port));
client.username_pw_set("mousti-trap@ttn", "NNSXS.2LFRQU7PYTR5WLL7XL7MO36UG6ABL7LRTBBBGLY.LIGYAWX3BSWECXTETKWG4WQ4MJAT3WUCBJ26QLCOETC3FHGJLRJQ")
 
// set callback handlers
client.onConnectionLost = onConnectionLost;
client.onMessageArrived = onMessageArrived;
 
// connect the client
client.connect({onSuccess:onConnect});
 
 
// called when the client connects
function onConnect() {
  // Once a connection has been made, make a subscription and send a message.
  console.log("onConnect");
  client.subscribe("#");
  message = new Paho.MQTT.Message("Hello");
  message.destinationName = "World";
  client.send(message);
}
 
// called when the client loses its connection
function onConnectionLost(responseObject) {
  if (responseObject.errorCode !== 0) {
    console.log("onConnectionLost:"+responseObject.errorMessage);
  }
}
 
// called when a message arrives
function onMessageArrived(message) {
  console.log("onMessageArrived:"+message.payloadString);
}

</script>