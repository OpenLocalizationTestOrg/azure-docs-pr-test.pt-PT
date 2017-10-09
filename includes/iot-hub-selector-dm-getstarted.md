> [!div class="op_single_selector"]
> * [Dispositivo: Node.js Serviço: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Dispositivo: Node.js Serviço: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Dispositivo: Serviço de Java: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Aplicações de back-end pode utilizar primitivos do IoT Hub do Azure, tal como [dispositivo duplo] [ lnk-devtwin] e [direcionar métodos][lnk-c2dmethod], tooremotely iniciar e monitorizar ações de gestão de dispositivos em dispositivos. Este tutorial mostra como uma aplicação de back-end e uma aplicação de dispositivo podem trabalhar em conjunto tooinitiate e monitorizar um reinício do dispositivo remoto utilizar o IoT Hub.

Utilize ações de gestão do dispositivo tooinitiate um método direto (por exemplo, o reinício, reposição de fábrica e atualização de firmware) a partir de uma aplicação de back-end na nuvem de Olá. dispositivo Olá é responsável por:

* A processar o pedido de método de Olá enviado a partir do IoT Hub.
* Iniciar a ação específicos do dispositivo correspondente Olá no dispositivo Olá.
* Fornecer atualizações de estado através de *comunicadas propriedades* tooIoT Hub.

Pode utilizar uma aplicação de back-end Olá nuvem toorun dispositivo duplo consultas tooreport em curso Olá das suas ações de gestão de dispositivos.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
