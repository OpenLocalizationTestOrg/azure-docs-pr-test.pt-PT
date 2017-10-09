---
title: aaaGet iniciado com o Azure IoT Hub (.NET) | Microsoft Docs
description: "Saiba como toosend dispositivo para nuvem mensagens tooAzure IoT Hub com os IoT SDKs do .NET. Criar dispositivo simulado e tooregister de aplicações de serviço, o dispositivo, enviar mensagens e ler mensagens a partir do IoT hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="042de-104">Ligar o seu hub IoT do dispositivo tooyour através do .NET</span><span class="sxs-lookup"><span data-stu-id="042de-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="042de-105">No final de Olá deste tutorial, terá três aplicações de consola .NET:</span><span class="sxs-lookup"><span data-stu-id="042de-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="042de-106">**CreateDeviceIdentity**, que cria uma identidade de dispositivo e tooconnect de chave de segurança associadas, a aplicação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="042de-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="042de-107">**ReadDeviceToCloudMessages**, que apresenta a telemetria de Olá enviada pela sua aplicação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="042de-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="042de-108">**SimulatedDevice**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e envia uma mensagem de telemetria a cada segundo através do protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="042de-109">Pode transferir ou clonar a solução do Visual Studio Olá, que contém Olá três aplicações a partir do Github.</span><span class="sxs-lookup"><span data-stu-id="042de-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="042de-110">Para obter informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun de aplicações em dispositivos e a sua solução de back-end, consulte o artigo [SDKs IoT do Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="042de-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="042de-111">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="042de-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="042de-112">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="042de-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="042de-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="042de-113">An active Azure account.</span></span> <span data-ttu-id="042de-114">(Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="042de-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="042de-115">Acabou de criar o hub IoT e tem o nome de anfitrião de Olá e a cadeia de ligação do IoT Hub que precisa de rest de Olá toocomplete deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="042de-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="042de-116">Receber mensagens dispositivo-nuvem</span><span class="sxs-lookup"><span data-stu-id="042de-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="042de-117">Nesta secção, irá criar uma aplicação de consola do .NET que lê mensagens do dispositivo para a cloud a partir do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042de-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="042de-118">Um IoT hub expõe um [Event Hubs do Azure][lnk-event-hubs-overview]-tooenable de ponto final compatível com que as mensagens do dispositivo para a nuvem de tooread.</span><span class="sxs-lookup"><span data-stu-id="042de-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="042de-119">ações de tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implementação com débito elevado.</span><span class="sxs-lookup"><span data-stu-id="042de-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="042de-120">toolearn como mensagens de tooprocess dispositivo para a nuvem à escala, consulte Olá [processar mensagens do dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="042de-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="042de-121">Para obter mais informações sobre como tooprocess mensagens de Event Hubs, consulte Olá [introdução ao Event Hubs] [ lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="042de-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="042de-122">(Este tutorial é pontos finais de toohello aplicável compatível com o evento de Hub IoT Hub.)</span><span class="sxs-lookup"><span data-stu-id="042de-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="042de-123">Olá o ponto final compatível com o Event Hub para ler mensagens do dispositivo para nuvem sempre utiliza Olá AMQP protocolo.</span><span class="sxs-lookup"><span data-stu-id="042de-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="042de-124">No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="042de-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="042de-125">Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="042de-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="042de-126">Projeto de Olá nome **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="042de-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][10a]

2. <span data-ttu-id="042de-128">No Explorador de soluções, faça duplo clique Olá **ReadDeviceToCloudMessages** projeto e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="042de-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="042de-129">No Olá **Gestor de pacotes NuGet** janela, procure **Windowsazure**, selecione **instalar**e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="042de-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="042de-130">Este procedimento transfere, instala e adiciona uma referência demasiado[Service Bus do Azure][lnk-servicebus-nuget], com as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="042de-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="042de-131">Este pacote permite Olá tooconnect toohello compatível com o Event Hub ponto final da aplicação no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="042de-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="042de-132">Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="042de-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="042de-133">Adicionar Olá seguintes campos toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="042de-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="042de-134">Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub para o hub de Olá que criou na secção "Criar um IoT hub" de Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="042de-135">Adicionar Olá seguinte método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="042de-135">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="042de-136">Este método utiliza um **EventHubReceiver** partições de receção de mensagens de tooreceive de instância de todos os Olá IoT hub dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="042de-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="042de-137">Repare como transmite um `DateTime.Now` parâmetro ao criar Olá **EventHubReceiver** objeto, para que apenas receber mensagens enviadas depois de iniciar.</span><span class="sxs-lookup"><span data-stu-id="042de-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="042de-138">Este filtro é útil num ambiente de teste para que possa ver o conjunto atual de Olá de mensagens.</span><span class="sxs-lookup"><span data-stu-id="042de-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="042de-139">Num ambiente de produção, o código deve Certifique-se de que processa todas as mensagens de Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="042de-140">Para obter mais informações, consulte o tutorial Olá [como tooprocess mensagens de dispositivo para a nuvem do IoT Hub][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="042de-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="042de-141">Por fim, adicione Olá seguintes linhas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="042de-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="042de-142">Criar uma aplicação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="042de-142">Create a device app</span></span>

<span data-ttu-id="042de-143">Nesta secção, crie uma aplicação de consola .NET que simula um dispositivo que envia o IoT hub tooan mensagens do dispositivo para nuvem.</span><span class="sxs-lookup"><span data-stu-id="042de-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="042de-144">No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="042de-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="042de-145">Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="042de-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="042de-146">Projeto de Olá nome **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="042de-146">Name hello project **SimulatedDevice**.</span></span>

    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][10b]

2. <span data-ttu-id="042de-148">No Explorador de soluções, faça duplo clique Olá **SimulatedDevice** projeto e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="042de-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="042de-149">No Olá **Gestor de pacotes NuGet** janela, selecione **procurar**, procure **Microsoft.Azure.Devices.Client**, selecione **instalar** Olá tooinstall **Microsoft.Azure.Devices.Client** do pacote e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="042de-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="042de-150">Este procedimento transfere, instala e adiciona uma referência toohello [pacote de SDK NuGet do dispositivo IoT do Azure] [ lnk-device-nuget] e as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="042de-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="042de-151">Adicione Olá seguinte `using` declaração, Olá parte superior do Olá **Program.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="042de-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="042de-152">Adicionar Olá seguintes campos toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="042de-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="042de-153">Substitute `{iot hub hostname}` com nome anfitrião Olá IoT hub que obteve na secção "Criar um IoT hub" de Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="042de-154">Substitute `{device key}` com a chave de dispositivo Olá que obteve na secção "Criar uma identidade de dispositivo" de Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="042de-155">Adicionar Olá seguinte método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="042de-155">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="042de-156">Este método envia uma nova mensagem dispositivo para nuvem a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="042de-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="042de-157">mensagem de saudação contém um objeto JSON serializado com o ID de dispositivo Olá e gerado aleatoriamente números toosimulate um sensor de temperatura e um sensor humidade.</span><span class="sxs-lookup"><span data-stu-id="042de-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="042de-158">Por fim, adicione Olá seguintes linhas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="042de-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="042de-159">Por predefinição, Olá **criar** método numa aplicação .NET Framework cria um **DeviceClient** instância que utiliza Olá AMQP protocolo toocommunicate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="042de-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="042de-160">Olá toouse protocolo MQTT ou HTTP, utilize a substituição de Olá do Olá **criar** método permite-lhe o protocolo de Olá toospecify.</span><span class="sxs-lookup"><span data-stu-id="042de-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="042de-161">Clientes UWP e PCL utilizam o protocolo HTTP de Olá por predefinição.</span><span class="sxs-lookup"><span data-stu-id="042de-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="042de-162">Se utilizar o protocolo de Olá HTTP, também deve adicionar Olá **Microsoft.AspNet.WebApi.Client** Olá do NuGet pacote tooyour projeto tooinclude **formatting** espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="042de-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="042de-163">Este tutorial orienta-Olá passos toocreate um IoT Hub aplicação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="042de-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="042de-164">Também pode utilizar Olá [serviço ligado para o IoT Hub do Azure] [ lnk-connected-service] Visual Studio extensão tooadd Olá código necessário tooyour aplicação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="042de-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="042de-165">ações de tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="042de-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="042de-166">No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="042de-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="042de-167">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="042de-167">Run hello apps</span></span>

<span data-ttu-id="042de-168">Agora, está pronto toorun Olá aplicações.</span><span class="sxs-lookup"><span data-stu-id="042de-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="042de-169">No Visual Studio, no Explorador de Soluções, clique com o botão direito do rato na sua solução e, em seguida, clique em **Definir projetos de Arranque**.</span><span class="sxs-lookup"><span data-stu-id="042de-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="042de-170">Selecione **vários projetos de arranque**e, em seguida, selecione **iniciar** como ação Olá para ambos os Olá **ReadDeviceToCloudMessages** e **SimulatedDevice** projetos.</span><span class="sxs-lookup"><span data-stu-id="042de-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Propriedades do projeto de arranque][41]

2. <span data-ttu-id="042de-172">Prima **F5** toostart ambas as aplicações em execução.</span><span class="sxs-lookup"><span data-stu-id="042de-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="042de-173">Olá, resultado da Olá consola **SimulatedDevice** mensagens hello mostra de aplicação a aplicação do dispositivo envia tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="042de-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="042de-174">Olá, resultado da Olá consola **ReadDeviceToCloudMessages** aplicação apresenta mensagens de Olá que recebe do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="042de-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Resultado da consola das aplicações][42]

3. <span data-ttu-id="042de-176">Olá **utilização** mosaico no Olá [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:</span><span class="sxs-lookup"><span data-stu-id="042de-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Mosaico Utilização do Portal do Azure][43]

## <a name="next-steps"></a><span data-ttu-id="042de-178">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="042de-178">Next steps</span></span>

<span data-ttu-id="042de-179">Neste tutorial, configurou um IoT hub no Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="042de-180">Utilizar este dispositivo identidade tooenable Olá dispositivo aplicação toosend mensagens do dispositivo para nuvem toohello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="042de-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="042de-181">Também criou uma aplicação que apresenta as mensagens de Olá recebidas pelo hub IoT de Olá.</span><span class="sxs-lookup"><span data-stu-id="042de-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="042de-182">toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="042de-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="042de-183">[Ligar o seu dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="042de-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="042de-184">[Getting started with device management (Introdução à gestão de dispositivos)][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="042de-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="042de-185">[Introdução ao IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="042de-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="042de-186">toolearn como tooextend as mensagens de dispositivo para a nuvem de IoT processo de solução e, em escala, consulte o artigo Olá [processar mensagens do dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="042de-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
