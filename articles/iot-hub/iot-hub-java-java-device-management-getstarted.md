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
# <a name="get-started-with-device-management-java"></a>Introdução à gestão de dispositivos (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Este tutorial mostrar-lhe como:

* Utilize Olá toocreate do portal do Azure, um IoT Hub e criar uma identidade de dispositivo no seu IoT hub.
* Crie uma aplicação de dispositivo simulado que implementa um dispositivo de Olá tooreboot método direto. Métodos diretos são invocados a partir da nuvem Olá.
* Crie uma aplicação que invoca o método de direta de reinício de Olá na aplicação de dispositivo simulado Olá através do seu IoT hub. Esta aplicação, em seguida, monitores Olá comunicadas propriedades de Olá dispositivo toosee quando a operação de reinício de Olá estiver concluída.

No final de Olá deste tutorial, tem duas aplicações de consola Java:

**simulated-device**. Esta aplicação:

* Estabelece ligação tooyour IoT hub com a identidade de dispositivo Olá criada anteriormente.
* Recebe uma chamada de método direta de reinício.
* Simula o reinício do sistema físico.
* Hora de Olá de relatórios do reinício do último Olá através de uma propriedade que relatados.

**reinício de Acionador**. Esta aplicação:

* Chama um método direto na aplicação de dispositivo simulado Olá.
* Apresenta a chamada método direto Olá resposta toohello enviada pelo dispositivo simulado Olá
* Olá apresenta atualizado comunicadas propriedades.

> [!NOTE]
> Para obter informações sobre Olá SDKs que pode utilizar toobuild toorun de aplicações em dispositivos e a sua solução de back-end, consulte [SDKs IoT do Azure][lnk-hub-sdks].

toocomplete neste tutorial, precisa de:

