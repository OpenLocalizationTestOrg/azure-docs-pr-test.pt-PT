---
title: aaaGet ao Azure IoT Hub (Python) | Microsoft Docs
description: "Saiba como toosend dispositivo para nuvem mensagens tooAzure IoT Hub com os IoT SDKs para o Python. Criar dispositivo simulado e tooregister de aplicações de serviço, o dispositivo, enviar mensagens e ler mensagens a partir do IoT hub."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Ligar o seu dispositivo simulado tooyour do IoT hub com o Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

No final de Olá deste tutorial, terá de duas aplicações de Python:

* **CreateDeviceIdentity.py**, que cria uma identidade de dispositivo e tooconnect de chave de segurança associadas, a aplicação de dispositivo simulado.
* **SimulatedDevice.py**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e, periodicamente envia uma telemetria mensagem através do protocolo MQTT Olá.

> [!NOTE]
> artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun ambas as aplicações em dispositivos e a sua solução de back-end.
> 
> 

toocomplete neste tutorial, terá de Olá seguintes:

* [Python 2.x ou 3.x][lnk-python-download]. Certifique-se toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração. Quando lhe for pedido durante a instalação de Olá, certifique-se de que variável de ambiente específico da plataforma do tooyour Python tooadd. Se estiver a utilizar o Python 2. x, poderá ter demasiado[instalar ou atualizar *pip*, hello Python do pacote sistema de gestão][lnk-install-pip].
* Se estiver a utilizar o sistema operativo Windows, em seguida, [pacote redistribuível do Visual C++] [ lnk-visual-c-redist] tooallow utilização Olá DLLs nativas do Python.
* [Node.js 4.0 ou posterior][lnk-node-download]. Certifique-se toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração. Isto é necessário tooinstall Olá [ferramenta Explorador do Hub IoT][lnk-iot-hub-explorer].
* Uma conta ativa do Azure. Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.

> [!NOTE]
> Olá *pip* pacotes para `azure-iothub-service-client` e `azure-iothub-device-client` estão atualmente disponíveis apenas para o sistema operativo Windows. SO de Linux/Mac, consulte toohello Linux e Mac específicas de SO secções Olá [preparar o ambiente de desenvolvimento para o Python] [ lnk-python-devbox] post.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Criou o seu hub IoT. Utilize Olá nome de anfitrião do IoT Hub e Olá cadeia de ligação do IoT Hub rest Olá deste tutorial.

> [!NOTE]
> Pode também criar facilmente o hub IoT numa linha de comandos, utilizando Olá Python ou Node.js com base CLI do Azure. artigo de Olá [criar um IoT hub com Olá Azure CLI 2.0] [ lnk-azure-cli-hub] mostra Olá toodo passos rápidos para. 
> 

## <a name="create-a-device-identity"></a>Criar uma identidade de dispositivo
Esta secção lista os passos de Olá toocreate uma aplicação de consola do Python, que cria uma identidade de dispositivo no registo de identidade Olá do seu IoT hub. Ligar um dispositivo pode apenas tooIoT Hub se tiver uma entrada no registo de identidade Olá. Para obter mais informações, consulte Olá **registo de identidade** secção Olá [guia para programadores do IoT Hub][lnk-devguide-identity]. Quando executar esta aplicação de consola, gera um ID de dispositivo exclusivo e chave que o seu dispositivo pode utilizar tooidentify próprio quando envia dispositivo para nuvem mensagens tooIoT Hub.

1. Abra uma linha de comandos e instalar Olá **SDK do serviço do Azure IoT Hub para o Python**. Feche a linha de comandos de Olá depois de instalar Olá SDK.

    ```
    pip install azure-iothub-service-client
    ```

2. Crie um ficheiro Python denominado **CreateDeviceIdentity.py**. Abri-lo no [um editor/IDE do Python à sua escolha][lnk-python-ide-list], por exemplo, Olá predefinido [INATIVO][lnk-idle].

