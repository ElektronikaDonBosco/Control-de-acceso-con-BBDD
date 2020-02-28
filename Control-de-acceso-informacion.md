  # Control de acceso

  # Introducción
  ### En este proyecto hemos hecho un control de acceso con varios componentes.
  # Requerimiento
   Nuestro proyecto se basa en un control de acesso que esta compuesto por un RFID y un lector de huellas que cuando 
  una de las dos cosas mencionadas anteriormente nos de acceso permitido hara diferentes acciones y un excell nos marcara 
  quien a entrado, tambien la hora en la que ha entrado. En el caso contrario de que el accceso sea denegado hara otras 
  acciones diferentes.

 # que necesitamos para llevar adelante el proyecto?
   Primeramente necesitaremos recopilar los siguientes materiales: Arduino Mega, nodeMCU, Pantalla LCD, Leds, servo, RFID, 
   Lector de huellas, Botones, buzzer y potenciometro. En otro apartado explicaremos para que sirve cada uno de ellos.
  
  # Esquema general
  ![](https://lh3.googleusercontent.com/K-c2ik4DJ0-8h-nurbdi9k-uAy1ctKgnbW3O8mtRsNSokAOZNzNiIMDtQZpuoY54uEdKFA=s162)
                                                                                              
  # Elementos utilizados
   En este apartado pondremos los elementos mas importantes que hemos utilizado.
  ## 1.  Arduino Mega 2560
    Este es el cerebro que administra los diferentes dispositivos que encontramos en el proyecto.
  ![](https://cdn-tienda.bricogeek.com/949-thickbox_default/arduino-mega-2560.jpg)
  ### 2.NodeMCU 
    Este modulo lo conectaremos a un Internet para que nos envié los datos a una base de datos en drive.
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

   
  
  
     

   



