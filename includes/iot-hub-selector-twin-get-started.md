> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Os dispositivos duplos são documentos JSON que armazenam informações de estado dos dispositivos (metadados, configurações e condições). IoT Hub mantém um dispositivo duplo para cada dispositivo que liga tooit.

Utilize dispositivos duplos para:

* Armazenar metadados do dispositivo da sua solução de back-end.
* Comunicarão as informações de estado atual, tais como condições (por exemplo, Olá conectividade método utilizado) e capacidades disponíveis da sua aplicação de dispositivo.
* Sincronize o estado de Olá de execução longa os fluxos de trabalho (tais como atualizações de firmware e de configuração) entre uma aplicação de dispositivo e uma aplicação de back-end.
* Consulta os metadados do dispositivo, a configuração ou o estado.

> [!NOTE]
> Dispositivos duplos foram concebidos para a sincronização de e para consultar as configurações de dispositivo e condições. Mais informations no quando toouse dispositivos duplos podem ser encontrados na [compreender dispositivos duplos][lnk-twins].

Dispositivos duplos são armazenados num IoT hub e contenham:

* *etiquetas*, os metadados do dispositivo acessível apenas a Olá solução de back-end;
* *pretender propriedades*, objetos JSON modificável pela solução de Olá back-end e observable pela aplicação de dispositivo Olá; e
* *comunicado propriedades*, objetos JSON modificável pela aplicação de dispositivo Olá e ser lido pelo Olá solução de back-end. As etiquetas e propriedades não podem conter matrizes, mas podem ser aninhados em objetos.

![][img-twin]

Além disso, Olá solução de back-end pode consultar dispositivos duplos com base em todos os Olá acima dados.
Consulte demasiado[compreender dispositivos duplos] [ lnk-twins] para obter mais informações sobre dispositivos duplos e toohello [idioma de consulta do IoT Hub] [ lnk-query] referência para consultas.

> [!NOTE]
> Neste momento, os dispositivos duplos são acessíveis apenas a partir de dispositivos que ligam tooIoT Hub através do protocolo MQTT Olá. Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como toouse de aplicação de dispositivo existente do tooconvert MQTT.

Este tutorial mostrar-lhe como:

* Criar uma aplicação de back-end que adiciona *etiquetas* tooa dispositivo duplo e uma aplicação de dispositivo simulado que comunica a conectividade de canal como um *comunicadas propriedade* no dispositivo duplo de Olá.
* Consultar os dispositivos da sua aplicação de back-end utilizando filtros em etiquetas Olá e as propriedades que criou anteriormente.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md