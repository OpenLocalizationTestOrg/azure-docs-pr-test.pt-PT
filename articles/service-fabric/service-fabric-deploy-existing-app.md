---
title: "aaaDeploy um tooAzure executável existente Service Fabric | Microsoft Docs"
description: "Obter instruções sobre como toopackage uma aplicação existente como um executável de convidado, pelo que pode ser implementado tooa cluster do Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="c21a5-103">Implementar um tooService executável convidado recursos de infraestrutura</span><span class="sxs-lookup"><span data-stu-id="c21a5-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="c21a5-104">Pode executar qualquer tipo de código, tal como o Node.js, Java ou C++ no Service Fabric do Azure como um serviço.</span><span class="sxs-lookup"><span data-stu-id="c21a5-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="c21a5-105">Service Fabric refere-se os tipos de toothese de serviços como convidado executáveis.</span><span class="sxs-lookup"><span data-stu-id="c21a5-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="c21a5-106">Executáveis de convidado são tratadas pelo serviço de recursos de infraestrutura, como serviços sem monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="c21a5-107">Como resultado, são colocadas em nós num cluster, com base na disponibilidade e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="c21a5-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="c21a5-108">Este artigo descreve como toopackage e implementar um cluster de Service Fabric tooa executável do convidado, utilizando o Visual Studio ou um utilitário da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="c21a5-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="c21a5-109">Neste artigo, iremos abranger Olá passos toopackage um convidado executável e implementá-la tooService recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="c21a5-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="c21a5-110">Benefícios da execução de um convidado executável no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c21a5-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="c21a5-111">Existem várias vantagens toorunning um convidado executável num cluster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="c21a5-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="c21a5-112">Elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c21a5-112">High availability.</span></span> <span data-ttu-id="c21a5-113">Aplicações executadas no Service Fabric que são efetuadas altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c21a5-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="c21a5-114">Service Fabric assegura que as instâncias de uma aplicação estão em execução.</span><span class="sxs-lookup"><span data-stu-id="c21a5-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="c21a5-115">Monitorização de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="c21a5-115">Health monitoring.</span></span> <span data-ttu-id="c21a5-116">Monitorização de estado de funcionamento do Service Fabric Deteta se uma aplicação está em execução e fornece informações de diagnóstico, se ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="c21a5-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="c21a5-117">Gestão de ciclo de vida de aplicações.</span><span class="sxs-lookup"><span data-stu-id="c21a5-117">Application lifecycle management.</span></span> <span data-ttu-id="c21a5-118">Para além de fornecer atualizações sem período de indisponibilidade, Service Fabric fornece a versão anterior do toohello Reversão automática se ocorrer um evento de estado de funcionamento incorreto comunicado durante uma atualização.</span><span class="sxs-lookup"><span data-stu-id="c21a5-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="c21a5-119">Densidade.</span><span class="sxs-lookup"><span data-stu-id="c21a5-119">Density.</span></span> <span data-ttu-id="c21a5-120">Pode executar várias aplicações num cluster, eliminando a necessidade de Olá de cada toorun de aplicação no seu próprio hardware.</span><span class="sxs-lookup"><span data-stu-id="c21a5-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="c21a5-121">Capacidade de Deteção: Utilizar REST pode chamar Olá Service Fabric Naming service toofind outros serviços no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="c21a5-122">Amostras</span><span class="sxs-lookup"><span data-stu-id="c21a5-122">Samples</span></span>
* [<span data-ttu-id="c21a5-123">Exemplo de empacotamento e implementação de um executável de convidado</span><span class="sxs-lookup"><span data-stu-id="c21a5-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="c21a5-124">Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST</span><span class="sxs-lookup"><span data-stu-id="c21a5-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="c21a5-125">Descrição geral da aplicação e ficheiros de manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="c21a5-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="c21a5-126">Como parte da implementação de um executável de convidado, é empacotamento de Service Fabric toounderstand útil Olá e modelo de implementação, tal como descrito no [modelo de aplicação](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="c21a5-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="c21a5-127">modelo de empacotamento de Service Fabric Olá baseia-se em dois ficheiros XML: Olá manifestos de aplicação e serviços.</span><span class="sxs-lookup"><span data-stu-id="c21a5-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="c21a5-128">Olá definição de esquema para a hello ficheiros ApplicationManifest.xml e ServiceManifest.xml com Olá SDK de Service Fabric para *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="c21a5-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="c21a5-129">**O manifesto da aplicação** manifesto da aplicação Olá é utilizado toodescribe Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="c21a5-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="c21a5-130">Lista os serviços de Olá que compõem-lo e outros parâmetros que são utilizado toodefine devem ser implementados como um ou mais serviços, tais como o número de Olá de instâncias.</span><span class="sxs-lookup"><span data-stu-id="c21a5-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="c21a5-131">No Service Fabric, uma aplicação é uma unidade de implementação e a atualização.</span><span class="sxs-lookup"><span data-stu-id="c21a5-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="c21a5-132">É possível atualizar uma aplicação como uma única unidade em que é geridos os potenciais falhas e reverte potenciais.</span><span class="sxs-lookup"><span data-stu-id="c21a5-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="c21a5-133">Service Fabric garante que os processo de atualização de Olá é efetuada com êxito, ou, se Olá atualização falhar, não deixe a Olá aplicação num Estado desconhecido ou instável.</span><span class="sxs-lookup"><span data-stu-id="c21a5-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="c21a5-134">**O manifesto do serviço** manifesto do serviço de Olá descreve Olá os componentes de um serviço.</span><span class="sxs-lookup"><span data-stu-id="c21a5-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="c21a5-135">Inclui dados, tais como o nome de Olá e tipo de serviço e o código e a configuração.</span><span class="sxs-lookup"><span data-stu-id="c21a5-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="c21a5-136">Olá manifesto do serviço também inclui alguns parâmetros adicionais que podem ser utilizados o serviço de Olá tooconfigure assim que for implementado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="c21a5-137">Estrutura de ficheiros do pacote de aplicação</span><span class="sxs-lookup"><span data-stu-id="c21a5-137">Application package file structure</span></span>
<span data-ttu-id="c21a5-138">toodeploy tooService uma aplicação dos recursos de infraestrutura, aplicação Olá deve seguir a estrutura de diretórios predefinidos.</span><span class="sxs-lookup"><span data-stu-id="c21a5-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="c21a5-139">Olá segue-se um exemplo dessa estrutura.</span><span class="sxs-lookup"><span data-stu-id="c21a5-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="c21a5-140">Olá ApplicationPackageRoot contém ficheiros de ApplicationManifest.xml Olá que define a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="c21a5-141">Um subdiretório para cada serviço incluído na aplicação Olá é utilizado toocontain Olá todos os artefactos Olá serviço necessita.</span><span class="sxs-lookup"><span data-stu-id="c21a5-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="c21a5-142">Estes subdiretórios são Olá ServiceManifest.xml e, normalmente, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="c21a5-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="c21a5-143">*Código*.</span><span class="sxs-lookup"><span data-stu-id="c21a5-143">*Code*.</span></span> <span data-ttu-id="c21a5-144">Este diretório contém o código do serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="c21a5-145">*Configuração*. Este diretório contém um ficheiro de Settings.xml (e outros ficheiros, se necessário) que o serviço de Olá consegue aceder às definições de configuração específicas de tooretrieve de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c21a5-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="c21a5-146">*Dados*.</span><span class="sxs-lookup"><span data-stu-id="c21a5-146">*Data*.</span></span> <span data-ttu-id="c21a5-147">Este é um diretório adicional toostore local dados adicionais que poderá ter o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="c21a5-148">Dados devem estar dados apenas efémeras toostore utilizados.</span><span class="sxs-lookup"><span data-stu-id="c21a5-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="c21a5-149">Service Fabric efetua uma cópia não replicar as alterações toohello dados diretório ou se precisa de serviço Olá toobe relocalizada (por exemplo, durante a ativação pós-falha).</span><span class="sxs-lookup"><span data-stu-id="c21a5-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="c21a5-150">Não tem toocreate Olá `config` e `data` diretórios se não precisar deles.</span><span class="sxs-lookup"><span data-stu-id="c21a5-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="c21a5-151">Pacote de um executável existente</span><span class="sxs-lookup"><span data-stu-id="c21a5-151">Package an existing executable</span></span>
<span data-ttu-id="c21a5-152">Quando empacotamento um executável de convidado, pode escolher qualquer toouse um modelo de projeto do Visual Studio ou demasiado[criar manualmente o pacote de aplicação Olá](#manually).</span><span class="sxs-lookup"><span data-stu-id="c21a5-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="c21a5-153">Com o Visual Studio, Olá a estrutura do pacote de aplicação e ficheiros de manifesto são criados pelo modelo de projeto novo Olá para si.</span><span class="sxs-lookup"><span data-stu-id="c21a5-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="c21a5-154">Olá toopackage da forma mais fácil um executável para um serviço existentes do Windows é toouse Visual Studio e em Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="c21a5-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="c21a5-155">Utilizar o Visual Studio toopackage e implementar um executável existente</span><span class="sxs-lookup"><span data-stu-id="c21a5-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="c21a5-156">O Visual Studio fornece uma infraestrutura de serviço toohelp de modelo de serviço implementar um cluster convidado do Service Fabric tooa executável.</span><span class="sxs-lookup"><span data-stu-id="c21a5-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="c21a5-157">Escolha **ficheiro** > **novo projeto**e crie uma aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c21a5-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="c21a5-158">Escolha **convidado executável** como modelo de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="c21a5-159">Clique em **procurar** pasta de Olá tooselect com os seus executável e preencha rest Olá do serviço de Olá Olá parâmetros toocreate.</span><span class="sxs-lookup"><span data-stu-id="c21a5-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="c21a5-160">*Comportamento de pacote de código*.</span><span class="sxs-lookup"><span data-stu-id="c21a5-160">*Code Package Behavior*.</span></span> <span data-ttu-id="c21a5-161">Pode ser conjunto toocopy todo o conteúdo de Olá do seu toohello pasta projeto do Visual Studio, que é útil se Olá executável não se altera.</span><span class="sxs-lookup"><span data-stu-id="c21a5-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="c21a5-162">Se esperar toochange executável Olá e quiser Olá capacidade toopick cópias de segurança novas compilações dinamicamente, pode escolher toolink toohello pasta em vez disso.</span><span class="sxs-lookup"><span data-stu-id="c21a5-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="c21a5-163">Pode utilizar as pastas de ligado ao criar o projeto de aplicação Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c21a5-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="c21a5-164">Esta ação liga a localização de origem toohello de dentro do projeto de Olá, tornando possíveis para tooupdate Olá convidado executável no respetivo destino de origem.</span><span class="sxs-lookup"><span data-stu-id="c21a5-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="c21a5-165">Essas atualizações passam a fazer parte do pacote de aplicação Olá na compilação.</span><span class="sxs-lookup"><span data-stu-id="c21a5-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="c21a5-166">*Programa* Especifica executável Olá que deve ser executado o serviço de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="c21a5-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="c21a5-167">*Argumentos* Especifica Olá argumentos que devem ser transmitidos toohello executável.</span><span class="sxs-lookup"><span data-stu-id="c21a5-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="c21a5-168">Pode ser uma lista de parâmetros com argumentos.</span><span class="sxs-lookup"><span data-stu-id="c21a5-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="c21a5-169">*WorkingFolder* Especifica o diretório de trabalho de Olá para o processo de Olá que vai toobe foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="c21a5-170">Pode especificar três valores:</span><span class="sxs-lookup"><span data-stu-id="c21a5-170">You can specify three values:</span></span>
     * <span data-ttu-id="c21a5-171">`CodeBase`Especifica o diretório de trabalho que Olá vai toobe definir o diretório de código toohello no pacote de aplicação Olá (`Code` directory apresentados no Olá anterior a estrutura de ficheiros).</span><span class="sxs-lookup"><span data-stu-id="c21a5-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="c21a5-172">`CodePackage`Especifica o diretório de trabalho que Olá vai toobe definir toohello raiz Olá do pacote de aplicação (`GuestService1Pkg` mostrado na Olá anterior a estrutura de ficheiros).</span><span class="sxs-lookup"><span data-stu-id="c21a5-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="c21a5-173">`Work`Especifica que os ficheiros de Olá são colocados num subdiretório chamado trabalho.</span><span class="sxs-lookup"><span data-stu-id="c21a5-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="c21a5-174">Dê um nome ao serviço e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c21a5-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="c21a5-175">Se o serviço precisa de um ponto final para a comunicação, agora pode adicionar Olá protocolo, porta e ficheiros do tipo toohello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c21a5-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="c21a5-176">Por exemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="c21a5-177">Agora pode utilizar o pacote de Olá e publique ação contra o seu cluster local através da depuração solução Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c21a5-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="c21a5-178">Quando estiver pronto, pode publicar cluster remoto do Olá aplicação tooa ou verifique no controlo de toosource Olá solução.</span><span class="sxs-lookup"><span data-stu-id="c21a5-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="c21a5-179">Aceda a fim de toohello do toosee artigo como tooview o serviço de executável de convidado em execução no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c21a5-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="c21a5-180">Utilizar Yoeman toopackage e implementar um executável existente no Linux</span><span class="sxs-lookup"><span data-stu-id="c21a5-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="c21a5-181">procedimento Olá para criar e implementar um convidado executável no Linux é Olá igual ao implementar uma aplicação csharp ou java.</span><span class="sxs-lookup"><span data-stu-id="c21a5-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="c21a5-182">Num terminal, escreva `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="c21a5-183">Dê um nome à aplicação.</span><span class="sxs-lookup"><span data-stu-id="c21a5-183">Name your application.</span></span>
3. <span data-ttu-id="c21a5-184">Nome do seu serviço e forneça detalhes Olá, incluindo o caminho de Olá executável e parâmetros de Olá que tem de ser invocado com.</span><span class="sxs-lookup"><span data-stu-id="c21a5-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="c21a5-185">Yeoman cria um pacote de aplicação com a aplicação apropriada Olá e ficheiros de manifesto juntamente com instalar e desinstalar scripts.</span><span class="sxs-lookup"><span data-stu-id="c21a5-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="c21a5-186">Manualmente o pacote e implementar um executável existente</span><span class="sxs-lookup"><span data-stu-id="c21a5-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="c21a5-187">processo de Olá de empacotamento manualmente um executável de convidado é baseado no Olá os seguintes passos gerais:</span><span class="sxs-lookup"><span data-stu-id="c21a5-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="c21a5-188">Crie a estrutura de diretórios do pacote de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="c21a5-189">Adicione ficheiros de código e a configuração da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="c21a5-190">Edite o ficheiro de manifesto do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="c21a5-191">Edite o ficheiro de manifesto da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="c21a5-192">Criar a estrutura de diretórios do pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="c21a5-192">Create hello package directory structure</span></span>
<span data-ttu-id="c21a5-193">Pode começar por criar a estrutura de diretórios Olá, conforme descrito em Olá anterior a secção, "Aplicação pacote estrutura de ficheiros."</span><span class="sxs-lookup"><span data-stu-id="c21a5-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="c21a5-194">Adicionar ficheiros de código e a configuração da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c21a5-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="c21a5-195">Depois de ter criado a estrutura de diretórios Olá, pode adicionar os ficheiros de código e a configuração da aplicação Olá em diretórios Olá de configuração e de código.</span><span class="sxs-lookup"><span data-stu-id="c21a5-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="c21a5-196">Também pode criar diretórios adicionais ou subdiretórios diretórios Olá de configuração ou de código.</span><span class="sxs-lookup"><span data-stu-id="c21a5-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="c21a5-197">Service Fabric um `xcopy` de conteúdo de Olá Olá aplicação raiz do diretório de, pelo que não existe nenhum toouse estrutura predefinidas que não sejam de criação de dois diretórios superiores, o código e definições.</span><span class="sxs-lookup"><span data-stu-id="c21a5-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="c21a5-198">(Pode escolher nomes diferentes se pretender.</span><span class="sxs-lookup"><span data-stu-id="c21a5-198">(You can pick different names if you want.</span></span> <span data-ttu-id="c21a5-199">Obter mais detalhes estão na secção seguinte, Olá).</span><span class="sxs-lookup"><span data-stu-id="c21a5-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="c21a5-200">Certifique-se de que inclui todos os ficheiros de Olá e dependências Olá necessidades de aplicação.</span><span class="sxs-lookup"><span data-stu-id="c21a5-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="c21a5-201">Service Fabric copia Olá conteúdo do pacote de aplicação Olá em todos os nós no cluster de olá onde os serviços da aplicação Olá são toobe contínuo implementado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="c21a5-202">pacote de Olá deve conter todo o código Olá que aplicação Olá tem toorun.</span><span class="sxs-lookup"><span data-stu-id="c21a5-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="c21a5-203">Não parta do princípio que dependências Olá já estão instaladas.</span><span class="sxs-lookup"><span data-stu-id="c21a5-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="c21a5-204">Editar o ficheiro de manifesto do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="c21a5-204">Edit hello service manifest file</span></span>
<span data-ttu-id="c21a5-205">Olá passo seguinte consiste nas Olá de tooinclude serviço de Olá do tooedit ficheiro de manifesto seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c21a5-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="c21a5-206">nome de Olá Olá do tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="c21a5-206">hello name of hello service type.</span></span> <span data-ttu-id="c21a5-207">Este é um ID que o Service Fabric utiliza tooidentify um serviço.</span><span class="sxs-lookup"><span data-stu-id="c21a5-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="c21a5-208">Olá comando toouse toolaunch Olá aplicação (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="c21a5-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="c21a5-209">Qualquer script que necessita de tooset toobe executar cópias de segurança aplicação Olá (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="c21a5-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="c21a5-210">Olá segue-se um exemplo de um `ServiceManifest.xml` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="c21a5-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="c21a5-211">Olá secções a seguir abordar as diferentes partes Olá do ficheiro de Olá terá tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c21a5-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="c21a5-212">Atualizar ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="c21a5-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="c21a5-213">Pode escolher qualquer nome que pretende para `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="c21a5-214">valor de Olá é utilizado no Olá `ApplicationManifest.xml` tooidentify Olá serviço ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c21a5-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="c21a5-215">Especifique `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="c21a5-216">Este atributo indica ao Service Fabric que o serviço de Olá baseia-se numa aplicação autónomo, pelo que necessita de todos os recursos de infraestrutura de serviço toodo é toolaunch-o como um processo e monitorizar o estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="c21a5-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="c21a5-217">Atualizar o CodePackage</span><span class="sxs-lookup"><span data-stu-id="c21a5-217">Update CodePackage</span></span>
<span data-ttu-id="c21a5-218">elemento de CodePackage Olá Especifica a localização de Olá (e versão) de código do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="c21a5-219">Olá `Name` elemento é o nome de Olá de toospecify utilizado do diretório de Olá no pacote de aplicação Olá que contém o código do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="c21a5-220">`CodePackage`Também tem Olá `version` atributo.</span><span class="sxs-lookup"><span data-stu-id="c21a5-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="c21a5-221">Isto pode ser utilizado toospecify Olá versão de código Olá e potencialmente também pode ser utilizado o código do serviço de Olá tooupgrade utilizando a infraestrutura de gestão de ciclo de vida de aplicação Olá no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c21a5-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="c21a5-222">Opcional: SetupEntrypoint de atualização</span><span class="sxs-lookup"><span data-stu-id="c21a5-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="c21a5-223">elemento de SetupEntryPoint Olá é toospecify utilizada qualquer ficheiro executável ou lote que deve ser executado antes do código do serviço de Olá for iniciado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="c21a5-224">Este passo é opcional, pelo que não é necessário toobe incluído se não houver nenhuma necessária inicialização.</span><span class="sxs-lookup"><span data-stu-id="c21a5-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="c21a5-225">Olá SetupEntryPoint é executada sempre que o serviço de Olá for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="c21a5-226">Não há SetupEntryPoint apenas uma, por isso, scripts de configuração precisam toobe agrupada num ficheiro batch único se a configuração da aplicação Olá necessitar de vários scripts.</span><span class="sxs-lookup"><span data-stu-id="c21a5-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="c21a5-227">Olá SetupEntryPoint pode executar qualquer tipo de ficheiro: ficheiros executáveis, ficheiros batch e cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c21a5-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="c21a5-228">Para obter mais detalhes, consulte [configurar SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="c21a5-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="c21a5-229">No Olá anterior exemplo, Olá SetupEntryPoint executa um ficheiro batch chamado `LaunchConfig.cmd` que está localizado no Olá `scripts` subdiretório do diretório de código Olá (partindo do princípio de elemento de WorkingFolder Olá está definido tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="c21a5-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="c21a5-230">Atualizar o ponto de entrada</span><span class="sxs-lookup"><span data-stu-id="c21a5-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="c21a5-231">Olá `EntryPoint` elemento no ficheiro de manifesto do serviço de Olá é toospecify utilizado como serviço de Olá toolaunch.</span><span class="sxs-lookup"><span data-stu-id="c21a5-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="c21a5-232">Olá `ExeHost` elemento Especifica Olá executável (e os argumentos) que deve ser utilizado o serviço de Olá toolaunch.</span><span class="sxs-lookup"><span data-stu-id="c21a5-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="c21a5-233">`Program`Especifica o nome de Olá do executável de Olá que deve iniciar o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="c21a5-234">`Arguments`Especifica os argumentos de Olá que devem ser transmitidos toohello executável.</span><span class="sxs-lookup"><span data-stu-id="c21a5-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="c21a5-235">Pode ser uma lista de parâmetros com argumentos.</span><span class="sxs-lookup"><span data-stu-id="c21a5-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="c21a5-236">`WorkingFolder`Especifica o diretório de trabalho de Olá para o processo de Olá que vai toobe foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="c21a5-237">Pode especificar três valores:</span><span class="sxs-lookup"><span data-stu-id="c21a5-237">You can specify three values:</span></span>
  * <span data-ttu-id="c21a5-238">`CodeBase`Especifica o diretório de trabalho que Olá vai toobe definir o diretório de código toohello no pacote de aplicação Olá (`Code` diretório no Olá anterior a estrutura de ficheiros).</span><span class="sxs-lookup"><span data-stu-id="c21a5-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="c21a5-239">`CodePackage`Especifica o diretório de trabalho que Olá vai toobe definir toohello raiz Olá do pacote de aplicação (`GuestService1Pkg` no Olá anterior a estrutura de ficheiros).</span><span class="sxs-lookup"><span data-stu-id="c21a5-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="c21a5-240">`Work`Especifica que os ficheiros de Olá são colocados num subdiretório chamado trabalho.</span><span class="sxs-lookup"><span data-stu-id="c21a5-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="c21a5-241">Olá WorkingFolder é o diretório de trabalho correto Olá tooset útil para que os caminhos relativos podem ser utilizados por qualquer um dos scripts de aplicação ou inicialização Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="c21a5-242">Atualizar pontos finais e registar com o serviço de nomenclatura para comunicação</span><span class="sxs-lookup"><span data-stu-id="c21a5-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="c21a5-243">No Olá anterior exemplo, Olá `Endpoint` elemento Especifica pontos finais de Olá que aplicação Olá pode escutar.</span><span class="sxs-lookup"><span data-stu-id="c21a5-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="c21a5-244">Neste exemplo, Olá aplicação Node.js escuta de http na porta 3000.</span><span class="sxs-lookup"><span data-stu-id="c21a5-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="c21a5-245">Além disso pode pedir ao Service Fabric toopublish este toohello ponto final de serviço de nomes para que outros serviços podem detetar o serviço de toothis de endereço de ponto final de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="c21a5-246">Isto permite-lhe toobe toocommunicate capaz de entre os serviços convidados executáveis.</span><span class="sxs-lookup"><span data-stu-id="c21a5-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="c21a5-247">Olá endereço do ponto final publicada é de formulário Olá `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="c21a5-248">`UriScheme`e `PathSuffix` são atributos opcionais.</span><span class="sxs-lookup"><span data-stu-id="c21a5-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="c21a5-249">`IPAddressOrFQDN`é Olá endereço IP ou nome de domínio completamente qualificado do nó de Olá este ficheiro executável obtém colocado e esta é calculada para si.</span><span class="sxs-lookup"><span data-stu-id="c21a5-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="c21a5-250">No hello exemplo seguinte, uma vez serviço de Olá é implementado, no Service Fabric Explorer verá um ponto final semelhante demasiado`http://10.1.4.92:3000/myapp/` publicados para a instância de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="c21a5-251">Ou se se tratar de um computador local, consulte `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="c21a5-252">Pode utilizar estes endereços com [proxy inverso](service-fabric-reverseproxy.md) toocommunicate entre serviços.</span><span class="sxs-lookup"><span data-stu-id="c21a5-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="c21a5-253">Editar o ficheiro de manifesto da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c21a5-253">Edit hello application manifest file</span></span>
<span data-ttu-id="c21a5-254">Assim que tiver configurado Olá `Servicemanifest.xml` ficheiro, terá de toomake toohello algumas alterações `ApplicationManifest.xml` ficheiro tooensure Olá são utilizados o tipo de serviço e o nome correto.</span><span class="sxs-lookup"><span data-stu-id="c21a5-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="c21a5-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="c21a5-255">ServiceManifestImport</span></span>
<span data-ttu-id="c21a5-256">No Olá `ServiceManifestImport` elemento, pode especificar um ou mais serviços que pretende que o tooinclude na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="c21a5-257">Os serviços são referenciados com `ServiceManifestName`, que especifica o nome de Olá do diretório de olá onde hello `ServiceManifest.xml` está localizado o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c21a5-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="c21a5-258">Configurar o registo</span><span class="sxs-lookup"><span data-stu-id="c21a5-258">Set up logging</span></span>
<span data-ttu-id="c21a5-259">Para executáveis de convidado, é útil toobe toosee capaz de consola registos toofind enviados se scripts de configuração e aplicação Olá mostram erros.</span><span class="sxs-lookup"><span data-stu-id="c21a5-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="c21a5-260">Redirecionamento de consola pode ser configurado no Olá `ServiceManifest.xml` ficheiro utilizando Olá `ConsoleRedirection` elemento.</span><span class="sxs-lookup"><span data-stu-id="c21a5-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="c21a5-261">Nunca utilize a política de redirecionamento de consola Olá numa aplicação que é implementada na produção porque isto pode afetar Olá ativação pós-falha de aplicação.</span><span class="sxs-lookup"><span data-stu-id="c21a5-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="c21a5-262">*Apenas* utilizá-lo para o desenvolvimento local e fins de depuração.</span><span class="sxs-lookup"><span data-stu-id="c21a5-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="c21a5-263">`ConsoleRedirection`pode ser o diretório de trabalho de tooa de saída (stdout e stderr) consola tooredirect utilizados.</span><span class="sxs-lookup"><span data-stu-id="c21a5-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="c21a5-264">Esta opção fornece Olá capacidade tooverify se não existirem erros durante a configuração de Olá ou execução da aplicação Olá no cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="c21a5-265">`FileRetentionCount`Determina quantos ficheiros são guardados no diretório de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="c21a5-266">Um valor de 5, por exemplo, significa que os ficheiros de registo de Olá para execuções de cinco anterior Olá são armazenados no diretório de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="c21a5-267">`FileMaxSizeInKb`Especifica o tamanho máximo do Olá Olá dos ficheiros de registo.</span><span class="sxs-lookup"><span data-stu-id="c21a5-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="c21a5-268">Ficheiros de registo são guardados dos diretórios de trabalho do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="c21a5-269">toodetermine onde estão localizados, ficheiros de Olá utilizar toodetermine de Service Fabric Explorer, o serviço de Olá do nó está em execução e o diretório de trabalho está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="c21a5-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="c21a5-270">Este processo é descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c21a5-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="c21a5-271">Implementação</span><span class="sxs-lookup"><span data-stu-id="c21a5-271">Deployment</span></span>
<span data-ttu-id="c21a5-272">último passo de Olá é demasiado[implementar a sua aplicação](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c21a5-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="c21a5-273">Olá a seguir mostra de script do PowerShell como toodeploy o cluster de desenvolvimento local toohello de aplicação e inicie um novo serviço de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c21a5-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="c21a5-274">[Comprimir pacote Olá](service-fabric-package-apps.md#compress-a-package) antes de copiar o arquivo de imagens toohello se o pacote Olá é grande ou tem vários ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c21a5-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="c21a5-275">Leia mais [aqui](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="c21a5-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="c21a5-276">Um serviço do Service Fabric pode ser implementado em várias "configurações".</span><span class="sxs-lookup"><span data-stu-id="c21a5-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="c21a5-277">Por exemplo, pode ser implementado como únicas ou várias instâncias, ou podem ser implementada de forma a que não há uma instância do serviço de Olá em cada nó do cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="c21a5-278">Olá `InstanceCount` parâmetro de Olá `New-ServiceFabricService` cmdlet é utilizado toospecify quantas instâncias do serviço de Olá devem ser iniciadas no cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="c21a5-279">Pode definir Olá `InstanceCount` valor, dependendo do tipo de Olá de aplicação que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="c21a5-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="c21a5-280">Olá dois os cenários mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="c21a5-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="c21a5-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="c21a5-282">Neste caso, apenas uma instância do serviço de Olá for implementada num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="c21a5-283">Programador de Service Fabric determina o serviço de Olá nó vai toobe implementado em.</span><span class="sxs-lookup"><span data-stu-id="c21a5-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="c21a5-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="c21a5-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="c21a5-285">Neste caso, uma instância do serviço de Olá é implementada em cada nó do cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="c21a5-286">resultado de Olá está a ter um (e apenas um) instância do serviço de Olá para cada nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="c21a5-287">Esta é uma configuração útil para aplicações de front-end (por exemplo, um ponto final do REST), porque as aplicações de cliente precisam de demasiado "ligar" tooany de nós de Olá num ponto final do Olá cluster toouse Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="c21a5-288">Esta configuração também pode ser utilizada quando, por exemplo, todos os nós do cluster do Service Fabric Olá tooa ligado Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c21a5-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="c21a5-289">O tráfego de cliente, em seguida, pode ser distribuído por serviço Olá que está a ser executado em todos os nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c21a5-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="c21a5-290">Verifique a sua aplicação em execução</span><span class="sxs-lookup"><span data-stu-id="c21a5-290">Check your running application</span></span>
<span data-ttu-id="c21a5-291">No Service Fabric Explorer, identifique o nó de olá onde o serviço de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="c21a5-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="c21a5-292">Neste exemplo, é executada no Nó1:</span><span class="sxs-lookup"><span data-stu-id="c21a5-292">In this example, it runs on Node1:</span></span>

![Nó onde o serviço está a ser executado](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="c21a5-294">Se navegar nó toohello e procurar toohello aplicação, consulte as informações de nó essencial Olá, incluindo a localização no disco.</span><span class="sxs-lookup"><span data-stu-id="c21a5-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Localização do disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="c21a5-296">Se procurar diretório toohello utilizando o Explorador de servidores, pode encontrar o diretório de trabalho de Olá e pasta de registo do serviço de Olá, conforme mostrado na seguinte captura de ecrã de Olá:</span><span class="sxs-lookup"><span data-stu-id="c21a5-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Localização do registo](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="c21a5-298">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c21a5-298">Next steps</span></span>
<span data-ttu-id="c21a5-299">Neste artigo, aprendeu como toopackage um executável de convidado e implementá-la tooService recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="c21a5-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="c21a5-300">Consulte Olá seguintes artigos para tarefas e informações relacionadas.</span><span class="sxs-lookup"><span data-stu-id="c21a5-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="c21a5-301">[Exemplo de empacotamento e implementação de um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluindo uma pré-lançamento toohello de ligação da ferramenta de empacotamento de Olá</span><span class="sxs-lookup"><span data-stu-id="c21a5-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="c21a5-302">Exemplo de dois convidado executáveis (c# e nodejs) comunicar através do serviço de nomes de Olá através de REST</span><span class="sxs-lookup"><span data-stu-id="c21a5-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="c21a5-303">Implementar vários executáveis convidados</span><span class="sxs-lookup"><span data-stu-id="c21a5-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="c21a5-304">Criar a primeira aplicação de Service Fabric com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c21a5-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
