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
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="287ab-104">Utilização pretendida propriedades tooconfigure dispositivos (nó)</span><span class="sxs-lookup"><span data-stu-id="287ab-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="287ab-105">No final de Olá deste tutorial, terá de duas aplicações de consola do Node.js:</span><span class="sxs-lookup"><span data-stu-id="287ab-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="287ab-106">**SimulateDeviceConfiguration.js**, uma aplicação de dispositivo simulado que aguarda uma atualização da configuração pretendida e relatórios de estado de Olá de um processo de atualização da configuração simulada.</span><span class="sxs-lookup"><span data-stu-id="287ab-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="287ab-107">**SetDesiredConfigurationAndQuery.js**, uma aplicação de back-end Node.js, que define Olá desired configuration num dispositivo e consultas Olá o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="287ab-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="287ab-108">artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild aplicações de dispositivo e o back-end.</span><span class="sxs-lookup"><span data-stu-id="287ab-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="287ab-109">toocomplete neste tutorial, precisar Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="287ab-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="287ab-110">Versão 0.10.x ou posterior do Node.js.</span><span class="sxs-lookup"><span data-stu-id="287ab-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="287ab-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="287ab-111">An active Azure account.</span></span> <span data-ttu-id="287ab-112">(Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="287ab-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="287ab-113">Se seguiu Olá [começar a utilizar dispositivos duplos] [ lnk-twin-tutorial] tutorial, já tiver um IoT hub e uma identidade de dispositivo chamado **myDeviceId**; e pode ignorar toohello [ Criar aplicação de dispositivo simulada Olá] [ lnk-how-to-configure-createapp] secção.</span><span class="sxs-lookup"><span data-stu-id="287ab-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="287ab-114">Criar aplicação de dispositivo simulada Olá</span><span class="sxs-lookup"><span data-stu-id="287ab-114">Create hello simulated device app</span></span>
<span data-ttu-id="287ab-115">Nesta secção, pode cria uma aplicação de consola do Node.js que estabelece ligação tooyour hub como **myDeviceId**, tem de aguardar durante uma atualização da configuração pretendida e, em seguida, os relatórios de atualizações no processo de atualização de configuração de Olá simulado.</span><span class="sxs-lookup"><span data-stu-id="287ab-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="287ab-116">Criar uma nova pasta vazia designada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="287ab-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="287ab-117">No Olá **simulatedeviceconfiguration** pasta, crie um novo ficheiro Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="287ab-118">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="287ab-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="287ab-119">Na sua linha de comandos Olá **simulatedeviceconfiguration** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device**, e **azure-iot-dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="287ab-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="287ab-120">Com um editor de texto, crie um novo **SimulateDeviceConfiguration.js** ficheiro Olá **simulatedeviceconfiguration** pasta.</span><span class="sxs-lookup"><span data-stu-id="287ab-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="287ab-121">Adicionar Olá seguinte código toohello **SimulateDeviceConfiguration.js** de ficheiros e substitua Olá **{cadeia de ligação do dispositivo}** marcador de posição pela cadeia de ligação do dispositivo Olá que copiou quando a criado Olá **myDeviceId** identidade de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="287ab-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="287ab-122">Olá **cliente** objeto expõe todos os Olá métodos necessários toointeract com dispositivos duplos do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="287ab-123">Olá código anterior, depois, inicializa Olá **cliente** objeto obtém Olá dispositivo duplo para **myDeviceId**e anexa um processador de atualização Olá nas propriedades pretendidas.</span><span class="sxs-lookup"><span data-stu-id="287ab-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="287ab-124">processador Olá verifica que existe é um pedido de alteração da configuração real comparando configIds Olá, em seguida, invoca um método que inicia a alteração da configuração Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="287ab-125">Tenha em atenção que, para sake Olá de simplicidade, código anterior Olá utiliza uma predefinição hard-coded para a configuração inicial do Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="287ab-126">Uma aplicação real, provavelmente, seria carregar que a configuração de um local de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="287ab-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="287ab-127">Eventos de alteração de propriedade pretendido sempre são emitidos uma vez na ligação do dispositivo, certifique-se toocheck se houver uma alteração real no Olá pretendido propriedades antes de efetuar qualquer ação.</span><span class="sxs-lookup"><span data-stu-id="287ab-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="287ab-128">Adicionar Olá seguintes métodos antes de Olá `client.open()` invocação:</span><span class="sxs-lookup"><span data-stu-id="287ab-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="287ab-129">Olá **initConfigChange** método atualizações reportados propriedades no objecto de duplo de dispositivo local Olá com pedido de actualização de configuração de Olá e conjuntos Olá estado demasiado**pendente**, em seguida, as atualizações Olá dispositivo duplo no serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="287ab-130">Depois de atualizar com êxito o dispositivo duplo de Olá, simula um processo de execução longa que termina em execução Olá **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="287ab-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="287ab-131">Este método atualizações Olá local dispositivo duplo do comunicadas propriedades a definir o estado de Olá demasiado**êxito** e remover Olá **pendingConfig** objeto.</span><span class="sxs-lookup"><span data-stu-id="287ab-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="287ab-132">Em seguida, atualiza duplo de dispositivo Olá no serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="287ab-133">Tenha em atenção que, a largura de banda toosave, comunicados propriedades são atualizadas ao especificar apenas o Olá propriedades toobe modificado (com o nome **patch** no Olá acima código), em vez de substituir Olá documento de todo.</span><span class="sxs-lookup"><span data-stu-id="287ab-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="287ab-134">Este tutorial não simular nenhum comportamento de atualizações de configuração em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="287ab-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="287ab-135">Alguns processos de atualização de configuração podem ser tooaccommodate capaz de alterações de configuração de destino durante a execução de atualização de Olá, outros utilizadores poderão ter tooqueue e outros foi rejeitá-las com uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="287ab-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="287ab-136">Certifique-se de que tooconsider Olá comportamento pretendido para o processo de configuração específica e adicione lógica adequado Olá antes de iniciar a alteração da configuração Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="287ab-137">Execute a aplicação de dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="287ab-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="287ab-138">Deverá ver a mensagem de saudação `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="287ab-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="287ab-139">Manter a aplicação Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="287ab-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="287ab-140">Criar Olá do app service</span><span class="sxs-lookup"><span data-stu-id="287ab-140">Create hello service app</span></span>
<span data-ttu-id="287ab-141">Nesta secção, irá criar uma aplicação de consola do Node.js que Olá atualizações *pretendido propriedades* no Olá dispositivo duplo associado **myDeviceId** com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="287ab-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="287ab-142">Em seguida, consulta Olá dispositivos duplos armazenados no hub IoT de Olá e mostra a diferença de Olá entre Olá pretendida e reportado configurações de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="287ab-143">Criar uma nova pasta vazia designada **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="287ab-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="287ab-144">No Olá **setdesiredandqueryapp** pasta, crie um novo ficheiro Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="287ab-145">Aceite todas as predefinições de Olá:</span><span class="sxs-lookup"><span data-stu-id="287ab-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="287ab-146">Na sua linha de comandos Olá **setdesiredandqueryapp** pasta, execute Olá Olá tooinstall de comando a seguir **azure iothub** pacote:</span><span class="sxs-lookup"><span data-stu-id="287ab-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="287ab-147">Com um editor de texto, crie um novo **SetDesiredAndQuery.js** ficheiro Olá **addtagsandqueryapp** pasta.</span><span class="sxs-lookup"><span data-stu-id="287ab-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="287ab-148">Adicionar Olá seguinte código toohello **SetDesiredAndQuery.js** de ficheiros e substitua Olá **{cadeia de ligação do hub iot}** marcador de posição pela cadeia de ligação do IoT Hub que copiou quando criou o seu hub de Olá :</span><span class="sxs-lookup"><span data-stu-id="287ab-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="287ab-149">Olá **registo** objeto expõe todos os Olá métodos necessários toointeract com dispositivos duplos do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="287ab-150">Olá código anterior, depois, inicializa Olá **registo** objeto obtém Olá dispositivo duplo para **myDeviceId**e atualiza as respetivas propriedades pretendidas com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="287ab-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="287ab-151">Depois disso, aquele invoca Olá **queryTwins** funcionar eventos 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="287ab-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="287ab-152">Esta aplicação consulta IoT Hub a cada 10 segundos para fins de ilustrativa.</span><span class="sxs-lookup"><span data-stu-id="287ab-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="287ab-153">Utilizar consulta toogenerate destinada ao utilizador relatórios em vários dispositivos e não toodetect alterações.</span><span class="sxs-lookup"><span data-stu-id="287ab-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="287ab-154">Se a sua solução requer notificações em tempo real de eventos do dispositivo, utilize [duplo notificações][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="287ab-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="287ab-155">.</span><span class="sxs-lookup"><span data-stu-id="287ab-155">.</span></span>

1. <span data-ttu-id="287ab-156">Adicionar Olá seguir o direito de código antes Olá `registry.getDeviceTwin()` Olá tooimplement de invocação **queryTwins** função:</span><span class="sxs-lookup"><span data-stu-id="287ab-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
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
   
    <span data-ttu-id="287ab-157">consultas de código anterior Olá Olá dispositivos duplos armazenados no hub IoT de Olá e impressões Olá pretendida e reportado configurações de telemetria.</span><span class="sxs-lookup"><span data-stu-id="287ab-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="287ab-158">Consulte toohello [idioma de consulta do IoT Hub] [ lnk-query] toolearn como toogenerate avançada relatórios em todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="287ab-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="287ab-159">Com **SimulateDeviceConfiguration.js** em execução, execute a aplicação de Olá com:</span><span class="sxs-lookup"><span data-stu-id="287ab-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="287ab-160">Deverá ver configuração comunicado Olá alterar **êxito** demasiado**pendente** demasiado**êxito** novamente com o Active Directory de nova Olá enviar uma frequência de cinco minutos em vez de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="287ab-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="287ab-161">Não há um atraso de cópia de segurança tooa minuto entre a operação de relatório de dispositivo Olá e o resultado da consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="287ab-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="287ab-162">Este é tooenable Olá consulta infraestrutura toowork em grande escala.</span><span class="sxs-lookup"><span data-stu-id="287ab-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="287ab-163">tooretrieve vistas consistente de um único dispositivo duplo utilizam Olá **getDeviceTwin** método Olá **registo** classe.</span><span class="sxs-lookup"><span data-stu-id="287ab-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="287ab-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="287ab-164">Next steps</span></span>
<span data-ttu-id="287ab-165">Neste tutorial, configurou uma configuração desejada como *pretendido propriedades* a partir de uma aplicação de back-end e escrito um toodetect de aplicação do dispositivo simulado que alterar e simular um processo de atualização de vários passos reporting o estado dele como  *comunicado propriedades* toohello dispositivo duplo.</span><span class="sxs-lookup"><span data-stu-id="287ab-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="287ab-166">Olá utilize, como os seguintes recursos toolearn para:</span><span class="sxs-lookup"><span data-stu-id="287ab-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="287ab-167">Enviar telemetria a partir de dispositivos com Olá [introdução ao IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="287ab-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="287ab-168">agendar ou efetuar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e as tarefas de difusão] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="287ab-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="287ab-169">controlar dispositivos interativamente (como ativar uma ventoinha a partir de uma aplicação controlados pelo utilizador), com Olá [utilizar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="287ab-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
