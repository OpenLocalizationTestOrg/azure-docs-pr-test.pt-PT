---
title: "aaaHow toouse Olá Plug-in do Maven para Web Apps do Azure toodeploy uma aplicação de arranque de mola no registo de contentor do Azure tooAzure do serviço de aplicações"
description: "Este tutorial irá guiá-lo embora Olá passos toodeploy uma aplicação de arranque de mola no registo de contentor do Azure tooAzure tooAzure do serviço de aplicações através da utilização de um plug-in do Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Como toouse hello Plug-in do Maven para Web Apps do Azure toodeploy uma aplicação de arranque de mola no registo de contentor do Azure tooAzure do serviço de aplicações

Olá  **[mola Framework]**  é uma arquitetura de open source popular, que ajuda os programadores de Java criar web, móveis e aplicações API. Este tutorial utiliza uma aplicação de exemplo criada utilizando [mola arranque], uma abordagem condicionada por Convenção para utilizar mola tooget a trabalhar rapidamente.

Este artigo demonstra como toodeploy tooAzure de aplicação de arranque a um exemplo registo de contentor e, em seguida, utilize hello Plug-in do Maven para Web Apps do Azure toodeploy tooAzure a aplicação do serviço de aplicações.

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
* A [Docker] cliente.

> [!NOTE]
>
> Devido a requisitos de Virtualização toohello deste tutorial, não pode seguir passos descritos neste artigo Olá numa máquina virtual; tem de utilizar um computador físico com funcionalidades de Virtualização ativadas.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Exemplo de Olá clone mola arranque na aplicação web de Docker

Nesta secção, clonar uma de aplicação de arranque de mola e testá-lo localmente.

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

1. Olá clone [arranque mola no Docker introdução] projeto de exemplo para o diretório de Olá criou; por exemplo:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. Altere o projeto do diretório toohello concluída; Por exemplo:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Deverá ver Olá seguir a mensagem apresentada: **Olá, mundo Docker**

   ![Procure a aplicação de exemplo localmente][SB01]

## <a name="create-an-azure-service-principal"></a>Criar um Azure principal de serviço

Nesta secção, vai criar um Azure principal de serviço que Olá utiliza de plug-in do Maven quando implementar a sua tooAzure de contentor.

1. Abra uma linha de comandos.

1. Inicie sessão na sua conta do Azure utilizando Olá CLI do Azure:
   ```azurecli
   az login
   ```
   Siga Olá instruções toocomplete Olá início de sessão no processo.

1. Crie um Azure principal de serviço:
   ```azurecli
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
   > Irá utilizar valores de Olá desta resposta JSON quando configurar Olá Maven Plug-in toodeploy tooAzure seu contentor. Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de marcador de posição, o que são utilizados em toomake este exemplo-lo mais fácil toomap estes valores tootheir respetivos elementos quando configura o Maven `settings.xml` ficheiros Olá seguinte secção.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Criar um registo de contentor do Azure utilizando Olá CLI do Azure

1. Abra uma linha de comandos.

1. Inicie sessão no tooyour conta do Azure:
   ```azurecli
   az login
   ```

1. Crie um grupo de recursos para Olá recursos do Azure que irá utilizar este artigo:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Substitua `wingtiptoysresources` neste exemplo, com um nome exclusivo para o grupo de recursos.

1. Crie um registo de contentor do Azure privado no grupo de recursos de Olá para a sua aplicação de arranque de mola: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Substitua `wingtiptoysregistry` neste exemplo, com um nome exclusivo para o registo de contentor.

1. Obter Olá palavra-passe para o registo do contentor:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure irá responder com a palavra-passe; Por exemplo:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Adicionar o registo de contentor do Azure e as definições de Maven principal tooyour de serviço do Azure

1. Abra o Maven `settings.xml` ficheiro num editor de texto; este ficheiro pode ser um caminho como Olá exemplos a seguir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Adicionar as definições de acesso do registo de contentor do Azure na secção anterior do Olá da toohello artigo `<servers>` coleção no Olá *settings.xml* ficheiro; por exemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<id>` | Contém o nome de Olá do seu registo de contentor do Azure privado.
   `<username>` | Contém o nome de Olá do seu registo de contentor do Azure privado.
   `<password>` | Contém a palavra-passe de Olá que obteve na secção anterior do Olá deste artigo.

1. Adicionar as definições de principal de serviço do Azure a partir de uma secção anterior deste artigo toohello `<servers>` coleção no Olá *settings.xml* ficheiro; por exemplo:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Compilar o Docker imagem do contentor e enviá-lo tooyour registo de contentor do Azure