* Java SE 8. <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.
* Maven 3.  <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.
* [Versão do node.js 0.10.0 ou posterior](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Acionar um reinício remoto no dispositivo Olá utilizando um método direto

Nesta secção, criar uma aplicação de consola do Java que:

1. Invoca o método de direta de reinício de Olá na aplicação de dispositivo simulada Olá.
1. Mostra a resposta Olá.
1. Olá inquéritos comunicadas propriedades enviadas pelo Olá dispositivo toodetermine quando reinício Olá estiver concluído.

Esta aplicação de consola liga tooyour IoT Hub método direta do tooinvoke Olá e leitura Olá comunicadas propriedades.

1. Crie uma pasta vazia designada dm-get-started.

1. Na pasta de Olá dm-get-started, crie um projeto Maven designado **acionador reinício** utilizando Olá seguinte comando na sua linha de comandos. seguinte Olá mostra um comando único, por extenso:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Na sua linha de comandos, navegue toohello acionador reinício pasta.

1. Com um editor de texto, abra o ficheiro pom.xml de Olá na pasta de reinício de Acionador de Olá e adicione Olá seguir dependência toohello **dependências** nós. Esta dependência permite-lhe toouse Olá cliente do serviço iot pacote na sua toocommunicate de aplicação com o seu IoT hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Pode verificar a versão mais recente do Olá do **cliente do serviço iot** utilizando [pesquisa Maven][lnk-maven-service-search].

1. Adicione Olá seguinte **criar** nó após Olá **dependências** nós. Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:

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

1. Guarde e feche o ficheiro pom.xml de Olá.

1. Com um editor de texto, abra o ficheiro de origem do Olá trigger-reboot\src\main\java\com\mycompany\app\App.java.

1. Adicione Olá seguinte **importar** ficheiro toohello de instruções:

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

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe. Substitua `{youriothubconnectionstring}` com a cadeia de ligação do IoT hub que anotou no Olá *criar um IoT Hub* secção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement um thread que lê Olá comunicadas propriedades do dispositivo duplo de Olá cada 10 segundos, adicione a seguinte de Olá aninhada classe toohello **aplicação** classe:

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

1. método direto do tooinvoke Olá reinício no dispositivo simulado Olá, adicionar Olá seguinte código toohello **principal** método:

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

1. toostart Olá thread toopoll Olá comunicadas propriedades do dispositivo simulado Olá, adicione Olá seguinte código toohello **principal** método:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable a toostop Olá aplicação, adicionar Olá seguinte código toohello **principal** método:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Guarde e feche o ficheiro de trigger-reboot\src\main\java\com\mycompany\app\App.java Olá.

1. Criar Olá **acionador reinício** aplicações back-end e corrigir os eventuais erros. Na sua linha de comandos, navegue toohello acionador reinício pasta e Olá execute os seguintes comandos:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada

Nesta secção, crie uma aplicação de consola do Java que simula um dispositivo. aplicação Olá escuta Olá chamada de método direta de reinício do seu IoT hub e responde imediatamente toothat chamada. Olá, aplicação, em seguida, permanecerá suspenso durante algum processo de reinício de Olá toosimulate antes de utilizar um Olá de toonotify propriedade comunicado **acionador reinício** aplicação de back-end que Olá reinício estiver concluída.

1. Na pasta de Olá dm-get-started, crie um projeto Maven designado **simulated-device** utilizando Olá seguinte comando na sua linha de comandos. Olá segue-se um comando único, por extenso:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Na sua linha de comandos, navegue pasta simulated-device de toohello.

1. Com um editor de texto, abra Olá pom.xml na pasta simulated-device de Olá e adicione Olá seguir dependência toohello **dependências** nós. Esta dependência permite-lhe toouse Olá cliente do serviço iot pacote na sua toocommunicate de aplicação com o seu IoT hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Pode verificar a versão mais recente do Olá do **cliente do dispositivo iot** utilizando [pesquisa Maven][lnk-maven-device-search].

1. Adicione Olá seguinte **criar** nó após Olá **dependências** nós. Esta configuração dá instruções ao Maven toouse Java 1.8 toobuild Olá aplicação:

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

1. Guarde e feche o ficheiro pom.xml de Olá.

1. Com um editor de texto, abra o ficheiro de origem do Olá simulated-device\src\main\java\com\mycompany\app\app.Java..

1. Adicione Olá seguinte **importar** ficheiro toohello de instruções:

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

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe. Substitua `{yourdeviceconnectionstring}` pela cadeia de ligação do dispositivo do Olá que anotou no Olá *criar uma identidade de dispositivo* secção:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement um processador de chamada de retorno para eventos de estado de método direto, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement um processador de chamada de retorno para eventos de estado do dispositivo duplo, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement um processador de chamada de retorno para eventos de propriedade, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:

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

1. tooimplement um reinício de dispositivo do thread toosimulate Olá, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe. o thread de Olá permanecerá suspenso durante cinco segundos e, em seguida, define Olá **lastReboot** comunicadas propriedade:

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

1. tooimplement Olá direta o método no dispositivo Olá, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe. Quando aplicação simulada Olá recebe uma chamada toohello **reiniciar** método direto, devolve uma função chamadora toohello de confirmação e, em seguida, inicia uma Olá tooprocess do thread de reinício:

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

1. Modificar a assinatura de Olá de Olá **principal** Olá do método toothrow seguintes exceções:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate um **DeviceClient**, adicionar Olá seguinte código toohello **principal** método:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart à escuta para chamadas de método direto, adicionar Olá seguinte código toohello **principal** método:

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

1. tooshut baixo simulador de dispositivo Olá, adicionar Olá seguinte código toohello **principal** método:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Guarde e feche o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá.

1. Criar Olá **simulated-device** aplicações back-end e corrigir os eventuais erros. Na sua linha de comandos, navegue pasta simulated-device de toohello e Olá execute os seguintes comandos:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicações de Olá

Agora, está pronto toorun Olá aplicações.

1. Numa linha de comandos da pasta simulated-device de Olá, execute Olá seguir toobegin comando à escuta para chamadas de método de reinício do seu IoT hub:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulated toolisten de aplicação de dispositivo para chamadas de método direta de reinício][1]

1. Numa linha de comandos na pasta de reinício de Acionador de Olá, execute Olá seguindo o método de reinício do comando toocall Olá do seu dispositivo simulado do seu IoT hub:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Método direto de reinício de Olá de toocall de aplicação de serviço de Java IoT Hub][2]

1. dispositivo simulado Olá responde a chamada de método direta de reinício de toohello:

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