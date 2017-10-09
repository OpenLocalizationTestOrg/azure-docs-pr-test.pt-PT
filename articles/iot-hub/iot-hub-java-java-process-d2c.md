---
title: aaaProcess mensagens de dispositivo para a nuvem do IoT Hub do Azure (Java) | Microsoft Docs
description: "Como tooprocess mensagens do dispositivo para a nuvem do IoT Hub utilizando regras de encaminhamento e os pontos finais personalizados toodispatch mensagens tooother serviços de back-end."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="4484d-103">Processar mensagens do dispositivo para a nuvem do IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="4484d-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="4484d-104">IoT Hub do Azure é um serviço completamente gerido que permite fiável e seguras comunicações bidirecionais entre milhões de dispositivos e uma solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="4484d-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="4484d-105">Outros tutoriais ([introdução ao IoT Hub] e [enviar mensagens da nuvem para o dispositivo com o IoT Hub][lnk-c2d]) mostram-lhe como toouse Olá básico dispositivo para nuvem e da nuvem para o dispositivo funcionalidade serviço de mensagens do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="4484d-106">Este tutorial de mensagens em fila baseia-se no código Olá mostrado Olá [introdução ao IoT Hub] tutorial e apresenta-lhe como toouse mensagem encaminhamento tooprocess de mensagens dispositivo-nuvem de uma forma escalável.</span><span class="sxs-lookup"><span data-stu-id="4484d-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="4484d-107">tutorial de Olá ilustra como tooprocess mensagens em fila que requerem ação imediata da solução de Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="4484d-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="4484d-108">Por exemplo, um dispositivo pode enviar uma mensagem de alarme que aciona a inserir um pedido de um sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="4484d-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="4484d-109">Por outro lado, as mensagens de ponto de dados simplesmente feed para um motor de análise.</span><span class="sxs-lookup"><span data-stu-id="4484d-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="4484d-110">Por exemplo, a telemetria de temperatura de um dispositivo que é toobe armazenado para análise posterior é uma mensagem de ponto de dados.</span><span class="sxs-lookup"><span data-stu-id="4484d-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="4484d-111">No final de Olá deste tutorial, execute três aplicações de consola Java:</span><span class="sxs-lookup"><span data-stu-id="4484d-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="4484d-112">**simulated-device**, uma versão modificada da aplicação Olá criada no Olá [introdução ao IoT Hub] tutorial, envia mensagens do dispositivo para a nuvem de ponto de dados de cada segundo e interativa dispositivo-nuvem mensagens cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="4484d-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="4484d-113">Esta aplicação utiliza Olá AMQP protocolo toocommunicate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="4484d-114">**Read-d2c-messages** apresenta a telemetria de Olá enviada pela sua aplicação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4484d-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="4484d-115">**leitura críticos fila** remove mensagens críticos hello do Olá barramento de serviço fila ligada toohello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="4484d-116">IoT Hub tem suporte SDK para várias plataformas de dispositivos e idiomas, incluindo C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4484d-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="4484d-117">Para obter instruções sobre como tooreplace Olá dispositivo neste tutorial com um dispositivo físico, e como tooconnect dispositivos tooan IoT Hub, consulte Olá [Centro de programadores do IoT do Azure].</span><span class="sxs-lookup"><span data-stu-id="4484d-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="4484d-118">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4484d-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4484d-119">Uma versão de trabalho completa do Olá [introdução ao IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4484d-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="4484d-120">Olá mais recente [8 de Kit de desenvolvimento do Java zar](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="4484d-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="4484d-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="4484d-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="4484d-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4484d-122">An active Azure account.</span></span> <span data-ttu-id="4484d-123">(Se não tiver uma conta, pode criar uma [conta gratuita] [lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="4484d-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="4484d-124">É necessário ter algum conhecimento básico de [Storage do Azure] e [Service Bus do Azure].</span><span class="sxs-lookup"><span data-stu-id="4484d-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="4484d-125">Enviar mensagens interativas de uma aplicação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="4484d-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="4484d-126">Nesta secção, pode modificar a aplicação de dispositivo de Olá que criou no Olá [introdução ao IoT Hub] tutorial toooccasionally enviar mensagens que necessitam de processamento de imediato.</span><span class="sxs-lookup"><span data-stu-id="4484d-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="4484d-127">Utilize o editor tooopen Olá simulated-device\src\main\java\com\mycompany\app\app.Java. ficheiro de texto.</span><span class="sxs-lookup"><span data-stu-id="4484d-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="4484d-128">Este ficheiro contém o código de Olá para Olá **simulated-device** aplicação que criou no Olá [introdução ao IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4484d-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="4484d-129">Substitua Olá **MessageSender** classe com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="4484d-129">Replace hello **MessageSender** class with hello following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="4484d-130">Este método aleatoriamente adiciona propriedade Olá `"level": "critical"` toomessages enviada pelo dispositivo Olá, o que simula uma mensagem que necessita de uma ação imediata por Olá aplicação back-end.</span><span class="sxs-lookup"><span data-stu-id="4484d-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="4484d-131">aplicação Olá transfere a informação nas propriedades de mensagem de Olá, em vez de no corpo da mensagem Olá, para que o IoT Hub pode encaminhar o destino do Olá mensagem toohello mensagem adequado.</span><span class="sxs-lookup"><span data-stu-id="4484d-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4484d-132">Pode utilizar mensagens de tooroute de propriedades de mensagem para vários cenários, incluindo frio-path processar, além disso exemplo de caminho frequente toohello mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="4484d-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="4484d-133">Guarde e feche o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá.</span><span class="sxs-lookup"><span data-stu-id="4484d-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4484d-134">Para sake Olá de simplicidade, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="4484d-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4484d-135">No código de produção, deve implementar uma política de repetição como término exponencial, como sugerido no artigo do MSDN Olá [processamento de erros transitórios].</span><span class="sxs-lookup"><span data-stu-id="4484d-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="4484d-136">Olá toobuild **simulated-device** aplicação com o Maven, execute Olá seguinte comando na linha de comandos Olá na pasta simulated-device de Olá:</span><span class="sxs-lookup"><span data-stu-id="4484d-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="4484d-137">Adicionar um IoT de tooyour fila em hub e encaminhar a tooit mensagens</span><span class="sxs-lookup"><span data-stu-id="4484d-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="4484d-138">Nesta secção, criar uma fila do Service Bus, ligue-tooyour IoT hub e configurar o seu IoT hub toosend toohello a fila de mensagens com base na presença de Olá de uma propriedade de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4484d-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="4484d-139">Para obter mais informações sobre como tooprocess mensagens de filas do Service Bus, consulte [introdução às filas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="4484d-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="4484d-140">Criar uma fila do Service Bus, conforme descrito em [introdução às filas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="4484d-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="4484d-141">Tome nota do nome de espaço de nomes e fila Olá.</span><span class="sxs-lookup"><span data-stu-id="4484d-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="4484d-142">No Olá portal do Azure, abra o seu IoT hub e clique em **pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="4484d-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Pontos finais do IoT hub][30]

3. <span data-ttu-id="4484d-144">No Olá **pontos finais** painel, clique em **adicionar** em Olá tooadd superior a fila tooyour do IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="4484d-145">Ponto final do nome Olá **CriticalQueue** e utilizar Olá listas pendentes tooselect **fila do Service Bus**, Olá espaço de nomes de barramento de serviço em que reside a sua fila e Olá nome da sua fila.</span><span class="sxs-lookup"><span data-stu-id="4484d-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="4484d-146">Quando tiver terminado, clique em **guardar** na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="4484d-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Adicionar um ponto final][31]

4. <span data-ttu-id="4484d-148">Agora, clique em **rotas** no seu IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="4484d-149">Clique em **adicionar** , Olá parte superior do Olá painel toocreate adicionada uma regra de encaminhamento encaminha mensagens toohello fila apenas.</span><span class="sxs-lookup"><span data-stu-id="4484d-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="4484d-150">Selecione **DeviceTelemetry** como origem de Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="4484d-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="4484d-151">Introduza `level="critical"` como condição Olá e escolha a fila de Olá acabou de adicionar como um ponto final personalizado como Olá ponto final de regra de encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="4484d-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="4484d-152">Quando tiver terminado, clique em **guardar** na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="4484d-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Adicionar uma rota][32]

    <span data-ttu-id="4484d-154">Certifique-se a rota de contingência Olá estiver definida demasiado**ON**.</span><span class="sxs-lookup"><span data-stu-id="4484d-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="4484d-155">Esta definição é a configuração predefinida Olá um IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Rota de contingência][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="4484d-157">(Opcional) Ler a partir do ponto final de fila de Olá</span><span class="sxs-lookup"><span data-stu-id="4484d-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="4484d-158">Opcionalmente, podem ler mensagens de Olá do ponto final de fila de Olá, seguindo as instruções Olá [introdução às filas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="4484d-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="4484d-159">Nome Olá aplicação **leitura críticos fila**.</span><span class="sxs-lookup"><span data-stu-id="4484d-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="4484d-160">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="4484d-160">Run hello applications</span></span>

<span data-ttu-id="4484d-161">Agora, está três aplicações de toorun pronto Olá.</span><span class="sxs-lookup"><span data-stu-id="4484d-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="4484d-162">Olá toorun **read-d2c-messages** aplicação, numa linha de comandos ou shell navegue pasta read-d2c de toohello e executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4484d-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Executar read-d2c-messages][readd2c]

2. <span data-ttu-id="4484d-164">Olá toorun **leitura críticos fila** aplicação, numa linha de comandos ou shell navegue toohello pasta de leitura fila críticos e executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4484d-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar leitura mensagens crítico][readqueue]

