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
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="9dda3-103">Criar a sua primeira aplicação Java Reliable Actors do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="9dda3-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dda3-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="9dda3-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="9dda3-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="9dda3-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="9dda3-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="9dda3-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="9dda3-107">Este guia de introdução ajuda-o a criar a sua primeira aplicação Java do Azure Service Fabric num ambiente de desenvolvimento do Linux em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9dda3-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="9dda3-108">Quando tiver terminado, terá uma aplicação de serviço única Java simples em execução no cluster de desenvolvimento local Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9dda3-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9dda3-109">Prerequisites</span></span>
<span data-ttu-id="9dda3-110">Antes de começar, instalar Olá SDK de Service Fabric, Olá CLI de recursos de infraestrutura de serviço e configurar um cluster de desenvolvimento no seu [ambiente de desenvolvimento do Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9dda3-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="9dda3-111">Se estiver a utilizar o Mac OS X, pode [configurar um ambiente de desenvolvimento do Linux numa máquina virtual com Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="9dda3-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="9dda3-112">Também convém tooinstall Olá [CLI de recursos de infraestrutura de serviço](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9dda3-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="9dda3-113">Instalar e configurar generators Olá para Java</span><span class="sxs-lookup"><span data-stu-id="9dda3-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="9dda3-114">O Service Fabric fornece ferramentas estruturais que irão ajudá-lo a criar uma aplicação Java do Service Fabric a partir do terminal, através do gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="9dda3-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="9dda3-115">Siga os passos de Olá abaixo tooensure que tiver gerador de modelo yeoman Olá Service Fabric para Java trabalhar no seu computador.</span><span class="sxs-lookup"><span data-stu-id="9dda3-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="9dda3-116">Instalar nodejs e NPM no seu computador</span><span class="sxs-lookup"><span data-stu-id="9dda3-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="9dda3-117">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) no seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="9dda3-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="9dda3-118">Instalar o gerador de aplicação de Service Fabric Yeo Java Olá de NPM</span><span class="sxs-lookup"><span data-stu-id="9dda3-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="9dda3-119">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="9dda3-119">Create hello application</span></span>
<span data-ttu-id="9dda3-120">Uma aplicação de Service Fabric contém um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="9dda3-121">gerador de Olá instalado na secção de último Olá, torna mais fácil toocreate seu próprio serviço e tooadd mais mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9dda3-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="9dda3-122">Também pode criar, construir e implementar aplicações Java do Service Fabric com um plug-in do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9dda3-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="9dda3-123">Veja [Criar e implementar a sua primeira aplicação Java com o Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9dda3-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="9dda3-124">Para este início rápido, utilize o Yeoman toocreate uma aplicação com um único serviço que armazena e obtém um valor de contador.</span><span class="sxs-lookup"><span data-stu-id="9dda3-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="9dda3-125">Num terminal, escreva ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="9dda3-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="9dda3-126">Dê um nome à aplicação.</span><span class="sxs-lookup"><span data-stu-id="9dda3-126">Name your application.</span></span>
3. <span data-ttu-id="9dda3-127">Escolha o tipo de Olá do seu primeiro serviço e nome.</span><span class="sxs-lookup"><span data-stu-id="9dda3-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="9dda3-128">Para este tutorial, escolha um Serviço Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="9dda3-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="9dda3-129">Para obter mais informações sobre Olá outros tipos de serviços, consulte [descrição geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="9dda3-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="9dda3-130">![Gerador Yeoman do Service Fabric para Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="9dda3-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="9dda3-131">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="9dda3-131">Build hello application</span></span>
<span data-ttu-id="9dda3-132">modelos de serviço Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que pode utilizar a aplicação Olá toobuild Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="9dda3-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="9dda3-133">As dependências Java do Service Fabric são obtidas do Maven.</span><span class="sxs-lookup"><span data-stu-id="9dda3-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="9dda3-134">toobuild e trabalho em aplicações de Java de recursos de infraestrutura do serviço de Olá, terá de tooensure que tiver JDK e Gradle instalado.</span><span class="sxs-lookup"><span data-stu-id="9dda3-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="9dda3-135">Se ainda não está instalado, pode executar Olá seguir tooinstall JDK(openjdk-8-jdk) e Gradle -</span><span class="sxs-lookup"><span data-stu-id="9dda3-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="9dda3-136">toobuild e pacote Olá aplicação, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9dda3-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="9dda3-137">Implementar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="9dda3-137">Deploy hello application</span></span>
<span data-ttu-id="9dda3-138">Uma vez que é criada a aplicação Olá, pode implementá-la toohello cluster local.</span><span class="sxs-lookup"><span data-stu-id="9dda3-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="9dda3-139">Ligue o cluster do Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="9dda3-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="9dda3-140">Script de instalação de execução Olá fornecida Olá modelo toocopy Olá arquivo de imagens do cluster de aplicação, pacote toohello, registar o tipo de aplicação Olá e criar uma instância da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="9dda3-141">Implementação da aplicação Olá incorporado é Olá mesmo como qualquer outra aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9dda3-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="9dda3-142">Consulte a documentação de Olá no [gerir uma aplicação de Service Fabric com Olá CLI de recursos de infraestrutura de serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="9dda3-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="9dda3-143">Comandos de toothese parâmetros podem ser encontrados em manifestos Olá gerado no interior do pacote de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="9dda3-144">Assim que tiver sido implementada a aplicação Olá, abra um browser e navegue para [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="9dda3-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="9dda3-145">Em seguida, expanda Olá **aplicações** nós e tenha em atenção que está agora uma entrada para o tipo de aplicação e outro para Olá primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="9dda3-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="9dda3-146">Iniciar o cliente de teste de Olá e efetuar uma ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="9dda3-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="9dda3-147">Atores não fazer nada, uma por si próprios, necessitam de outro toosend de serviço ou cliente mensagens-las.</span><span class="sxs-lookup"><span data-stu-id="9dda3-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="9dda3-148">modelo de ator Olá inclui um script de teste simples que pode utilizar toointeract com o serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="9dda3-149">Execute script de Olá utilizando Olá veja utilitário toosee Olá saída do serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="9dda3-150">script de teste de Olá chama Olá `setCountAsync()` chama o método no Olá ator tooincrement um contador, Olá `getCountAsync()` método no Olá ator tooget Olá novo valor e apresenta o valor toohello consola.</span><span class="sxs-lookup"><span data-stu-id="9dda3-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="9dda3-151">No Service Fabric Explorer, localize Olá nó alojamento Olá réplica primária para o serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="9dda3-152">Olá captura de ecrã abaixo, é nó 3.</span><span class="sxs-lookup"><span data-stu-id="9dda3-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="9dda3-153">Olá serviço primário réplica identificadores de leitura e operações de escrita.</span><span class="sxs-lookup"><span data-stu-id="9dda3-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="9dda3-154">As alterações no estado do serviço, em seguida, são replicadas toohello réplicas secundárias, em execução em nós 0 e 1, no ecrã de Olá captura abaixo.</span><span class="sxs-lookup"><span data-stu-id="9dda3-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Localizar a réplica primária Olá no Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="9dda3-156">No **nós**, clique com o nó de Olá encontrado no passo anterior Olá, em seguida, selecione **desativar (reiniciar)** no menu de Olá ações.</span><span class="sxs-lookup"><span data-stu-id="9dda3-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="9dda3-157">Esta ação reinicia nó Olá com réplica de serviço principal Olá e força uma tooone de ativação pós-falha das réplicas secundárias Olá em execução no outro nó.</span><span class="sxs-lookup"><span data-stu-id="9dda3-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="9dda3-158">Essa réplica secundária é promovida tooprimary, réplica secundária de outra é criada num nó diferente e começa a réplica primária Olá tootake operações de leitura/escrita.</span><span class="sxs-lookup"><span data-stu-id="9dda3-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="9dda3-159">Como reinicia o nó de Olá, veja o resultado de hello do cliente de teste de Olá e tenha em atenção que contador Olá continua tooincrement, apesar de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="9dda3-160">Remover aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="9dda3-160">Remove hello application</span></span>
<span data-ttu-id="9dda3-161">Utilizar script de desinstalação de Olá fornecido na instância da aplicação Olá modelo toodelete Olá, anular o registo do pacote de aplicação Olá e remover o pacote de aplicação Olá do cluster Olá arquivo de imagens.</span><span class="sxs-lookup"><span data-stu-id="9dda3-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="9dda3-162">No Explorador de recursos de infraestrutura de serviço que vê que aplicação Olá e tipo de aplicação já não são apresentados no Olá **aplicações** nós.</span><span class="sxs-lookup"><span data-stu-id="9dda3-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="9dda3-163">Bibliotecas Java do Service Fabric no Maven</span><span class="sxs-lookup"><span data-stu-id="9dda3-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="9dda3-164">As bibliotecas Java do Service Fabric foram alojadas no Maven.</span><span class="sxs-lookup"><span data-stu-id="9dda3-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="9dda3-165">Pode adicionar Olá dependências no Olá ``pom.xml`` ou ``build.gradle`` das suas bibliotecas de Service Fabric Java toouse projetos de **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="9dda3-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="9dda3-166">Atores</span><span class="sxs-lookup"><span data-stu-id="9dda3-166">Actors</span></span>

<span data-ttu-id="9dda3-167">Suporte de Reliable Actor do Service Fabric para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9dda3-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="9dda3-168">Serviços</span><span class="sxs-lookup"><span data-stu-id="9dda3-168">Services</span></span>

<span data-ttu-id="9dda3-169">Suporte de Serviço sem Estado do Service Fabric para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9dda3-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="9dda3-170">Outros</span><span class="sxs-lookup"><span data-stu-id="9dda3-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="9dda3-171">Transporte</span><span class="sxs-lookup"><span data-stu-id="9dda3-171">Transport</span></span>

<span data-ttu-id="9dda3-172">Suporte da camada de transporte para a aplicação Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9dda3-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="9dda3-173">Não é necessário adicionar tooexplicitly esta dependência tooyour Ator fiável ou aplicações de serviço, a menos que o programa na camada de transporte de Olá.</span><span class="sxs-lookup"><span data-stu-id="9dda3-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="9dda3-174">Suporte para o Fabric</span><span class="sxs-lookup"><span data-stu-id="9dda3-174">Fabric support</span></span>

<span data-ttu-id="9dda3-175">Suporte de nível de sistema para que a sua toonative Service Fabric runtime do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9dda3-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="9dda3-176">Não é necessário tooexplicitly adicionar esta dependência tooyour Ator fiável ou aplicações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9dda3-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="9dda3-177">Este obtém recuperado automaticamente do Maven, ao incluir Olá outras dependências acima.</span><span class="sxs-lookup"><span data-stu-id="9dda3-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="9dda3-178">Migrar antigo toobe de aplicações Java de recursos de infraestrutura de serviço utilizado com o Maven</span><span class="sxs-lookup"><span data-stu-id="9dda3-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="9dda3-179">Foi recentemente movido bibliotecas de Java de recursos de infraestrutura de serviço do repositório de tooMaven do SDK de Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9dda3-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="9dda3-180">Enquanto as aplicações novas Olá gerar a utilizar o Yeoman ou Eclipse, irá gerar projetos atualizados mais recente (que serão capaz de toowork com o Maven), pode atualizar o seu existente Service Fabric sem monitorização de estado ou aplicações de Java ator, o que estava a utilizar Olá serviço Recursos de infraestrutura Java SDK anteriormente, as dependências do Service Fabric Java de Olá toouse do Maven.</span><span class="sxs-lookup"><span data-stu-id="9dda3-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="9dda3-181">Siga os passos de Olá mencionados [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure a aplicação mais antiga funciona com o Maven.</span><span class="sxs-lookup"><span data-stu-id="9dda3-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dda3-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9dda3-182">Next steps</span></span>

* [<span data-ttu-id="9dda3-183">Create your first Service Fabric Java application on Linux using Eclipse (Criar a sua primeira aplicação Java do Service Fabric no Linux com o Eclipse)</span><span class="sxs-lookup"><span data-stu-id="9dda3-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="9dda3-184">Saiba mais sobre os Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="9dda3-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="9dda3-185">Interagir com clusters do Service Fabric através da Olá CLI de recursos de infraestrutura de serviço</span><span class="sxs-lookup"><span data-stu-id="9dda3-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="9dda3-186">Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="9dda3-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="9dda3-187">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9dda3-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
