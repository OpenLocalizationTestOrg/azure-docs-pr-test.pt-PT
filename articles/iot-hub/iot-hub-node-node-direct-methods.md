---
title: "aaaAzure IoT Hub direcionar métodos (nó) | Microsoft Docs"
description: "Como toouse IoT Hub do Azure direcionar os métodos. Utilize Olá SDKs de IoT do Azure para Node.js tooimplement uma aplicação de dispositivo simulado que inclui um método direto e uma aplicação de serviço que invoca o método direto Olá."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Utilize métodos diretos no seu dispositivo IoT com o Node.js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

No final de Olá deste tutorial, tem duas aplicações de consola do Node.js:

* **CallMethodOnDevice.js**, que chama um método na aplicação de dispositivo simulado Olá e mostra a resposta Olá.
* **SimulatedDevice.js**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e responde método toohello chamado pela nuvem Olá.

> [!NOTE]
> artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun ambas as aplicações em dispositivos e a sua solução de back-end.
> 
> 

toocomplete neste tutorial, terá de Olá seguintes:

* Versão 0.10.x ou posterior do Node.js.
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada
Nesta secção, crie uma aplicação de consola do Node.js que responde método tooa chamado pela nuvem Olá.

1. Crie uma nova pasta vazia designada **simulateddevice**. No Olá **simulateddevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá. Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```
2. Na sua linha de comandos Olá **simulateddevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device** pacote do SDK do dispositivo e **azure-iot-dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Com um editor de texto, crie um novo **SimulatedDevice.js** ficheiro Olá **simulateddevice** pasta.
4. Adicione Olá seguinte `require` as instruções em Olá início do Olá **SimulatedDevice.js** ficheiro:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Adicionar um **connectionString** variável e utilize-toocreate um **DeviceClient** instância. Substitua **{cadeia de ligação do dispositivo}** pela cadeia de ligação do dispositivo Olá que gerou no Olá *criar uma identidade de dispositivo* secção:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Adicione Olá seguindo o método de Olá tooimplement de função do dispositivo Olá:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Abra Olá ligação tooyour IoT hub e iniciar o serviço de escuta do inicializar Olá método:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Guarde e feche Olá **SimulatedDevice.js** ficheiro.

> [!NOTE]
> ações de tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar as políticas de repetição (como tentativas de ligação), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Chamar um método num dispositivo
Nesta secção, crie uma aplicação de consola do Node.js que chama um método na aplicação de dispositivo simulado Olá e, em seguida, mostra a resposta Olá.

1. Criar uma nova pasta vazia designada **callmethodondevice**. No Olá **callmethodondevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá. Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```
2. Na sua linha de comandos Olá **callmethodondevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure iothub** pacote:
   
    ```
    npm install azure-iothub --save
    ```
3. Com um editor de texto, crie um **CallMethodOnDevice.js** ficheiro Olá **callmethodondevice** pasta.
4. Adicione Olá seguinte `require` as instruções em Olá início do Olá **CallMethodOnDevice.js** ficheiro:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Adicionar Olá seguinte declaração de variável e substitua o valor do marcador de posição de Olá Olá cadeia de ligação do IoT Hub para o seu hub:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Crie Olá cliente tooopen Olá ligação tooyour do IoT hub.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Adicione Olá função tooinvoke Olá dispositivo método impressão Olá dispositivo resposta toohello consola e os seguintes:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Guarde e feche Olá **CallMethodOnDevice.js** ficheiro.

## <a name="run-hello-apps"></a>Executar aplicações de Olá
Agora, está pronto toorun Olá aplicações.

1. Numa linha de comandos da Olá **simulateddevice** pasta, execute Olá seguir toostart comando à escuta para chamadas de método do seu IoT Hub:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. Numa linha de comandos da Olá **callmethodondevice** pasta, execute Olá seguir toobegin comando monitorização do seu IoT hub:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Verá que o dispositivo Olá reagir toohello método por imprimindo mensagem de saudação e aplicação Olá denominada resposta de Olá Olá método apresentação do dispositivo Olá:
   
    ![][9]

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Este dispositivo identidade tooenable Olá simulado dispositivo aplicação tooreact toomethods invocado pela nuvem Olá que utilizou. Também criou uma aplicação que invoca os métodos no dispositivo Olá e mostra a resposta de Olá do dispositivo Olá. 

toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Introdução ao IoT Hub]
* [Agenda de tarefas em vários dispositivos][lnk-devguide-jobs]

toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introdução ao IoT Hub]: iot-hub-node-node-getstarted.md
