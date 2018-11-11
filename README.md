# Control-De-Excedentes
Control de Excedentes para sistema fotovoltaico
Como utilizar un facilmente un relé de estado solido mediante esp8266 y pwm.

11-11-2018

Componentes necesarios:
- [x] Relé estado sólido, los hay de diversos tipos y amperajes, [ puede ser uno como éste.](https://es.aliexpress.com/item/solid-state-relay-SSR-40DA-H-40A-3-32V-DC-TO-90-480V-AC-SSR-40DA/1843393093.html)
- [x] Una placa con el dispositivo esp8266, bien puede ser un Lolin, un Wemos, un Nodemcu, etc, en este caso [la que tengo es un wemos mini.](https://es.aliexpress.com/store/product/D1-mini-Mini-NodeMcu-4M-bytes-Lua-WIFI-Internet-of-Things-development-board-based-ESP8266-by/1084082_32651747570.html)

Pasos a seguir:
- [x] Descargar la última versión de EspEasy, a día de hoy es la versión ESPEasy_R120 y la tienes [disponible aquí](http://www.letscontrolit.com/downloads/ESPEasy_R120.zip)
- [x] Si no tienes habilidades informáticas o simplemente no tienes tiempo, voy a indicar unos sencillos pasos a seguir para subir el binario compilado  la placa esp8266. 
  - Una vez descargado el archivo, descomprimes y accede a la carpeta, en esa carpeta veras subcarpetas y archivos ejecutables, accede a la subcarpeta (bin) y dependiendo de tu placa ESP tendrás que elegir el binario adecuado, mi placa es de 4Mb así que elijo la versión "ESP_Easy_normal_ESP8266_4096.bin".
  - Copia el archivo y vuelve al directorio anterior donde lo pegas, ahora ejecuta el archivo "FlashESP8266.exe", conecta la placa al ordenador mediante el cable adecuado y una vez que detecte el puerto de comunicaciones, selecciona el binario a introducir en la placa y dale al botón para subirlo a la placa.
- [x] Una vez finalizado correctamente el proceso de flaseo, desconecta la placa y la vuelves a conectar, espera un par de minutos a que la placa termine de procesar la información.
- [x] Ahora vamos a configurar el dispositivo, busca una red wifi que se llama "ESP_Easy_0" o similar, conectate a ella con el siguiente password "configesp"(sin comillas) y en el navegador te conectarás a la siguiente dirección: http://192.168.4.1 introduce los datos de tu red wifi.
- [x] Si todo ha ido bien ya tienes el esp8266 conectado a la red wifi, a traves del navegador accede a la ip de la placa y puedes manejar los GPIO´s de la siguientes formas:
  - Por mqtt: mosquitto_pub -q 1 -d -t "/esp-sysname/gpio/2:command:ON:1"
  - Integración en Openhab: Switch MQTTLEDPULSE { mqtt=">[mosquitto:/openhabdemo/cmd:command:ON:pulse,2,0,500], >[mosquitto:/openhabdemo/cmd:command:OFF:pulse,2,0,500]" }
  - Por URL: http://192.168.1.23/control?cmd=PWM,5,50  donde 5 es el GPIO y 50 es el pulso.
  - !OJO¡ No confundas el GPIO con el pin, pongo el siguiente ejemplo a título ilustrativo, el pin 5 del wemos mini se corresponde con el GPIO 14. 
![My image](https://github.com/ABarrosoG/Control-De-Excedentes/blob/master/pines-wemos-mini.jpg)
  
