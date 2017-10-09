---
title: "passos de criação de projeto dos recursos de infraestrutura do aaaService seguintes | Microsoft Docs"
description: "Este artigo contém ligações tooa conjunto de tarefas de desenvolvimento de núcleos de Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="15877-103">A aplicação de Service Fabric e os passos seguintes</span><span class="sxs-lookup"><span data-stu-id="15877-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="15877-104">Foi criada a sua aplicação de Service Fabric do Azure.</span><span class="sxs-lookup"><span data-stu-id="15877-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="15877-105">Este artigo descreve makeup Olá do seu projeto e alguns passos potenciais.</span><span class="sxs-lookup"><span data-stu-id="15877-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="15877-106">A aplicação</span><span class="sxs-lookup"><span data-stu-id="15877-106">Your application</span></span>
<span data-ttu-id="15877-107">Cada nova aplicação inclui um projeto de aplicação.</span><span class="sxs-lookup"><span data-stu-id="15877-107">Every new application includes an application project.</span></span> <span data-ttu-id="15877-108">Pode haver um ou dois projetos adicionais, dependendo do tipo de Olá de serviço escolhido.</span><span class="sxs-lookup"><span data-stu-id="15877-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="15877-109">projeto de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="15877-109">hello application project</span></span>
<span data-ttu-id="15877-110">projeto de aplicação Olá consiste em:</span><span class="sxs-lookup"><span data-stu-id="15877-110">hello application project consists of:</span></span>

