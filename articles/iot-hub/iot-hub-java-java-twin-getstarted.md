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
# <a name="get-started-with-device-twins-java"></a>Começar a utilizar dispositivos duplos (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Neste tutorial, crie duas aplicações de consola Java:

* **Adicionar-etiquetas-consulta**, uma aplicação de back-end do Java que adiciona as etiquetas e a consulta dispositivos duplos.
* **simulated-device**, uma aplicação de dispositivo do Java que que estabelece ligação tooyour IoT hub e relatórios a condição de conectividade com uma propriedade que relatados.

> [!NOTE]
> artigo de Olá [SDKs IoT do Azure](iot-hub-devguide-sdks.md) fornece informações sobre Olá SDKs IoT do Azure que pode utilizar toobuild aplicações de dispositivo e o back-end.

toocomplete neste tutorial, precisa de:

* Olá mais recente [8 de Kit de desenvolvimento do Java zar](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se não tiver uma conta, pode criar um [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se preferir identidade de dispositivo toocreate Olá através de programação, leia a secção correspondente Olá Olá [ligar o dispositivo tooyour IoT hub com Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artigo.

## <a name="create-hello-service-app"></a>Criar Olá do app service

Nesta secção, pode cria uma aplicação de Java que adiciona os metadados de localização como um dispositivo duplo do tag toohello no IoT Hub associados com **myDeviceId**. aplicação Olá consulta primeiro o IoT hub para dispositivos localizados no Olá E.U.A. e, em seguida, para dispositivos que reportam uma ligação de rede celular.

1. No computador de desenvolvimento, crie uma pasta vazia designada `iot-java-twin-getstarted`.

1. No Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven designado **adicionar-etiquetas-consulta** utilizando Olá seguinte comando na sua linha de comandos. Tenha em atenção que se trata de um comando único, por extenso:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Na sua linha de comandos, navegue toohello `add-tags-query` pasta.

1. Com um editor de texto, abra Olá `pom.xml` ficheiro Olá `add-tags-query` pasta e adicione Olá seguir dependência toohello **dependências** nó. Esta dependência permite-lhe toouse Olá **cliente do serviço iot** pacote na sua toocommunicate de aplicação com o seu IoT hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Pode verificar a versão mais recente do Olá do **cliente do serviço iot** utilizando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Guarde e feche Olá `pom.xml` ficheiro.

1. Com um editor de texto, abra Olá `add-tags-query\src\main\java\com\mycompany\app\App.java` ficheiro.

1. Adicione Olá seguinte **importar** ficheiro toohello de instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicação** classe. Substitua `{youriothubconnectionstring}` com a cadeia de ligação do IoT hub que anotou no Olá *criar um IoT Hub* secção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Olá atualização **principal** seguinte do método assinatura tooinclude Olá `throws` cláusula:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Adicionar Olá seguinte código toohello **principal** Olá do método toocreate **DeviceTwin** e **DeviceTwinDevice** objetos. Olá **DeviceTwin** objeto processa comunicação Olá com o seu IoT hub. Olá **DeviceTwinDevice** objeto representa duplo de dispositivo Olá com as respetivas etiquetas e propriedades:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Adicione Olá seguinte `try/catch` bloquear toohello **principal** método:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. Olá tooupdate **região** e **maquinaria** etiquetas de duplo de dispositivo no seu dispositivo duplo, adicionar Olá seguinte código no Olá `try` blocos:

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

1. tooquery Olá dispositivos duplos no IoT hub, adicionar Olá seguinte código toohello `try` bloco depois código Olá adicionado no passo anterior Olá. código de Olá executa duas consultas. Cada consulta devolve um máximo de 100 dispositivos:

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

1. Guarde e feche Olá `add-tags-query\src\main\java\com\mycompany\app\App.java` ficheiro

1. Criar Olá **adicionar-etiquetas-consulta** aplicação e corrigir os eventuais erros. Na sua linha de comandos, navegue toohello `add-tags-query` pasta e Olá execute os seguintes comandos:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Criar uma aplicação de dispositivo

Nesta secção, crie uma aplicação de consola do Java que define um valor de propriedade comunicados que é enviado tooIoT Hub.

1. No Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven designado **simulated-device** utilizando Olá seguinte comando na sua linha de comandos. Tenha em atenção que se trata de um comando único, por extenso:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Na sua linha de comandos, navegue toohello `simulated-device` pasta.

1. Com um editor de texto, abra Olá `pom.xml` ficheiro Olá `simulated-device` pasta e adicione Olá seguintes dependências toohello **dependências** nós. Esta dependência permite-lhe toouse Olá **cliente do dispositivo iot** pacote na sua toocommunicate de aplicação com o seu IoT hub:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Pode verificar a versão mais recente do Olá do **cliente do dispositivo iot** utilizando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Guarde e feche Olá `pom.xml` ficheiro.

1. Com um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` ficheiro.

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
    ```

    Esta aplicação de exemplo utiliza Olá **protocolo** variável para instanciar um **DeviceClient** objeto. Atualmente, toouse duplo funcionalidades do dispositivo tem de utilizar o protocolo MQTT Olá.

1. Adicionar Olá seguinte código toohello **principal** método para:
    * Crie um toocommunicate de cliente do dispositivo IoT hub.
    * Criar um **dispositivo** toostore Olá dispositivo duplo propriedades do objeto.

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

1. Adicionar Olá seguinte código toohello **principal** método toocreate um **connectivityType** comunicadas propriedade e enviá-lo tooIoT Hub:

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

1. Adicionar Olá seguir final toohello código Olá **principal** método. A aguardar Olá **Enter** chave permite tempo para o estado do IoT Hub tooreport Olá Olá duplo de operações do dispositivo:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Guarde e feche Olá `simulated-device\src\main\java\com\mycompany\app\App.java` ficheiro.

1. Criar Olá **simulated-device** aplicação e corrigir os eventuais erros. Na sua linha de comandos, navegue toohello `simulated-device` pasta e Olá execute os seguintes comandos:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicações de Olá

Agora, está pronto toorun Olá consola aplicações.

1. Numa linha de comandos da Olá `add-tags-query` pasta, execute Olá Olá toorun de comando a seguir **adicionar-etiquetas-consulta** do app service:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicação de serviço de Java IoT Hub valores de etiqueta e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Pode ver Olá **maquinaria** e **região** etiquetas adicionado toohello dispositivo duplo. consulta primeiro Olá devolve o seu dispositivo, mas Olá segundo não.

1. Numa linha de comandos da Olá `simulated-device` pasta, execute Olá Olá tooadd de comando a seguir **connectivityType** comunicadas dispositivo duplo toohello propriedade:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![cliente de dispositivo Olá adiciona Olá * * connectivityType * * comunicadas propriedade](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. Numa linha de comandos da Olá `add-tags-query` pasta, execute Olá Olá toorun de comando a seguir **adicionar-etiquetas-consulta** uma segunda vez do app service:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicação de serviço de Java IoT Hub valores de etiqueta e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Agora o seu dispositivo enviou Olá **connectivityType** propriedade tooIoT Hub, consulta segundo Olá devolve o seu dispositivo.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, configurou um novo IoT hub na Olá portal do Azure e, em seguida, criou uma identidade de dispositivo no registo de identidade do hub IoT Olá. Adicionar metadados do dispositivo como etiquetas a partir de uma aplicação de back-end e escreveu a informação da conectividade um dispositivo aplicação tooreport dispositivo no dispositivo duplo de Olá. Também aprendeu como tooquery Olá informações do dispositivo duplo utilizando a linguagem de consulta Olá como o SQL Server IoT Hub.

Olá utilize, como os seguintes recursos toolearn para:

* Enviar telemetria a partir de dispositivos com Olá [introdução ao IoT Hub](iot-hub-java-java-getstarted.md) tutorial.
* Controlar dispositivos interativamente (como ativar uma ventoinha a partir de uma aplicação controlados pelo utilizador) com Olá [utilizar métodos diretos](iot-hub-java-java-direct-methods.md) tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
