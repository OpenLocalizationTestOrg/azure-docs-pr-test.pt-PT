---
title: "aaaGet iniciado com a gestão de dispositivos do IoT Hub do Azure (nó) | Microsoft Docs"
description: "Como toouse tooinitiate de gestão de dispositivos do IoT Hub remota do dispositivo ser reiniciado. Utilizar Olá IoT do Azure SDK para Node.js tooimplement uma aplicação de dispositivo simulado que inclui um método direto e uma aplicação de serviço que invoca o método direto Olá."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Introdução à gestão de dispositivos (nó)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Este tutorial mostrar-lhe como:

* Utilize Olá toocreate do portal do Azure, um IoT Hub e criar uma identidade de dispositivo no seu IoT hub.
* Crie uma aplicação de dispositivo simulado que contém um método direto que reinicia nesse dispositivo. Métodos diretos são invocados a partir da nuvem Olá.
* Crie uma aplicação de consola do Node.js que chama o método de direta de reinício de Olá na aplicação de dispositivo simulado Olá através do seu IoT hub.

No final de Olá deste tutorial, tem duas aplicações de consola do Node.js:

**dmpatterns_getstarted_device.js**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente, recebe um método direta de reinício, simula reiniciar o computador físico, relatórios e tempo de Olá reinício último Olá.

**dmpatterns_getstarted_service.js**, que chama um método direto na aplicação de dispositivo simulado Olá, mostra a resposta Olá e Olá apresenta atualizado comunicado propriedades.

toocomplete neste tutorial, terá de Olá seguintes:

* Versão do node.js 0.12 ou posterior <br/>  [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node.js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada
Nesta secção, irá

* Criar uma aplicação de consola do Node.js que responde método direto tooa chamado pela nuvem Olá
* Acionar um reinício do dispositivo simulado
* Olá de utilização comunicados propriedades tooenable dispositivos duplo consultas tooidentify dispositivos e quando estes pela última vez reiniciado

1. Crie uma pasta vazia designada **manageddevice**.  No Olá **manageddevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.  Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```
2. Na sua linha de comandos Olá **manageddevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device** pacote do SDK do dispositivo e **azure-iot-dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Com um editor de texto, crie um **dmpatterns_getstarted_device.js** ficheiro Olá **manageddevice** pasta.
4. Adicione a seguinte Olá 'exigir' instruções início Olá de Olá **dmpatterns_getstarted_device.js** ficheiro:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Adicionar um **connectionString** variável e utilize-toocreate um **cliente** instância.  Substitua a cadeia de ligação de Olá com a cadeia de ligação do dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Adicionar Olá seguinte método direta do função tooimplement Olá no dispositivo Olá
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Abra Olá ligação tooyour IoT hub e iniciar o serviço de escuta do Olá método direto:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Guarde e feche Olá **dmpatterns_getstarted_device.js** ficheiro.

> [!NOTE]
> ações de tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Acionar um reinício remoto no dispositivo Olá utilizando um método direto
Nesta secção, crie uma aplicação de consola do Node.js que inicia um reinício remoto num dispositivo utilizando um método direto. aplicação Olá utiliza Olá do dispositivo duplo consultas toodiscover hora da última reinicialização para que o dispositivo.

1. Crie uma pasta vazia designada **triggerrebootondevice**.  No Olá **triggerrebootondevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.  Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```
2. Na sua linha de comandos Olá **triggerrebootondevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure iothub** pacote do SDK do dispositivo e **azure-iot-dispositivo-mqtt** pacote:
   
    ```
    npm install azure-iothub --save
    ```
3. Com um editor de texto, crie um **dmpatterns_getstarted_service.js** ficheiro Olá **triggerrebootondevice** pasta.
4. Adicione a seguinte Olá 'exigir' instruções início Olá de Olá **dmpatterns_getstarted_service.js** ficheiro:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Adicione Olá seguintes declarações de variável e substitua os valores de marcador de posição de Olá:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Adicione Olá seguinte função tooinvoke Olá dispositivo método tooreboot Olá dispositivo de destino:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Adicione o seguinte Olá funciona tooquery para dispositivo Olá e obter Olá hora da última reinicialização:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Adicione Olá seguinte código toocall Olá as funções que acionam Olá reiniciar método direto e a consulta para Olá reiniciar pela última vez:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Guarde e feche Olá **dmpatterns_getstarted_service.js** ficheiro.

## <a name="run-hello-apps"></a>Executar aplicações de Olá
Agora, está pronto toorun Olá aplicações.

1. Na linha de comandos Olá Olá **manageddevice** pasta, execute Olá toobegin comando à escuta para o método de direta de reinício de Olá a seguir.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Na linha de comandos Olá Olá **triggerrebootondevice** pasta, execute Olá os seguintes comandos tootrigger Olá remoto reiniciar e consultar para Olá do Olá dispositivo duplo toofind reinicie pela última vez.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Consulte Olá dispositivo resposta toohello direta método na consola de Olá.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
