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
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="06ef8-104">Utilize métodos diretos no seu dispositivo IoT com o Node.js</span><span class="sxs-lookup"><span data-stu-id="06ef8-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="06ef8-105">No final de Olá deste tutorial, tem duas aplicações de consola do Node.js:</span><span class="sxs-lookup"><span data-stu-id="06ef8-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="06ef8-106">**CallMethodOnDevice.js**, que chama um método na aplicação de dispositivo simulado Olá e mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="06ef8-107">**SimulatedDevice.js**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e responde método toohello chamado pela nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="06ef8-108">artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun ambas as aplicações em dispositivos e a sua solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="06ef8-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="06ef8-109">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="06ef8-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="06ef8-110">Versão 0.10.x ou posterior do Node.js.</span><span class="sxs-lookup"><span data-stu-id="06ef8-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="06ef8-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="06ef8-111">An active Azure account.</span></span> <span data-ttu-id="06ef8-112">(Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="06ef8-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="06ef8-113">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="06ef8-113">Create a simulated device app</span></span>
<span data-ttu-id="06ef8-114">Nesta secção, crie uma aplicação de consola do Node.js que responde método tooa chamado pela nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="06ef8-115">Crie uma nova pasta vazia designada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="06ef8-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="06ef8-116">No Olá **simulateddevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="06ef8-117">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="06ef8-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="06ef8-118">Na sua linha de comandos Olá **simulateddevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device** pacote do SDK do dispositivo e **azure-iot-dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="06ef8-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="06ef8-119">Com um editor de texto, crie um novo **SimulatedDevice.js** ficheiro Olá **simulateddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="06ef8-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="06ef8-120">Adicione Olá seguinte `require` as instruções em Olá início do Olá **SimulatedDevice.js** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="06ef8-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="06ef8-121">Adicionar um **connectionString** variável e utilize-toocreate um **DeviceClient** instância.</span><span class="sxs-lookup"><span data-stu-id="06ef8-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="06ef8-122">Substitua **{cadeia de ligação do dispositivo}** pela cadeia de ligação do dispositivo Olá que gerou no Olá *criar uma identidade de dispositivo* secção:</span><span class="sxs-lookup"><span data-stu-id="06ef8-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="06ef8-123">Adicione Olá seguindo o método de Olá tooimplement de função do dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="06ef8-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
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
7. <span data-ttu-id="06ef8-124">Abra Olá ligação tooyour IoT hub e iniciar o serviço de escuta do inicializar Olá método:</span><span class="sxs-lookup"><span data-stu-id="06ef8-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="06ef8-125">Guarde e feche Olá **SimulatedDevice.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="06ef8-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="06ef8-126">ações de tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="06ef8-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="06ef8-127">No código de produção, deve implementar as políticas de repetição (como tentativas de ligação), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="06ef8-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="06ef8-128">Chamar um método num dispositivo</span><span class="sxs-lookup"><span data-stu-id="06ef8-128">Call a method on a device</span></span>
<span data-ttu-id="06ef8-129">Nesta secção, crie uma aplicação de consola do Node.js que chama um método na aplicação de dispositivo simulado Olá e, em seguida, mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="06ef8-130">Criar uma nova pasta vazia designada **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="06ef8-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="06ef8-131">No Olá **callmethodondevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="06ef8-132">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="06ef8-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="06ef8-133">Na sua linha de comandos Olá **callmethodondevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure iothub** pacote:</span><span class="sxs-lookup"><span data-stu-id="06ef8-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="06ef8-134">Com um editor de texto, crie um **CallMethodOnDevice.js** ficheiro Olá **callmethodondevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="06ef8-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="06ef8-135">Adicione Olá seguinte `require` as instruções em Olá início do Olá **CallMethodOnDevice.js** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="06ef8-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="06ef8-136">Adicionar Olá seguinte declaração de variável e substitua o valor do marcador de posição de Olá Olá cadeia de ligação do IoT Hub para o seu hub:</span><span class="sxs-lookup"><span data-stu-id="06ef8-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="06ef8-137">Crie Olá cliente tooopen Olá ligação tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="06ef8-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="06ef8-138">Adicione Olá função tooinvoke Olá dispositivo método impressão Olá dispositivo resposta toohello consola e os seguintes:</span><span class="sxs-lookup"><span data-stu-id="06ef8-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
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
8. <span data-ttu-id="06ef8-139">Guarde e feche Olá **CallMethodOnDevice.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="06ef8-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="06ef8-140">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="06ef8-140">Run hello apps</span></span>
<span data-ttu-id="06ef8-141">Agora, está pronto toorun Olá aplicações.</span><span class="sxs-lookup"><span data-stu-id="06ef8-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="06ef8-142">Numa linha de comandos da Olá **simulateddevice** pasta, execute Olá seguir toostart comando à escuta para chamadas de método do seu IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="06ef8-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="06ef8-143">Numa linha de comandos da Olá **callmethodondevice** pasta, execute Olá seguir toobegin comando monitorização do seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="06ef8-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="06ef8-144">Verá que o dispositivo Olá reagir toohello método por imprimindo mensagem de saudação e aplicação Olá denominada resposta de Olá Olá método apresentação do dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="06ef8-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="06ef8-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06ef8-145">Next steps</span></span>
<span data-ttu-id="06ef8-146">Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="06ef8-147">Este dispositivo identidade tooenable Olá simulado dispositivo aplicação tooreact toomethods invocado pela nuvem Olá que utilizou.</span><span class="sxs-lookup"><span data-stu-id="06ef8-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="06ef8-148">Também criou uma aplicação que invoca os métodos no dispositivo Olá e mostra a resposta de Olá do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="06ef8-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="06ef8-149">toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="06ef8-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="06ef8-150">[Introdução ao IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="06ef8-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="06ef8-151">[Agenda de tarefas em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="06ef8-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="06ef8-152">toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="06ef8-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
