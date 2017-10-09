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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Ligar o seu hub IoT do dispositivo tooyour através do .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

No final de Olá deste tutorial, terá três aplicações de consola .NET:

* **CreateDeviceIdentity**, que cria uma identidade de dispositivo e tooconnect de chave de segurança associadas, a aplicação do dispositivo.
* **ReadDeviceToCloudMessages**, que apresenta a telemetria de Olá enviada pela sua aplicação de dispositivo.
* **SimulatedDevice**, que liga tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e envia uma mensagem de telemetria a cada segundo através do protocolo MQTT Olá.

Pode transferir ou clonar a solução do Visual Studio Olá, que contém Olá três aplicações a partir do Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Para obter informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun de aplicações em dispositivos e a sua solução de back-end, consulte o artigo [SDKs IoT do Azure][lnk-hub-sdks].

toocomplete neste tutorial, terá de Olá seguintes:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Acabou de criar o hub IoT e tem o nome de anfitrião de Olá e a cadeia de ligação do IoT Hub que precisa de rest de Olá toocomplete deste tutorial.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Receber mensagens dispositivo-nuvem
Nesta secção, irá criar uma aplicação de consola do .NET que lê mensagens do dispositivo para a cloud a partir do Hub IoT. Um IoT hub expõe um [Event Hubs do Azure][lnk-event-hubs-overview]-tooenable de ponto final compatível com que as mensagens do dispositivo para a nuvem de tooread. ações de tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implementação com débito elevado. toolearn como mensagens de tooprocess dispositivo para a nuvem à escala, consulte Olá [processar mensagens do dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial. Para obter mais informações sobre como tooprocess mensagens de Event Hubs, consulte Olá [introdução ao Event Hubs] [ lnk-eventhubs-tutorial] tutorial. (Este tutorial é pontos finais de toohello aplicável compatível com o evento de Hub IoT Hub.)

> [!NOTE]
> Olá o ponto final compatível com o Event Hub para ler mensagens do dispositivo para nuvem sempre utiliza Olá AMQP protocolo.

1. No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior. Projeto de Olá nome **ReadDeviceToCloudMessages**.

    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][10a]

2. No Explorador de soluções, faça duplo clique Olá **ReadDeviceToCloudMessages** projeto e, em seguida, clique em **gerir pacotes NuGet**.

3. No Olá **Gestor de pacotes NuGet** janela, procure **Windowsazure**, selecione **instalar**e aceite os termos de Olá de utilização. Este procedimento transfere, instala e adiciona uma referência demasiado[Service Bus do Azure][lnk-servicebus-nuget], com as respetivas dependências. Este pacote permite Olá tooconnect toohello compatível com o Event Hub ponto final da aplicação no seu IoT hub.

4. Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Adicionar Olá seguintes campos toohello **programa** classe. Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub para o hub de Olá que criou na secção "Criar um IoT hub" de Olá.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Adicionar Olá seguinte método toohello **programa** classe:

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

    Este método utiliza um **EventHubReceiver** partições de receção de mensagens de tooreceive de instância de todos os Olá IoT hub dispositivo para a nuvem. Repare como transmite um `DateTime.Now` parâmetro ao criar Olá **EventHubReceiver** objeto, para que apenas receber mensagens enviadas depois de iniciar. Este filtro é útil num ambiente de teste para que possa ver o conjunto atual de Olá de mensagens. Num ambiente de produção, o código deve Certifique-se de que processa todas as mensagens de Olá. Para obter mais informações, consulte o tutorial Olá [como tooprocess mensagens de dispositivo para a nuvem do IoT Hub][lnk-process-d2c-tutorial].

7. Por fim, adicione Olá seguintes linhas toohello **Main** método:

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

## <a name="create-a-device-app"></a>Criar uma aplicação de dispositivo

Nesta secção, crie uma aplicação de consola .NET que simula um dispositivo que envia o IoT hub tooan mensagens do dispositivo para nuvem.

1. No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior. Projeto de Olá nome **SimulatedDevice**.

    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][10b]

