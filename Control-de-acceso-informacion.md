  # Control de acceso
  # Introducción
   En este proyecto hemos hecho un control de acceso con varios componentes.
  # Requerimiento
   Nuestro proyecto se basa en un control de acceso que esta compuesto por un RFID y un lector de huellas que cuando 
  una de las dos cosas mencionadas anteriormente nos de acceso permitido hara diferentes acciones y un excell nos marcara 
  quien a entrado, tambien la hora en la que ha entrado. En el caso contrario de que el accceso sea denegado hara otras 
  acciones diferentes.

 # Que necesitamos para llevar adelante el proyecto?
   Primeramente necesitaremos recopilar los siguientes materiales: Arduino Mega, nodeMCU, Pantalla LCD, Leds, servo, RFID, 
   Lector de huellas, Botones, buzzer y potenciometro. En otro apartado explicaremos para que sirve cada uno de ellos.
  
  # Esquema general
  
                                                                                              
  # Elementos utilizados
   En este apartado pondremos los elementos mas importantes que hemos utilizado.
  ## 1.  Arduino Mega 2560
   Este es el cerebro que administra los diferentes dispositivos que encontramos en el proyecto. Tiene un voltaje de 
   entrada de 7v-12v. En el pin de entrada/salida de 5v tiene una corriente de 40mA y en el pin de entrada/salida de 3,3v 
   tiene una corriente de 50mA. Tiene una velocidad de reloj de 16Mhz y una memoria EEPROM de 4kb.
  ![](https://cdn-tienda.bricogeek.com/949-thickbox_default/arduino-mega-2560.jpg)
  ![](https://content.arduino.cc/assets/Pinout-Mega2560rev3_latest.png)
  ## 2.NodeMCU 
    Este módulo lo conectaremos a un Internet para que nos envié los datos a una base de datos en drive. La placa se  
    alimenta a 5v, En el pin de entrada/salida de 5v tiene una corriente de 10mA y en el pin de entrada/salida de 3,3v 
    tiene una corriente de 12mA. Tiene una velocidad de reloj de 26-52Mhz y tiene una memoria Sram de 64kb. 
  ![](https://cdn-tienda.bricogeek.com/4392-thickbox_default/nodemcu-v3-esp8266.jpg)
  ## 3. RFID
    Este modulo lo utilizaremos para hacer la lectura de tarjetas.
  ![](https://image.made-in-china.com/202f0j10HaKUqzrdYDbW/Mfrc-522-RC522-RFID-RF-IC-Card-Inductive-Module-with-Free-S50-Fudan-Card-Key-Chain-Wholesale-for-Arduino-Kits.jpg)
  ## 4. Lector de huellas
    Es un modulo que almacena huellas y tiene el limite de 174 huellas.
  ![](https://images-na.ssl-images-amazon.com/images/I/51vua1sfoBL._SY355_.jpg)
  ## 5. Buzzer
     Es un dispositivo que hemos utilizado dependiendo del pitido que haga si es acceso permitido o denegado.
   ![](https://www.tiendatec.es/3393-large_default/buzzer-zumbador-activo-electromagnetico-5v.jpg)
  ## 6. Pantalla LCD
    La pantalla lo hemos utilizado para mostrar los diferentes textos que encontramos en la programacion.
   ![](https://images-na.ssl-images-amazon.com/images/I/51EaDiaiQZL._SY355_.jpg)
  # Conexiones
   En este apartado explicaremos las diferentes conexiones de los modulos que se encuentran en nuestro proyecto. 
  a continuacion,explicaremos las conexiones que hemos hecho en el RFID:

     pines       Arduino mega
     RST          D8
     SDA(SS)      D9
     MOSI         D51
     MISO         D50
     SCK          D52
     VCC          3.3V
     GND          GND
   Para continuar pondremos los pines que hemos utilizado para el sensor de huellas:
  
    Pines     Arduino Mega
    Huellas - Amarillo D11
    Huellas - Blanco D10
    VCC -     5V
    GND -     GND
   Para finalizar pondremos los pines que corresponden a la pantalla:
 
      Pines     Arduino mega
      //VSS -   GND
      //VDD     + 5
      //A       + 5
      //K -     GND
      //VO      MEDIO POT
      //RS      D2
      //RW -    GND
      //E       D3
      //D4      D4
      //D5      D5 
      //D6      D6
      //D7      D7
      
   # Interfaces de comunicación
   En este proyecto hemos utilizado los diferentes interfaces de comunicación, como por ejemplo USB, Wifi y serie. 
   El apartado del wifi lo utilizaremos en el nodeMCU, por otra parte el USB lo utilizaremos para conectar el Arduino mega 
   con el ordenador, y el serie es para cumplir diferentes comunicaciones en el proyecto (Lector de huellas y NodeMCU).
   
   # Testeo y ajustes
   
   # Coclusiones
   En este apartado vamos a analizar las posibles mejoras que tiene nuestro proyecto y también explicaremos las diferentes 
   dificultades que hemos tenido durante el reto:
   * Mejoras
     * Registro automático de huellas dactilares mediante el uso del permiso de un administrador.
     * Reemplazar servo por una cerradura eléctrica.
     * Hacer una tarjeta de administrador con permisos especiales.
   * Dificultades
     * Comunicación con lector de huellas. Pines de comunicación son fijos en la  placa arduino.
     * Movimiento de puerta. No tuvimos tiempo para poner unas bisagras y tuvimos que poner una puerta impresa en 3d.
     * Comunicación nodeMCU/Arduino Mega. No conseguíamos realizar la comunicación.

     # Software 
      
     **NodeMCU**

    `#include <ESP8266WiFi.h>
     #include "HTTPSRedirect.h"
     #include "DebugMacros.h"

     #include <SoftwareSerial.h>
     SoftwareSerial s(14,12); //D5,D6

     const int inputPin = 13;
     int value = 0;
     int data;
     String izena;

     const char *ssid = "13";
     const char *password = "12345678";

     const char* host = "script.google.com";
     const char *GScriptId = "AKfycbx_ptPJGEpJ0sQE7hXoOX8cqTQDQiC5liYTaNuO";
     const int httpsPort = 443;

     const char* fingerprint = "";
     String url;

     String payload_base =  "{\"command\": \"appendRow\", \
                    \"sheet_name\": \"Sheet1\", \
                    \"values\": ";
     String payload = "";

     HTTPSRedirect* client = nullptr;

     unsigned int free_heap_before = 0;
     unsigned int free_stack_before = 0;

     void setup() {
     Serial.begin(9600);
     s.begin(9600);

     free_heap_before = ESP.getFreeHeap();
     free_stack_before = ESP.getFreeContStack();
  
     Serial.println();
     Serial.print("Connecting to wifi: ");
     Serial.println(ssid);
     Serial.flush();
 
     WiFi.begin(ssid, password);
     while (WiFi.status() != WL_CONNECTED) {
     delay(500);
     Serial.print(".");
     }
     Serial.println("");
     Serial.println("WiFi connected");
     Serial.println("IP address: ");
     Serial.println(WiFi.localIP()); 
     }

     void loop() {
     value = digitalRead(inputPin);  
     if (value == LOW) {
     data=s.read();
     Serial.println(data);
     if (data==1)
     {
     izena = "Lander";
     Serial.println(izena);
     }
     else if (data==2){
     izena = "Jon";
     Serial.println(izena);
     }
     else if (data==3){
     izena = "Abierto";
     Serial.println(izena);
     }
     else if (data==0){
     izena = "Abierto";
     Serial.println(izena);
     }
     else {
     izena = "Abierto";
     Serial.println(izena);
     } 

     static int error_count = 0;
     static int connect_count = 0;
 
     client = new HTTPSRedirect(httpsPort);
     client->setInsecure();
     client->setPrintResponseBody(true);
     client->setContentTypeHeader("application/json");
  
     Serial.print("Connecting to ");
     Serial.println(host);

     // Try to connect for a maximum of 5 times
     bool flag = false;
     for (int i=0; i<5; i++){
     int retval = client->connect(host, httpsPort);
     if (retval == 1) {
     flag = true;
     break;
     }
     else
     Serial.println("Connection failed. Retrying...");
     }

     if (!flag){
     Serial.print("Could not connect to server: ");
     Serial.println(host);
     Serial.println("Exiting...");
     return;
     }
     //String val = valor; 
     url = String("/macros/s/") + GScriptId + "/exec?value=" + izena;
     client->GET(url, host);
 
     delete client;
     client = nullptr;
     }
     else {return;}
     }

__Control de acceso__
 

    `//Librerías

     #include <Servo.h>

     #include <LiquidCrystal.h>

     #include <SPI.h>
                    
     #include <MFRC522.h>

     #include <SoftwareSerial.h>

     #include <Adafruit_Fingerprint.h>`
  
    `//Comunicaciones

     SoftwareSerial mySerial(11, 10);  // Comunicación lector de huellas

     Adafruit_Fingerprint finger = Adafruit_Fingerprint(&mySerial);

     SoftwareSerial s(15, 14);   // Comunicación con NodeMCU

     LiquidCrystal lcd(2, 3, 4, 5, 6, 7);   //_ Comunicación con pantalla LCD_`

     `//Variables

     Servo servoMotor;
 
     const int RST_PIN = 8;        // _Pin 8 para el reset del RC522_

     const int SS_PIN = 9;        // _Pin 9 para el SS (SDA) del RC522_

     MFRC522 mfrc522(SS_PIN, RST_PIN);   // _Crear instancia del MFRC522_

     const int buzzer = 13;

     int led = 48;

     int rojo = 49;

     int encendido = 42;

     int boton = 46;

     int estadoboton = 0;

     int boton2 =45;

     int estadoboton2 = 0;

     int cerrar = 44;

     int estadocerrar = 0;

     int output = 22;`

     `//IDs válidas RFID
 
     byte LecturaUID[4];

     byte Lander[4]={0xDD, 0x6B, 0xD5, 0xE5};
  
     byte Jon[4]={0xF0, 0x35, 0xB1, 0xC5};`

     `//Función para comparar dos vectores

     bool isEqualArray(byte* arrayA, byte* arrayB, int length)
     {
     for (int index = 0; index < length; index++) 
     {
     if (arrayA[index] != arrayB[index]) return false;
     } 
     return true;
     }
     uint8_t id;`

     `void setup() {
      Serial.begin(9600);    // Puerto Serie
      SPI.begin();           // Iniciar SPI
      mfrc522.PCD_Init();    // Iniciar MFRC522
      pinMode (led, OUTPUT);
      pinMode (rojo, OUTPUT);
      pinMode (encendido, OUTPUT);
      pinMode (boton, INPUT);
      pinMode (boton2, INPUT);
      pinMode (cerrar, INPUT);
      pinMode (buzzer, OUTPUT);
      pinMode (output, OUTPUT);
      servoMotor.attach(12);
      servoMotor.write(180);  //_Servo en posición de cerrado_
      lcd.begin(16,2);
      lcd.setCursor(0,0);
      lcd.write("Comprobando");
      lcd.setCursor(0,1);
      lcd.write("Acceso..........");
      digitalWrite (output, HIGH);

      // Detectar lector huella

      while (!Serial);  
      delay(100);
  
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.write("Buscando sensor");
      lcd.setCursor(0,1);
      lcd.write(".............................");

      finger.begin(57600);
      delay(2000);
      if (finger.verifyPassword()) {
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.write("Sensor detectado");
      delay(3000);
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.write("Comprobando");
      lcd.setCursor(0,1);
      lcd.write("Acceso..........");
      } 
      else {
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.write("No detectado");
      while (1) { delay(1); }
      }
      digitalWrite (encendido, HIGH);   // _Led de encendido_
      }`
      `void loop() {

       getFingerprintIDez();
       delay(50);            //_don't ned to run this at full speed_.

       //_Lectura botones_

       estadoboton = digitalRead (boton);
       estadoboton2 = digitalRead (boton2);
       estadocerrar = digitalRead (cerrar);
  
       // _Detectar tarjeta_
       if (mfrc522.PICC_IsNewCardPresent())
       {
       //Seleccionamos una tarjeta
       if (mfrc522.PICC_ReadCardSerial())
       {
       // Comparar ID con las claves válidas
       if (isEqualArray(mfrc522.uid.uidByte,Lander,4)) {
       lcd.clear();
       lcd.setCursor(0,0);
       lcd.write("Bienvenido");
       lcd.setCursor(0,1);
       lcd.write("Lander");
       int zein =1;        
       permitido (zein);
       }
       else if (isEqualArray(mfrc522.uid.uidByte,Jon,4)){
       lcd.clear();
       lcd.setCursor(0,0);
       lcd.write("Bienvenido");
       lcd.setCursor(0,1);
       lcd.write("Jon");
       int zein =2; 
       permitido (zein);
       }
       else  {   // _Si la ID no coincide cumple la función denegado_
       denegado ();
       }

       // _Finalizar lectura actual_
       mfrc522.PICC_HaltA();
       }
       }
       delay(250);`
       `if (estadoboton == LOW){   //Botón con función de leer IDs de tarjetas en la pantalla LCD
        // Detecta tarjeta
        if ( mfrc522.PICC_IsNewCardPresent()) 
        {  
        // Seleccionamos una tarjeta
        if ( mfrc522.PICC_ReadCardSerial()) 
        {
        // Enviamos serialemente su UID
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.print("Card UID");
        lcd.setCursor(0,1);
        for (byte i = 0; i < mfrc522.uid.size; i++) { 
        // Visualizamos en la pantalla la UID
        lcd.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
        lcd.print(mfrc522.uid.uidByte[i], HEX);
        lcd.print(" ");
        } 
        Serial.println();
        // Terminamos la lectura de la tarjeta  actual
        mfrc522.PICC_HaltA();         
        } 
        delay (1500);
        lcd.setCursor(0,0);
        lcd.write("Comprobando");
        lcd.setCursor(0,1);
        lcd.write("Acceso..........");
        delay(1500);      
        }
        }
        if (estadoboton2 == LOW){  // _Botón con la función de registrar nuevas huellas dactilares mediante monitor serie_
        Serial.println("Ready to enroll a fingerprint!");
        Serial.println("Please type in the ID # (from 1 to 127) you want to save this finger as...");
        id = readnumber();
        if (id == 0) {// ID #0 not allowed, try again!
        return;
        }
        Serial.print("Enrolling ID #");
        Serial.println(id);
  
        while (!  getFingerprintEnroll() );  // Función  getFingerprintEnroll
        }

        if (estadocerrar == LOW){  // Botón con la función de cerrar la puerta
        servoMotor.write(180);
        delay (500);
        lcd.setCursor(0,0);
        lcd.write("Comprobando");
        lcd.setCursor(0,1);
        lcd.write("Acceso..........");
        }
      
        }

        void permitido (int zein){  // Función que se cumple siempre que alguien presenta su acceso permitido
        Serial.println(zein);
        digitalWrite(output, LOW);
        s.write(zein); 
        digitalWrite(led, HIGH);
        // Servo abierta
        servoMotor.write(90);
        // Sonido de buzzer
        tone(buzzer, 2000, 500);
        delay (600);
        digitalWrite(output, HIGH);
        noTone(buzzer);
        delay (200);
        digitalWrite(led, LOW);
        delay (500);
        // Texto para cerrar la puerta en la pantalla
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.write("Cerrar");
        lcd.setCursor(0,1);
        lcd.write("Puerta");
        delay(100);
        }

        void denegado (){   // Función que se cumple cuando se presenta alguien sin acceso
        // Texto de acceso denegado en la pantalla
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.write("Acceso");
        lcd.setCursor(0,1);
        lcd.write("Denegado");
        digitalWrite(rojo, HIGH);
        // Puerta bloqueada
        servoMotor.write(180);
        // _Tres pitidos de buzzer_
        tone(buzzer, 4000, 1000);
        delay (300);
        noTone(buzzer);
        delay (300);
        tone(buzzer, 4000, 1000);
        delay (300);
        noTone(buzzer);
        delay (300);
        tone(buzzer, 4000, 1000);
        delay (300);
        noTone(buzzer);
        delay (200);
        digitalWrite(rojo, LOW);
        delay (500);
        lcd.setCursor(0,0);
        lcd.write("Comprobando");
        lcd.setCursor(0,1);
        lcd.write("Acceso..........");
        }`
       `// returns -1 if failed, otherwise returns ID #
        int getFingerprintIDez() {
        uint8_t p = finger.getImage();
        if (p != FINGERPRINT_OK){  
        return -1;  
        }`

        p = finger.image2Tz();
        if (p != FINGERPRINT_OK) {
        return -1; 
        }

        p = finger.fingerFastSearch();
        if (p != FINGERPRINT_OK) { 
        // Huella sin coincidencia, cumple la función denegado
        denegado ();    
        return -1; 
        }
  
        // _Encuentra coincidencia con huella registrada_
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.write("Bienvenido");
        int zein =3;
        permitido (zein);
        return finger.fingerID; 
        }`


        uint8_t readnumber(void) {  // _Función para el registro de huellas_
        uint8_t num = 0;
        while (num == 0) {
        while (! Serial.available());
        num = Serial.parseInt();
        }
        return num;
        }

        uint8_t getFingerprintEnroll() {   // Función para el registro de huellas
        int p = -1;
        Serial.print("Waiting for valid finger to enroll as #"); 
        Serial.println(id);
        while (p != FINGERPRINT_OK) {
        p = finger.getImage();
        switch (p) {
        case FINGERPRINT_OK:
        Serial.println("Image taken");
        break;
        case FINGERPRINT_NOFINGER:
        Serial.println(".");
        break;
        case FINGERPRINT_PACKETRECIEVEERR:
        Serial.println("Communication error");
        break;
        case FINGERPRINT_IMAGEFAIL:
        Serial.println("Imaging error");
        break;
        default:
        Serial.println("Unknown error");
        break;
        }
        }`
        `// OK success!

        p = finger.image2Tz(1);
        switch (p) {
        case FINGERPRINT_OK:
        Serial.println("Image converted");
        break;
        case FINGERPRINT_IMAGEMESS:
        Serial.println("Image too messy");
        return p;
        case FINGERPRINT_PACKETRECIEVEERR:
        Serial.println("Communication error");
        return p;
        case FINGERPRINT_FEATUREFAIL:
        Serial.println("Could not find fingerprint features");
        return p;
        case FINGERPRINT_INVALIDIMAGE:
        Serial.println("Could not find fingerprint features");
        return p;
        default:
        Serial.println("Unknown error");
        return p;
        }
  
        Serial.println("Remove finger");
        delay(2000);
        p = 0;
        while (p != FINGERPRINT_NOFINGER) {
        p = finger.getImage();
        }
        Serial.print("ID "); Serial.println(id);
        p = -1;
        Serial.println("Place same finger again");
        while (p != FINGERPRINT_OK) {
        p = finger.getImage();
        switch (p) {
        case FINGERPRINT_OK:
        Serial.println("Image taken");
        break;
        case FINGERPRINT_NOFINGER:
        Serial.print(".");
        break;
        case FINGERPRINT_PACKETRECIEVEERR:
        Serial.println("Communication error");
        break;
        case FINGERPRINT_IMAGEFAIL:
        Serial.println("Imaging error");
        break;
        default:
        Serial.println("Unknown error");
        break;
        }
        }

        // OK success!
        p = finger.image2Tz(2);
        switch (p) {
        case FINGERPRINT_OK:
        Serial.println("Image converted");
        break;
        case FINGERPRINT_IMAGEMESS:
        Serial.println("Image too messy");
        return p;
        case FINGERPRINT_PACKETRECIEVEERR:
        Serial.println("Communication error");
        return p;
        case FINGERPRINT_FEATUREFAIL:
        Serial.println("Could not find fingerprint features");
        return p;
        case FINGERPRINT_INVALIDIMAGE:
        Serial.println("Could not find fingerprint features");
        return p;
        default:
        Serial.println("Unknown error");
        return p;
        }
  
       // OK converted!
        Serial.print("Creating model for #"); 
        Serial.println(id);
        p = finger.createModel();
        if (p == FINGERPRINT_OK) {
        Serial.println("Prints matched!");
        } else if (p == FINGERPRINT_PACKETRECIEVEERR) {
        Serial.println("Communication error");
        return p;
        } else if (p == FINGERPRINT_ENROLLMISMATCH) {
        Serial.println("Fingerprints did not match");
        return p;
        } else {
        Serial.println("Unknown error");
        return p;
        }   
  
        Serial.print("ID "); 
        Serial.println(id);
        p = finger.storeModel(id);
        if (p == FINGERPRINT_OK) {
        Serial.println("Stored!");
        } else if (p == FINGERPRINT_PACKETRECIEVEERR) {
        Serial.println("Communication error");
        return p;
        } else if (p == FINGERPRINT_BADLOCATION) {
        Serial.println("Could not store in that location");
        return p;
        } else if (p == FINGERPRINT_FLASHERR) {
        Serial.println("Error writing to flash");
        return p;
        } else {
        Serial.println("Unknown error");
        return p;
        }
       }`
        
        
      
         
      
       

