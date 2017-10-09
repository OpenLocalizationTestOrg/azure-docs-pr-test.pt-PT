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
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="54ba4-104">Utilize métodos diretos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="54ba4-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="54ba4-105">Neste tutorial, iremos são curso toodevelop duas .NET consola aplicações:</span><span class="sxs-lookup"><span data-stu-id="54ba4-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="54ba4-106">**CallMethodOnDevice**, uma aplicação de back-end que chama um método na aplicação de dispositivo simulado Olá e mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="54ba4-107">**SimulateDeviceMethods**, uma aplicação de consola que simula um dispositivo ligar tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente e responde método toohello chamado pela nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="54ba4-108">artigo de Olá [SDKs IoT do Azure] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild toorun ambas as aplicações em dispositivos e a sua solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="54ba4-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="54ba4-109">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="54ba4-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="54ba4-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="54ba4-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="54ba4-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="54ba4-111">An active Azure account.</span></span> <span data-ttu-id="54ba4-112">(Se não tiver uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="54ba4-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="54ba4-113">Se pretender que a identidade de dispositivo toocreate Olá programaticamente em vez disso, leia a secção correspondente Olá Olá [ligar o dispositivo simulado tooyour IoT hub com .NET] [ lnk-device-identity-csharp] artigo.</span><span class="sxs-lookup"><span data-stu-id="54ba4-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="54ba4-114">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="54ba4-114">Create a simulated device app</span></span>
<span data-ttu-id="54ba4-115">Nesta secção, crie uma aplicação de consola .NET que responde método de tooa chamado pela solução de Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="54ba4-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="54ba4-116">No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="54ba4-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="54ba4-117">Projeto de Olá nome **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="54ba4-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Nova aplicação de dispositivo Visual c# clássico do Windows][img-createdeviceapp]
    
1. <span data-ttu-id="54ba4-119">No Explorador de soluções, faça duplo clique Olá **SimulateDeviceMethods** projeto e, em seguida, clique em **gerir pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="54ba4-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="54ba4-120">No Olá **Gestor de pacotes NuGet** janela, selecione **procurar** e procure **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="54ba4-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="54ba4-121">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** do pacote e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="54ba4-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="54ba4-122">Este procedimento transfere, instala e adiciona uma referência toohello [dispositivos IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="54ba4-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicação de cliente de janela do Gestor de pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="54ba4-124">Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="54ba4-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="54ba4-125">Adicionar Olá seguintes campos toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="54ba4-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="54ba4-126">Substitua o valor do marcador de posição de Olá pela cadeia de ligação de dispositivo de Olá que anotou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="54ba4-127">Adicione Olá seguinte método direta do tooimplement Olá no dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="54ba4-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="54ba4-128">Por fim, adicione Olá seguinte código toohello **Main** método tooopen Olá ligação tooyour IoT hub e inicializar Olá método serviço de escuta:</span><span class="sxs-lookup"><span data-stu-id="54ba4-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
        
