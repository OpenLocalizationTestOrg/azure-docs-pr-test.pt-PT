---
title: aaaTroubleshooting com o rastreio de eventos | Microsoft Docs
description: "problemas mais comuns de Olá encontrados durante a implementação de serviços no Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="553a4-103">Resolver problemas comuns quando implementar serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="553a4-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="553a4-104">Quando estiver a executar serviços no seu computador de programador, é fácil toouse [ferramentas de depuração do Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="553a4-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="553a4-105">Para clusters remotos, [relatórios de estado de funcionamento](service-fabric-view-entities-aggregated-health.md) são sempre toostart um bom local.</span><span class="sxs-lookup"><span data-stu-id="553a4-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="553a4-106">Olá mais fácil tooaccess formas estes relatórios são através do PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="553a4-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="553a4-107">Este artigo assume que está a depurar um cluster remoto e que têm um conhecimento básico de como toouse qualquer uma destas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="553a4-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="553a4-108">Falhas de aplicação</span><span class="sxs-lookup"><span data-stu-id="553a4-108">Application crash</span></span>
<span data-ttu-id="553a4-109">Olá "partição está abaixo contagem de instâncias ou de réplica de destino" relatório é um bom indicador de que o serviço esteja a falhar.</span><span class="sxs-lookup"><span data-stu-id="553a4-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="553a4-110">toofind enviados em que esteja a falhar o serviço demora investigação mais um pequeno.</span><span class="sxs-lookup"><span data-stu-id="553a4-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="553a4-111">Quando o serviço está em execução em escala, sua melhor amigo será um conjunto de rastreios de well thought Escalamento.</span><span class="sxs-lookup"><span data-stu-id="553a4-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="553a4-112">Sugerimos que tente [diagnósticos do Azure](service-fabric-diagnostics-how-to-setup-wad.md) para recolher os rastreios e através de uma solução, como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para ver e procurar rastreios Olá.</span><span class="sxs-lookup"><span data-stu-id="553a4-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![O estado de funcionamento do SFX partição](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="553a4-114">Durante a inicialização do serviço ou ator</span><span class="sxs-lookup"><span data-stu-id="553a4-114">During service or actor initialization</span></span>
<span data-ttu-id="553a4-115">Quaisquer exceções antes de inicializar o tipo de serviço Olá fará Olá toocrash de processo.</span><span class="sxs-lookup"><span data-stu-id="553a4-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="553a4-116">Para estes tipos de falhas, o registo de eventos de aplicações de Olá irá mostrar erro Olá do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="553a4-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="553a4-117">Estes são Olá mais comuns exceções toosee antes de inicializar o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="553a4-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="553a4-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="553a4-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="553a4-119">Este erro é frequentemente devido a dependências de assemblagem toomissing.</span><span class="sxs-lookup"><span data-stu-id="553a4-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="553a4-120">Verificar a propriedade de CopyLocal de Olá no Visual Studio ou da cache de assemblagem global Olá para o nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="553a4-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="553a4-121">***System.Runtime.InteropServices.COMException*** *em System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="553a4-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="553a4-122">Isto indica que esse nome de tipo de serviço registado Olá não corresponde ao manifesto do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="553a4-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="553a4-123">[Diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) pode ser configurado tooupload registo de eventos de aplicações Olá para todos os seus nós automaticamente.</span><span class="sxs-lookup"><span data-stu-id="553a4-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="553a4-124">RunAsync() ou OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="553a4-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="553a4-125">Se a falhas de Olá acontece durante a inicialização de Olá ou em execução do seu tipo de serviço registado ou ator, Olá excepção será detectada pelo Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="553a4-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="553a4-126">Pode ver estes de fornecedores de EventSource Olá detalhados Olá "Passos" secção.</span><span class="sxs-lookup"><span data-stu-id="553a4-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="553a4-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="553a4-127">Next steps</span></span>
<span data-ttu-id="553a4-128">Saiba mais sobre os diagnósticos existentes fornecidos pelo serviço de recursos de infraestrutura:</span><span class="sxs-lookup"><span data-stu-id="553a4-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="553a4-129">Diagnóstico do Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="553a4-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="553a4-130">Diagnóstico de serviços fiável</span><span class="sxs-lookup"><span data-stu-id="553a4-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