3. <span data-ttu-id="4484d-166">Olá toorun **simulated-device** aplicação, numa linha de comandos ou shell navegue pasta simulated-device de toohello e executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4484d-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="4484d-168">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4484d-168">Next steps</span></span>

<span data-ttu-id="4484d-169">Neste tutorial, aprendeu como tooreliably emitir mensagens do dispositivo para nuvem utilizando a funcionalidade de encaminhamento de mensagens de Olá do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4484d-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="4484d-170">Olá [como mensagens de toosend nuvem para o dispositivo com o IoT Hub] [ lnk-c2d] mostra-lhe como toosend mensagens tooyour dispositivos da sua solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="4484d-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="4484d-171">Exemplos de toosee de soluções ponto-a-ponto completas que utilizam o IoT Hub, consulte [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="4484d-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="4484d-172">toolearn mais informações sobre desenvolver soluções de IoT hub, consulte Olá [guia para programadores do IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="4484d-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="4484d-173">toolearn mais informações sobre o encaminhamento de mensagens do IoT Hub, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="4484d-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Storage do Azure]: https://azure.microsoft.com/documentation/services/storage/
[Service Bus do Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[guia para programadores do IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[introdução ao IoT Hub]: iot-hub-java-java-getstarted.md
[Centro de programadores do IoT do Azure]: https://azure.microsoft.com/develop/iot
[processamento de erros transitórios]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Processamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
