---
title: "aaaCreate uma aplicação de Java do Azure Service Fabric reliable actors no Linux | Microsoft Docs"
description: "Saiba como toocreate e implementar uma aplicação de reliable actors Java Service Fabric em cinco minutos."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Criar a sua primeira aplicação Java Reliable Actors do Service Fabric no Linux
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Este guia de introdução ajuda-o a criar a sua primeira aplicação Java do Azure Service Fabric num ambiente de desenvolvimento do Linux em apenas alguns minutos.  Quando tiver terminado, terá uma aplicação de serviço única Java simples em execução no cluster de desenvolvimento local Olá.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, instalar Olá SDK de Service Fabric, Olá CLI de recursos de infraestrutura de serviço e configurar um cluster de desenvolvimento no seu [ambiente de desenvolvimento do Linux](service-fabric-get-started-linux.md). Se estiver a utilizar o Mac OS X, pode [configurar um ambiente de desenvolvimento do Linux numa máquina virtual com Vagrant](service-fabric-get-started-mac.md).

Também convém tooinstall Olá [CLI de recursos de infraestrutura de serviço](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Instalar e configurar generators Olá para Java
O Service Fabric fornece ferramentas estruturais que irão ajudá-lo a criar uma aplicação Java do Service Fabric a partir do terminal, através do gerador de modelos Yeoman. Siga os passos de Olá abaixo tooensure que tiver gerador de modelo yeoman Olá Service Fabric para Java trabalhar no seu computador.
1. Instalar nodejs e NPM no seu computador

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) no seu computador a partir do NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar o gerador de aplicação de Service Fabric Yeo Java Olá de NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Criar aplicação Olá
Uma aplicação de Service Fabric contém um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade da aplicação Olá. gerador de Olá instalado na secção de último Olá, torna mais fácil toocreate seu próprio serviço e tooadd mais mais tarde.  Também pode criar, construir e implementar aplicações Java do Service Fabric com um plug-in do Eclipse. Veja [Criar e implementar a sua primeira aplicação Java com o Eclipse](service-fabric-get-started-eclipse.md). Para este início rápido, utilize o Yeoman toocreate uma aplicação com um único serviço que armazena e obtém um valor de contador.

1. Num terminal, escreva ``yo azuresfjava``.
2. Dê um nome à aplicação.
3. Escolha o tipo de Olá do seu primeiro serviço e nome. Para este tutorial, escolha um Serviço Reliable Actor. Para obter mais informações sobre Olá outros tipos de serviços, consulte [descrição geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).
   ![Gerador Yeoman do Service Fabric para Java][sf-yeoman]

## <a name="build-hello-application"></a>Criar aplicação Olá
modelos de serviço Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que pode utilizar a aplicação Olá toobuild Olá terminal.
As dependências Java do Service Fabric são obtidas do Maven. toobuild e trabalho em aplicações de Java de recursos de infraestrutura do serviço de Olá, terá de tooensure que tiver JDK e Gradle instalado. Se ainda não está instalado, pode executar Olá seguir tooinstall JDK(openjdk-8-jdk) e Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild e pacote Olá aplicação, execute Olá seguinte:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Implementar a aplicação Olá
Uma vez que é criada a aplicação Olá, pode implementá-la toohello cluster local.

1. Ligue o cluster do Service Fabric local toohello.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Script de instalação de execução Olá fornecida Olá modelo toocopy Olá arquivo de imagens do cluster de aplicação, pacote toohello, registar o tipo de aplicação Olá e criar uma instância da aplicação Olá.

    ```bash
    ./install.sh
    ```

