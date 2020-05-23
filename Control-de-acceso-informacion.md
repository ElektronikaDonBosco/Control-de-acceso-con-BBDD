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
  A continuación mostramos una imagen de nuestro esquema de bloques con las partes que tiene nuestro proyecto, y como 
  están comunicados entre ellos:
  ![](https://raw.githubusercontent.com/Jon123456789-cmd/Control-de-acceso-con-base-de-datos/master/imagenes/Conexi%C3%B3n_bloques.jpg)
                                                                                              
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
   En este apartado explicaremos cómo hemos ido probando cada uno de los bloques del proyecto :

   ### Rfid
   Para comenzar, hemos empezado conectando el RFID a una protoboard haciendo las conexiones pertinentes al Arduino mega. 
   Luego, subimos un programa básico para comprobar si el RFID funciona correctamente y entender su funcionamiento. A 
   continuación pondremos  una foto de las conexiones : 

   ![](https://raw.githubusercontent.com/Jon123456789-cmd/Control-de-acceso-con-base-de-datos/master/imagenes/RFID.png)

   ### Lector de Huellas
   A continuación, hemos conectado el lector de huellas en el Arduino mega y hemos procedido a meterle el programa de 
   registrar huellas dactilares y luego subido el programa de comprobar las huellas para saber si se habían guardado 
   correctamente. Ahora pondremos una imagen de las conexiones: 

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
      
     El software estará en el apartado de code de esta misma pagina. A continuación pondremos un enlace , la cual podréis 
     acceder a las diferentes programaciones: https://github.com/Jon123456789-cmd/Control-de-acceso-con-base-de-datos.

     # Referencias
     En este apartado pondremos las diferentes referencias en las que hemos encontrado la información:
     * http://elcajondeardu.blogspot.com/2013/12/tutorial-conectando-una-pantalla-lcd.html
     * https://www.instructables.com/id/MFRC522-RFID-Reader-Interfaced-With-NodeMCU/
     * https://www.theengineeringprojects.com/2015/12/arduino-mega-2560-library-proteus.html
     * https://www.prometec.net/lector-de-huellas/
     * https://forum.arduino.cc/index.php?topic=292255.0 (Huella dactilar)
     * https://forum.arduino.cc/index.php?topic=499058.0 (Arduino Mega con RFID)

     # Anexos
     ## Listado de materiales y datasheet
     * 3 x Leds   http://www1.futureelectronics.com/doc/EVERLIGHT%C2%A0/334-15__T1C1-4WYA.pdf
     * 3 x Botones  https://www.arduino.cc/documents/datasheets/Button.pdf
     * 6 X Resistencias(220 X3) y (10k X3)     
     * 1 X pantalla LCD   https://components101.com/sites/default/files/component_datasheet/16x2%20LCD%20Datasheet.pdf
     * 1 X Arduino Mega  http://manueldelgadocrespo.blogspot.com/p/arduino-mega-2560.html
     * 1 X NodeMCU  https://cdn-shop.adafruit.com/datasheets/ESP8266_Specifications_English.pdf
     * 1 X RFID (Lector de tarjetas y llaves electrónicas)  http://www.puntoflotante.net/RC522-RFID.htm
     * 1 X Lector de huellas https://candy-ho.com/Drivers/huellas.pdf
     * 1 X Servomotor http://www.ee.ic.ac.uk/pcheung/teaching/DE1_EE/stores/sg90_datasheet.pdf
     * 1 X Buzzer  https://components101.com/sites/default/files/component_datasheet/Buzzer%20Datasheet.pdf
     * 1 X Potenciometro 10k  https://www.sparkfun.com/datasheets/Components/General/R12-0-.pdf
     * Metraquilato 
     
     
   
     
     
      
        
        
      
         
      
       

