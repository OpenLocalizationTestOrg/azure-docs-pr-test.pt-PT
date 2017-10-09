> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

IoT Hub do Azure é um serviço completamente gerido que permite fiável e seguras comunicações bidirecionais entre milhões de dispositivos e uma solução de back-end. Tutoriais anteriores ([introdução ao IoT Hub] e [enviar mensagens da nuvem para o dispositivo com o IoT Hub]) ilustrar Olá dispositivo para nuvem e da nuvem para o dispositivo mensagens funcionalidades básicas do IoT Hub. IoT Hub, também oferece a capacidade tooinvoke não durável os métodos no dispositivos a partir da nuvem Olá de Olá. Direcionar métodos representam uma interação de pedido-resposta com um dispositivo tooan semelhante HTTP chamar em que são ou não bem-sucedidos imediatamente (após um tempo limite especificado de um utilizador) utilizador de Olá toolet saber o estado de Olá chamada Olá. [Invocar um método direto num dispositivo] [ lnk-devguide-methods] descreve diretos métodos em mais detalhe e oferece orientação para quando toouse direcionar métodos em vez de mensagens da nuvem para o dispositivo ou propriedades pretendidas.

Este tutorial mostrar-lhe como:

* Utilize Olá toocreate do portal do Azure, um hub IoT e criar uma identidade de dispositivo no seu IoT hub.
* Crie uma aplicação de dispositivo simulado que tem um método direto, que pode ser chamado por nuvem Olá.
* Crie uma aplicação de consola que chama um método direto na aplicação de dispositivo simulado Olá através do seu IoT hub.

> [!NOTE]
> Neste momento, os métodos diretos são apenas suportados em dispositivos que estabeleçam ligação através do Hub tooIoT Olá protocolo MQTT. Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como toouse de aplicação de dispositivo existente do tooconvert MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[enviar mensagens da nuvem para o dispositivo com o IoT Hub]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[introdução ao IoT Hub]: ../articles/iot-hub/iot-hub-node-node-getstarted.md