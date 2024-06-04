void tempHum(){
    
    unsigned long milisActuais = millis();

    if (milisActuais - milisAnteriores >= 10000) {
      milisAnteriores = milisActuais;

      if (!client.connected()) {
        reconnect();
      }
    
    // Leemos a temperatura en Celcius
      float temperatura = dht.readTemperature();
      // Leemos a humidade
      float humidade = dht.readHumidity();

        // Nada para enviar. Avisamos sobre MQTT depuracion_topic e enton vai a durmir durante un bo rato.
      if ( isnan(temperatura) || isnan(humidade)) {
        Serial.println("[ERROR] Chequear o sensor DHT !");
        client.publish(depuracion_topic, "[ERROR] Chequear o sensor DHT !", true);      
      }
      else{
    
        if ( depuracion ) {
          Serial.print("Temperatura : ");
          Serial.print(temperatura);
          Serial.print(" | Humidade : ");
          Serial.println(humidade);
        } 
        // Publicación de valores nos temas MQTT
        client.publish(temperatura_topic, String(temperatura).c_str(), true);   
        if ( depuracion ) {    
          Serial.println("Temperatura enviada sobre MQTT.");
        }
        delay(100); //Poñemos un pequeno retardo para que o servidor (broker) mqtt acepte a mensaxe
        client.publish(humidade_topic, String(humidade).c_str(), true);      
        if ( depuracion ) {
        Serial.println("Humidade enviada sobre MQTT.");

      }
      }
      }   
  }
