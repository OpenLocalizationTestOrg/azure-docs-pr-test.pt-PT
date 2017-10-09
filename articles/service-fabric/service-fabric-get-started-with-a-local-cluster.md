---
title: "aaaDeploy e atualizar micro-serviços do Azure localmente | Microsoft Docs"
description: "Saiba como implementar um tooit de aplicação existentes tooset configurar um cluster do Service Fabric local e, em seguida, atualizar essa aplicação."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="048c3-103">Introdução à implementação e atualização de aplicações no seu cluster local</span><span class="sxs-lookup"><span data-stu-id="048c3-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="048c3-104">Olá SDK de Service Fabric do Azure inclui um ambiente de desenvolvimento local completo que pode utilizar tooquickly introdução à implementação e gestão de aplicações num local cluster.</span><span class="sxs-lookup"><span data-stu-id="048c3-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="048c3-105">Neste artigo, criar um cluster local, implementar um tooit aplicação existente e, em seguida, atualizar essa aplicação tooa nova versão, tudo a partir do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="048c3-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="048c3-106">Este artigo assume que já [configurou o seu ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="048c3-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="048c3-107">Criar um cluster local</span><span class="sxs-lookup"><span data-stu-id="048c3-107">Create a local cluster</span></span>
<span data-ttu-id="048c3-108">Um cluster de Service Fabric representa um conjunto de recursos de hardware em que pode implementar aplicações.</span><span class="sxs-lookup"><span data-stu-id="048c3-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="048c3-109">Normalmente, um cluster é constituído por qualquer ponto de cinco toomany milhares de máquinas.</span><span class="sxs-lookup"><span data-stu-id="048c3-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="048c3-110">No entanto, Olá SDK de Service Fabric inclui uma configuração de cluster que pode ser executadas num único computador.</span><span class="sxs-lookup"><span data-stu-id="048c3-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="048c3-111">É importante toounderstand Olá cluster do Service Fabric local não é um emulador ou simulador.</span><span class="sxs-lookup"><span data-stu-id="048c3-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="048c3-112">Este é executado Olá mesmo código de plataforma que se encontra nos clusters de várias máquinas.</span><span class="sxs-lookup"><span data-stu-id="048c3-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="048c3-113">Step-by-Olá única diferença é que os processos de plataforma de Olá que normalmente estão dispersos por cinco máquinas num computador que executa.</span><span class="sxs-lookup"><span data-stu-id="048c3-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="048c3-114">Olá SDK fornece duas formas tooset configurar um cluster local: um Windows PowerShell script e Olá Gestor de clusters locais aplicação de tabuleiro sistema.</span><span class="sxs-lookup"><span data-stu-id="048c3-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="048c3-115">Neste tutorial, utilizamos o script do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="048c3-116">Se já criou um cluster local quando implementou uma aplicação do Visual Studio, pode ignorar esta secção.</span><span class="sxs-lookup"><span data-stu-id="048c3-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="048c3-117">Inicie uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="048c3-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="048c3-118">Execute script de configuração de cluster Olá a partir da pasta SDK Olá:</span><span class="sxs-lookup"><span data-stu-id="048c3-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="048c3-119">A configuração do cluster demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="048c3-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="048c3-120">Após a conclusão do programa de configuração, deverá ver resultados semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="048c3-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Saída do programa de configuração do cluster][cluster-setup-success]
   
    <span data-ttu-id="048c3-122">Agora, está pronto tootry implementar um cluster de tooyour de aplicação.</span><span class="sxs-lookup"><span data-stu-id="048c3-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="048c3-123">Implementar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="048c3-123">Deploy an application</span></span>
<span data-ttu-id="048c3-124">Olá SDK de Service Fabric inclui um conjunto avançado de estruturas e ferramentas para programadores para criar aplicações.</span><span class="sxs-lookup"><span data-stu-id="048c3-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="048c3-125">Se estiver interessado no learning como toocreate aplicações no Visual Studio, consulte [criar a primeira aplicação de Service Fabric no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="048c3-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="048c3-126">Neste tutorial, a utilização de uma aplicação de exemplo existente (denominada WordCount) para poder concentrar nos aspetos de gestão de Olá da plataforma de Olá: implementação, monitorização e a atualização.</span><span class="sxs-lookup"><span data-stu-id="048c3-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="048c3-127">Inicie uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="048c3-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="048c3-128">Importe o módulo do PowerShell de SDK do Service Fabric de Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="048c3-129">Crie uma aplicação Olá toostore de diretório que transferir e implementar, tais como C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="048c3-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="048c3-130">[Transferir a aplicação de WordCount Olá](http://aka.ms/servicefabric-wordcountapp) toohello localização criada.</span><span class="sxs-lookup"><span data-stu-id="048c3-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="048c3-131">Nota: o browser Microsoft Edge de Olá guarda o ficheiro de Olá com um *. zip* extensão.</span><span class="sxs-lookup"><span data-stu-id="048c3-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="048c3-132">Alterar a extensão de ficheiro Olá demasiado*. sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="048c3-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="048c3-133">Ligue o toohello local cluster:</span><span class="sxs-lookup"><span data-stu-id="048c3-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="048c3-134">Crie uma nova aplicação utilizando o comando de implementação do SDK Olá com um nome e um pacote de aplicação toohello do caminho.</span><span class="sxs-lookup"><span data-stu-id="048c3-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="048c3-135">Se tudo correr bem, deverá ver Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="048c3-135">If all goes well, you should see hello following output:</span></span>
   
    ![Implementar um cluster local de toohello de aplicação][deploy-app-to-local-cluster]
