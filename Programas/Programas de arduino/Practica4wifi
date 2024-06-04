void setup_wifi() {
  delay(20);
  Serial.println();
  Serial.print("Conectando a ");
  Serial.println(wifi_ssid);
  
  WiFi.begin(wifi_ssid, wifi_contrasinal);
 
  while (WiFi.status() != WL_CONNECTED) {
    delay(300);
    Serial.print(".");
  }
 
 Serial.println("");
 Serial.println("Conexión correcta ");
 Serial.print("=> ESP32 a dirección IP address é: ");
 Serial.print(WiFi.localIP());
 Serial.println("");
}

void callback(char* topic, byte* message, unsigned int length) {
  Serial.print("Chegou mensaxe ao topic: ");
  Serial.print(topic);
  Serial.print(". Mensaxe: ");
  String messageTemp;
  
  for (int i = 0; i < length; i++) {
    Serial.print((char)message[i]);
    messageTemp += (char)message[i];
  }
  Serial.println();

  // Cambia o estado da saída de acordo coa mensaxe
  if (String(topic) == rele_topic) {
    Serial.print("Cambiando a saída a  ");
    if(messageTemp == "true"){
      Serial.println("on");
      digitalWrite(relePin, LOW);
    }
    else if(messageTemp == "false"){
      Serial.println("off");
      digitalWrite(relePin, HIGH);
    }
  }
}

  
//Reconexión a wifi si a conexión se perdeu
void reconnect() {
 
  while (!client.connected()) {
    Serial.print("Conectando ao MQTT broker ...");
    if (client.connect("ESP32Client")) {
      Serial.println("Reconexión ao servidor mqtt correcta");
       client.subscribe(rele_topic);
    } else {
      Serial.print("[Error] Non conectado ao servidor mqtt: ");
      Serial.print(client.state());
      Serial.println("Esperando 5 segundos antes de reintentalo.");
      delay(5000);
    }
  }
}
