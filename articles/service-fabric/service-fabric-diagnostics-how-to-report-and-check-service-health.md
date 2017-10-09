---
title: "aaaReport e verificação de estado de funcionamento com o Azure Service Fabric | Microsoft Docs"
description: "Saiba como os relatórios de estado de toosend do código do serviço e como o estado de funcionamento do toocheck Olá do seu serviço utilizando o estado de funcionamento de Olá ferramentas de monitorização que Azure Service Fabric fornece."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="6a7d0-103">Comunicar e verificar o estado de funcionamento dos serviços</span><span class="sxs-lookup"><span data-stu-id="6a7d0-103">Report and check service health</span></span>
<span data-ttu-id="6a7d0-104">Quando os serviços de encontrarem problemas, os incidentes de correção capacidade toorespond tooand e falhas depende os problemas de Olá toodetect capacidade rapidamente.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="6a7d0-105">Se comunicar problemas e falhas de Gestor de estado de funcionamento do Azure Service Fabric toohello do código do serviço, pode utilizar o estado de funcionamento padrão ferramentas que o Service Fabric fornece o estado de funcionamento de Olá toocheck de monitorização.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="6a7d0-106">Existem três formas que pode comunicar o estado de funcionamento do serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="6a7d0-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="6a7d0-107">Utilize [partição](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objetos.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="6a7d0-108">Pode utilizar Olá `Partition` e `CodePackageActivationContext` objetos de estado de funcionamento do tooreport Olá dos elementos que fazem parte do contexto atual Olá.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="6a7d0-109">Por exemplo, o código que é executado como parte de uma réplica pode comunicar o estado de funcionamento apenas essa réplica, Olá partição que pertence e aplicação Olá que faz parte do.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="6a7d0-110">Utilize `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="6a7d0-111">Pode utilizar `FabricClient` tooreport estado de funcionamento a partir do código do serviço de Olá cluster Olá não esteja [segura](service-fabric-cluster-security.md) ou se o serviço de Olá está em execução com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="6a7d0-112">A maioria dos cenários no mundo real não utilizar clusters protegidas, ou forneça privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="6a7d0-113">Com `FabricClient`, pode comunicar o estado de funcionamento em qualquer entidade que faz parte do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="6a7d0-114">Idealmente, no entanto, código do serviço deve apenas enviar relatórios que estão relacionados tooits própria estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="6a7d0-115">Utilize Olá REST APIs no cluster Olá, aplicação, aplicação implementada, serviço, o pacote de serviço, partição, réplica ou níveis de nó.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="6a7d0-116">Isto pode ser utilizado tooreport o estado de funcionamento da num contentor.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="6a7d0-117">Este artigo explica como um exemplo que comunica o estado de funcionamento a partir do código do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="6a7d0-118">exemplo de Olá também mostra como as ferramentas de Olá fornecidas pelo serviço de recursos de infraestrutura podem ser utilizados toocheck Olá o estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="6a7d0-119">Este artigo é um Estado de funcionamento introdução rápida toohello capacidades dos recursos de infraestrutura do serviço de monitorização de toobe pretendido.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="6a7d0-120">Para obter informações mais detalhadas, pode ler série Olá dos artigos aprofundados sobre o estado de funcionamento que começam com ligação Olá no fim de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a7d0-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a7d0-121">Prerequisites</span></span>
<span data-ttu-id="6a7d0-122">Tem de ter o seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="6a7d0-122">You must have hello following installed:</span></span>