1. <span data-ttu-id="54ba4-129">No Olá Explorador de soluções do Visual Studio, clique com o botão direito a solução e, em seguida, clique em **definir projetos de arranque...** . Selecione **projeto de arranque único**e, em seguida, selecione Olá **SimulateDeviceMethods** projeto no menu pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="54ba4-130">ações de tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="54ba4-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="54ba4-131">No código de produção, deve implementar as políticas de repetição (como tentativas de ligação), como sugerido no artigo do MSDN Olá [processamento de erros transitórios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="54ba4-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="54ba4-132">Chamar um método direto num dispositivo</span><span class="sxs-lookup"><span data-stu-id="54ba4-132">Call a direct method on a device</span></span>
<span data-ttu-id="54ba4-133">Nesta secção, crie uma aplicação de consola do .NET que chama um método na aplicação de dispositivo simulado Olá e, em seguida, mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="54ba4-134">No Visual Studio, adicione uma Visual c# Windows ambiente de trabalho clássico projeto toohello atual solução utilizando Olá **aplicação de consola** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="54ba4-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="54ba4-135">Certifique-se de versão do .NET Framework Olá 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="54ba4-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="54ba4-136">Projeto de Olá nome **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="54ba4-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Novo projeto do Visual C# no Ambiente de Trabalho Clássico do Windows][img-createserviceapp]
2. <span data-ttu-id="54ba4-138">No Explorador de soluções, faça duplo clique Olá **CallMethodOnDevice** projeto e, em seguida, clique em **gerir pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="54ba4-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="54ba4-139">No Olá **Gestor de pacotes NuGet** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** do pacote e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="54ba4-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="54ba4-140">Este procedimento transfere, instala e adiciona uma referência toohello [SDK do serviço do Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e as respetivas dependências.</span><span class="sxs-lookup"><span data-stu-id="54ba4-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela Gestor de Pacote NuGet][img-servicenuget]

4. <span data-ttu-id="54ba4-142">Adicione Olá seguinte `using` declarações na parte superior de Olá de Olá **Program.cs** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="54ba4-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="54ba4-143">Adicionar Olá seguintes campos toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="54ba4-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="54ba4-144">Substitua o valor do marcador de posição de Olá com Olá cadeia de ligação do IoT Hub hub Olá que criou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="54ba4-145">Adicionar Olá seguinte método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="54ba4-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="54ba4-146">Este método invoca um método direto com o nome `writeLine` no Olá `myDeviceId` dispositivo.</span><span class="sxs-lookup"><span data-stu-id="54ba4-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="54ba4-147">Em seguida, escreve resposta Olá fornecida pelo dispositivo Olá na consola de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="54ba4-148">Tenha em atenção a como é possível toospecify um valor de tempo limite para Olá toorespond de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="54ba4-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="54ba4-149">Por fim, adicione Olá seguintes linhas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="54ba4-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="54ba4-150">No Olá Explorador de soluções do Visual Studio, clique com o botão direito a solução e, em seguida, clique em **definir projetos de arranque...** . Selecione **projeto de arranque único**e, em seguida, selecione Olá **CallMethodOnDevice** projeto no menu pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="54ba4-151">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="54ba4-151">Run hello applications</span></span>
<span data-ttu-id="54ba4-152">Agora, está pronto toorun aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="54ba4-153">Executar a aplicação de dispositivo do .NET Olá **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="54ba4-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="54ba4-154">Deve começar a escutar para chamadas de método do seu IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="54ba4-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Aplicação de dispositivo a executar][img-deviceapprun]
1. <span data-ttu-id="54ba4-156">Agora que o dispositivo Olá está ligado e a aguardar que as invocações de método, executar Olá .NET **CallMethodOnDevice** método Olá de tooinvoke de aplicação na aplicação de dispositivo simulado Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="54ba4-157">Deverá ver a resposta de dispositivo Olá escrita na consola de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-157">You should see hello device response written in hello console.</span></span>
   
    ![Aplicação de serviço, executar][img-serviceapprun]
1. <span data-ttu-id="54ba4-159">dispositivo Olá reage, em seguida, o método toohello por esta mensagem de impressão:</span><span class="sxs-lookup"><span data-stu-id="54ba4-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Método direto invocado no dispositivo Olá][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="54ba4-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="54ba4-161">Next steps</span></span>
<span data-ttu-id="54ba4-162">Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="54ba4-163">Este dispositivo identidade tooenable Olá simulado dispositivo aplicação tooreact toomethods invocado pela nuvem Olá que utilizou.</span><span class="sxs-lookup"><span data-stu-id="54ba4-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="54ba4-164">Também criou uma aplicação que invoca os métodos no dispositivo Olá e mostra a resposta de Olá do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="54ba4-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="54ba4-165">toocontinue introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="54ba4-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="54ba4-166">[Introdução ao IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="54ba4-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="54ba4-167">[Agenda de tarefas em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="54ba4-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="54ba4-168">toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="54ba4-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
