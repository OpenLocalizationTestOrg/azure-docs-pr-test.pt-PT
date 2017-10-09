---
title: "aaaGet iniciado com a gestão de dispositivos do IoT Hub do Azure (Java) | Microsoft Docs"
description: "Como tooinitiate de gestão de dispositivos de IoT Hub do Azure toouse remota do dispositivo ser reiniciado. Utilizar dispositivos de IoT do Azure Olá SDK para Java tooimplement uma aplicação de dispositivo simulado que inclui um método direto e Olá o serviço de IoT do Azure SDK para Java tooimplement uma aplicação de serviço que invoca o método direto Olá."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="358f4-104">Introdução à gestão de dispositivos (Java)</span><span class="sxs-lookup"><span data-stu-id="358f4-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="358f4-105">Este tutorial mostrar-lhe como:</span><span class="sxs-lookup"><span data-stu-id="358f4-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="358f4-106">Utilize Olá toocreate do portal do Azure, um IoT Hub e criar uma identidade de dispositivo no seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="358f4-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="358f4-107">Crie uma aplicação de dispositivo simulado que implementa um dispositivo de Olá tooreboot método direto.</span><span class="sxs-lookup"><span data-stu-id="358f4-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="358f4-108">Métodos diretos são invocados a partir da nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="358f4-109">Crie uma aplicação que invoca o método de direta de reinício de Olá na aplicação de dispositivo simulado Olá através do seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="358f4-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="358f4-110">Esta aplicação, em seguida, monitores Olá comunicadas propriedades de Olá dispositivo toosee quando a operação de reinício de Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="358f4-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="358f4-111">No final de Olá deste tutorial, tem duas aplicações de consola Java:</span><span class="sxs-lookup"><span data-stu-id="358f4-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="358f4-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="358f4-112">**simulated-device**.</span></span> <span data-ttu-id="358f4-113">Esta aplicação:</span><span class="sxs-lookup"><span data-stu-id="358f4-113">This app:</span></span>

* <span data-ttu-id="358f4-114">Estabelece ligação tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="358f4-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="358f4-115">Recebe uma chamada de método direta de reinício.</span><span class="sxs-lookup"><span data-stu-id="358f4-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="358f4-116">Simula o reinício do sistema físico.</span><span class="sxs-lookup"><span data-stu-id="358f4-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="358f4-117">Hora de Olá de relatórios do reinício do último Olá através de uma propriedade que relatados.</span><span class="sxs-lookup"><span data-stu-id="358f4-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="358f4-118">**reinício de Acionador**.</span><span class="sxs-lookup"><span data-stu-id="358f4-118">**trigger-reboot**.</span></span> <span data-ttu-id="358f4-119">Esta aplicação:</span><span class="sxs-lookup"><span data-stu-id="358f4-119">This app:</span></span>