1. Navegue (por exemplo, o diretório de projeto toohello concluída para a sua aplicação de arranque de mola "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra Olá *pom.xml* ficheiro com um editor de texto.

1. Olá atualização `<properties>` coleção no Olá *pom.xml* ficheiro com o valor de início de sessão hello do servidor para o registo de contentor do Azure na secção anterior do Olá deste tutorial; por exemplo:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<azure.containerRegistry>` | Especifica o nome de Olá do seu registo de contentor do Azure privado.
   `<docker.image.prefix>` | Especifica o URL de Olá do seu registo de contentor do Azure privado, que é derivado acrescentando ". azurecr.io" toohello nome do seu registo de contentor privada.

1. Certifique-se de que `<plugin>` de plug-in de Olá Docker no seu *pom.xml* ficheiro contém propriedades correto do Olá Olá início de sessão e registo de endereço do nome de servidor do passo anterior Olá neste tutorial. Por exemplo:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<serverId>` | Especifica a propriedade de Olá que contém o nome do seu registo de contentor do Azure privado.
   `<registryUrl>` | Especifica a propriedade de Olá que contém o URL de Olá do seu registo de contentor do Azure privado.

1. Navegue toohello concluída o diretório de projeto para a sua aplicação de arranque de mola e executar Olá seguintes aplicações do comando toorebuild Olá e push Olá contentor tooyour registo de contentor do Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

1. OPCIONAL: Procurar toohello [portal do Azure] e verifique se existe com o nome de imagem do contentor de Docker **gs-mola arranque docker** no seu registo de contentor.

   ![Certifique-se contentor no portal do Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Personalizar a sua pom.xml, em seguida, criar e implementar tooAzure o contentor

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Existem vários valores que pode modificar para o plug-in do Maven Olá e uma descrição detalhada para cada um destes elementos está disponível no Olá [Plug-in do Maven para Web Apps do Azure] documentação. Que a ser consiga aceder tal, existem vários valores, realçando neste artigo:

Elemento | Descrição
---|---|---
`<version>` | Especifica uma versão de Olá Olá [Plug-in do Maven para Web Apps do Azure]. Deve verificar a versão de Olá listada no Olá [Respository Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que está a utilizar Olá versão mais recente.
`<authentication>` | Especifica as informações de autenticação de Olá do Azure, que, neste exemplo, contém um `<serverId>` elemento que contenha `azure-auth`; Maven utiliza toolook esse valor dos valores de principal de serviço do Azure Olá no seu Maven *settings.xml* ficheiro, que é definida uma secção anterior deste artigo.
`<resourceGroup>` | Especifica o grupo de recursos do Olá destino, que é `wingtiptoysresources` neste exemplo. grupo de recursos de Olá será criado durante a implementação, se já existir.
`<appName>` | Especifica o nome de destino Olá para a sua aplicação web. Neste exemplo, é o nome de destino Olá `maven-linux-app-${maven.build.timestamp}`, em que hello `${maven.build.timestamp}` é acrescentado um sufixo neste conflito de tooavoid de exemplo. (Olá timestamp é opcional; pode especificar qualquer cadeia exclusiva para o nome da aplicação Olá).
`<region>` | Especifica a região de destino Olá, que, neste exemplo, é `westus`. (Uma lista completa está a ser Olá [Plug-in do Maven para Web Apps do Azure] documentação.)
`<containerSettings>` | Especifica as propriedades de Olá que contêm o nome de Olá e o URL do seu contentor.
`<appSettings>` | Especifica as definições de exclusivas para Maven toouse quando implementar a sua tooAzure de aplicação web. Neste exemplo, um `<property>` elemento contém um par nome/valor de elementos subordinados que especifique a porta de Olá para a sua aplicação.

> [!NOTE]
>
> número de porta do Olá definições toochange Olá neste exemplo, apenas são necessários quando está a alterar a porta de Olá da predefinição de Olá.
>

1. Olá linha de comandos ou janela de terminal que estava a utilizar anteriormente, reconstrua o ficheiro JAR de Olá com o Maven se tiver efetuado quaisquer alterações toohello *pom.xml* ficheiro; por exemplo:
   ```shell
   mvn clean package
   ```

1. Implementar o tooAzure de aplicação web com o Maven; Por exemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven irá implementar a sua tooAzure de aplicação web; Se a aplicação web de Olá ainda não existir, será criado.

> [!NOTE]
>
> Se região Olá que especificou nas Olá `<region>` elemento do seu *pom.xml* ficheiro não tem suficiente servidores disponíveis quando iniciar a implementação, poderá ver um erro toohello semelhante seguinte exemplo:
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Se isto acontecer, pode especificar que outra região e volte a executar Olá toodeploy de comando Maven a aplicação.
>
>

Quando a web tiver sido implementada, será capaz de toomanage-lo utilizando Olá [portal do Azure].

* A aplicação web será listada no **serviços aplicacionais**:

   ![Aplicação Web listada no portal do Azure serviços aplicacionais][AP01]

* E Olá URL para a sua aplicação web será listada no Olá **descrição geral** para a sua aplicação web:

   ![Determinar o URL de Olá para a sua aplicação web][AP02]

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá várias tecnologias abordadas neste artigo, consulte Olá seguintes artigos:

* [Plug-in do Maven para Web Apps do Azure]

* [Inicie sessão no tooAzure de Olá CLI do Azure](/azure/xplat-cli-connect)

* [Criar um Azure principal de serviço com o Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de definições do maven](https://maven.apache.org/settings.html)

* [Plug-in do docker para Maven]

<!-- URL List -->

[Interface de linha de comandos do Azure (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Plug-in do Maven para Web Apps do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in do docker para Maven]: https://github.com/spotify/docker-maven-plugin
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefícios de subscritor do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[mola arranque]: http://projects.spring.io/spring-boot/
[arranque mola no Docker introdução]: https://github.com/spring-guides/gs-spring-boot-docker
[mola Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
