# Control de acceso

  # Introducción
  ### En este proyecto hemos hecho un control de acceso con varios componentes.
  
  # Esquema general
  ![](https://lh3.googleusercontent.com/K-c2ik4DJ0-8h-nurbdi9k-uAy1ctKgnbW3O8mtRsNSokAOZNzNiIMDtQZpuoY54uEdKFA=s162)
                                                                                              
  # Elementos utilizados
  ### En este apartado pondremos los elementos mas importantes que hemos utilizado.
  ## 1.  Arduino Mega 2560
  ### Este es el cerebro que administra los diferentes dispositivos que encontramos en el proyecto.
  ![](https://cdn-tienda.bricogeek.com/949-thickbox_default/arduino-mega-2560.jpg)
  ## 2. NodeMCU 
  ### este modulo lo conectaremos a un Internet para que nos envié los datos a una base de datos en drive.
  ![](https://cdn-tienda.bricogeek.com/4392-thickbox_default/nodemcu-v3-esp8266.jpg)
  ## 3. RFID
  ### Este modulo lo utilizaremos para hacer la lectura de tarjetas.
  ![](https://image.made-in-china.com/202f0j10HaKUqzrdYDbW/Mfrc-522-RC522-RFID-RF-IC-Card-Inductive-Module-with-Free-S50-Fudan-Card-Key-Chain-Wholesale-for-Arduino-Kits.jpg)
  ## 4. Lector de huellas
  ### Es un modulo que almacena huellas y tiene el limite de 174 huellas.
  ![](https://images-na.ssl-images-amazon.com/images/I/51vua1sfoBL._SY355_.jpg)
  ## 5. Buzzer
  ### Es un dispositivo que hemos utilizado dependiendo del pitido que haga si es acceso permitido o denegado.
   ![](https://www.tiendatec.es/3393-large_default/buzzer-zumbador-activo-electromagnetico-5v.jpg)
  ## 6. Pantalla LCD
  ### La pantalla lo hemos utilizado para mostrar los diferentes textos que encontramos en la programacion.
  ![](https://www.tvnalber.com/content/images/thumbs/0193151_modulo-pantalla-lcd-16x2-caracteres-compatible-arduino.jpeg)
  # Conexiones
  ### En este apartado explicaremos las diferentes conexiones de los modulos que se encuentran en nuestro proyecto. 
  a continuacion,explicaremos las conexiones que hemos hecho en el RFID:
 ###  Pines       Arduino Mega
     * RST          D8
     * SDA(SS)      D9
     * MOSI         D51
     * MISO         D50
     * SCK          D52
   
  
  
     

   



