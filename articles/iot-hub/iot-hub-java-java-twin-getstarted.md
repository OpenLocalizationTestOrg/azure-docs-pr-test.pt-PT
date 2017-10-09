---
title: "aaaGet começar a utilizar dispositivos duplos de IoT Hub do Azure (Java) | Microsoft Docs"
description: "Como toouse IoT Hub do Azure dispositivos duplos tooadd etiquetas e, em seguida, utilize uma consulta do IoT Hub. Utilizar dispositivos de IoT do Azure Olá SDK para aplicação de dispositivo do Java tooimplement Olá e Olá o serviço de IoT do Azure SDK para Java tooimplement uma aplicação de serviço que adiciona as etiquetas de Olá e executa Olá consulta do IoT Hub."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="2c40b-104">Começar a utilizar dispositivos duplos (Java)</span><span class="sxs-lookup"><span data-stu-id="2c40b-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="2c40b-105">Neste tutorial, crie duas aplicações de consola Java:</span><span class="sxs-lookup"><span data-stu-id="2c40b-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="2c40b-106">**Adicionar-etiquetas-consulta**, uma aplicação de back-end do Java que adiciona as etiquetas e a consulta dispositivos duplos.</span><span class="sxs-lookup"><span data-stu-id="2c40b-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="2c40b-107">**simulated-device**, uma aplicação de dispositivo do Java que que estabelece ligação tooyour IoT hub e relatórios a condição de conectividade com uma propriedade que relatados.</span><span class="sxs-lookup"><span data-stu-id="2c40b-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="2c40b-108">artigo de Olá [SDKs IoT do Azure](iot-hub-devguide-sdks.md) fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild aplicações de dispositivo e o back-end.</span><span class="sxs-lookup"><span data-stu-id="2c40b-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="2c40b-109">toocomplete neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="2c40b-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2c40b-110">Olá mais recente [8 de Kit de desenvolvimento do Java zar](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="2c40b-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="2c40b-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="2c40b-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="2c40b-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c40b-112">An active Azure account.</span></span> <span data-ttu-id="2c40b-113">(Se não tiver uma conta, pode criar um [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="2c40b-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="2c40b-114">Se preferir identidade de dispositivo toocreate Olá através de programação, leia a secção correspondente Olá Olá [ligar o dispositivo tooyour IoT hub com Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artigo.</span><span class="sxs-lookup"><span data-stu-id="2c40b-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="2c40b-115">Criar Olá do app service</span><span class="sxs-lookup"><span data-stu-id="2c40b-115">Create hello service app</span></span>

<span data-ttu-id="2c40b-116">Nesta secção, pode cria uma aplicação de Java que adiciona os metadados de localização como um dispositivo duplo do tag toohello no IoT Hub associados com **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2c40b-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="2c40b-117">aplicação Olá consulta primeiro o IoT hub para dispositivos localizados no Olá E.U.A. e, em seguida, para dispositivos que reportam uma ligação de rede celular.</span><span class="sxs-lookup"><span data-stu-id="2c40b-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="2c40b-118">No computador de desenvolvimento, crie uma pasta vazia designada `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="2c40b-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="2c40b-119">No Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven designado **adicionar-etiquetas-consulta** utilizando Olá seguinte comando na sua linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="2c40b-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="2c40b-120">Tenha em atenção que se trata de um comando único, por extenso:</span><span class="sxs-lookup"><span data-stu-id="2c40b-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2c40b-121">Na sua linha de comandos, navegue toohello `add-tags-query` pasta.</span><span class="sxs-lookup"><span data-stu-id="2c40b-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="2c40b-122">Com um editor de texto, abra Olá `pom.xml` ficheiro Olá `add-tags-query` pasta e adicione Olá seguir dependência toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="2c40b-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="2c40b-123">Esta dependência permite-lhe toouse Olá **cliente do serviço iot** pacote na sua toocommunicate de aplicação com o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="2c40b-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2c40b-124">Pode verificar a versão mais recente do Olá do **cliente do serviço iot** utilizando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2c40b-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2c40b-125">Adicione Olá seguinte **criar** nó após Olá **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="2c40b-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2c40b-126">Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="2c40b-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2c40b-127">Guarde e feche Olá `pom.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2c40b-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2c40b-128">Com um editor de texto, abra Olá `add-tags-query\src\main\java\com\mycompany\app\App.java` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2c40b-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2c40b-129">Adicione Olá seguinte **importar** ficheiro toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="2c40b-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="2c40b-130">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="2c40b-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2c40b-131">Substitua `{youriothubconnectionstring}` com a cadeia de ligação do IoT hub que anotou no Olá *criar um IoT Hub* secção:</span><span class="sxs-lookup"><span data-stu-id="2c40b-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="2c40b-132">Olá atualização **principal** seguinte do método assinatura tooinclude Olá `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="2c40b-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="2c40b-133">Adicionar Olá seguinte código toohello **principal** Olá do método toocreate **DeviceTwin** e **DeviceTwinDevice** objetos.</span><span class="sxs-lookup"><span data-stu-id="2c40b-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="2c40b-134">Olá **DeviceTwin** objeto processa comunicação Olá com o seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2c40b-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="2c40b-135">Olá **DeviceTwinDevice** objeto representa duplo de dispositivo Olá com as respetivas etiquetas e propriedades:</span><span class="sxs-lookup"><span data-stu-id="2c40b-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="2c40b-136">Adicione Olá seguinte `try/catch` bloquear toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="2c40b-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="2c40b-137">Olá tooupdate **região** e **maquinaria** etiquetas de duplo de dispositivo no seu dispositivo duplo, adicionar Olá seguinte código no Olá `try` blocos:</span><span class="sxs-lookup"><span data-stu-id="2c40b-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="2c40b-138">tooquery Olá dispositivos duplos no IoT hub, adicionar Olá seguinte código toohello `try` bloco depois código Olá adicionado no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="2c40b-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="2c40b-139">código de Olá executa duas consultas.</span><span class="sxs-lookup"><span data-stu-id="2c40b-139">hello code runs two queries.</span></span> <span data-ttu-id="2c40b-140">Cada consulta devolve um máximo de 100 dispositivos:</span><span class="sxs-lookup"><span data-stu-id="2c40b-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="2c40b-141">Guarde e feche Olá `add-tags-query\src\main\java\com\mycompany\app\App.java` ficheiro</span><span class="sxs-lookup"><span data-stu-id="2c40b-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="2c40b-142">Criar Olá **adicionar-etiquetas-consulta** aplicação e corrigir os eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="2c40b-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="2c40b-143">Na sua linha de comandos, navegue toohello `add-tags-query` pasta e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2c40b-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="2c40b-144">Criar uma aplicação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="2c40b-144">Create a device app</span></span>

<span data-ttu-id="2c40b-145">Nesta secção, crie uma aplicação de consola do Java que define um valor de propriedade comunicados que é enviado tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2c40b-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="2c40b-146">No Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven designado **simulated-device** utilizando Olá seguinte comando na sua linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="2c40b-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="2c40b-147">Tenha em atenção que se trata de um comando único, por extenso:</span><span class="sxs-lookup"><span data-stu-id="2c40b-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2c40b-148">Na sua linha de comandos, navegue toohello `simulated-device` pasta.</span><span class="sxs-lookup"><span data-stu-id="2c40b-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="2c40b-149">Com um editor de texto, abra Olá `pom.xml` ficheiro Olá `simulated-device` pasta e adicione Olá seguintes dependências toohello **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="2c40b-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="2c40b-150">Esta dependência permite-lhe toouse Olá **cliente do dispositivo iot** pacote na sua toocommunicate de aplicação com o seu IoT hub:</span><span class="sxs-lookup"><span data-stu-id="2c40b-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2c40b-151">Pode verificar a versão mais recente do Olá do **cliente do dispositivo iot** utilizando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2c40b-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2c40b-152">Adicione Olá seguinte **criar** nó após Olá **dependências** nós.</span><span class="sxs-lookup"><span data-stu-id="2c40b-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2c40b-153">Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="2c40b-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2c40b-154">Guarde e feche Olá `pom.xml` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2c40b-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2c40b-155">Com um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2c40b-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2c40b-156">Adicione Olá seguinte **importar** ficheiro toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="2c40b-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="2c40b-157">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe.</span><span class="sxs-lookup"><span data-stu-id="2c40b-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2c40b-158">Substituir `{youriothubname}` com o nome do seu IoT hub e `{yourdevicekey}` com o valor de chave de dispositivo de Olá gerou no Olá *criar uma identidade de dispositivo* secção:</span><span class="sxs-lookup"><span data-stu-id="2c40b-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="2c40b-159">Esta aplicação de exemplo utiliza Olá **protocolo** variável para instanciar um **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="2c40b-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="2c40b-160">Atualmente, toouse duplo funcionalidades do dispositivo tem de utilizar o protocolo MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="2c40b-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="2c40b-161">Adicionar Olá seguinte código toohello **principal** método para:</span><span class="sxs-lookup"><span data-stu-id="2c40b-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="2c40b-162">Crie um toocommunicate de cliente do dispositivo IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2c40b-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="2c40b-163">Criar um **dispositivo** toostore Olá dispositivo duplo propriedades do objeto.</span><span class="sxs-lookup"><span data-stu-id="2c40b-163">Create a **Device** object toostore hello device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="2c40b-164">Adicionar Olá seguinte código toohello **principal** método toocreate um **connectivityType** comunicadas propriedade e enviá-lo tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="2c40b-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="2c40b-165">Adicionar Olá seguir final toohello código Olá **principal** método.</span><span class="sxs-lookup"><span data-stu-id="2c40b-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="2c40b-166">A aguardar Olá **Enter** chave permite tempo para o estado do IoT Hub tooreport Olá Olá duplo de operações do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="2c40b-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="2c40b-167">Guarde e feche Olá `simulated-device\src\main\java\com\mycompany\app\App.java` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2c40b-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2c40b-168">Criar Olá **simulated-device** aplicação e corrigir os eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="2c40b-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="2c40b-169">Na sua linha de comandos, navegue toohello `simulated-device` pasta e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2c40b-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="2c40b-170">Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="2c40b-170">Run hello apps</span></span>

<span data-ttu-id="2c40b-171">Agora, está pronto toorun Olá consola aplicações.</span><span class="sxs-lookup"><span data-stu-id="2c40b-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="2c40b-172">Numa linha de comandos da Olá `add-tags-query` pasta, execute Olá Olá toorun de comando a seguir **adicionar-etiquetas-consulta** do app service:</span><span class="sxs-lookup"><span data-stu-id="2c40b-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicação de serviço de Java IoT Hub valores de etiqueta e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="2c40b-174">Pode ver Olá **maquinaria** e **região** etiquetas adicionado toohello dispositivo duplo.</span><span class="sxs-lookup"><span data-stu-id="2c40b-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="2c40b-175">consulta primeiro Olá devolve o seu dispositivo, mas Olá segundo não.</span><span class="sxs-lookup"><span data-stu-id="2c40b-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="2c40b-176">Numa linha de comandos da Olá `simulated-device` pasta, execute Olá Olá tooadd de comando a seguir **connectivityType** comunicadas dispositivo duplo toohello propriedade:</span><span class="sxs-lookup"><span data-stu-id="2c40b-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![cliente de dispositivo Olá adiciona Olá * * connectivityType * * comunicadas propriedade](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="2c40b-178">Numa linha de comandos da Olá `add-tags-query` pasta, execute Olá Olá toorun de comando a seguir **adicionar-etiquetas-consulta** uma segunda vez do app service:</span><span class="sxs-lookup"><span data-stu-id="2c40b-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicação de serviço de Java IoT Hub valores de etiqueta e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="2c40b-180">Agora o seu dispositivo enviou Olá **connectivityType** propriedade tooIoT Hub, consulta segundo Olá devolve o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2c40b-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c40b-181">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2c40b-181">Next steps</span></span>

<span data-ttu-id="2c40b-182">Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá.</span><span class="sxs-lookup"><span data-stu-id="2c40b-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="2c40b-183">Adicionar metadados do dispositivo como etiquetas a partir de uma aplicação de back-end e escreveu a informação da conectividade um dispositivo aplicação tooreport dispositivo no dispositivo duplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="2c40b-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="2c40b-184">Também aprendeu como tooquery Olá informações do dispositivo duplo utilizando a linguagem de consulta Olá como o SQL Server IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2c40b-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="2c40b-185">Olá utilize, como os seguintes recursos toolearn para:</span><span class="sxs-lookup"><span data-stu-id="2c40b-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="2c40b-186">Enviar telemetria a partir de dispositivos com Olá [introdução ao IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="2c40b-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="2c40b-187">Controlar dispositivos interativamente (como ativar uma ventoinha a partir de uma aplicação controlados pelo utilizador) com Olá [utilizar métodos diretos](iot-hub-java-java-direct-methods.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="2c40b-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
