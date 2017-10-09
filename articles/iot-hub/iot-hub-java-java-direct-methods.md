---
title: "aaaUse IoT Hub do Azure direcionar métodos (Java) | Microsoft Docs"
description: "Como toouse IoT Hub do Azure direcionar os métodos. Utilizar dispositivos de IoT do Azure Olá SDK para Java tooimplement uma aplicação de dispositivo simulado que inclui um método direto e Olá o serviço de IoT do Azure SDK para Java tooimplement uma aplicação de serviço que invoca o método direto Olá."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="a99fd-104">Utilize métodos diretos (Java)</span><span class="sxs-lookup"><span data-stu-id="a99fd-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="a99fd-105">Neste tutorial, crie duas aplicações de consola Java:</span><span class="sxs-lookup"><span data-stu-id="a99fd-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="a99fd-106">**Invoke-direta-method**, uma aplicação de back-end do Java que chama um método na aplicação de dispositivo simulado Olá e mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="a99fd-107">**simulated-device**, uma aplicação de Java que simula um dispositivo ligar tooyour IoT hub com a identidade de dispositivo Olá que cria.</span><span class="sxs-lookup"><span data-stu-id="a99fd-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="a99fd-108">Esta aplicação responde toohello direta invocada a partir de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="a99fd-109">Para obter informações sobre Olá SDKs que pode utilizar toobuild toorun de aplicações em dispositivos e a sua solução de back-end, consulte [SDKs IoT do Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="a99fd-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="a99fd-110">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="a99fd-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="a99fd-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="a99fd-111">Java SE 8.</span></span> <br/> <span data-ttu-id="a99fd-112">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="a99fd-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a99fd-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="a99fd-113">Maven 3.</span></span>  <br/> <span data-ttu-id="a99fd-114">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="a99fd-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a99fd-115">[Versão do node.js 0.10.0 ou posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a99fd-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a99fd-116">Criar uma aplicação de dispositivo simulada</span><span class="sxs-lookup"><span data-stu-id="a99fd-116">Create a simulated device app</span></span>

