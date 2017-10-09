---
title: "aaaCreate um serviço fiável de Service Fabric do Azure com c#"
description: "Crie, implemente e depure uma aplicação Reliable Service compilada no Azure Service Fabric com o Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="5b2af-103">Criar a sua primeira aplicação Reliable Services sem monitorização de estado do Service Fabric em C#</span><span class="sxs-lookup"><span data-stu-id="5b2af-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="5b2af-104">Saiba como toodeploy sua primeira aplicação de Service Fabric para .NET no Windows em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5b2af-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="5b2af-105">Quando tiver terminado, terá um cluster local em execução com uma aplicação do Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="5b2af-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b2af-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b2af-106">Prerequisites</span></span>

<span data-ttu-id="5b2af-107">Antes de começar, certifique-se de que [configurou o seu ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5b2af-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="5b2af-108">Isto inclui a instalação Olá SDK de Service Fabric e Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="5b2af-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="5b2af-109">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="5b2af-109">Create hello application</span></span>

<span data-ttu-id="5b2af-110">Inicie o Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="5b2af-111">Criar um projeto com `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="5b2af-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="5b2af-112">No Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicação de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="5b2af-113">Nome da aplicação Olá **MinhaAplicação** e prima **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Caixa de diálogo de novo projeto no Visual Studio][1]

<span data-ttu-id="5b2af-115">Pode criar qualquer tipo de aplicação de Service Fabric da caixa de diálogo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="5b2af-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="5b2af-116">Neste Início Rápido, escolha **Serviço Com Estado** .</span><span class="sxs-lookup"><span data-stu-id="5b2af-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="5b2af-117">Nome do serviço de Olá **MyStatefulService** e prima **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Caixa de diálogo novo serviço no Visual Studio][2]


<span data-ttu-id="5b2af-119">Visual Studio cria o projeto de aplicação Olá e projeto de serviço com estado Olá e apresenta-os no Explorador de soluções.</span><span class="sxs-lookup"><span data-stu-id="5b2af-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Explorador de Soluções a seguir a criação da aplicação com o serviço com estado][3]

<span data-ttu-id="5b2af-121">projeto de aplicação Olá (**MinhaAplicação**) não contém qualquer código diretamente.</span><span class="sxs-lookup"><span data-stu-id="5b2af-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="5b2af-122">Em vez disso, referencia um conjunto de projetos de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b2af-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="5b2af-123">Além disso, contém outros três tipos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="5b2af-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="5b2af-124">**Perfis de publicação**</span><span class="sxs-lookup"><span data-stu-id="5b2af-124">**Publish profiles**</span></span>  
<span data-ttu-id="5b2af-125">Perfis para a implementação de ambientes de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="5b2af-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="5b2af-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="5b2af-126">**Scripts**</span></span>  
<span data-ttu-id="5b2af-127">Script do PowerShell para implementar/atualizar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="5b2af-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="5b2af-128">**Definição da aplicação**</span><span class="sxs-lookup"><span data-stu-id="5b2af-128">**Application definition**</span></span>  
<span data-ttu-id="5b2af-129">Inclui o ficheiro de ApplicationManifest.xml Olá em *ApplicationPackageRoot* que descreve a composição da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="5b2af-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="5b2af-130">Os ficheiros de parâmetro de aplicação associada são em *ApplicationParameters*, que pode ser utilizado toospecify parâmetros específico do ambiente.</span><span class="sxs-lookup"><span data-stu-id="5b2af-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="5b2af-131">Perfil de publicação Visual seleciona de Studio associado a um ficheiro de parâmetros de aplicação que é especificado no Olá durante ambiente específico de tooa de implementação.</span><span class="sxs-lookup"><span data-stu-id="5b2af-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="5b2af-132">Para obter uma descrição geral do conteúdo de Olá do projeto de serviço Olá, consulte [introdução a Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="5b2af-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="5b2af-133">Implementar e depurar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="5b2af-133">Deploy and debug hello application</span></span>

<span data-ttu-id="5b2af-134">Agora que tem uma aplicação, execute-a.</span><span class="sxs-lookup"><span data-stu-id="5b2af-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="5b2af-135">No Visual Studio, prima `F5` aplicação de Olá toodeploy de depuração.</span><span class="sxs-lookup"><span data-stu-id="5b2af-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="5b2af-136">Olá pela primeira vez, executar e implementar a aplicação de Olá localmente, Visual Studio cria um cluster local para a depuração.</span><span class="sxs-lookup"><span data-stu-id="5b2af-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="5b2af-137">Esta operação pode demorar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="5b2af-137">This may take some time.</span></span> <span data-ttu-id="5b2af-138">o estado de criação do cluster Olá é apresentado na janela de saída do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="5b2af-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="5b2af-139">Quando Olá cluster estiver pronto, receberá uma notificação de Olá local cluster sistema tabuleiro a aplicação do manager incluída com Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="5b2af-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Notificação do tabuleiro de sistema do cluster local][4]

<span data-ttu-id="5b2af-141">Uma vez iniciado o aplicação Olá, Visual Studio automaticamente aparece Olá **Visualizador de eventos de diagnóstico**, onde pode ver os resultados de rastreio do seu serviços.</span><span class="sxs-lookup"><span data-stu-id="5b2af-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Visualizador de eventos de diagnóstico][5]

<span data-ttu-id="5b2af-143">Olá modelo de serviço com estado utilizámos simplesmente mostra um valor de contador incrementando no Olá `RunAsync` método **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="5b2af-144">Expanda um dos Olá eventos toosee mais detalhes, incluindo o nó de olá onde código Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="5b2af-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="5b2af-145">Neste caso, é \_Nó\_, embora possa ser diferente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="5b2af-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Detalhe do visualizador de eventos de diagnóstico][6]

<span data-ttu-id="5b2af-147">cluster local Olá contém cinco nós alojados num único computador.</span><span class="sxs-lookup"><span data-stu-id="5b2af-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="5b2af-148">Num ambiente de produção, cada nó é alojada num computador físico ou virtual diferente.</span><span class="sxs-lookup"><span data-stu-id="5b2af-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="5b2af-149">perda de Olá toosimulate de uma máquina ao exercising Olá Visual Studio debugger em Olá mesmo tempo, desativemos um de nós de Olá no cluster local Olá.</span><span class="sxs-lookup"><span data-stu-id="5b2af-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="5b2af-150">No Olá **Explorador de soluções** janela, abra **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="5b2af-151">Determinar Olá `RunAsync` método e o conjunto de um ponto de interrupção na linha de primeiro Olá do método Olá.</span><span class="sxs-lookup"><span data-stu-id="5b2af-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Método RunAsync com ponto de interrupção do serviço com estado ][7]

<span data-ttu-id="5b2af-153">Iniciar Olá **Service Fabric Explorer** ferramenta clicando no Olá **Gestor de clusters locais** aplicação de tabuleiro de sistema e escolha **gerir Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Iniciar o Explorador de recursos de infraestrutura de serviço de Olá Gestor de clusters locais][systray-launch-sfx]

<span data-ttu-id="5b2af-155">O [**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) oferece uma representação visual de um cluster.</span><span class="sxs-lookup"><span data-stu-id="5b2af-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="5b2af-156">Inclui o conjunto de Olá de aplicações implementadas tooit e conjunto de Olá nós físicos que o constituem.</span><span class="sxs-lookup"><span data-stu-id="5b2af-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="5b2af-157">No painel esquerdo Olá, expanda **Cluster > nós** e localizar Olá nó onde o código está em execução.</span><span class="sxs-lookup"><span data-stu-id="5b2af-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="5b2af-158">Clique em **ações > desativar (reiniciar)** toosimulate um reinício do computador.</span><span class="sxs-lookup"><span data-stu-id="5b2af-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Parar um nó no Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="5b2af-160">Momentaneamente, deverá ver o ponto de interrupção atingido no Visual Studio, como o cálculo de Olá que estava a fazer num nó totalmente integrada a ativação pós-falha tooanother.</span><span class="sxs-lookup"><span data-stu-id="5b2af-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="5b2af-161">Em seguida, devolver toohello Visualizador de eventos de diagnóstico e observe mensagens hello.</span><span class="sxs-lookup"><span data-stu-id="5b2af-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="5b2af-162">contador Olá tem continuou incrementando, apesar de eventos de Olá, na verdade, provenientes de um nó diferente.</span><span class="sxs-lookup"><span data-stu-id="5b2af-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Visualizador de eventos de diagnóstico após falha][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="5b2af-164">A limpar cluster local Olá (opcional)</span><span class="sxs-lookup"><span data-stu-id="5b2af-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="5b2af-165">Lembre-se de que este cluster local é real.</span><span class="sxs-lookup"><span data-stu-id="5b2af-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="5b2af-166">Parar o depurador Olá remove a instância da aplicação e tipo de aplicação Olá anula o registo.</span><span class="sxs-lookup"><span data-stu-id="5b2af-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="5b2af-167">No entanto, o cluster de Olá continua toorun em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b2af-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="5b2af-168">Quando tiver um cluster local do toostop pronto Olá, existem algumas opções.</span><span class="sxs-lookup"><span data-stu-id="5b2af-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="5b2af-169">Manter os dados da aplicação e de rastreio</span><span class="sxs-lookup"><span data-stu-id="5b2af-169">Keep application and trace data</span></span>

<span data-ttu-id="5b2af-170">Encerrar o cluster de Olá clicando no Olá **Gestor de clusters locais** aplicação de tabuleiro de sistema e, em seguida, escolha **parar Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="5b2af-171">Eliminar cluster Olá e todos os dados</span><span class="sxs-lookup"><span data-stu-id="5b2af-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="5b2af-172">Remover cluster Olá clicando no Olá **Gestor de clusters locais** aplicação de tabuleiro de sistema e, em seguida, escolha **remover Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="5b2af-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="5b2af-173">Se escolher esta opção, o Visual Studio irá Reimplementar Olá de cluster Olá próxima vez que a execução Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="5b2af-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="5b2af-174">Selecione esta opção se não tenciona cluster local do toouse Olá durante algum tempo ou se precisar de tooreclaim recursos.</span><span class="sxs-lookup"><span data-stu-id="5b2af-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b2af-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5b2af-175">Next steps</span></span>
<span data-ttu-id="5b2af-176">Leia mais sobre o [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5b2af-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
