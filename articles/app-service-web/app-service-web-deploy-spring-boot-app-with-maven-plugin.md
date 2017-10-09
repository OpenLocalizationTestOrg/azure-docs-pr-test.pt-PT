---
title: "aaaHow toouse Olá Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque da mola"
description: "Saiba como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque de mola."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque da mola

Olá [Plug-in do Maven para Web Apps do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do App Service do Azure em projetos Maven e simplifica o processo de Olá para os programadores toodeploy web apps tooAzure do serviço de aplicações.

Este artigo demonstra utilizando Olá Plug-in do Maven para Web Apps do Azure toodeploy tooAzure de aplicação de arranque a um exemplo serviços aplicacionais.

> [!NOTE]
>
> Olá Plug-in do Maven para Web Apps do Azure está atualmente disponível como uma pré-visualização. Por agora, a publicação de FTP só é suportada, embora as funcionalidades adicionais estejam planeadas para Olá futura.
>

## <a name="prerequisites"></a>Pré-requisitos

Ordem toocomplete Olá passos deste tutorial, terá de Olá toohave os seguintes pré-requisitos:

* Uma subscrição do Azure; Se ainda não tiver uma subscrição do Azure, pode ativar o [benefícios de subscritor do MSDN] ou inscrever-se um [conta do Azure gratuita].
* Olá [Interface de linha de comandos do Azure (CLI)].
* Um atualizados [Java Development Kit (JDK)], versão 1.7 ou posterior.
* Do Apache [Maven] criar ferramenta (versão 3).
* A [Git] cliente.

## <a name="clone-hello-sample-spring-boot-web-app"></a>Aplicação de web de arranque de mola de exemplo de Olá clone

Nesta secção, clonar uma aplicação de arranque de mola concluída e testá-lo localmente.

1. Abra uma linha de comandos ou janela de terminal e criar um diretório local toohold da aplicação de arranque de mola e alteração toothat diretório; Por exemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Olá clone [mola arranque introdução] projeto de exemplo para o diretório de Olá criou; por exemplo:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Altere o projeto do diretório toohello concluída; Por exemplo:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Criar o ficheiro JAR de Olá com o Maven; Por exemplo:
   ```shell
   mvn clean package
   ```

1. Quando tiver sido criada a aplicação web de Olá, iniciar a aplicação de web de Olá com o Maven; Por exemplo:
   ```shell
   mvn spring-boot:run
   ```

1. Testar a aplicação web de Olá navegando tooit localmente utilizando um browser. Por exemplo, pode utilizar Olá se tiver o curl disponível os seguintes comandos:
   ```shell
   curl http://localhost:8080
   ```

1. Deverá ver Olá seguir a mensagem apresentada: **saudações de arranque de mola!**

## <a name="create-an-azure-service-principal"></a>Criar um Azure principal de serviço

Nesta secção, vai criar um Azure principal de serviço que Olá utiliza de plug-in do Maven quando implementar a sua tooAzure de aplicação web.

1. Abra uma linha de comandos.

1. Inicie sessão na sua conta do Azure utilizando Olá CLI do Azure:
   ```shell
   az login
   ```
   Siga Olá instruções toocomplete Olá início de sessão no processo.

1. Crie um Azure principal de serviço:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Onde `uuuuuuuu` é o nome de utilizador de Olá e `pppppppp` é Olá palavra-passe para o principal de serviço Olá.

1. Azure responde com JSON que se assemelha Olá seguinte exemplo:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Irá utilizar os valores Olá esta resposta JSON quando configurar Olá Maven Plug-in toodeploy sua tooAzure de aplicação web. Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de marcador de posição, o que são utilizados em toomake este exemplo-lo mais fácil toomap estes valores tootheir respetivos elementos quando configura o Maven `settings.xml` ficheiros Olá seguinte secção.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Configurar Maven toouse o principal de serviço do Azure

Nesta secção, utilize os valores de Olá da sua autenticação Olá principal tooconfigure de serviço do Azure que Maven utiliza ao implementar a sua tooAzure de aplicação web.

1. Abra o Maven `settings.xml` ficheiro num editor de texto; este ficheiro pode ser um caminho como Olá exemplos a seguir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Adicionar as definições de principal de serviço do Azure na secção anterior do Olá deste tutorial toohello `<servers>` coleção no Olá *settings.xml* ficheiro; por exemplo:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<id>` | Especifica um nome exclusivo que Maven utiliza toolook configurar as definições de segurança quando implementa o tooAzure de aplicação web.
   `<client>` | Contém Olá `appId` valor do seu principal de serviço.
   `<tenant>` | Contém Olá `tenant` valor do seu principal de serviço.
   `<key>` | Contém Olá `password` valor do seu principal de serviço.
   `<environment>` | Define o ambiente de nuvem do Azure do Olá destino, que é `AZURE` neste exemplo. (Uma lista completa dos ambientes está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação)

1. Guarde e feche Olá *settings.xml* ficheiro.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>OPCIONAL: Personalizar o pom.xml antes de implementar a sua tooAzure de aplicação web

Abra Olá `pom.xml` de ficheiros para a sua aplicação de arranque de mola num editor de texto e, em seguida, localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`. Este elemento deve assemelhar-se Olá seguinte exemplo:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Existem vários valores que pode modificar para o plug-in do Maven Olá e uma descrição detalhada para cada um destes elementos está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação. Que a ser consiga aceder tal, existem vários valores, realçando neste artigo:

Elemento | Descrição
---|---|---
`<version>` | Especifica uma versão de Olá Olá [Plug-in do Maven para Web Apps do Azure]. Deve verificar a versão de Olá listada no Olá [Respository Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que está a utilizar Olá versão mais recente.
`<authentication>` | Especifica as informações de autenticação de Olá do Azure, que, neste exemplo, contém um `<serverId>` elemento que contenha `azure-auth`; Maven utiliza toolook esse valor dos valores de principal de serviço do Azure Olá no seu Maven *settings.xml* ficheiro, que é definida uma secção anterior deste artigo.
`<resourceGroup>` | Especifica o grupo de recursos do Olá destino, que é `maven-plugin` neste exemplo. grupo de recursos de Olá é criado durante a implementação, se já existir.
`<appName>` | Especifica o nome de destino Olá para a sua aplicação web. Neste exemplo, é o nome de destino Olá `maven-web-app-${maven.build.timestamp}`, em que hello `${maven.build.timestamp}` é acrescentado um sufixo neste conflito de tooavoid de exemplo. (Olá timestamp é opcional; pode especificar qualquer cadeia exclusiva para o nome da aplicação Olá).
`<region>` | Especifica a região de destino Olá, que, neste exemplo, é `westus`. (Uma lista completa está a ser Olá [Plug-in do Maven para Web Apps do Azure] documentação.)
`<javaVersion>` | Especifica a versão de tempo de execução Java Olá para a sua aplicação web. (Uma lista completa está a ser Olá [Plug-in do Maven para Web Apps do Azure] documentação.)
`<deploymentType>` | Especifica o tipo de implementação para a sua aplicação web. Por agora, apenas `ftp` é suportada, embora suporte para outros tipos de implementação é de desenvolvimento.
`<resources>` | Especifica os recursos e destinos de destino que utiliza o Maven quando implementar a sua tooAzure de aplicação web. Neste exemplo, dois `<resource>` elementos especificar que Maven irão implementar o ficheiro JAR de Olá para a sua aplicação web e Olá *Web. config* ficheiros do projeto de arranque de mola Olá.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Criar e implementar a sua tooAzure de aplicação web

Assim que tiver configurado o todas as definições de Olá no Olá precedente secções deste artigo, está pronto toodeploy sua tooAzure de aplicação web. toodo por isso, utilize Olá os seguintes passos:

1. Olá linha de comandos ou janela de terminal que estava a utilizar anteriormente, reconstrua o ficheiro JAR de Olá com o Maven se tiver efetuado quaisquer alterações toohello *pom.xml* ficheiro; por exemplo:
   ```shell
   mvn clean package
   ```

1. Implementar o tooAzure de aplicação web com o Maven; Por exemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven irá implementar a sua tooAzure de aplicação web; Se a aplicação web de Olá ainda não existir, será criado.

Quando a web tiver sido implementada, será capaz de toomanage-lo utilizando Olá [portal do Azure].

* A aplicação web será listada no **serviços aplicacionais**:

   ![Aplicação Web listada no portal do Azure serviços aplicacionais][AP01]

* E Olá URL para a sua aplicação web será listada no Olá **descrição geral** para a sua aplicação web:

   ![Determinar o URL de Olá para a sua aplicação web][AP02]

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá várias tecnologias abordadas neste artigo, consulte Olá seguintes artigos:

* [Plug-in do Maven para Web Apps do Azure]

* [Inicie sessão no tooAzure de Olá CLI do Azure](/azure/xplat-cli-connect)

* [Como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy um tooAzure de aplicação de arranque da mola](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Criar um Azure principal de serviço com o Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de definições do maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Interface de linha de comandos do Azure (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefícios de subscritor do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[mola arranque introdução]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in do Maven para Web Apps do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
