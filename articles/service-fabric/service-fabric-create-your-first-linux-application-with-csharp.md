---
title: "aaaCreate sua primeira aplicação do Azure micro-serviços no Linux utilizando c# | Microsoft Docs"
description: "Criar e implementar uma aplicação do Service Fabric com C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="2b753-103">Criar a sua primeira aplicação do Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2b753-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b753-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="2b753-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="2b753-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="2b753-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="2b753-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="2b753-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="2b753-107">O Service Fabric disponibiliza SDKs para criar serviços no Linux em .NET Core e Java.</span><span class="sxs-lookup"><span data-stu-id="2b753-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="2b753-108">Neste tutorial, vamos ver como toocreate uma aplicação para Linux e compilação um serviço com a c# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="2b753-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b753-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2b753-109">Prerequisites</span></span>
<span data-ttu-id="2b753-110">Antes de começar, certifique-se de que [configurou o seu ambiente de desenvolvimento do Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2b753-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="2b753-111">Se estiver a utilizar o Mac OS X, pode [configurar um ambiente de uma caixa do Linux numa máquina virtual com Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="2b753-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="2b753-112">Também convém tooinstall Olá [CLI de recursos de infraestrutura de serviço](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2b753-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="2b753-113">Instalar e configurar generators Olá para CSharp</span><span class="sxs-lookup"><span data-stu-id="2b753-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="2b753-114">O Service Fabric fornece ferramentas estruturais que irão ajudá-lo a criar uma aplicação CSharp do Service Fabric a partir do terminal, através do gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="2b753-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="2b753-115">Siga os passos de Olá abaixo tooensure que tiver o gerador de modelo yeoman Olá Service Fabric para CSharp trabalhar no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2b753-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="2b753-116">Instalar nodejs e NPM no seu computador</span><span class="sxs-lookup"><span data-stu-id="2b753-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="2b753-117">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) no seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="2b753-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="2b753-118">Instalar o gerador de aplicação de Service Fabric Yeo Java Olá de NPM</span><span class="sxs-lookup"><span data-stu-id="2b753-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="2b753-119">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="2b753-119">Create hello application</span></span>
<span data-ttu-id="2b753-120">Uma aplicação de Service Fabric pode conter um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="2b753-121">Olá Service Fabric [Yeoman](http://yeoman.io/) gerador do CSharp, que instalou no último passo, torna mais fácil toocreate seu próprio serviço e tooadd mais mais tarde.</span><span class="sxs-lookup"><span data-stu-id="2b753-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="2b753-122">Vamos utilizar Yeoman toocreate uma aplicação com um único serviço.</span><span class="sxs-lookup"><span data-stu-id="2b753-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="2b753-123">Num terminal, escreva Olá toostart comando Criar andaime Olá os seguintes:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="2b753-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="2b753-124">Dê um nome à aplicação.</span><span class="sxs-lookup"><span data-stu-id="2b753-124">Name your application.</span></span>
3. <span data-ttu-id="2b753-125">Escolha o tipo de Olá do seu primeiro serviço e nome.</span><span class="sxs-lookup"><span data-stu-id="2b753-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="2b753-126">Para efeitos de Olá deste tutorial, vamos escolher um serviço de Atores fiável.</span><span class="sxs-lookup"><span data-stu-id="2b753-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Gerador Yeoman do Service Fabric para C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="2b753-128">Para obter mais informações sobre as opções de Olá, consulte [descrição geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="2b753-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="2b753-129">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="2b753-129">Build hello application</span></span>
<span data-ttu-id="2b753-130">os modelos de serviço Fabric Yeoman Olá incluem um script de compilação que pode utilizar a aplicação de Olá toobuild de Olá terminal (após navegar toohello pasta da aplicação).</span><span class="sxs-lookup"><span data-stu-id="2b753-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="2b753-131">Implementar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="2b753-131">Deploy hello application</span></span>

<span data-ttu-id="2b753-132">Uma vez que é criada a aplicação Olá, pode implementá-la toohello cluster local.</span><span class="sxs-lookup"><span data-stu-id="2b753-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="2b753-133">Ligue o cluster do Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="2b753-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="2b753-134">Script de instalação de execução Olá fornecida Olá modelo toocopy Olá arquivo de imagens do cluster de aplicação, pacote toohello, registar o tipo de aplicação Olá e criar uma instância da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="2b753-135">Implementação da aplicação Olá incorporado é Olá mesmo como qualquer outra aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2b753-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="2b753-136">Consulte a documentação de Olá no [gerir uma aplicação de Service Fabric com Olá CLI de recursos de infraestrutura de serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="2b753-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="2b753-137">Comandos de toothese parâmetros podem ser encontrados em manifestos Olá gerado no interior do pacote de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="2b753-138">Assim que tiver sido implementada a aplicação Olá, abra um browser e navegue para [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="2b753-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="2b753-139">Em seguida, expanda Olá **aplicações** nós e tenha em atenção que está agora uma entrada para o tipo de aplicação e outro para Olá primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="2b753-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="2b753-140">Iniciar o cliente de teste de Olá e efetuar uma ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="2b753-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="2b753-141">Os projetos de ator não fazem nada só por si.</span><span class="sxs-lookup"><span data-stu-id="2b753-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="2b753-142">Necessitam de outro toosend de serviço ou cliente mensagens-las.</span><span class="sxs-lookup"><span data-stu-id="2b753-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="2b753-143">modelo de ator Olá inclui um script de teste simples que pode utilizar toointeract com o serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="2b753-144">Execute script de Olá utilizando Olá veja utilitário toosee Olá saída do serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="2b753-145">No Service Fabric Explorer, localize o nó que aloja a réplica primária do Olá para o serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="2b753-146">Olá captura de ecrã abaixo, é nó 3.</span><span class="sxs-lookup"><span data-stu-id="2b753-146">In hello screenshot below, it is node 3.</span></span>

    ![Localizar a réplica primária Olá no Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="2b753-148">Clique com o nó de Olá encontrado no passo anterior Olá, em seguida, selecione **desativar (reiniciar)** no menu de Olá ações.</span><span class="sxs-lookup"><span data-stu-id="2b753-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="2b753-149">Esta ação reinicia um nó do cluster local forçar uma réplica secundária de ativação pós-falha tooa em execução no outro nó.</span><span class="sxs-lookup"><span data-stu-id="2b753-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="2b753-150">Como efetuar esta ação, paga saída de toohello atenção do cliente de teste de Olá e tenha em atenção que contador Olá continua tooincrement, apesar de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="2b753-151">Adicionar mais serviços tooan aplicação existente</span><span class="sxs-lookup"><span data-stu-id="2b753-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="2b753-152">tooadd outra tooan aplicação de serviço já criadas utilizando `yo`, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2b753-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="2b753-153">Alterar a raiz de toohello do diretório da aplicação existente Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="2b753-154">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é aplicação Olá criada pelo Yeoman.</span><span class="sxs-lookup"><span data-stu-id="2b753-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="2b753-155">Execute `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="2b753-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="2b753-156">Migrar do project.json too.csproj</span><span class="sxs-lookup"><span data-stu-id="2b753-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="2b753-157">Executar 'dotnet migrar' no diretório de raiz do projeto irá migrar todos os formato de toocsproj de project.json Olá.</span><span class="sxs-lookup"><span data-stu-id="2b753-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="2b753-158">Projeto de Olá de atualização em conformidade referencia toocsproj ficheiros nos ficheiros de projeto.</span><span class="sxs-lookup"><span data-stu-id="2b753-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="2b753-159">Atualize ficheiros toocsproj nomes de ficheiro de projeto de Olá no build.sh.</span><span class="sxs-lookup"><span data-stu-id="2b753-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b753-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2b753-160">Next steps</span></span>

* [<span data-ttu-id="2b753-161">Saiba mais sobre os Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2b753-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="2b753-162">Interagir com clusters do Service Fabric através da Olá CLI de recursos de infraestrutura de serviço</span><span class="sxs-lookup"><span data-stu-id="2b753-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="2b753-163">Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="2b753-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="2b753-164">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2b753-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
