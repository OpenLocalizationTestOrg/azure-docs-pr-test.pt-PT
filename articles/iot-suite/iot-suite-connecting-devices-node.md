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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Ligar o seu toohello de dispositivo (Node.js) de solução pré-configurada de monitorização remota
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Criar uma solução de exemplo de node.js

Certifique-se de que a versão Node.js 0.11.5 ou posterior está instalado no computador de desenvolvimento. Pode executar `node --version` na versão de Olá toocheck do Olá linha de comandos.

1. Crie uma pasta denominada **RemoteMonitoring** no computador de desenvolvimento. Navegue toothis pasta no seu ambiente de linha de comandos.

1. Olá execute os seguintes comandos toodownload e instalar pacotes de Olá precisa de aplicação de exemplo de Olá toocomplete:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. No Olá **RemoteMonitoring** pasta, crie um ficheiro chamado **remote_monitoring.js**. Abra este ficheiro num editor de texto.

1. No Olá **remote_monitoring.js** ficheiro, adicione o seguinte Olá `require` instruções:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Adicionar Olá seguintes declarações de variável após Olá `require` instruções. Substitua os valores do marcador de posição de Olá [Id de dispositivo] e [chave do dispositivo] com valores que apontou para o seu dispositivo no dashboard de solução de monitorização remota de Olá. Utilize Olá o nome de anfitrião do IoT Hub do tooreplace de dashboard de solução Olá [IoTHub nome]. Por exemplo, se o Nome de anfitrião do seu Hub IoT for **contoso.azure devices.net**, substitua [IoTHub Name] por **contoso**:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Adicione Olá seguintes variáveis toodefine alguns dados de telemetria base:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Adicione Olá os resultados da operação do programa auxiliar função tooprint os seguintes:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Adicione Olá valores de telemetria do programa auxiliar função toouse toorandomize Olá os seguintes:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Adicionar Olá seguinte definição para Olá **DeviceInfo** dispositivo do objeto Olá envia no arranque:

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

1. Adicione Olá seguinte definição para o dispositivo duplo de Olá comunicadas valores. Esta definição inclui descrições dos métodos direta Olá Olá dispositivo suporta:

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

1. Adicionar Olá seguir Olá toohandle de função **reiniciar** direcionar a chamada de método:

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

1. Adicionar Olá seguir Olá toohandle de função **InitiateFirmwareUpdate** direcionar a chamada de método. Este método direto utiliza uma parâmetro toospecify Olá localização toodownload de imagem de firmware Olá e inicia Olá atualização de firmware no dispositivo Olá de forma assíncrona:

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

1. Adicione Olá seguinte código toocreate uma instância de cliente:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Adicione Olá código para os seguintes:

    * Abrir a ligação de Olá.
    * Enviar Olá **DeviceInfo** objeto.
    * Configure um processador para propriedades pretendidos.
    * Envie comunicadas propriedades.
    * Registe processadores para métodos direta Olá.
    * Começar a enviar telemetria.

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

1. Guardar Olá alterações toohello **remote_monitoring.js** ficheiro.

1. Execute Olá seguinte comando, uma aplicação de exemplo de Olá de toolaunch de linha de comandos:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
