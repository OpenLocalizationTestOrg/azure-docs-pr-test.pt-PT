---
title: "Propriedades do aaaUse IoT Hub do Azure dispositivo duplo (nó) | Microsoft Docs"
description: "Como toouse IoT Hub do Azure dispositivos duplos tooconfigure dispositivos. Utilize Olá SDKs de IoT do Azure para Node.js tooimplement uma aplicação de dispositivo simulada e uma aplicação de serviço que modifica uma configuração de dispositivo utilizando um dispositivo duplo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Utilização pretendida propriedades tooconfigure dispositivos (nó)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

No final de Olá deste tutorial, terá de duas aplicações de consola do Node.js:

* **SimulateDeviceConfiguration.js**, uma aplicação de dispositivo simulado que aguarda uma atualização da configuração pretendida e relatórios de estado de Olá de um processo de atualização da configuração simulada.
* **SetDesiredConfigurationAndQuery.js**, uma aplicação de back-end Node.js, que define Olá desired configuration num dispositivo e consultas Olá o processo de atualização de configuração.

> [!NOTE]
> artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild aplicações de dispositivo e o back-end.
> 
> 

toocomplete neste tutorial, precisar Olá seguinte:

* Versão 0.10.x ou posterior do Node.js.
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

Se seguiu Olá [começar a utilizar dispositivos duplos] [ lnk-twin-tutorial] tutorial, já tiver um IoT hub e uma identidade de dispositivo chamado **myDeviceId**; e pode ignorar toohello [ Criar aplicação de dispositivo simulada Olá] [ lnk-how-to-configure-createapp] secção.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Criar aplicação de dispositivo simulada Olá
Nesta secção, pode cria uma aplicação de consola do Node.js que estabelece ligação tooyour hub como **myDeviceId**, tem de aguardar durante uma atualização da configuração pretendida e, em seguida, os relatórios de atualizações no processo de atualização de configuração de Olá simulado.