* <span data-ttu-id="358f4-120">Chama um método direto na aplicação de dispositivo simulado Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="358f4-121">Apresenta a chamada método direto Olá resposta toohello enviada pelo dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="358f4-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="358f4-122">Olá apresenta atualizado comunicadas propriedades.</span><span class="sxs-lookup"><span data-stu-id="358f4-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="358f4-123">Para obter informações sobre Olá SDKs que pode utilizar toobuild toorun de aplicações em dispositivos e a sua solução de back-end, consulte [SDKs IoT do Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="358f4-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="358f4-124">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="358f4-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="358f4-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="358f4-125">Java SE 8.</span></span> <br/> <span data-ttu-id="358f4-126">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="358f4-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="358f4-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="358f4-127">Maven 3.</span></span>  <br/> <span data-ttu-id="358f4-128">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="358f4-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="358f4-129">[Versão do node.js 0.10.0 ou posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="358f4-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="358f4-130">Acionar um reinício remoto no dispositivo Olá utilizando um método direto</span><span class="sxs-lookup"><span data-stu-id="358f4-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="358f4-131">Nesta secção, criar uma aplicação de consola do Java que:</span><span class="sxs-lookup"><span data-stu-id="358f4-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="358f4-132">Invoca o método de direta de reinício de Olá na aplicação de dispositivo simulada Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="358f4-133">Mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-133">Displays hello response.</span></span>
1. <span data-ttu-id="358f4-134">Olá inquéritos comunicadas propriedades enviadas pelo Olá dispositivo toodetermine quando reinício Olá estiver concluído.</span><span class="sxs-lookup"><span data-stu-id="358f4-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="358f4-135">Esta aplicação de consola liga tooyour IoT Hub método direta do tooinvoke Olá e leitura Olá comunicadas propriedades.</span><span class="sxs-lookup"><span data-stu-id="358f4-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="358f4-136">Crie uma pasta vazia designada dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="358f4-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="358f4-137">Na pasta de Olá dm-get-started, crie um projeto Maven designado **acionador reinício** utilizando Olá seguinte comando na sua linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="358f4-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="358f4-138">seguinte Olá mostra um comando único, por extenso:</span><span class="sxs-lookup"><span data-stu-id="358f4-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="358f4-139">Na sua linha de comandos, navegue toohello acionador reinício pasta.</span><span class="sxs-lookup"><span data-stu-id="358f4-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="358f4-140">Com um editor de texto, abra o ficheiro pom.xml de Olá na pasta de reinício de Acionador de Olá e adicione Olá seguir dependência toohello **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="358f4-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="358f4-141">Esta dependência permite-lhe toouse Olá cliente do serviço iot pacote na sua toocommunicate de aplicação com o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="358f4-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="358f4-142">Pode verificar a versão mais recente do Olá do **cliente do serviço iot** utilizando [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="358f4-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="358f4-143">Adicione Olá seguinte **criar** nó após Olá **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="358f4-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="358f4-144">Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="358f4-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="358f4-145">Guarde e feche o ficheiro pom.xml de Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="358f4-146">Com um editor de texto, abra o ficheiro de origem do Olá trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="358f4-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="358f4-147">Adicione Olá seguinte **importar** ficheiro toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="358f4-147">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="358f4-148">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="358f4-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="358f4-149">Substitua `{youriothubconnectionstring}` com a cadeia de ligação do IoT hub que anotou no Olá *criar um IoT Hub* secção:</span><span class="sxs-lookup"><span data-stu-id="358f4-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="358f4-150">tooimplement um thread que lê Olá comunicadas propriedades do dispositivo duplo de Olá cada 10 segundos, adicione a seguinte de Olá aninhada classe toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="358f4-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="358f4-151">método direto do tooinvoke Olá reinício no dispositivo simulado Olá, adicionar Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="358f4-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="358f4-152">toostart Olá thread toopoll Olá comunicadas propriedades do dispositivo simulado Olá, adicione Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="358f4-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="358f4-153">tooenable a toostop Olá aplicação, adicionar Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="358f4-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="358f4-154">Guarde e feche o ficheiro de trigger-reboot\src\main\java\com\mycompany\app\App.java Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="358f4-155">Criar Olá **acionador reinício** aplicações back-end e corrigir os eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="358f4-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="358f4-156">Na sua linha de comandos, navegue toohello acionador reinício pasta e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="358f4-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="358f4-157">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="358f4-157">Create a simulated device app</span></span>

<span data-ttu-id="358f4-158">Nesta secção, crie uma aplicação de consola do Java que simula um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="358f4-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="358f4-159">aplicação Olá escuta Olá chamada de método direta de reinício do seu IoT hub e responde imediatamente toothat chamada.</span><span class="sxs-lookup"><span data-stu-id="358f4-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="358f4-160">Olá, aplicação, em seguida, permanecerá suspenso durante algum processo de reinício de Olá toosimulate antes de utilizar um Olá de toonotify propriedade comunicado **acionador reinício** aplicação de back-end que Olá reinício estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="358f4-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="358f4-161">Na pasta de Olá dm-get-started, crie um projeto Maven designado **simulated-device** utilizando Olá seguinte comando na sua linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="358f4-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="358f4-162">Olá segue-se um comando único, por extenso:</span><span class="sxs-lookup"><span data-stu-id="358f4-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="358f4-163">Na sua linha de comandos, navegue pasta simulated-device de toohello.</span><span class="sxs-lookup"><span data-stu-id="358f4-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="358f4-164">Com um editor de texto, abra Olá pom.xml na pasta simulated-device de Olá e adicione Olá seguir dependência toohello **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="358f4-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="358f4-165">Esta dependência permite-lhe toouse Olá cliente do serviço iot pacote na sua toocommunicate de aplicação com o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="358f4-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="358f4-166">Pode verificar a versão mais recente do Olá do **cliente do dispositivo iot** utilizando [pesquisa Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="358f4-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="358f4-167">Adicione Olá seguinte **criar** nó após Olá **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="358f4-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="358f4-168">Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="358f4-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="358f4-169">Guarde e feche o ficheiro pom.xml de Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="358f4-170">Com um editor de texto, abra o ficheiro de origem do Olá simulated-device\src\main\java\com\mycompany\app\app.Java..</span><span class="sxs-lookup"><span data-stu-id="358f4-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="358f4-171">Adicione Olá seguinte **importar** ficheiro toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="358f4-171">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="358f4-172">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="358f4-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="358f4-173">Substitua `{yourdeviceconnectionstring}` pela cadeia de ligação do dispositivo do Olá que anotou no Olá *criar uma identidade de dispositivo* secção:</span><span class="sxs-lookup"><span data-stu-id="358f4-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="358f4-174">tooimplement um processador de chamada de retorno para eventos de estado de método direto, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="358f4-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="358f4-175">tooimplement um processador de chamada de retorno para eventos de estado do dispositivo duplo, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="358f4-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="358f4-176">tooimplement um processador de chamada de retorno para eventos de propriedade, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="358f4-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="358f4-177">tooimplement um reinício de dispositivo do thread toosimulate Olá, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="358f4-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="358f4-178">o thread de Olá permanecerá suspenso durante cinco segundos e, em seguida, define Olá **lastReboot** comunicadas propriedade:</span><span class="sxs-lookup"><span data-stu-id="358f4-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="358f4-179">tooimplement Olá direta o método no dispositivo Olá, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="358f4-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="358f4-180">Quando aplicação simulada Olá recebe uma chamada toohello **reiniciar** método direto, devolve uma função chamadora toohello de confirmação e, em seguida, inicia uma Olá tooprocess do thread de reinício:</span><span class="sxs-lookup"><span data-stu-id="358f4-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="358f4-181">Modificar a assinatura de Olá de Olá **principal** Olá do método toothrow seguintes exceções:</span><span class="sxs-lookup"><span data-stu-id="358f4-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="358f4-182">tooinstantiate um **DeviceClient**, adicionar Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="358f4-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="358f4-183">toostart à escuta para chamadas de método direto, adicionar Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="358f4-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="358f4-184">tooshut baixo simulador de dispositivo Olá, adicionar Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="358f4-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="358f4-185">Guarde e feche o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá.</span><span class="sxs-lookup"><span data-stu-id="358f4-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="358f4-186">Criar Olá **simulated-device** aplicações back-end e corrigir os eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="358f4-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="358f4-187">Na sua linha de comandos, navegue pasta simulated-device de toohello e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="358f4-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="358f4-188">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="358f4-188">Run hello apps</span></span>

<span data-ttu-id="358f4-189">Agora, está pronto toorun Olá aplicações.</span><span class="sxs-lookup"><span data-stu-id="358f4-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="358f4-190">Numa linha de comandos da pasta simulated-device de Olá, execute Olá seguir toobegin comando à escuta para chamadas de método de reinício do seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="358f4-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulated toolisten de aplicação de dispositivo para chamadas de método direta de reinício][1]

1. <span data-ttu-id="358f4-192">Numa linha de comandos na pasta de reinício de Acionador de Olá, execute Olá seguindo o método de reinício do comando toocall Olá do seu dispositivo simulado do seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="358f4-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Método direto de reinício de Olá de toocall de aplicação de serviço de Java IoT Hub][2]

1. <span data-ttu-id="358f4-194">dispositivo simulado Olá responde a chamada de método direta de reinício de toohello:</span><span class="sxs-lookup"><span data-stu-id="358f4-194">hello simulated device responds toohello reboot direct method call:</span></span>

    ![Aplicação de dispositivo simulada Java IoT Hub responde toohello chamada de método direto][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22