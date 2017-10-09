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
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="0bd4d-104">Introdução à gestão de dispositivos (nó)</span><span class="sxs-lookup"><span data-stu-id="0bd4d-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="0bd4d-105">Este tutorial mostrar-lhe como:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="0bd4d-106">Utilize Olá toocreate do portal do Azure, um IoT Hub e criar uma identidade de dispositivo no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="0bd4d-107">Crie uma aplicação de dispositivo simulado que contém um método direto que reinicia nesse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="0bd4d-108">Métodos diretos são invocados a partir da nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="0bd4d-109">Crie uma aplicação de consola do Node.js que chama o método de direta de reinício de Olá na aplicação de dispositivo simulado Olá através do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="0bd4d-110">No final de Olá deste tutorial, tem duas aplicações de consola do Node.js:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="0bd4d-111">**dmpatterns_getstarted_device.js**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente, recebe um método direta de reinício, simula reiniciar o computador físico, relatórios e tempo de Olá reinício último Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="0bd4d-112">**dmpatterns_getstarted_service.js**, que chama um método direto na aplicação de dispositivo simulado Olá, mostra a resposta Olá e Olá apresenta atualizado comunicado propriedades.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="0bd4d-113">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0bd4d-114">Versão do node.js 0.12 ou posterior</span><span class="sxs-lookup"><span data-stu-id="0bd4d-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="0bd4d-115">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node.js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="0bd4d-116">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-116">An active Azure account.</span></span> <span data-ttu-id="0bd4d-117">(Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="0bd4d-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="0bd4d-118">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="0bd4d-118">Create a simulated device app</span></span>
<span data-ttu-id="0bd4d-119">Nesta secção, irá</span><span class="sxs-lookup"><span data-stu-id="0bd4d-119">In this section, you will</span></span>

* <span data-ttu-id="0bd4d-120">Criar uma aplicação de consola do Node.js que responde método direto tooa chamado pela nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="0bd4d-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="0bd4d-121">Acionar um reinício do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="0bd4d-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="0bd4d-122">Olá de utilização comunicados propriedades tooenable dispositivos duplo consultas tooidentify dispositivos e quando estes pela última vez reiniciado</span><span class="sxs-lookup"><span data-stu-id="0bd4d-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="0bd4d-123">Crie uma pasta vazia designada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="0bd4d-124">No Olá **manageddevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="0bd4d-125">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0bd4d-126">Na sua linha de comandos Olá **manageddevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device** pacote do SDK do dispositivo e **azure-iot-dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="0bd4d-127">Com um editor de texto, crie um **dmpatterns_getstarted_device.js** ficheiro Olá **manageddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="0bd4d-128">Adicione a seguinte Olá 'exigir' instruções início Olá de Olá **dmpatterns_getstarted_device.js** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="0bd4d-129">Adicionar um **connectionString** variável e utilize-toocreate um **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="0bd4d-130">Substitua a cadeia de ligação de Olá com a cadeia de ligação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="0bd4d-131">Adicionar Olá seguinte método direta do função tooimplement Olá no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="0bd4d-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="0bd4d-132">Abra Olá ligação tooyour IoT hub e iniciar o serviço de escuta do Olá método direto:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="0bd4d-133">Guarde e feche Olá **dmpatterns_getstarted_device.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="0bd4d-134">ações de tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0bd4d-135">No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="0bd4d-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="0bd4d-136">Acionar um reinício remoto no dispositivo Olá utilizando um método direto</span><span class="sxs-lookup"><span data-stu-id="0bd4d-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="0bd4d-137">Nesta secção, crie uma aplicação de consola do Node.js que inicia um reinício remoto num dispositivo utilizando um método direto.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="0bd4d-138">aplicação Olá utiliza Olá do dispositivo duplo consultas toodiscover hora da última reinicialização para que o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="0bd4d-139">Crie uma pasta vazia designada **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="0bd4d-140">No Olá **triggerrebootondevice** pasta, crie um ficheiro de Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="0bd4d-141">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0bd4d-142">Na sua linha de comandos Olá **triggerrebootondevice** pasta, execute Olá Olá tooinstall de comando a seguir **azure iothub** pacote do SDK do dispositivo e **azure-iot-dispositivo-mqtt** pacote:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="0bd4d-143">Com um editor de texto, crie um **dmpatterns_getstarted_service.js** ficheiro Olá **triggerrebootondevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="0bd4d-144">Adicione a seguinte Olá 'exigir' instruções início Olá de Olá **dmpatterns_getstarted_service.js** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="0bd4d-145">Adicione Olá seguintes declarações de variável e substitua os valores de marcador de posição de Olá:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="0bd4d-146">Adicione Olá seguinte função tooinvoke Olá dispositivo método tooreboot Olá dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
7. <span data-ttu-id="0bd4d-147">Adicione o seguinte Olá funciona tooquery para dispositivo Olá e obter Olá hora da última reinicialização:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
8. <span data-ttu-id="0bd4d-148">Adicione Olá seguinte código toocall Olá as funções que acionam Olá reiniciar método direto e a consulta para Olá reiniciar pela última vez:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="0bd4d-149">Guarde e feche Olá **dmpatterns_getstarted_service.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="0bd4d-150">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="0bd4d-150">Run hello apps</span></span>
<span data-ttu-id="0bd4d-151">Agora, está pronto toorun Olá aplicações.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="0bd4d-152">Na linha de comandos Olá Olá **manageddevice** pasta, execute Olá toobegin comando à escuta para o método de direta de reinício de Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="0bd4d-153">Na linha de comandos Olá Olá **triggerrebootondevice** pasta, execute Olá os seguintes comandos tootrigger Olá remoto reiniciar e consultar para Olá do Olá dispositivo duplo toofind reinicie pela última vez.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="0bd4d-154">Consulte Olá dispositivo resposta toohello direta método na consola de Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-154">You see hello device response toohello direct method in hello console.</span></span>

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
