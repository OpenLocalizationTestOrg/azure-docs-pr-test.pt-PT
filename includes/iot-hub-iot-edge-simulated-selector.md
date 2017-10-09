> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Estas instruções de Olá [nuvem dispositivo simulado carregar exemplo] mostra-lhe como toouse [limite do Azure IoT] [ lnk-sdk] toosend telemetria do dispositivo para nuvem tooIoT Hub da simulada dispositivos.

Estas instruções abrangem:

* **Arquitetura**: as informações da arquitetura sobre Olá [nuvem dispositivo simulado carregar exemplo].
* **Compilar e executar**: Olá passos necessários toobuild e exemplo de Olá execução.

## <a name="architecture"></a>Arquitetura

Olá [nuvem dispositivo simulado carregar exemplo] mostra como toocreate um gateway que envia a telemetria de simulated o IoT hub tooan dispositivos. Um dispositivo não pode ser capaz de tooconnect diretamente tooIoT Hub porque dispositivo Olá:

* Não utilize um protocolo de comunicações abrangido pelo IoT Hub.
* Não é suficientemente inteligente tooremember Olá identidade atribuída tooit pelo IoT Hub.

Um gateway de IoT pode resolver estes problemas no Olá seguintes formas:

* gateway de Olá compreende o protocolo de Olá utilizado pelo dispositivo Olá, recebe a telemetria do dispositivo para nuvem dos dispositivos de Olá e reencaminha esses tooIoT mensagens Hub utilizando um protocolo abrangido pelo Olá IoT hub.

* gateway de Olá mapeia toodevices de identidades do IoT Hub e age como um proxy quando um dispositivo envia mensagens tooIoT Hub.

Olá seguinte diagrama mostra Olá componentes principais do exemplo Olá, incluindo Olá módulos de limite de IoT:

![][1]

módulos de Olá não passa mensagens diretamente tooeach outro. módulos de Olá publicar mensagens tooan interno mediador que fornece Olá mensagens toohello outros módulos utilizando um mecanismo de subscrição. Para obter mais informações, consulte [introdução ao Azure IoT Edge][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Módulo de ingestão de protocolo

Este módulo é Olá a ponto para a receção de dados a partir de dispositivos, através do gateway de Olá e na nuvem de Olá. Exemplo de Olá, módulo Olá:

1. Cria dados de temperatura simulada. Se utilizar dispositivos físicos, módulo Olá lê dados a partir desses dispositivos físicos.
1. Cria uma mensagem.
1. Coloca Olá simulado temperatura dados no conteúdo da mensagem Olá.
1. Adiciona uma propriedade com uma mensagem de toohello de endereço MAC falsificada.
1. Faz com que o módulo seguinte do Olá mensagem toohello disponíveis na cadeia de Olá.

módulo Olá chamado **ingestão de protocolo X** Olá diagrama anterior é designado **dispositivo simulado** no código de origem Olá.

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; Módulo de ID do Hub IoT

Este módulo verifica a existência de mensagens em fila que tem uma propriedade de endereço Mac. Exemplo de Olá, o módulo de ingestão de protocolo de Olá adiciona propriedade de endereço MAC Olá. Se o módulo Olá localiza essa propriedade, adiciona outra propriedade com uma mensagem de toohello chave do dispositivo IoT Hub. módulo Olá, em seguida, faz com que o módulo seguinte do Olá mensagem toohello disponíveis na cadeia de Olá.

Programador Olá configura um mapeamento entre os endereços MAC e dispositivos do IoT Hub identidades tooassociate Olá simulado com identidades de dispositivo do IoT Hub. Programador Olá adiciona manualmente mapeamento Olá como parte da configuração do módulo Olá.

> [!NOTE]
> Esta amostra utiliza um endereço MAC como identificador de dispositivo exclusivo e correlaciona-o com uma identidade de dispositivo Hub IoT. No entanto, pode escrever o seu próprio módulo que utiliza um identificador exclusivo diferente. Por exemplo, os seus dispositivos podem ter exclusivos de números de série ou dados de telemetria de Olá podem incluir um nome único para o dispositivo incorporado.

### <a name="iot-hub-communication-module"></a>Módulo de comunicação do Hub IoT

Este módulo demora mensagens com um IoT Hub propriedade de chave do dispositivo que foi atribuída pelo módulo Olá de anterior. módulo Olá envia a mensagem de saudação tooIoT conteúdo Hub utilizando Olá protocolo HTTP. HTTP é uma das Olá três protocolos abrangidos pelo IoT Hub.

Em vez de abrir uma ligação para cada dispositivo simulado, este módulo é aberta uma ligação HTTP única do hub IoT do Olá gateway toohello. em seguida, o módulo Olá multiplexes ligações a partir de todos os dispositivos de Olá simulado através dessa ligação. Esta abordagem permite que um único gateway tooconnect muitos mais dispositivos.

## <a name="before-you-get-started"></a>Antes de começar

Antes de começar, tem de:

* [Criar um hub IoT] [ lnk-create-hub] na sua subscrição do Azure, terá de nome de Olá do seu hub toocomplete estas instruções. Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* Adicionar dois iothub de tooyour dispositivos e anote os respetivos ids e as chaves de dispositivo. Pode utilizar Olá [Explorador de dispositivo] [ lnk-device-explorer] ou [iothub explorer] [ lnk-iothub-explorer] ferramenta tooadd dispositivos toohello hub IoT que criou no Olá anterior passo e obter as respetivas chaves.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[nuvem dispositivo simulado carregar exemplo]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md