7. <span data-ttu-id="048c3-137">aplicação de Olá toosee em ação, inicie Olá navegador e navegue demasiado[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="048c3-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="048c3-138">Deverá ver:</span><span class="sxs-lookup"><span data-stu-id="048c3-138">You should see:</span></span>
   
    ![Interface do utilizador da aplicação implementada][deployed-app-ui]
   
    <span data-ttu-id="048c3-140">Olá aplicação WordCount é simple.</span><span class="sxs-lookup"><span data-stu-id="048c3-140">hello WordCount application is simple.</span></span> <span data-ttu-id="048c3-141">Inclui o lado do cliente JavaScript código toogenerate aleatórios cinco carateres "palavras", que são, em seguida, retransmitidas toohello aplicação através da API Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="048c3-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="048c3-142">Um serviço com estado controla o número de Olá de palavras contadas.</span><span class="sxs-lookup"><span data-stu-id="048c3-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="048c3-143">Criam-se partições com base no primeiro caráter de Olá do word Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="048c3-144">Pode encontrar o código de origem Olá para a aplicação de WordCount Olá no Olá [clássico exemplos de introdução](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="048c3-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="048c3-145">aplicação Olá que foi implementada contém quatro partições.</span><span class="sxs-lookup"><span data-stu-id="048c3-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="048c3-146">Para que as palavras que começam de À G são armazenadas na partição primeiro Olá, palavras de h a N são armazenadas na segunda partição de Olá e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="048c3-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="048c3-147">Ver detalhes e estado da aplicação</span><span class="sxs-lookup"><span data-stu-id="048c3-147">View application details and status</span></span>
<span data-ttu-id="048c3-148">Agora que Implementámos a aplicação Olá, vamos ver alguns dos detalhes da aplicação Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="048c3-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="048c3-149">Consulta todas as aplicações implementadas no cluster de Olá:</span><span class="sxs-lookup"><span data-stu-id="048c3-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="048c3-150">Partindo do princípio que só implementou a aplicação de WordCount Olá, verá algo semelhante a:</span><span class="sxs-lookup"><span data-stu-id="048c3-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Consultar todas as aplicações implementadas no PowerShell][ps-getsfapp]
2. <span data-ttu-id="048c3-152">Aceda toohello próximo nível consultando o conjunto de Olá de serviços que estão incluídos na aplicação de WordCount Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista de serviços para aplicação Olá no PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="048c3-154">aplicação Olá é constituída por dois serviços, o front-end Olá web e o serviço de monitorização de estado Olá que gere palavras Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="048c3-155">Por fim, observe lista Olá de partições para WordCountService:</span><span class="sxs-lookup"><span data-stu-id="048c3-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Ver Olá partições de serviço no PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="048c3-157">Olá, conjunto de comandos que utilizou como todos os comandos do PowerShell de Service Fabric, estão disponíveis para qualquer cluster a que poderá ligar, local ou remoto.</span><span class="sxs-lookup"><span data-stu-id="048c3-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="048c3-158">Para um toointeract de forma mais visual com o cluster de Olá, pode utilizar a ferramenta de Service Fabric Explorer baseado na web Olá navegando demasiado[http://localhost:19080/Explorer](http://localhost:19080/Explorer) no browser Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Ver detalhes da aplicação no Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="048c3-160">toolearn mais acerca do Service Fabric Explorer, consulte [visualizar o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="048c3-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="048c3-161">Atualizar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="048c3-161">Upgrade an application</span></span>
<span data-ttu-id="048c3-162">O Service Fabric fornece atualizações sem tempo de indisponibilidade através da monitorização de estado de funcionamento de Olá da aplicação Olá, que implementa no cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="048c3-163">Efetue uma atualização de Olá aplicação WordCount.</span><span class="sxs-lookup"><span data-stu-id="048c3-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="048c3-164">nova versão de Olá da aplicação Olá agora conta apenas as palavras que começam por uma vogal.</span><span class="sxs-lookup"><span data-stu-id="048c3-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="048c3-165">Como Olá atualização se faz, vemos duas alterações de comportamento da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="048c3-166">Em primeiro lugar, taxa de Olá que aumenta a contagem de Olá mais lenta, uma vez que estão a ser contadas menos palavras.</span><span class="sxs-lookup"><span data-stu-id="048c3-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="048c3-167">Segundo, uma vez que a primeira partição de Olá tem duas vogais (A e E) e todas as outras partições contêm apenas uma, a contagem deverá finalmente deve começar toooutpace Olá outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="048c3-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="048c3-168">[Transferir o pacote de versão 2 do WordCount Olá](http://aka.ms/servicefabric-wordcountappv2) toohello mesma localização onde transferiu o pacote de versão 1 olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="048c3-169">Devolver a janela do PowerShell tooyour e utilize o comando de atualização do SDK de Olá tooregister Olá nova versão no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="048c3-170">Em seguida, comece a atualizar a infraestrutura de Olá: / aplicação WordCount.</span><span class="sxs-lookup"><span data-stu-id="048c3-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="048c3-171">Deverá ver a seguinte Olá saída no PowerShell, como Olá atualização começa.</span><span class="sxs-lookup"><span data-stu-id="048c3-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Progresso da atualização do PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="048c3-173">Enquanto Olá atualização está a decorrer, pode encontrá-lo mais fácil toomonitor o estado do Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="048c3-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="048c3-174">Inicie uma janela do browser e navegue demasiado[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="048c3-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="048c3-175">Expanda **aplicações** na árvore de Olá Olá esquerda, em seguida, escolha **WordCount**e, finalmente, **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="048c3-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="048c3-176">No separador de essentials Olá, ver estado Olá da atualização de Olá como medida que avança nos domínios de atualização do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Parar um nó no Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="048c3-178">Como as prossegue atualização Olá através de cada domínio, verificações de estado de funcionamento são executada tooensure que aplicação Olá está a comportar corretamente.</span><span class="sxs-lookup"><span data-stu-id="048c3-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="048c3-179">Se voltar a executar Olá anteriormente consultar do conjunto de Olá de serviços nos recursos de infraestrutura Olá: / WordCount aplicação, tenha em atenção que a versão do wordcountservice foi alterada de Olá mas Olá versão do WordCountWebService não:</span><span class="sxs-lookup"><span data-stu-id="048c3-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar os serviços de aplicações após atualização][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="048c3-181">Este exemplo realça como o Service Fabric gere as atualizações de aplicações.</span><span class="sxs-lookup"><span data-stu-id="048c3-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="048c3-182">Toca apenas Olá conjunto de serviços (ou pacotes de código/configuração dentro desses serviços) que tenham sido alterados, tornando o processo de Olá de atualização mais rápido e mais fiável.</span><span class="sxs-lookup"><span data-stu-id="048c3-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="048c3-183">Por último, regresse toohello browser tooobserve Olá comportamento nova versão da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="048c3-184">Conforme esperado, Olá contagem avança-ser mais lentamente e Olá primeira partição termina com um pouco mais de volume Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Nova versão da vista Olá da aplicação Olá no browser Olá][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="048c3-186">Limpeza</span><span class="sxs-lookup"><span data-stu-id="048c3-186">Cleaning up</span></span>
<span data-ttu-id="048c3-187">Antes de concluir, é importante tooremember Olá local cluster é real.</span><span class="sxs-lookup"><span data-stu-id="048c3-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="048c3-188">As aplicações continuam toorun em segundo plano de Olá até que remova-os.</span><span class="sxs-lookup"><span data-stu-id="048c3-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="048c3-189">Dependendo da natureza Olá das suas aplicações, uma aplicação em execução pode consumir recursos significativos no seu computador.</span><span class="sxs-lookup"><span data-stu-id="048c3-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="048c3-190">Tem várias aplicações de toomanage opções e cluster Olá:</span><span class="sxs-lookup"><span data-stu-id="048c3-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="048c3-191">tooremove uma aplicação individual e todos os-lo da dados, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="048c3-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="048c3-192">Ou, elimine a aplicação Olá da Olá Service Fabric Explorer **AÇÕES** menu ou o menu de contexto de Olá na vista de lista do lado esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Eliminar uma aplicação no Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="048c3-194">Depois de eliminar aplicação Olá do cluster de Olá, anular o registo das versões 1.0.0 e 2.0.0 do Olá tipo de aplicação de WordCount.</span><span class="sxs-lookup"><span data-stu-id="048c3-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="048c3-195">Eliminação remove pacotes de aplicações de Olá, incluindo o código de Olá e a configuração, do cluster Olá arquivo de imagens.</span><span class="sxs-lookup"><span data-stu-id="048c3-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="048c3-196">Ou, no Service Fabric Explorer, escolha **tipo de não aprovisionamento** para aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="048c3-197">tooshut baixo cluster Olá, mas manter dados da aplicação Olá e rastreios, clique em **parar Cluster Local** na aplicação de tabuleiro de sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="048c3-198">cluster de Olá toodelete totalmente, clique em **remover Cluster Local** na aplicação de tabuleiro de sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="048c3-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="048c3-199">Esta opção resultará na outra Olá de implementação lenta próxima vez que premir F5 no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="048c3-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="048c3-200">Remova cluster local Olá apenas se não tenciona toouse-la para algum tempo ou se necessitar de tooreclaim recursos.</span><span class="sxs-lookup"><span data-stu-id="048c3-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="048c3-201">Modo do cluster de cinco nós e um nó</span><span class="sxs-lookup"><span data-stu-id="048c3-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="048c3-202">Ao desenvolver aplicações, irá frequentemente fazer iterações rápidas de escrita de código, depuração e alteração de código.</span><span class="sxs-lookup"><span data-stu-id="048c3-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="048c3-203">toohelp otimizar este processo, o cluster local Olá pode executar em dois modos: um nó ou cinco nós.</span><span class="sxs-lookup"><span data-stu-id="048c3-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="048c3-204">Ambos os modos de cluster têm as suas vantagens.</span><span class="sxs-lookup"><span data-stu-id="048c3-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="048c3-205">Modo de cluster de cinco nós permite-lhe toowork com um cluster real.</span><span class="sxs-lookup"><span data-stu-id="048c3-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="048c3-206">Pode testar cenários de ativação pós-falha, trabalhar com mais instâncias e réplicas dos seus serviços.</span><span class="sxs-lookup"><span data-stu-id="048c3-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="048c3-207">O modo de um nó de cluster é toodo otimizada de implementação rápida e o registo dos serviços, toohelp rapidamente validar o código utilizando o tempo de execução do Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="048c3-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="048c3-208">Os modos do cluster de um nó e de cinco nós não são um emulador ou simulador.</span><span class="sxs-lookup"><span data-stu-id="048c3-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="048c3-209">cluster de desenvolvimento local Olá executa Olá mesmo código de plataforma que se encontra nos clusters de várias máquinas.</span><span class="sxs-lookup"><span data-stu-id="048c3-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="048c3-210">Quando alterar o modo de cluster de Olá, o cluster atual Olá é removido do sistema e é criado um novo cluster.</span><span class="sxs-lookup"><span data-stu-id="048c3-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="048c3-211">dados de Olá armazenados Olá cluster são eliminados quando alterar o modo de cluster.</span><span class="sxs-lookup"><span data-stu-id="048c3-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="048c3-212">toochange Olá modo tooone cluster de nó, selecione **comutador Cluster modo** no Olá Gestor de clusters locais do serviço de recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="048c3-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Alternar o modo do cluster][switch-cluster-mode]

<span data-ttu-id="048c3-214">Em alternativa, alterar o modo de cluster Olá através do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="048c3-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="048c3-215">Inicie uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="048c3-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="048c3-216">Execute script de configuração de cluster Olá a partir da pasta SDK Olá:</span><span class="sxs-lookup"><span data-stu-id="048c3-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="048c3-217">A configuração do cluster demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="048c3-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="048c3-218">Após a conclusão do programa de configuração, deverá ver resultados semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="048c3-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Saída do programa de configuração do cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="048c3-220">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="048c3-220">Next steps</span></span>
* <span data-ttu-id="048c3-221">Agora que implementou e atualizou algumas aplicações pré-criadas, pode [tentar criar a sua no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="048c3-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="048c3-222">Todas as ações de Olá executadas no cluster local Olá este artigo podem ser efetuadas num [cluster do Azure](service-fabric-cluster-creation-via-portal.md) bem.</span><span class="sxs-lookup"><span data-stu-id="048c3-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="048c3-223">atualização de Olá que efetuámos neste artigo foi básica.</span><span class="sxs-lookup"><span data-stu-id="048c3-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="048c3-224">Consulte Olá [documentação de atualização](service-fabric-application-upgrade.md) toolearn mais informações sobre a capacidade de Olá e a flexibilidade das atualizações do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="048c3-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
