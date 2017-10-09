---
title: aaaConnect um dispositivo com o Node.js | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurada solução de monitorização remota, utilizando uma aplicação de escrita no Node.js."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="e6688-103">Ligar o seu toohello de dispositivo (Node.js) de solução pré-configurada de monitorização remota</span><span class="sxs-lookup"><span data-stu-id="e6688-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="e6688-104">Criar uma solução de exemplo de node.js</span><span class="sxs-lookup"><span data-stu-id="e6688-104">Create a node.js sample solution</span></span>

<span data-ttu-id="e6688-105">Certifique-se de que a versão Node.js 0.11.5 ou posterior está instalado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e6688-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="e6688-106">Pode executar `node --version` na versão de Olá toocheck do Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="e6688-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="e6688-107">Crie uma pasta denominada **RemoteMonitoring** no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e6688-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="e6688-108">Navegue toothis pasta no seu ambiente de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="e6688-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="e6688-109">Olá execute os seguintes comandos toodownload e instalar pacotes de Olá precisa de aplicação de exemplo de Olá toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e6688-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="e6688-110">No Olá **RemoteMonitoring** pasta, crie um ficheiro chamado **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="e6688-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="e6688-111">Abra este ficheiro num editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e6688-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="e6688-112">No Olá **remote_monitoring.js** ficheiro, adicione o seguinte Olá `require` instruções:</span><span class="sxs-lookup"><span data-stu-id="e6688-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="e6688-113">Adicionar Olá seguintes declarações de variável após Olá `require` instruções.</span><span class="sxs-lookup"><span data-stu-id="e6688-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="e6688-114">Substitua os valores do marcador de posição de Olá [Id de dispositivo] e [chave do dispositivo] com valores que apontou para o seu dispositivo no dashboard de solução de monitorização remota de Olá.</span><span class="sxs-lookup"><span data-stu-id="e6688-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="e6688-115">Utilize Olá o nome de anfitrião do IoT Hub do tooreplace de dashboard de solução Olá [IoTHub nome].</span><span class="sxs-lookup"><span data-stu-id="e6688-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="e6688-116">Por exemplo, se o Nome de anfitrião do seu Hub IoT for **contoso.azure devices.net**, substitua [IoTHub Name] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="e6688-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="e6688-117">Adicione Olá seguintes variáveis toodefine alguns dados de telemetria base:</span><span class="sxs-lookup"><span data-stu-id="e6688-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="e6688-118">Adicione Olá os resultados da operação do programa auxiliar função tooprint os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e6688-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="e6688-119">Adicione Olá valores de telemetria do programa auxiliar função toouse toorandomize Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e6688-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="e6688-120">Adicionar Olá seguinte definição para Olá **DeviceInfo** dispositivo do objeto Olá envia no arranque:</span><span class="sxs-lookup"><span data-stu-id="e6688-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="e6688-121">Adicione Olá seguinte definição para o dispositivo duplo de Olá comunicadas valores.</span><span class="sxs-lookup"><span data-stu-id="e6688-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="e6688-122">Esta definição inclui descrições dos métodos direta Olá Olá dispositivo suporta:</span><span class="sxs-lookup"><span data-stu-id="e6688-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. <span data-ttu-id="e6688-123">Adicionar Olá seguir Olá toohandle de função **reiniciar** direcionar a chamada de método:</span><span class="sxs-lookup"><span data-stu-id="e6688-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="e6688-124">Adicionar Olá seguir Olá toohandle de função **InitiateFirmwareUpdate** direcionar a chamada de método.</span><span class="sxs-lookup"><span data-stu-id="e6688-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="e6688-125">Este método direto utiliza uma parâmetro toospecify Olá localização toodownload de imagem de firmware Olá e inicia Olá atualização de firmware no dispositivo Olá de forma assíncrona:</span><span class="sxs-lookup"><span data-stu-id="e6688-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. <span data-ttu-id="e6688-126">Adicione Olá seguinte código toocreate uma instância de cliente:</span><span class="sxs-lookup"><span data-stu-id="e6688-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="e6688-127">Adicione Olá código para os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e6688-127">Add hello following code to:</span></span>

    * <span data-ttu-id="e6688-128">Abrir a ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="e6688-128">Open hello connection.</span></span>
    * <span data-ttu-id="e6688-129">Enviar Olá **DeviceInfo** objeto.</span><span class="sxs-lookup"><span data-stu-id="e6688-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="e6688-130">Configure um processador para propriedades pretendidos.</span><span class="sxs-lookup"><span data-stu-id="e6688-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="e6688-131">Envie comunicadas propriedades.</span><span class="sxs-lookup"><span data-stu-id="e6688-131">Send reported properties.</span></span>
    * <span data-ttu-id="e6688-132">Registe processadores para métodos direta Olá.</span><span class="sxs-lookup"><span data-stu-id="e6688-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="e6688-133">Começar a enviar telemetria.</span><span class="sxs-lookup"><span data-stu-id="e6688-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="e6688-134">Guardar Olá alterações toohello **remote_monitoring.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e6688-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="e6688-135">Execute Olá seguinte comando, uma aplicação de exemplo de Olá de toolaunch de linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="e6688-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