Implementação da aplicação Olá incorporado é Olá mesmo como qualquer outra aplicação de Service Fabric. Consulte a documentação de Olá no [gerir uma aplicação de Service Fabric com Olá CLI de recursos de infraestrutura de serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.

Comandos de toothese parâmetros podem ser encontrados em manifestos Olá gerado no interior do pacote de aplicação Olá.

Assim que tiver sido implementada a aplicação Olá, abra um browser e navegue para [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer).
Em seguida, expanda Olá **aplicações** nós e tenha em atenção que está agora uma entrada para o tipo de aplicação e outro para Olá primeira instância desse tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Iniciar o cliente de teste de Olá e efetuar uma ativação pós-falha
Atores não fazer nada, uma por si próprios, necessitam de outro toosend de serviço ou cliente mensagens-las. modelo de ator Olá inclui um script de teste simples que pode utilizar toointeract com o serviço de atores Olá.

1. Execute script de Olá utilizando Olá veja utilitário toosee Olá saída do serviço de atores Olá.  script de teste de Olá chama Olá `setCountAsync()` chama o método no Olá ator tooincrement um contador, Olá `getCountAsync()` método no Olá ator tooget Olá novo valor e apresenta o valor toohello consola.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. No Service Fabric Explorer, localize Olá nó alojamento Olá réplica primária para o serviço de atores Olá. Olá captura de ecrã abaixo, é nó 3. Olá serviço primário réplica identificadores de leitura e operações de escrita.  As alterações no estado do serviço, em seguida, são replicadas toohello réplicas secundárias, em execução em nós 0 e 1, no ecrã de Olá captura abaixo.

    ![Localizar a réplica primária Olá no Service Fabric Explorer][sfx-primary]

3. No **nós**, clique com o nó de Olá encontrado no passo anterior Olá, em seguida, selecione **desativar (reiniciar)** no menu de Olá ações. Esta ação reinicia nó Olá com réplica de serviço principal Olá e força uma tooone de ativação pós-falha das réplicas secundárias Olá em execução no outro nó.  Essa réplica secundária é promovida tooprimary, réplica secundária de outra é criada num nó diferente e começa a réplica primária Olá tootake operações de leitura/escrita. Como reinicia o nó de Olá, veja o resultado de hello do cliente de teste de Olá e tenha em atenção que contador Olá continua tooincrement, apesar de ativação pós-falha de Olá.

## <a name="remove-hello-application"></a>Remover aplicação Olá
Utilizar script de desinstalação de Olá fornecido na instância da aplicação Olá modelo toodelete Olá, anular o registo do pacote de aplicação Olá e remover o pacote de aplicação Olá do cluster Olá arquivo de imagens.

```bash
./uninstall.sh
```

No Explorador de recursos de infraestrutura de serviço que vê que aplicação Olá e tipo de aplicação já não são apresentados no Olá **aplicações** nós.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliotecas Java do Service Fabric no Maven
As bibliotecas Java do Service Fabric foram alojadas no Maven. Pode adicionar Olá dependências no Olá ``pom.xml`` ou ``build.gradle`` das suas bibliotecas de Service Fabric Java toouse projetos de **mavenCentral**.

### <a name="actors"></a>Atores

Suporte de Reliable Actor do Service Fabric para a sua aplicação.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Serviços

Suporte de Serviço sem Estado do Service Fabric para a sua aplicação.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Outros
#### <a name="transport"></a>Transporte

Suporte da camada de transporte para a aplicação Java do Service Fabric. Não é necessário adicionar tooexplicitly esta dependência tooyour Ator fiável ou aplicações de serviço, a menos que o programa na camada de transporte de Olá.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Suporte para o Fabric

Suporte de nível de sistema para que a sua toonative Service Fabric runtime do Service Fabric. Não é necessário tooexplicitly adicionar esta dependência tooyour Ator fiável ou aplicações de serviço. Este obtém recuperado automaticamente do Maven, ao incluir Olá outras dependências acima.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrar antigo toobe de aplicações Java de recursos de infraestrutura de serviço utilizado com o Maven
Foi recentemente movido bibliotecas de Java de recursos de infraestrutura de serviço do repositório de tooMaven do SDK de Java do Service Fabric. Enquanto as aplicações novas Olá gerar a utilizar o Yeoman ou Eclipse, irá gerar projetos atualizados mais recente (que serão capaz de toowork com o Maven), pode atualizar o seu existente Service Fabric sem monitorização de estado ou aplicações de Java ator, o que estava a utilizar Olá serviço Recursos de infraestrutura Java SDK anteriormente, as dependências do Service Fabric Java de Olá toouse do Maven. Siga os passos de Olá mencionados [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure a aplicação mais antiga funciona com o Maven.

## <a name="next-steps"></a>Passos seguintes

* [Create your first Service Fabric Java application on Linux using Eclipse (Criar a sua primeira aplicação Java do Service Fabric no Linux com o Eclipse)](service-fabric-get-started-eclipse.md)
* [Saiba mais sobre os Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interagir com clusters do Service Fabric através da Olá CLI de recursos de infraestrutura de serviço](service-fabric-cli.md)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