* <span data-ttu-id="15877-111">Um conjunto de serviços de toohello referências que compõem a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="15877-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="15877-112">Publicar três perfis (1-nó Local, 5-nó Local e nuvem) que pode utilizar as preferências de toomaintain para trabalhar com ambientes diferentes – como o ponto final de cluster do preferências tooa relacionados e se tooperform atualizar implementações por predefinição.</span><span class="sxs-lookup"><span data-stu-id="15877-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="15877-113">Três ficheiros parâmetro da aplicação (igual ao acima) que pode utilizar configurações de aplicação específico do ambiente de toomaintain, como número de Olá de partições toocreate para um serviço.</span><span class="sxs-lookup"><span data-stu-id="15877-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="15877-114">Um script de implementação que é possível utilizar toodeploy a aplicação a partir da linha de comandos Olá ou como parte de um pipeline de integração e a implementação contínuo automatizado.</span><span class="sxs-lookup"><span data-stu-id="15877-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="15877-115">Olá manifesto da aplicação, que descreve a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="15877-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="15877-116">Pode encontrar o manifesto de Olá na pasta de ApplicationPackageRoot Olá.</span><span class="sxs-lookup"><span data-stu-id="15877-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="15877-117">Sem estado</span><span class="sxs-lookup"><span data-stu-id="15877-117">Stateless service</span></span>
<span data-ttu-id="15877-118">Quando adiciona um novo serviço sem monitorização de estado, o Visual Studio adiciona uma solução de tooyour do projeto de serviço que inclui um tipo descended de `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="15877-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="15877-119">serviço de Olá incrementa uma variável local um contador.</span><span class="sxs-lookup"><span data-stu-id="15877-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="15877-120">Serviço com estado</span><span class="sxs-lookup"><span data-stu-id="15877-120">Stateful service</span></span>
<span data-ttu-id="15877-121">Quando adiciona um novo serviço de monitorização de estado, o Visual Studio adiciona uma solução de tooyour do projeto de serviço que inclui um tipo descended de `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="15877-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="15877-122">Olá serviço incrementos de um contador no respetivo `RunAsync` método e arquivos Olá resultado um `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="15877-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="15877-123">Serviço de atores</span><span class="sxs-lookup"><span data-stu-id="15877-123">Actor service</span></span>
<span data-ttu-id="15877-124">Quando adiciona um novo ator fiável, Visual Studio adiciona a solução de tooyour dois projetos: um projeto de ator e um projeto de interface.</span><span class="sxs-lookup"><span data-stu-id="15877-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="15877-125">projeto de ator Olá fornece métodos para definição e ao obter valor Olá de um contador que é fiável continuado no estado do ator Olá.</span><span class="sxs-lookup"><span data-stu-id="15877-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="15877-126">Olá interface projeto fornece uma interface que outros serviços pode utilizar o actor de Olá tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="15877-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="15877-127">API de Web sem monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="15877-127">Stateless Web API</span></span>
<span data-ttu-id="15877-128">projeto Web API sem monitorização de estado do Olá fornece num nível básico que é possível utilizar tooopen os clientes de tooexternal de aplicação de serviço web.</span><span class="sxs-lookup"><span data-stu-id="15877-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="15877-129">Para obter mais informações sobre como o projeto de Olá estruturados, consulte [serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="15877-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="15877-130">Núcleo ASP.NET</span><span class="sxs-lookup"><span data-stu-id="15877-130">ASP.NET core</span></span>
<span data-ttu-id="15877-131">Olá SDK de Service Fabric fornece Olá mesmo conjunto de modelos de núcleo de ASP.NET que estão disponíveis para autónomo ASP.NET Core projetos: vazio, [Web API][aspnet-webapi], e [aplicação Web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="15877-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="15877-132">Contentores executáveis e de convidado de convidado</span><span class="sxs-lookup"><span data-stu-id="15877-132">Guest executables and guest containers</span></span>

<span data-ttu-id="15877-133">Um recurso de infraestrutura do serviço 'Convidado' é um serviço que não está incorporado com modelos de programação da plataforma Olá.</span><span class="sxs-lookup"><span data-stu-id="15877-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="15877-134">Pode compactar binários Olá para um convidado está [diretamente no pacote de aplicação Olá](service-fabric-deploy-existing-app.md) ou [através de uma imagem de contentor](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="15877-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="15877-135">Em ambos os casos, o Visual Studio cria Olá artefactos necessários em Olá **ApplicationPackageRoot** na pasta do projeto de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="15877-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="15877-136">Visual Studio não irá criar um novo projeto de serviço porque o código de Olá já existe noutro local.</span><span class="sxs-lookup"><span data-stu-id="15877-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="15877-137">Se quiser toomanage o convidado projetos em conjunto com o projeto de aplicação de Service Fabric Olá, pode adicioná-los toohello mesma solução Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15877-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15877-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="15877-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="15877-139">Criar um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="15877-139">Create an Azure cluster</span></span>
<span data-ttu-id="15877-140">Olá SDK de Service Fabric fornece um cluster local para desenvolvimento e testes.</span><span class="sxs-lookup"><span data-stu-id="15877-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="15877-141">toocreate um cluster no Azure, consulte [configurar um cluster do Service Fabric do portal do Azure de Olá][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="15877-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="15877-142">Publicar a aplicação tooAzure</span><span class="sxs-lookup"><span data-stu-id="15877-142">Publish your application tooAzure</span></span>
<span data-ttu-id="15877-143">Pode publicar a aplicação diretamente a partir do Visual Studio tooan cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="15877-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="15877-144">como, consulte toolearn [publicar a aplicação tooAzure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="15877-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="15877-145">Utilizar o cluster de Service Fabric Explorer toovisualize</span><span class="sxs-lookup"><span data-stu-id="15877-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="15877-146">Service Fabric Explorer proporciona uma forma fácil toovisualize o cluster, incluindo aplicações implementadas e o esquema físico.</span><span class="sxs-lookup"><span data-stu-id="15877-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="15877-147">toolearn mais, consulte [visualizar o cluster utilizando o Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="15877-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="15877-148">Versão e atualizar os serviços</span><span class="sxs-lookup"><span data-stu-id="15877-148">Version and upgrade your services</span></span>
<span data-ttu-id="15877-149">Service Fabric permite o controlo de versões independente e atualização dos serviços independentes de uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="15877-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="15877-150">toolearn mais, consulte [controlo de versões e atualizar os serviços][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="15877-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="15877-151">Configurar a integração contínua com o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="15877-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="15877-152">toolearn como pode configurar um processo de integração contínua para a sua aplicação de Service Fabric, consulte [configurar a integração contínua com o Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="15877-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