<span data-ttu-id="a99fd-117">Nesta secção, crie uma aplicação de consola do Java que responde método de tooa chamado pela solução de Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="a99fd-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="a99fd-118">Crie uma pasta designada iot-java-direta-method.</span><span class="sxs-lookup"><span data-stu-id="a99fd-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="a99fd-119">Na pasta iot-java-direta-method de Olá, crie um projeto Maven designado **simulated-device** utilizando Olá seguinte comando na sua linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="a99fd-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="a99fd-120">Olá seguir o comando é um comando único, por extenso:</span><span class="sxs-lookup"><span data-stu-id="a99fd-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a99fd-121">Na sua linha de comandos, navegue pasta simulated-device de toohello.</span><span class="sxs-lookup"><span data-stu-id="a99fd-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="a99fd-122">Com um editor de texto, abra Olá pom.xml na pasta simulated-device de Olá e adicione Olá seguintes dependências toohello **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="a99fd-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="a99fd-123">Esta dependência permite-lhe toouse Olá cliente do dispositivo iot pacote na sua toocommunicate de aplicação com o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a99fd-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a99fd-124">Pode verificar a versão mais recente do Olá do **cliente do dispositivo iot** utilizando [pesquisa Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="a99fd-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="a99fd-125">Adicione Olá seguinte **criar** nó após Olá **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="a99fd-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="a99fd-126">Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="a99fd-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="a99fd-127">Guarde e feche o ficheiro pom.xml de Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="a99fd-128">Com um editor de texto, abra o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a99fd-129">Adicione Olá seguinte **importar** ficheiro toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="a99fd-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="a99fd-130">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="a99fd-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="a99fd-131">Substituir `{youriothubname}` com o nome do seu IoT hub e `{yourdevicekey}` com o valor de chave de dispositivo de Olá gerou no Olá *criar uma identidade de dispositivo* secção:</span><span class="sxs-lookup"><span data-stu-id="a99fd-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="a99fd-132">Esta aplicação de exemplo utiliza Olá **protocolo** variável para instanciar um **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="a99fd-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="a99fd-133">Atualmente, toouse direcionar métodos tem de utilizar o protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="a99fd-134">tooreturn um hub IoT tooyour código de estado, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="a99fd-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="a99fd-135">invocações de método direto Olá toohandle de Olá solução de back-end, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="a99fd-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="a99fd-136">toocreate um **DeviceClient** e oiça invocações de método direto, adicione um **principal** método toohello **aplicação** classe:</span><span class="sxs-lookup"><span data-stu-id="a99fd-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="a99fd-137">Guarde e feche o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá</span><span class="sxs-lookup"><span data-stu-id="a99fd-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="a99fd-138">Criar Olá **simulated-device** aplicação e corrigir os eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="a99fd-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="a99fd-139">Na sua linha de comandos, navegue pasta simulated-device de toohello e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a99fd-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="a99fd-140">Chamar um método direto num dispositivo</span><span class="sxs-lookup"><span data-stu-id="a99fd-140">Call a direct method on a device</span></span>

<span data-ttu-id="a99fd-141">Nesta secção, crie uma aplicação de consola do Java que invoca um método direto e, em seguida, mostra a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="a99fd-142">Esta aplicação de consola liga tooyour método direto do IoT Hub tooinvoke Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="a99fd-143">Na pasta iot-java-direta-method de Olá, crie um projeto Maven designado **invoke-direta-method** utilizando Olá seguinte comando na sua linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="a99fd-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="a99fd-144">Olá seguir o comando é um comando único, por extenso:</span><span class="sxs-lookup"><span data-stu-id="a99fd-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a99fd-145">Na sua linha de comandos, navegue pasta de invoke-direta-method toohello.</span><span class="sxs-lookup"><span data-stu-id="a99fd-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="a99fd-146">Com um editor de texto, abra o ficheiro pom.xml de Olá na pasta de invoke-direta-method de Olá e adicione Olá seguir dependência toohello **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="a99fd-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="a99fd-147">Esta dependência permite-lhe toouse Olá cliente do serviço iot pacote na sua toocommunicate de aplicação com o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a99fd-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a99fd-148">Pode verificar a versão mais recente do Olá do **cliente do serviço iot** utilizando [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="a99fd-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="a99fd-149">Adicione Olá seguinte **criar** nó após Olá **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="a99fd-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="a99fd-150">Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="a99fd-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="a99fd-151">Guarde e feche o ficheiro pom.xml de Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="a99fd-152">Com um editor de texto, abra o ficheiro de invoke-direct-method\src\main\java\com\mycompany\app\App.java de Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a99fd-153">Adicione Olá seguinte **importar** ficheiro toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="a99fd-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="a99fd-154">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="a99fd-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="a99fd-155">Substitua `{youriothubconnectionstring}` com a cadeia de ligação do IoT hub que anotou no Olá *criar um IoT Hub* secção:</span><span class="sxs-lookup"><span data-stu-id="a99fd-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="a99fd-156">método de Olá tooinvoke no dispositivo simulado Olá, adicionar Olá seguinte código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="a99fd-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="a99fd-157">Guarde e feche o ficheiro de invoke-direct-method\src\main\java\com\mycompany\app\App.java Olá</span><span class="sxs-lookup"><span data-stu-id="a99fd-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="a99fd-158">Criar Olá **invoke-direta-method** aplicação e corrigir os eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="a99fd-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="a99fd-159">Na sua linha de comandos, navegue pasta de invoke-direta-method toohello e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a99fd-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="a99fd-160">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="a99fd-160">Run hello apps</span></span>

<span data-ttu-id="a99fd-161">Agora, está pronto toorun Olá consola aplicações.</span><span class="sxs-lookup"><span data-stu-id="a99fd-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="a99fd-162">Numa linha de comandos da pasta simulated-device de Olá, execute Olá seguir toobegin comando à escuta para chamadas de método do seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a99fd-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulated toolisten de aplicação de dispositivo para chamadas de método direto][8]

1. <span data-ttu-id="a99fd-164">Numa linha de comandos na pasta de invoke-direta-method Olá, execute Olá toocall de comando a seguir um método no seu dispositivo simulado do seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a99fd-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall de aplicação de serviço do Java IoT Hub um método direto][7]

1. <span data-ttu-id="a99fd-166">dispositivo simulado Olá responde a chamada de método direto toohello:</span><span class="sxs-lookup"><span data-stu-id="a99fd-166">hello simulated device responds toohello direct method call:</span></span>

    ![Aplicação de dispositivo simulada Java IoT Hub responde toohello chamada de método direto][9]

## <a name="next-steps"></a><span data-ttu-id="a99fd-168">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a99fd-168">Next steps</span></span>

<span data-ttu-id="a99fd-169">Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="a99fd-170">Este dispositivo identidade tooenable Olá simulado dispositivo aplicação tooreact toomethods invocado pela nuvem Olá que utilizou.</span><span class="sxs-lookup"><span data-stu-id="a99fd-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="a99fd-171">Também criou uma aplicação que invoca os métodos no dispositivo Olá e mostra a resposta de Olá do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="a99fd-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="a99fd-172">tooexplore outros cenários de IoT, consulte [agendar tarefas em vários dispositivos][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="a99fd-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="a99fd-173">toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a99fd-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