* <span data-ttu-id="6a7d0-123">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6a7d0-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="6a7d0-124">SDK do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6a7d0-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="6a7d0-125">toocreate um cluster de desenvolvimento seguro local</span><span class="sxs-lookup"><span data-stu-id="6a7d0-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="6a7d0-126">Abra o PowerShell com privilégios de administrador e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a7d0-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Os comandos que mostram como toocreate um cluster de desenvolvimento seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="6a7d0-128">toodeploy uma aplicação e verificar o estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="6a7d0-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="6a7d0-129">Abra o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="6a7d0-130">Criar um projeto utilizando Olá **serviço de monitorização de estado** modelo.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Criar uma aplicação de Service Fabric com o serviço de monitorização de estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="6a7d0-132">Prima **F5** aplicação de Olá toorun no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="6a7d0-133">aplicação Olá é cluster local toohello implementado.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="6a7d0-134">Após a aplicação Olá está em execução, clique no ícone do Gestor de clusters locais Olá na área de notificação de Olá e selecione **gerir Cluster Local** de tooopen de menu de atalho Olá Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Abra o Explorador de recursos de infraestrutura de serviço da área de notificação](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="6a7d0-136">Estado de funcionamento da aplicação Olá deverá ser apresentado como esta imagem.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="6a7d0-137">Neste momento, aplicação Olá deve estar em bom estado sem erros.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Aplicação bom estado de funcionamento no Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="6a7d0-139">Também pode verificar o estado de funcionamento de Olá utilizando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="6a7d0-140">Pode utilizar ```Get-ServiceFabricApplicationHealth``` toocheck pode utilizar o estado de funcionamento de uma aplicação e ```Get-ServiceFabricServiceHealth``` toocheck estado de funcionamento de um serviço.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="6a7d0-141">Olá, relatório de estado de funcionamento para Olá mesma aplicação no PowerShell está nesta imagem.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Aplicação bom estado de funcionamento no PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="6a7d0-143">código do serviço tooyour tooadd estado de funcionamento personalizado eventos</span><span class="sxs-lookup"><span data-stu-id="6a7d0-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="6a7d0-144">Olá modelos de projeto de Service Fabric no Visual Studio contêm código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="6a7d0-145">Olá passos seguintes mostram como pode comunicar eventos de estado de funcionamento personalizado a partir do seu código de serviço.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="6a7d0-146">Esses relatórios apareçam automaticamente nas ferramentas padrão de Olá para que o Service Fabric fornece, como o Service Fabric Explorer, vista de estado de funcionamento de portal do Azure e do PowerShell de monitorização de estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="6a7d0-147">Reabra a aplicação Olá que criou anteriormente no Visual Studio ou criar uma nova aplicação utilizando Olá **serviço de monitorização de estado** modelo do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="6a7d0-148">Abrir o ficheiro de Stateful1.cs Olá e determinar Olá `myDictionary.TryGetValueAsync` chamada em Olá `RunAsync` método.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="6a7d0-149">Pode ver que este método devolve um `result` que detém Olá valor atual do contador de Olá porque Olá lógica chave esta aplicação é tookeep uma execução de contagem.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="6a7d0-150">Se isto foram real da aplicação e se a falta de Olá de resultado representado uma falha, seria aconselhável tooflag esse evento.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="6a7d0-151">tooreport um evento de estado de funcionamento quando a falta de Olá de resultado representa uma falha, adicione Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="6a7d0-152">a.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-152">a.</span></span> <span data-ttu-id="6a7d0-153">Adicionar Olá `System.Fabric.Health` espaço de nomes toohello Stateful1.cs ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="6a7d0-154">b.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-154">b.</span></span> <span data-ttu-id="6a7d0-155">Adicionar Olá seguinte código após Olá `myDictionary.TryGetValueAsync` chamar</span><span class="sxs-lookup"><span data-stu-id="6a7d0-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="6a7d0-156">Elaboramos relatórios de estado de funcionamento de réplica porque está a ser reportado num serviço de monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="6a7d0-157">Olá `HealthInformation` parâmetro armazena informações sobre o problema de estado de funcionamento de Olá que está a ser reportado.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="6a7d0-158">Se criou um serviço sem monitorização de estado, utilize Olá seguinte código</span><span class="sxs-lookup"><span data-stu-id="6a7d0-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="6a7d0-159">Se o serviço está em execução com privilégios de administrador ou se hello o cluster não está [segura](service-fabric-cluster-security.md), também pode utilizar `FabricClient` tooreport de estado de funcionamento conforme mostrado no Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="6a7d0-160">a.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-160">a.</span></span> <span data-ttu-id="6a7d0-161">Criar Olá `FabricClient` instância após Olá `var myDictionary` declaração.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="6a7d0-162">b.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-162">b.</span></span> <span data-ttu-id="6a7d0-163">Adicionar Olá seguinte código após Olá `myDictionary.TryGetValueAsync` chamada.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="6a7d0-164">Vamos simular desta falha e veja-apareçam nas ferramentas de monitorização de estado de funcionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="6a7d0-165">Falha de Olá toosimulate, comente a primeira linha de Olá no estado de funcionamento de Olá reporting código que adicionou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="6a7d0-166">Depois de comente a primeira linha de Olá, código de Olá terá um aspeto semelhante Olá seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="6a7d0-167">Este código desencadeado relatório de estado de funcionamento de Olá sempre `RunAsync` executa.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="6a7d0-168">Depois de efetuar Olá alterar, prima **F5** aplicação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="6a7d0-169">Após a aplicação Olá está em execução, abra o estado de funcionamento do Service Fabric Explorer toocheck Olá da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="6a7d0-170">Neste momento, Service Fabric Explorer mostra que a aplicação Olá está danificada.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="6a7d0-171">Trata-se devido ao erro Olá que foi reportado a partir do código Olá que adicionamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Aplicação mau estado de funcionamento no Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="6a7d0-173">Se selecionar a réplica primária Olá na vista de árvore Olá do Service Fabric Explorer, verá que **estado de funcionamento** indica um erro, demasiado.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="6a7d0-174">Service Fabric Explorer apresenta também o relatório de estado de funcionamento de Olá detalhes que foram adicionados toohello `HealthInformation` parâmetro Olá code.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="6a7d0-175">Pode ver Olá mesmo relatórios de estado de funcionamento no PowerShell e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Estado de funcionamento de réplica no Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="6a7d0-177">Este relatório permanece no Gestor de estado de funcionamento de Olá até é substituído por outro relatório ou até que esta réplica foi eliminada.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="6a7d0-178">Porque não foi possível definir não `TimeToLive` para este relatório de estado de funcionamento no Olá `HealthInformation` objeto relatório Olá nunca expira.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="6a7d0-179">Recomendamos que o estado de funcionamento deve ser comunicado no nível mais granular Olá, que neste caso é réplica Olá.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="6a7d0-180">Também pode comunicar o estado de funcionamento no `Partition`.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="6a7d0-181">Estado de funcionamento tooreport em `Application`, `DeployedApplication`, e `DeployedServicePackage`, utilize `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="6a7d0-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="6a7d0-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6a7d0-182">Next steps</span></span>
* [<span data-ttu-id="6a7d0-183">Descrição profunda sobre o estado de funcionamento do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6a7d0-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="6a7d0-184">API REST para os relatórios do Estado de funcionamento do serviço</span><span class="sxs-lookup"><span data-stu-id="6a7d0-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="6a7d0-185">API REST para os relatórios do Estado de funcionamento da aplicação</span><span class="sxs-lookup"><span data-stu-id="6a7d0-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

