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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="927a7-104">Ligar o seu dispositivo simulado tooyour do IoT hub com o Python</span><span class="sxs-lookup"><span data-stu-id="927a7-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="927a7-105">No final de Olá deste tutorial, terá de duas aplicações de Python:</span><span class="sxs-lookup"><span data-stu-id="927a7-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="927a7-106">**CreateDeviceIdentity.py**, que cria uma identidade de dispositivo e tooconnect de chave de segurança associadas, a aplicação de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="927a7-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="927a7-107">**SimulatedDevice.py**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e, periodicamente envia uma telemetria mensagem através do protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="927a7-108">artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun ambas as aplicações em dispositivos e a sua solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="927a7-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="927a7-109">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="927a7-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="927a7-110">[Python 2.x ou 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="927a7-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="927a7-111">Certifique-se toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração.</span><span class="sxs-lookup"><span data-stu-id="927a7-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="927a7-112">Quando lhe for pedido durante a instalação de Olá, certifique-se de que variável de ambiente específico da plataforma do tooyour Python tooadd.</span><span class="sxs-lookup"><span data-stu-id="927a7-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="927a7-113">Se estiver a utilizar o Python 2. x, poderá ter demasiado[instalar ou atualizar *pip*, hello Python do pacote sistema de gestão][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="927a7-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="927a7-114">Se estiver a utilizar o sistema operativo Windows, em seguida, [pacote redistribuível do Visual C++] [ lnk-visual-c-redist] tooallow utilização Olá DLLs nativas do Python.</span><span class="sxs-lookup"><span data-stu-id="927a7-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="927a7-115">[Node.js 4.0 ou posterior][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="927a7-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="927a7-116">Certifique-se toouse Olá 32 bits ou 64 bits instalação conforme exigido pela sua configuração.</span><span class="sxs-lookup"><span data-stu-id="927a7-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="927a7-117">Isto é necessário tooinstall Olá [ferramenta Explorador do Hub IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="927a7-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="927a7-118">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="927a7-118">An active Azure account.</span></span> <span data-ttu-id="927a7-119">Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="927a7-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="927a7-120">Olá *pip* pacotes para `azure-iothub-service-client` e `azure-iothub-device-client` estão atualmente disponíveis apenas para o sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="927a7-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="927a7-121">SO de Linux/Mac, consulte toohello Linux e Mac específicas de SO secções Olá [preparar o ambiente de desenvolvimento para o Python] [ lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="927a7-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="927a7-122">Criou o seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="927a7-122">You have now created your IoT hub.</span></span> <span data-ttu-id="927a7-123">Utilize Olá nome de anfitrião do IoT Hub e Olá cadeia de ligação do IoT Hub rest Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="927a7-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="927a7-124">Pode também criar facilmente o hub IoT numa linha de comandos, utilizando Olá Python ou Node.js com base CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="927a7-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="927a7-125">artigo de Olá [criar um IoT hub com Olá Azure CLI 2.0] [ lnk-azure-cli-hub] mostra Olá toodo passos rápidos para.</span><span class="sxs-lookup"><span data-stu-id="927a7-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="927a7-126">Criar uma identidade de dispositivo</span><span class="sxs-lookup"><span data-stu-id="927a7-126">Create a device identity</span></span>
<span data-ttu-id="927a7-127">Esta secção lista os passos de Olá toocreate uma aplicação de consola do Python, que cria uma identidade de dispositivo no registo de identidade Olá do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="927a7-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="927a7-128">Ligar um dispositivo pode apenas tooIoT Hub se tiver uma entrada no registo de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="927a7-129">Para obter mais informações, consulte Olá **registo de identidade** secção Olá [guia para programadores do IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="927a7-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="927a7-130">Quando executar esta aplicação de consola, gera um ID de dispositivo exclusivo e chave que o seu dispositivo pode utilizar tooidentify próprio quando envia dispositivo para nuvem mensagens tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="927a7-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="927a7-131">Abra uma linha de comandos e instalar Olá **SDK do serviço do Azure IoT Hub para o Python**.</span><span class="sxs-lookup"><span data-stu-id="927a7-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="927a7-132">Feche a linha de comandos de Olá depois de instalar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="927a7-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="927a7-133">Crie um ficheiro Python denominado **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="927a7-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="927a7-134">Abri-lo no [um editor/IDE do Python à sua escolha][lnk-python-ide-list], por exemplo, Olá predefinido [INATIVO][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="927a7-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="927a7-135">Adicione Olá seguintes módulos do código tooimport Olá necessário de SDK do serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="927a7-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="927a7-136">Adicionar Olá código a seguir, substituindo o marcador de posição de Olá para `[IoTHub Connection String]` pela cadeia de ligação de Olá para Olá IoT hub que criou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="927a7-137">Pode utilizar qualquer nome como Olá `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="927a7-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="927a7-138">Adicionar Olá seguintes função tooprint algumas das informações do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="927a7-139">Adicione Olá seguinte identificação dispositivo função toocreate Olá utilizando Olá Gestor de registo.</span><span class="sxs-lookup"><span data-stu-id="927a7-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="927a7-140">Por fim, adicione a função principal Olá da seguinte forma e guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="927a7-141">Na linha de comandos Olá, execute Olá **CreateDeviceIdentity.py** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="927a7-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="927a7-142">Deverá ver o dispositivo simulado Olá obter criado.</span><span class="sxs-lookup"><span data-stu-id="927a7-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="927a7-143">Tome nota dos Olá **deviceId** e Olá **primaryKey** deste dispositivo.</span><span class="sxs-lookup"><span data-stu-id="927a7-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="927a7-144">Precisar mais tarde estes valores quando criar uma aplicação que liga tooIoT Hub como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="927a7-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Dispositivo criado com êxito][1]

> [!NOTE]
> <span data-ttu-id="927a7-146">Olá registo de identidade do IoT Hub apenas armazena dispositivo identidades tooenable acesso seguro toohello do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="927a7-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="927a7-147">Armazena toouse de IDs e chaves de dispositivo como credenciais de segurança e um sinalizador ativado/desativado que pode utilizar toodisable acesso de um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="927a7-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="927a7-148">Se a sua aplicação tiver toostore outros metadados específicos do dispositivo, deverá utilizar um armazenamento específico da aplicação.</span><span class="sxs-lookup"><span data-stu-id="927a7-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="927a7-149">Para obter mais informações, consulte Olá [guia para programadores do IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="927a7-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="927a7-150">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="927a7-150">Create a simulated device app</span></span>
<span data-ttu-id="927a7-151">Esta secção lista os passos de Olá toocreate uma aplicação de consola do Python, que simula um dispositivo e envia o IoT hub tooyour mensagens do dispositivo para nuvem.</span><span class="sxs-lookup"><span data-stu-id="927a7-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="927a7-152">Abra uma nova linha de comandos e instalar Olá SDK de dispositivo do Azure IoT Hub para o Python da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="927a7-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="927a7-153">Feche a linha de comandos de Olá após a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="927a7-154">Crie um ficheiro chamado **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="927a7-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="927a7-155">Abra-o num editor/IDE para Python à sua escolha (por exemplo, o IDLE).</span><span class="sxs-lookup"><span data-stu-id="927a7-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="927a7-156">Adicione Olá seguintes módulos de Olá necessário tooimport de código de dispositivo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="927a7-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="927a7-157">Adicione o seguinte Olá code e substitua o marcador de posição de Olá para `[IoTHub Device Connection String]` pela cadeia de ligação de Olá para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="927a7-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="927a7-158">cadeia de ligação do dispositivo Olá é normalmente Olá no formato `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="927a7-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="927a7-159">Olá utilize **deviceId** e **primaryKey** do dispositivo Olá que criou no Olá tooreplace da secção anterior do Olá `<deviceId>` e `<primaryKey>` respetivamente.</span><span class="sxs-lookup"><span data-stu-id="927a7-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="927a7-160">Substitua `<hostName>` pelo nome de anfitrião do hub IoT, geralmente como `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="927a7-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="927a7-161">Adicione o seguinte código toodefine uma chamada de retorno de confirmação de envio de Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="927a7-162">Adicione Olá cliente de dispositivo do código tooinitialize Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="927a7-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="927a7-163">Adicione o seguinte Olá funcione tooformat e envia uma mensagem a partir do seu IoT hub do dispositivo simulado tooyour.</span><span class="sxs-lookup"><span data-stu-id="927a7-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="927a7-164">Por fim, adicione a função principal Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="927a7-165">Guarde e feche Olá **SimulatedDevice.py** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="927a7-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="927a7-166">Está agora pronto toorun esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="927a7-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="927a7-167">ações de tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="927a7-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="927a7-168">No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="927a7-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="927a7-169">Receber mensagens do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="927a7-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="927a7-170">mensagens de telemetria de tooreceive do seu dispositivo, terá de toouse um [Event Hubs][lnk-event-hubs-overview]-ponto final compatível com exposta pelo Olá que lê mensagens hello do dispositivo para a nuvem do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="927a7-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="927a7-171">Olá leitura [introdução ao Event Hubs] [ lnk-eventhubs-tutorial] tutorial para obter informações sobre como tooprocess mensagens de Hubs de eventos para o ponto final compatível com o Event Hub do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="927a7-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="927a7-172">Os Event Hubs não suporta a telemetria no Python ainda, pelo que pode criar um [Node.js](iot-hub-node-node-getstarted.md#D2C_node) ou um [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) mensagens dispositivo-nuvem Olá de tooread de aplicação de consola baseada em Event Hubs do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="927a7-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="927a7-173">Este tutorial mostra como pode utilizar Olá [ferramenta Explorador do Hub IoT] [ lnk-iot-hub-explorer] tooread estas mensagens do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="927a7-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="927a7-174">Abra uma linha de comandos e instale Olá Explorador do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="927a7-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="927a7-175">Executar Olá seguinte comando na linha de comandos Olá, toobegin monitorização Olá mensagens do dispositivo para a nuvem do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="927a7-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="927a7-176">Utilizar cadeia de ligação do seu IoT hub no marcador de posição de Olá após `--login`.</span><span class="sxs-lookup"><span data-stu-id="927a7-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="927a7-177">Abra uma nova linha de comandos e navegue diretório toohello Olá **SimulatedDevice.py** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="927a7-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="927a7-178">Executar Olá **SimulatedDevice.py** ficheiro, que envia periodicamente do IoT hub telemetria dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="927a7-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="927a7-179">Observe mensagens hello do dispositivo na linha de comandos Olá executar Olá Explorador do Hub IoT da secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Mensagens do dispositivo para a cloud Python][2]

## <a name="next-steps"></a><span data-ttu-id="927a7-181">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="927a7-181">Next steps</span></span>
<span data-ttu-id="927a7-182">Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="927a7-183">Utilizar este dispositivo identidade tooenable Olá simulado dispositivo aplicação toosend mensagens do dispositivo para nuvem toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="927a7-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="927a7-184">Observados mensagens hello recebidas pelo Olá IoT hub com ajuda Olá da ferramenta de IoT Hub Explorer Olá.</span><span class="sxs-lookup"><span data-stu-id="927a7-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="927a7-185">tooexplore Olá Python SDK para utilização do IoT Hub do Azure em profundidade, visite [neste repositório de Git Hub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="927a7-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="927a7-186">tooreview Olá mensagens as capacidades de Olá SDK do serviço do Azure IoT Hub para o Python, pode transferir e executar [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="927a7-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="927a7-187">Para simulação de lado de dispositivo utilizando Olá SDK de dispositivo do Azure IoT Hub para o Python, pode transferir e executar Olá [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="927a7-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="927a7-188">toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="927a7-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="927a7-189">[Ligar o seu dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="927a7-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="927a7-190">[Getting started with device management (Introdução à gestão de dispositivos)][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="927a7-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="927a7-191">[Começar a utilizar o Edge IoT do Azure][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="927a7-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="927a7-192">toolearn como tooextend as mensagens de dispositivo para a nuvem de IoT processo de solução e, em escala, consulte o artigo Olá [processar mensagens do dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="927a7-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