1. Criar uma nova pasta vazia designada **simulatedeviceconfiguration**. No Olá **simulatedeviceconfiguration** pasta, crie um novo ficheiro Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá. Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```
2. Na sua linha de comandos Olá **simulatedeviceconfiguration** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device**, e **azure-iot-dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Com um editor de texto, crie um novo **SimulateDeviceConfiguration.js** ficheiro Olá **simulatedeviceconfiguration** pasta.
4. Adicionar Olá seguinte código toohello **SimulateDeviceConfiguration.js** de ficheiros e substitua Olá **{cadeia de ligação do dispositivo}** marcador de posição pela cadeia de ligação do dispositivo Olá que copiou quando a criado Olá **myDeviceId** identidade de dispositivo:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Olá **cliente** objeto expõe todos os Olá métodos necessários toointeract com dispositivos duplos do dispositivo Olá. Olá código anterior, depois, inicializa Olá **cliente** objeto obtém Olá dispositivo duplo para **myDeviceId**e anexa um processador de atualização Olá nas propriedades pretendidas. processador Olá verifica que existe é um pedido de alteração da configuração real comparando configIds Olá, em seguida, invoca um método que inicia a alteração da configuração Olá.
   
    Tenha em atenção que, para sake Olá de simplicidade, código anterior Olá utiliza uma predefinição hard-coded para a configuração inicial do Olá. Uma aplicação real, provavelmente, seria carregar que a configuração de um local de armazenamento.
   
   > [!IMPORTANT]
   > Eventos de alteração de propriedade pretendido sempre são emitidos uma vez na ligação do dispositivo, certifique-se toocheck se houver uma alteração real no Olá pretendido propriedades antes de efetuar qualquer ação.
   > 
   > 
5. Adicionar Olá seguintes métodos antes de Olá `client.open()` invocação:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Olá **initConfigChange** método atualizações reportados propriedades no objecto de duplo de dispositivo local Olá com pedido de actualização de configuração de Olá e conjuntos Olá estado demasiado**pendente**, em seguida, as atualizações Olá dispositivo duplo no serviço de Olá. Depois de atualizar com êxito o dispositivo duplo de Olá, simula um processo de execução longa que termina em execução Olá **completeConfigChange**. Este método atualizações Olá local dispositivo duplo do comunicadas propriedades a definir o estado de Olá demasiado**êxito** e remover Olá **pendingConfig** objeto. Em seguida, atualiza duplo de dispositivo Olá no serviço de Olá.
   
    Tenha em atenção que, a largura de banda toosave, comunicados propriedades são atualizadas ao especificar apenas o Olá propriedades toobe modificado (com o nome **patch** no Olá acima código), em vez de substituir Olá documento de todo.
   
   > [!NOTE]
   > Este tutorial não simular nenhum comportamento de atualizações de configuração em simultâneo. Alguns processos de atualização de configuração podem ser tooaccommodate capaz de alterações de configuração de destino durante a execução de atualização de Olá, outros utilizadores poderão ter tooqueue e outros foi rejeitá-las com uma condição de erro. Certifique-se de que tooconsider Olá comportamento pretendido para o processo de configuração específica e adicione lógica adequado Olá antes de iniciar a alteração da configuração Olá.
   > 
   > 
6. Execute a aplicação de dispositivo Olá:
   
        node SimulateDeviceConfiguration.js
   
    Deverá ver a mensagem de saudação `retrieved device twin`. Manter a aplicação Olá em execução.

## <a name="create-hello-service-app"></a>Criar Olá do app service
Nesta secção, irá criar uma aplicação de consola do Node.js que Olá atualizações *pretendido propriedades* no Olá dispositivo duplo associado **myDeviceId** com um novo objeto de configuração de telemetria. Em seguida, consulta Olá dispositivos duplos armazenados no hub IoT de Olá e mostra a diferença de Olá entre Olá pretendida e reportado configurações de dispositivo Olá.

1. Criar uma nova pasta vazia designada **setdesiredandqueryapp**. No Olá **setdesiredandqueryapp** pasta, crie um novo ficheiro Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá. Aceite todas as predefinições de Olá:
   
    ```
    npm init
    ```
2. Na sua linha de comandos Olá **setdesiredandqueryapp** pasta, execute Olá Olá tooinstall de comando a seguir **azure iothub** pacote:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Com um editor de texto, crie um novo **SetDesiredAndQuery.js** ficheiro Olá **addtagsandqueryapp** pasta.
4. Adicionar Olá seguinte código toohello **SetDesiredAndQuery.js** de ficheiros e substitua Olá **{cadeia de ligação do hub iot}** marcador de posição pela cadeia de ligação do IoT Hub que copiou quando criou o seu hub de Olá :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Olá **registo** objeto expõe todos os Olá métodos necessários toointeract com dispositivos duplos do serviço de Olá. Olá código anterior, depois, inicializa Olá **registo** objeto obtém Olá dispositivo duplo para **myDeviceId**e atualiza as respetivas propriedades pretendidas com um novo objeto de configuração de telemetria. Depois disso, aquele invoca Olá **queryTwins** funcionar eventos 10 segundos.

    > [!IMPORTANT]
    > Esta aplicação consulta IoT Hub a cada 10 segundos para fins de ilustrativa. Utilizar consulta toogenerate destinada ao utilizador relatórios em vários dispositivos e não toodetect alterações. Se a sua solução requer notificações em tempo real de eventos do dispositivo, utilize [duplo notificações][lnk-twin-notifications].
    > 
    >.

1. Adicionar Olá seguir o direito de código antes Olá `registry.getDeviceTwin()` Olá tooimplement de invocação **queryTwins** função:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    consultas de código anterior Olá Olá dispositivos duplos armazenados no hub IoT de Olá e impressões Olá pretendida e reportado configurações de telemetria. Consulte toohello [idioma de consulta do IoT Hub] [ lnk-query] toolearn como toogenerate avançada relatórios em todos os seus dispositivos.
2. Com **SimulateDeviceConfiguration.js** em execução, execute a aplicação de Olá com:
   
        node SetDesiredAndQuery.js 5m
   
    Deverá ver configuração comunicado Olá alterar **êxito** demasiado**pendente** demasiado**êxito** novamente com o Active Directory de nova Olá enviar uma frequência de cinco minutos em vez de 24 horas.
   
   > [!IMPORTANT]
   > Não há um atraso de cópia de segurança tooa minuto entre a operação de relatório de dispositivo Olá e o resultado da consulta Olá. Este é tooenable Olá consulta infraestrutura toowork em grande escala. tooretrieve vistas consistente de um único dispositivo duplo utilizam Olá **getDeviceTwin** método Olá **registo** classe.
   > 
   > 

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou uma configuração desejada como *pretendido propriedades* a partir de uma aplicação de back-end e escrito um toodetect de aplicação do dispositivo simulado que alterar e simular um processo de atualização de vários passos reporting o estado dele como  *comunicado propriedades* toohello dispositivo duplo.

Olá utilize, como os seguintes recursos toolearn para:

* Enviar telemetria a partir de dispositivos com Olá [introdução ao IoT Hub] [ lnk-iothub-getstarted] tutorial,
* agendar ou efetuar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e as tarefas de difusão] [ lnk-schedule-jobs] tutorial.
* controlar dispositivos interativamente (como ativar uma ventoinha a partir de uma aplicação controlados pelo utilizador), com Olá [utilizar métodos diretos] [ lnk-methods-tutorial] tutorial.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