2. No Explorador de soluções, faça duplo clique Olá **SimulatedDevice** projeto e, em seguida, clique em **gerir pacotes NuGet**.

3. No Olá **Gestor de pacotes NuGet** janela, selecione **procurar**, procure **Microsoft.Azure.Devices.Client**, selecione **instalar** Olá tooinstall **Microsoft.Azure.Devices.Client** do pacote e aceite os termos de Olá de utilização. Este procedimento transfere, instala e adiciona uma referência toohello [pacote de SDK NuGet do dispositivo IoT do Azure] [ lnk-device-nuget] e as respetivas dependências.

4. Adicione Olá seguinte `using` declaração, Olá parte superior do Olá **Program.cs** ficheiro:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Adicionar Olá seguintes campos toohello **programa** classe. Substitute `{iot hub hostname}` com nome anfitrião Olá IoT hub que obteve na secção "Criar um IoT hub" de Olá. Substitute `{device key}` com a chave de dispositivo Olá que obteve na secção "Criar uma identidade de dispositivo" de Olá.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Adicionar Olá seguinte método toohello **programa** classe:

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

    Este método envia uma nova mensagem dispositivo para nuvem a cada segundo. mensagem de saudação contém um objeto JSON serializado com o ID de dispositivo Olá e gerado aleatoriamente números toosimulate um sensor de temperatura e um sensor humidade.

7. Por fim, adicione Olá seguintes linhas toohello **Main** método:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Por predefinição, Olá **criar** método numa aplicação .NET Framework cria um **DeviceClient** instância que utiliza Olá AMQP protocolo toocommunicate com o IoT Hub. Olá toouse protocolo MQTT ou HTTP, utilize a substituição de Olá do Olá **criar** método permite-lhe o protocolo de Olá toospecify. Clientes UWP e PCL utilizam o protocolo HTTP de Olá por predefinição. Se utilizar o protocolo de Olá HTTP, também deve adicionar Olá **Microsoft.AspNet.WebApi.Client** Olá do NuGet pacote tooyour projeto tooinclude **formatting** espaço de nomes.

Este tutorial orienta-Olá passos toocreate um IoT Hub aplicação de dispositivo. Também pode utilizar Olá [serviço ligado para o IoT Hub do Azure] [ lnk-connected-service] Visual Studio extensão tooadd Olá código necessário tooyour aplicação do dispositivo.

> [!NOTE]
> ações de tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar as políticas de repetição (como um término exponencial), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].

## <a name="run-hello-apps"></a>Executar aplicações de Olá

Agora, está pronto toorun Olá aplicações.

1. No Visual Studio, no Explorador de Soluções, clique com o botão direito do rato na sua solução e, em seguida, clique em **Definir projetos de Arranque**. Selecione **vários projetos de arranque**e, em seguida, selecione **iniciar** como ação Olá para ambos os Olá **ReadDeviceToCloudMessages** e **SimulatedDevice** projetos.

    ![Propriedades do projeto de arranque][41]

2. Prima **F5** toostart ambas as aplicações em execução. Olá, resultado da Olá consola **SimulatedDevice** mensagens hello mostra de aplicação a aplicação do dispositivo envia tooyour IoT hub. Olá, resultado da Olá consola **ReadDeviceToCloudMessages** aplicação apresenta mensagens de Olá que recebe do seu IoT hub.

    ![Resultado da consola das aplicações][42]

3. Olá **utilização** mosaico no Olá [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:

    ![Mosaico Utilização do Portal do Azure][43]

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, configurou um IoT hub no Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Utilizar este dispositivo identidade tooenable Olá dispositivo aplicação toosend mensagens do dispositivo para nuvem toohello IoT hub. Também criou uma aplicação que apresenta as mensagens de Olá recebidas pelo hub IoT de Olá.

toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Ligar o seu dispositivo][lnk-connect-device]
* [Getting started with device management (Introdução à gestão de dispositivos)][lnk-device-management]
* [Introdução ao IoT Edge][lnk-iot-edge]

toolearn como tooextend as mensagens de dispositivo para a nuvem de IoT processo de solução e, em escala, consulte o artigo Olá [processar mensagens do dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.

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