3. Adicione Olá seguintes módulos do código tooimport Olá necessário de SDK do serviço de Olá:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Adicionar Olá código a seguir, substituindo o marcador de posição de Olá para `[IoTHub Connection String]` pela cadeia de ligação de Olá para Olá IoT hub que criou na secção anterior Olá. Pode utilizar qualquer nome como Olá `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Adicionar Olá seguintes função tooprint algumas das informações do dispositivo Olá.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Adicione Olá seguinte identificação dispositivo função toocreate Olá utilizando Olá Gestor de registo. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Por fim, adicione a função principal Olá da seguinte forma e guarde o ficheiro de Olá.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. Na linha de comandos Olá, execute Olá **CreateDeviceIdentity.py** da seguinte forma:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Deverá ver o dispositivo simulado Olá obter criado. Tome nota dos Olá **deviceId** e Olá **primaryKey** deste dispositivo. Precisar mais tarde estes valores quando criar uma aplicação que liga tooIoT Hub como um dispositivo.

    ![Dispositivo criado com êxito][1]

> [!NOTE]
> Olá registo de identidade do IoT Hub apenas armazena dispositivo identidades tooenable acesso seguro toohello do IoT hub. Armazena toouse de IDs e chaves de dispositivo como credenciais de segurança e um sinalizador ativado/desativado que pode utilizar toodisable acesso de um dispositivo individual. Se a sua aplicação tiver toostore outros metadados específicos do dispositivo, deverá utilizar um armazenamento específico da aplicação. Para obter mais informações, consulte Olá [guia para programadores do IoT Hub][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada
Esta secção lista os passos de Olá toocreate uma aplicação de consola do Python, que simula um dispositivo e envia o IoT hub tooyour mensagens do dispositivo para nuvem.

1. Abra uma nova linha de comandos e instalar Olá SDK de dispositivo do Azure IoT Hub para o Python da seguinte forma. Feche a linha de comandos de Olá após a instalação de Olá.

    ```
    pip install azure-iothub-device-client
    ```
2. Crie um ficheiro chamado **SimulatedDevice.py**. Abra-o num editor/IDE para Python à sua escolha (por exemplo, o IDLE).

3. Adicione Olá seguintes módulos de Olá necessário tooimport de código de dispositivo Olá SDK.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Adicione o seguinte Olá code e substitua o marcador de posição de Olá para `[IoTHub Device Connection String]` pela cadeia de ligação de Olá para o seu dispositivo. cadeia de ligação do dispositivo Olá é normalmente Olá no formato `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Olá utilize **deviceId** e **primaryKey** do dispositivo Olá que criou no Olá tooreplace da secção anterior do Olá `<deviceId>` e `<primaryKey>` respetivamente. Substitua `<hostName>` pelo nome de anfitrião do hub IoT, geralmente como `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Adicione o seguinte código toodefine uma chamada de retorno de confirmação de envio de Olá. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Adicione Olá cliente de dispositivo do código tooinitialize Olá a seguir.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Adicione o seguinte Olá funcione tooformat e envia uma mensagem a partir do seu IoT hub do dispositivo simulado tooyour.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Por fim, adicione a função principal Olá. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Guarde e feche Olá **SimulatedDevice.py** ficheiro. Está agora pronto toorun esta aplicação.

> [!NOTE]
> ações de tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Receber mensagens do dispositivo simulado
mensagens de telemetria de tooreceive do seu dispositivo, terá de toouse um [Event Hubs][lnk-event-hubs-overview]-ponto final compatível com exposta pelo Olá que lê mensagens hello do dispositivo para a nuvem do IoT Hub. Olá leitura [introdução ao Event Hubs] [ lnk-eventhubs-tutorial] tutorial para obter informações sobre como tooprocess mensagens de Hubs de eventos para o ponto final compatível com o Event Hub do seu IoT hub. Os Event Hubs não suporta a telemetria no Python ainda, pelo que pode criar um [Node.js](iot-hub-node-node-getstarted.md#D2C_node) ou um [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) mensagens dispositivo-nuvem Olá de tooread de aplicação de consola baseada em Event Hubs do IoT Hub. Este tutorial mostra como pode utilizar Olá [ferramenta Explorador do Hub IoT] [ lnk-iot-hub-explorer] tooread estas mensagens do dispositivo.

1. Abra uma linha de comandos e instale Olá Explorador do Hub IoT. 

    ```
    npm install -g iothub-explorer
    ```

2. Executar Olá seguinte comando na linha de comandos Olá, toobegin monitorização Olá mensagens do dispositivo para a nuvem do seu dispositivo. Utilizar cadeia de ligação do seu IoT hub no marcador de posição de Olá após `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Abra uma nova linha de comandos e navegue diretório toohello Olá **SimulatedDevice.py** ficheiro.

4. Executar Olá **SimulatedDevice.py** ficheiro, que envia periodicamente do IoT hub telemetria dados tooyour. 
   
    ```
    python SimulatedDevice.py
    ```
5. Observe mensagens hello do dispositivo na linha de comandos Olá executar Olá Explorador do Hub IoT da secção anterior Olá. 

    ![Mensagens do dispositivo para a cloud Python][2]

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Utilizar este dispositivo identidade tooenable Olá simulado dispositivo aplicação toosend mensagens do dispositivo para nuvem toohello hub IoT. Observados mensagens hello recebidas pelo Olá IoT hub com ajuda Olá da ferramenta de IoT Hub Explorer Olá. 

tooexplore Olá Python SDK para utilização do IoT Hub do Azure em profundidade, visite [neste repositório de Git Hub][lnk-python-github]. tooreview Olá mensagens as capacidades de Olá SDK do serviço do Azure IoT Hub para o Python, pode transferir e executar [iothub_messaging_sample.py][lnk-messaging-sample]. Para simulação de lado de dispositivo utilizando Olá SDK de dispositivo do Azure IoT Hub para o Python, pode transferir e executar Olá [iothub_client_sample.py][lnk-client-sample].

toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Ligar o seu dispositivo][lnk-connect-device]
* [Getting started with device management (Introdução à gestão de dispositivos)][lnk-device-management]
* [Começar a utilizar o Edge IoT do Azure][lnk-iot-edge]

toolearn como tooextend as mensagens de dispositivo para a nuvem de IoT processo de solução e, em escala, consulte o artigo Olá [processar mensagens do dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
