---
title: "aaaGet começar a utilizar dispositivos duplos de IoT Hub do Azure (nó/.NET) | Microsoft Docs"
description: "Como toouse IoT Hub do Azure dispositivos duplos tooadd etiquetas e, em seguida, utilize uma consulta do IoT Hub. Utilizar dispositivos de IoT do Azure Olá SDK para Node.js tooimplement Olá aplicação de dispositivo simulada e Olá o serviço de IoT do Azure SDK para .NET tooimplement uma aplicação de serviço que adiciona as etiquetas de Olá e executa Olá consulta do IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a>Começar a utilizar dispositivos duplos (.NET/nó)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

No final de Olá deste tutorial, terá uma .NET e uma aplicação de consola do Node.js:

* **AddTagsAndQuery.sln**, uma aplicação de back-end .NET, a qual adiciona as etiquetas e a consulta dispositivos duplos.
* **TwinSimulatedDevice.js**, uma aplicação Node.js que simula um dispositivo que estabelece ligação tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e reporta a condição de conectividade.

> [!NOTE]
> artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild aplicações de dispositivo e o back-end.
> 
> 

toocomplete neste tutorial, precisar Olá seguinte:

* Visual Studio 2015 ou Visual Studio 2017.
* Versão 0.10.x ou posterior do Node.js.
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Criar Olá do app service
Nesta secção, vai criar uma aplicação de consola do .NET (utilizando c#) adiciona localização metadados toohello dispositivo duplo associado **myDeviceId**. Em seguida, consultas dispositivos duplos da Olá armazenados no Olá do IoT hub selecionar dispositivos de Olá localizados no Olá-nos e, em seguida, Olá aqueles que comunicou uma ligação de rede móvel.

1. No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola** modelo de projeto. Projeto de Olá nome **AddTagsAndQuery**.
   
    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][img-createapp]
1. No Explorador de soluções, faça duplo clique Olá **AddTagsAndQuery** projeto e, em seguida, clique em **gerir pacotes NuGet...** .
1. No Olá **Gestor de pacotes NuGet** janela, selecione **procurar** e procure **microsoft.azure.devices**. Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** do pacote e aceite os termos de Olá de utilização. Este procedimento transfere, instala e adiciona uma referência toohello [SDK do serviço do Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e as respetivas dependências.
   
    ![Janela Gestor de Pacote NuGet][img-servicenuget]
1. Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:
   
        using Microsoft.Azure.Devices;
1. Adicionar Olá seguintes campos toohello **programa** classe. Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub hub Olá que criou na secção anterior Olá.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Adicionar Olá seguinte método toohello **programa** classe:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Olá **RegistryManager** classe expõe todos os Olá métodos necessários toointeract com dispositivos duplos do serviço de Olá. código anterior Olá primeiro inicializa Olá **registryManager** objeto, em seguida, obtém Olá dispositivo duplo para **myDeviceId**e, finalmente, atualiza respetivas etiquetas com informações de localização de Olá assim o desejar.
   
    Depois de atualizar, ser executada duas consultas: Olá primeiro seleciona apenas Olá dispositivos duplos de dispositivos localizados no Olá **Redmond43** maquinaria e Olá segundo refines Olá consulta tooselect apenas Olá para dispositivos que também estão ligados através do rede celular.
   
    Tenha em atenção que código anterior Olá, quando cria Olá **consulta** objeto, especifica um número máximo de documentos devolvidos. Olá **consulta** objeto contém uma **HasMoreResults** booleana propriedade que pode utilizar tooinvoke Olá **GetNextAsTwinAsync** métodos várias vezes tooretrieve todos os resultados. Um método chamado **GetNextAsJson** está disponível para os resultados que são não dispositivos duplos, por exemplo, os resultados de consultas de agregação.
1. Por fim, adicione Olá seguintes linhas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. No Explorador de soluções Olá, abra Olá **definir projetos de arranque...**  e certifique-se de que Olá **ação** para **AddTagsAndQuery** projeto é **iniciar**. Compilar a solução de Olá.
1. Executar esta aplicação ao clicar no Olá **AddTagsAndQuery** projeto e selecionar **depurar**, seguido **iniciar nova instância**. Deverá ver um dispositivo nos resultados de Olá para Olá solicitando a consulta para todos os dispositivos localizados no **Redmond43** e nenhum para consulta Olá que restringe Olá resulta toodevices que utilize uma rede celular.
   
    ![Na janela de resultados da consulta][img-addtagapp]

Na secção seguinte, Olá, vai criar uma aplicação de dispositivo que comunica a informação da conectividade Olá e alterações Olá resultado da consulta de Olá na secção anterior Olá.

## <a name="create-hello-device-app"></a>Criar aplicação de dispositivo Olá
Nesta secção, pode cria uma aplicação de consola do Node.js que estabelece ligação tooyour hub como **myDeviceId**e, em seguida, atualiza as respetivas propriedades comunicado toocontain Olá informações que esteja ligada através de uma rede celular.

1. Criar uma nova pasta vazia designada **reportconnectivity**. No Olá **reportconnectivity** pasta, crie um novo ficheiro Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá. Aceite todas as predefinições de Olá.
   
    ```
    npm init
    ```
1. Na sua linha de comandos Olá **reportconnectivity** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device**, e **azure-iot-dispositivo-mqtt** pacote :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Com um editor de texto, crie um novo **ReportConnectivity.js** ficheiro Olá **reportconnectivity** pasta.
1. Adicionar Olá seguinte código toohello **ReportConnectivity.js** de ficheiros e substitua o marcador de posição de Olá para a cadeia de ligação do dispositivo com Olá um copiou quando criou Olá **myDeviceId** dispositivo identidade:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Olá **cliente** objeto expõe todos os métodos de Olá requerem toointeract com dispositivos duplos do dispositivo Olá. Olá código anterior, depois, inicializa Olá **cliente** objeto obtém Olá dispositivo duplo para **myDeviceId** e atualiza a respetiva propriedade comunicada com informações de conectividade Olá.
1. Executar a aplicação de dispositivo Olá
   
        node ReportConnectivity.js
   
    Deverá ver a mensagem de saudação `twin state reported`.
1. Agora que hello dispositivo reportado as respetivas informações de conectividade, deverão ser apresentados em ambas as consultas. Executar Olá .NET **AddTagsAndQuery** Olá toorun de aplicação consulta novamente. Neste momento **myDeviceId** deve aparecer em ambos os resultados da consulta.
   
    ![][img-addtagapp2]

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Adicionar metadados do dispositivo como etiquetas a partir de uma aplicação de back-end e escreveu a informação da conectividade um dispositivo simulado aplicação tooreport dispositivo no dispositivo duplo de Olá. Também aprendeu como tooquery estas informações utilizando a linguagem de consulta Olá como o SQL Server IoT Hub.

Olá utilize, como os seguintes recursos toolearn para:

* Enviar telemetria a partir de dispositivos com Olá [introdução ao IoT Hub] [ lnk-iothub-getstarted] tutorial,
* configurar dispositivos com propriedades pretendida do dispositivo duplo Olá [assim o desejar utilizar dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,
* controlar dispositivos interativamente (como ativar uma ventoinha a partir de uma aplicação controlados pelo utilizador) com Olá [utilizar métodos diretos] [ lnk-methods-tutorial] tutorial.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

