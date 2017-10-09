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
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="3808f-104">Começar a utilizar dispositivos duplos (.NET/nó)</span><span class="sxs-lookup"><span data-stu-id="3808f-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="3808f-105">No final de Olá deste tutorial, terá uma .NET e uma aplicação de consola do Node.js:</span><span class="sxs-lookup"><span data-stu-id="3808f-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="3808f-106">**AddTagsAndQuery.sln**, uma aplicação de back-end .NET, a qual adiciona as etiquetas e a consulta dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="3808f-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="3808f-107">**TwinSimulatedDevice.js**, uma aplicação Node.js que simula um dispositivo que estabelece ligação tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e reporta a condição de conectividade.</span><span class="sxs-lookup"><span data-stu-id="3808f-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="3808f-108">artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild aplicações de dispositivo e o back-end.</span><span class="sxs-lookup"><span data-stu-id="3808f-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="3808f-109">toocomplete neste tutorial, precisar Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="3808f-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="3808f-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3808f-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3808f-111">Versão 0.10.x ou posterior do Node.js.</span><span class="sxs-lookup"><span data-stu-id="3808f-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="3808f-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3808f-112">An active Azure account.</span></span> <span data-ttu-id="3808f-113">(Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="3808f-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="3808f-114">Criar Olá do app service</span><span class="sxs-lookup"><span data-stu-id="3808f-114">Create hello service app</span></span>
<span data-ttu-id="3808f-115">Nesta secção, vai criar uma aplicação de consola do .NET (utilizando c#) adiciona localização metadados toohello dispositivo duplo associado **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3808f-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="3808f-116">Em seguida, consultas dispositivos duplos da Olá armazenados no Olá do IoT hub selecionar dispositivos de Olá localizados no Olá-nos e, em seguida, Olá aqueles que comunicou uma ligação de rede móvel.</span><span class="sxs-lookup"><span data-stu-id="3808f-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="3808f-117">No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="3808f-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="3808f-118">Projeto de Olá nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="3808f-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][img-createapp]
1. <span data-ttu-id="3808f-120">No Explorador de soluções, faça duplo clique Olá **AddTagsAndQuery** projeto e, em seguida, clique em **gerir pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="3808f-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3808f-121">No Olá **Gestor de pacotes NuGet** janela, selecione **procurar** e procure **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="3808f-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="3808f-122">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** do pacote e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="3808f-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="3808f-123">Este procedimento transfere, instala e adiciona uma referência toohello [SDK do serviço do Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="3808f-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela Gestor de Pacote NuGet][img-servicenuget]
1. <span data-ttu-id="3808f-125">Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="3808f-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="3808f-126">Adicionar Olá seguintes campos toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="3808f-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="3808f-127">Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub hub Olá que criou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="3808f-128">Adicionar Olá seguinte método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="3808f-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="3808f-129">Olá **RegistryManager** classe expõe todos os Olá métodos necessários toointeract com dispositivos duplos do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="3808f-130">código anterior Olá primeiro inicializa Olá **registryManager** objeto, em seguida, obtém Olá dispositivo duplo para **myDeviceId**e, finalmente, atualiza respetivas etiquetas com informações de localização de Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="3808f-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="3808f-131">Depois de atualizar, ser executada duas consultas: Olá primeiro seleciona apenas Olá dispositivos duplos de dispositivos localizados no Olá **Redmond43** maquinaria e Olá segundo refines Olá consulta tooselect apenas Olá para dispositivos que também estão ligados através do rede celular.</span><span class="sxs-lookup"><span data-stu-id="3808f-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="3808f-132">Tenha em atenção que código anterior Olá, quando cria Olá **consulta** objeto, especifica um número máximo de documentos devolvidos.</span><span class="sxs-lookup"><span data-stu-id="3808f-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="3808f-133">Olá **consulta** objeto contém uma **HasMoreResults** booleana propriedade que pode utilizar tooinvoke Olá **GetNextAsTwinAsync** métodos várias vezes tooretrieve todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="3808f-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="3808f-134">Um método chamado **GetNextAsJson** está disponível para os resultados que são não dispositivos duplos, por exemplo, os resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="3808f-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="3808f-135">Por fim, adicione Olá seguintes linhas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="3808f-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="3808f-136">No Explorador de soluções Olá, abra Olá **definir projetos de arranque...**  e certifique-se de que Olá **ação** para **AddTagsAndQuery** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="3808f-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="3808f-137">Compilar a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-137">Build hello solution.</span></span>
1. <span data-ttu-id="3808f-138">Executar esta aplicação ao clicar no Olá **AddTagsAndQuery** projeto e selecionar **depurar**, seguido **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="3808f-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="3808f-139">Deverá ver um dispositivo nos resultados de Olá para Olá solicitando a consulta para todos os dispositivos localizados no **Redmond43** e nenhum para consulta Olá que restringe Olá resulta toodevices que utilize uma rede celular.</span><span class="sxs-lookup"><span data-stu-id="3808f-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Na janela de resultados da consulta][img-addtagapp]

<span data-ttu-id="3808f-141">Na secção seguinte, Olá, vai criar uma aplicação de dispositivo que comunica a informação da conectividade Olá e alterações Olá resultado da consulta de Olá na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="3808f-142">Criar aplicação de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="3808f-142">Create hello device app</span></span>
<span data-ttu-id="3808f-143">Nesta secção, pode cria uma aplicação de consola do Node.js que estabelece ligação tooyour hub como **myDeviceId**e, em seguida, atualiza as respetivas propriedades comunicado toocontain Olá informações que esteja ligada através de uma rede celular.</span><span class="sxs-lookup"><span data-stu-id="3808f-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="3808f-144">Criar uma nova pasta vazia designada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="3808f-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="3808f-145">No Olá **reportconnectivity** pasta, crie um novo ficheiro Package. JSON utilizando o seguinte comando na sua linha de comandos de Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="3808f-146">Aceite todas as predefinições de Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="3808f-147">Na sua linha de comandos Olá **reportconnectivity** pasta, execute Olá Olá tooinstall de comando a seguir **azure-iot-device**, e **azure-iot-dispositivo-mqtt** pacote :</span><span class="sxs-lookup"><span data-stu-id="3808f-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="3808f-148">Com um editor de texto, crie um novo **ReportConnectivity.js** ficheiro Olá **reportconnectivity** pasta.</span><span class="sxs-lookup"><span data-stu-id="3808f-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="3808f-149">Adicionar Olá seguinte código toohello **ReportConnectivity.js** de ficheiros e substitua o marcador de posição de Olá para a cadeia de ligação do dispositivo com Olá um copiou quando criou Olá **myDeviceId** dispositivo identidade:</span><span class="sxs-lookup"><span data-stu-id="3808f-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="3808f-150">Olá **cliente** objeto expõe todos os métodos de Olá requerem toointeract com dispositivos duplos do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="3808f-151">Olá código anterior, depois, inicializa Olá **cliente** objeto obtém Olá dispositivo duplo para **myDeviceId** e atualiza a respetiva propriedade comunicada com informações de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="3808f-152">Executar a aplicação de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="3808f-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="3808f-153">Deverá ver a mensagem de saudação `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="3808f-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="3808f-154">Agora que hello dispositivo reportado as respetivas informações de conectividade, deverão ser apresentados em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="3808f-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="3808f-155">Executar Olá .NET **AddTagsAndQuery** Olá toorun de aplicação consulta novamente.</span><span class="sxs-lookup"><span data-stu-id="3808f-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="3808f-156">Neste momento **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="3808f-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="3808f-157">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3808f-157">Next steps</span></span>
<span data-ttu-id="3808f-158">Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="3808f-159">Adicionar metadados do dispositivo como etiquetas a partir de uma aplicação de back-end e escreveu a informação da conectividade um dispositivo simulado aplicação tooreport dispositivo no dispositivo duplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3808f-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="3808f-160">Também aprendeu como tooquery estas informações utilizando a linguagem de consulta Olá como o SQL Server IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3808f-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="3808f-161">Olá utilize, como os seguintes recursos toolearn para:</span><span class="sxs-lookup"><span data-stu-id="3808f-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="3808f-162">Enviar telemetria a partir de dispositivos com Olá [introdução ao IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="3808f-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="3808f-163">configurar dispositivos com propriedades pretendida do dispositivo duplo Olá [assim o desejar utilizar dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="3808f-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="3808f-164">controlar dispositivos interativamente (como ativar uma ventoinha a partir de uma aplicação controlados pelo utilizador) com Olá [utilizar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3808f-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

