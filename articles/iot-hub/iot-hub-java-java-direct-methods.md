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
# <a name="use-direct-methods-java"></a>Utilize métodos diretos (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Neste tutorial, crie duas aplicações de consola Java:

* **Invoke-direta-method**, uma aplicação de back-end do Java que chama um método na aplicação de dispositivo simulado Olá e mostra a resposta Olá.
* **simulated-device**, uma aplicação de Java que simula um dispositivo ligar tooyour IoT hub com a identidade de dispositivo Olá que cria. Esta aplicação responde toohello direta invocada a partir de back-end Olá.

> [!NOTE]
> Para obter informações sobre Olá SDKs que pode utilizar toobuild toorun de aplicações em dispositivos e a sua solução de back-end, consulte [SDKs IoT do Azure][lnk-hub-sdks].

toocomplete neste tutorial, precisa de:

* Java SE 8. <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.
* Maven 3.  <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.
* [Versão do node.js 0.10.0 ou posterior](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar uma aplicação de dispositivo simulada

Nesta secção, crie uma aplicação de consola do Java que responde método de tooa chamado pela solução de Olá back-end.

1. Crie uma pasta designada iot-java-direta-method.

1. Na pasta iot-java-direta-method de Olá, crie um projeto Maven designado **simulated-device** utilizando Olá seguinte comando na sua linha de comandos. Olá seguir o comando é um comando único, por extenso:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Na sua linha de comandos, navegue pasta simulated-device de toohello.

1. Com um editor de texto, abra Olá pom.xml na pasta simulated-device de Olá e adicione Olá seguintes dependências toohello **dependências** nós. Esta dependência permite-lhe toouse Olá cliente do dispositivo iot pacote na sua toocommunicate de aplicação com o seu IoT hub:

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

1. Com um editor de texto, abra o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá.

1. Adicione Olá seguinte **importar** ficheiro toohello de instruções:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe. Substituir `{youriothubname}` com o nome do seu IoT hub e `{yourdevicekey}` com o valor de chave de dispositivo de Olá gerou no Olá *criar uma identidade de dispositivo* secção:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Esta aplicação de exemplo utiliza Olá **protocolo** variável para instanciar um **DeviceClient** objeto. Atualmente, toouse direcionar métodos tem de utilizar o protocolo MQTT Olá.

1. tooreturn um hub IoT tooyour código de estado, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. invocações de método direto Olá toohandle de Olá solução de back-end, adicione o seguinte de Olá aninhada classe toohello **aplicação** classe:

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

1. toocreate um **DeviceClient** e oiça invocações de método direto, adicione um **principal** método toohello **aplicação** classe:

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

1. Guarde e feche o ficheiro simulated-device\src\main\java\com\mycompany\app\app.Java. de Olá

1. Criar Olá **simulated-device** aplicação e corrigir os eventuais erros. Na sua linha de comandos, navegue pasta simulated-device de toohello e Olá execute os seguintes comandos:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Chamar um método direto num dispositivo

Nesta secção, crie uma aplicação de consola do Java que invoca um método direto e, em seguida, mostra a resposta Olá. Esta aplicação de consola liga tooyour método direto do IoT Hub tooinvoke Olá.

1. Na pasta iot-java-direta-method de Olá, crie um projeto Maven designado **invoke-direta-method** utilizando Olá seguinte comando na sua linha de comandos. Olá seguir o comando é um comando único, por extenso:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Na sua linha de comandos, navegue pasta de invoke-direta-method toohello.

1. Com um editor de texto, abra o ficheiro pom.xml de Olá na pasta de invoke-direta-method de Olá e adicione Olá seguir dependência toohello **dependências** nós. Esta dependência permite-lhe toouse Olá cliente do serviço iot pacote na sua toocommunicate de aplicação com o seu IoT hub:

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

1. Com um editor de texto, abra o ficheiro de invoke-direct-method\src\main\java\com\mycompany\app\App.java de Olá.

1. Adicione Olá seguinte **importar** ficheiro toohello de instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe. Substitua `{youriothubconnectionstring}` com a cadeia de ligação do IoT hub que anotou no Olá *criar um IoT Hub* secção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. método de Olá tooinvoke no dispositivo simulado Olá, adicionar Olá seguinte código toohello **principal** método:

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

1. Guarde e feche o ficheiro de invoke-direct-method\src\main\java\com\mycompany\app\App.java Olá

1. Criar Olá **invoke-direta-method** aplicação e corrigir os eventuais erros. Na sua linha de comandos, navegue pasta de invoke-direta-method toohello e Olá execute os seguintes comandos:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicações de Olá

Agora, está pronto toorun Olá consola aplicações.

1. Numa linha de comandos da pasta simulated-device de Olá, execute Olá seguir toobegin comando à escuta para chamadas de método do seu IoT hub:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulated toolisten de aplicação de dispositivo para chamadas de método direto][8]

1. Numa linha de comandos na pasta de invoke-direta-method Olá, execute Olá toocall de comando a seguir um método no seu dispositivo simulado do seu IoT hub:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall de aplicação de serviço do Java IoT Hub um método direto][7]

1. dispositivo simulado Olá responde a chamada de método direto toohello:

    ![Aplicação de dispositivo simulada Java IoT Hub responde toohello chamada de método direto][9]

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Este dispositivo identidade tooenable Olá simulado dispositivo aplicação tooreact toomethods invocado pela nuvem Olá que utilizou. Também criou uma aplicação que invoca os métodos no dispositivo Olá e mostra a resposta de Olá do dispositivo Olá.

tooexplore outros cenários de IoT, consulte [agendar tarefas em vários dispositivos][lnk-devguide-jobs].

toolearn como tooextend chama o método de agenda e soluções de IoT em vários dispositivos, consulte Olá [agenda e as tarefas de difusão] [ lnk-tutorial-jobs] tutorial.

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
