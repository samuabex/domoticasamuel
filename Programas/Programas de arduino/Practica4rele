

/* Proxecto casa domótica. Práctica 7. Sensor DHT11 */
#include <WiFi.h>
#include <PubSubClient.h>

#include <DHT.h> // Libraria para sensores DHT
#include <DHT_U.h>        

#include "config.h"
#include "topics.hpp"
#include "ESP32Wifi.hpp"
#include "tempHum.hpp"

void setup() {
  Serial.begin(115200);     
  setup_wifi();                           //Conexíon a rede Wifi
  setup_pines();
  client.setServer(mqtt_servidor, 1883);  // Configura a conexión MQTT
  client.setCallback(callback);
  reconnect();
  dht.begin();
}


 
void loop() { 

 tempHum();

 if (!client.connected()) {
    reconnect();
  }
  client.loop();

  long now = millis();
  if (now - lastMsg > 5000) {
    lastMsg = now;
    
    
  }
}


     
  


  
