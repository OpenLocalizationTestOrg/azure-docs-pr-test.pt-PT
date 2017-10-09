---
title: "aaaUse IoT Hub do Azure direcionar métodos (.NET/.NET) | Microsoft Docs"
description: "Como toouse IoT Hub do Azure direcionar os métodos. Utilizar dispositivos de IoT do Azure Olá SDK para .NET tooimplement uma aplicação de dispositivo simulado que inclui um método direto e Olá o serviço de IoT do Azure SDK para .NET tooimplement uma aplicação de serviço que invoca o método direto Olá."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Utilize métodos diretos (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Neste tutorial, iremos são curso toodevelop duas .NET consola aplicações:

* **CallMethodOnDevice**, uma aplicação de back-end que chama um método na aplicação de dispositivo simulado Olá e mostra a resposta Olá.
* **SimulateDeviceMethods**, uma aplicação de consola que simula um dispositivo ligar tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e responde método toohello chamado pela nuvem Olá.

> [!NOTE]
> artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun ambas as aplicações em dispositivos e a sua solução de back-end.
> 
> 

toocomplete neste tutorial, precisa de:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se pretender que a identidade de dispositivo toocreate Olá programaticamente em vez disso, leia a secção correspondente Olá Olá [ligar o dispositivo simulado tooyour IoT hub com .NET] [ lnk-device-identity-csharp] artigo.


## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada
Nesta secção, crie uma aplicação de consola .NET que responde método de tooa chamado pela solução de Olá back-end.

1. No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola** modelo de projeto. Projeto de Olá nome **SimulateDeviceMethods**.
   
    ![Nova aplicação de dispositivo Visual c# clássico do Windows][img-createdeviceapp]
    
1. No Explorador de soluções, faça duplo clique Olá **SimulateDeviceMethods** projeto e, em seguida, clique em **gerir pacotes NuGet...** .
1. No Olá **Gestor de pacotes NuGet** janela, selecione **procurar** e procure **microsoft.azure.devices.client**. Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** do pacote e aceite os termos de Olá de utilização. Este procedimento transfere, instala e adiciona uma referência toohello [dispositivos IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e as respetivas dependências.
   
    ![Aplicação de cliente de janela do Gestor de pacotes NuGet][img-clientnuget]
1. Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Adicionar Olá seguintes campos toohello **programa** classe. Substitua o valor do marcador de posição de Olá pela cadeia de ligação de dispositivo de Olá que anotou na secção anterior Olá.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Adicione Olá seguinte método direta do tooimplement Olá no dispositivo Olá:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Por fim, adicione Olá seguinte código toohello **Main** método tooopen Olá ligação tooyour IoT hub e inicializar Olá método serviço de escuta:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. No Olá Explorador de soluções do Visual Studio, clique com o botão direito a solução e, em seguida, clique em **definir projetos de arranque...** . Selecione **projeto de arranque único**e, em seguida, selecione Olá **SimulateDeviceMethods** projeto no menu pendente de Olá.        

> [!NOTE]
> ações de tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, deve implementar as políticas de repetição (como tentativas de ligação), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Chamar um método direto num dispositivo
Nesta secção, crie uma aplicação de consola do .NET que chama um método na aplicação de dispositivo simulado Olá e, em seguida, mostra a resposta Olá.

1. No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola** modelo de projeto. Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior. Projeto de Olá nome **CallMethodOnDevice**.
   
    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][img-createserviceapp]
2. No Explorador de soluções, faça duplo clique Olá **CallMethodOnDevice** projeto e, em seguida, clique em **gerir pacotes NuGet...** .
3. No Olá **Gestor de pacotes NuGet** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** do pacote e aceite os termos de Olá de utilização. Este procedimento transfere, instala e adiciona uma referência toohello [SDK do serviço do Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e as respetivas dependências.
   
    ![Janela Gestor de Pacote NuGet][img-servicenuget]

4. Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Adicionar Olá seguintes campos toohello **programa** classe. Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub hub Olá que criou na secção anterior Olá.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Adicionar Olá seguinte método toohello **programa** classe:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Este método invoca um método direto com o nome `writeLine` no Olá `myDeviceId` dispositivo. Em seguida, escreve resposta Olá fornecida pelo dispositivo Olá na consola de Olá. Tenha em atenção a como é possível toospecify um valor de tempo limite para Olá toorespond de dispositivo.
7. Por fim, adicione Olá seguintes linhas toohello **Main** método:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. No Olá Explorador de soluções do Visual Studio, clique com o botão direito a solução e, em seguida, clique em **definir projetos de arranque...** . Selecione **projeto de arranque único**e, em seguida, selecione Olá **CallMethodOnDevice** projeto no menu pendente de Olá.

## <a name="run-hello-applications"></a>Executar aplicações de Olá
Agora, está pronto toorun aplicações de Olá.

1. Executar a aplicação de dispositivo do .NET Olá **SimulateDeviceMethods**. Deve começar a escutar para chamadas de método do seu IoT Hub: 

    ![Aplicação de dispositivo a executar][img-deviceapprun]
1. Agora que o dispositivo Olá está ligado e a aguardar que as invocações de método, executar Olá .NET **CallMethodOnDevice** método Olá de tooinvoke de aplicação na aplicação de dispositivo simulado Olá. Deverá ver a resposta de dispositivo Olá escrita na consola de Olá.
   
    ![Aplicação de serviço, executar][img-serviceapprun]
1. dispositivo Olá reage, em seguida, o método toohello por esta mensagem de impressão:
   
    ![Método direto invocado no dispositivo Olá][img-directmethodinvoked]

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Este dispositivo identidade tooenable Olá simulado dispositivo aplicação tooreact toomethods invocado pela nuvem Olá que utilizou. Também criou uma aplicação que invoca os métodos no dispositivo Olá e mostra a resposta de Olá do dispositivo Olá. 

toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Introdução ao IoT Hub]
* [Agenda de tarefas em vários dispositivos][lnk-devguide-jobs]

toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introdução ao IoT Hub]: iot-hub-node-node-getstarted.md
