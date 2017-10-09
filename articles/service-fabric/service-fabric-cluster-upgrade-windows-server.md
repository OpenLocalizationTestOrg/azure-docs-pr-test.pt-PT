---
title: "aaaUpgrade autónoma Azure Service Fabric de cluster no Windows Server | Microsoft Docs"
description: "Atualize o código de Azure Service Fabric Olá e/ou de configuração que executa um cluster do Service Fabric autónomo, incluindo a definição do modo de atualização de cluster Olá."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="b0c1b-103">Atualizar o seu autónomo Azure Service Fabric no cluster do Windows Server</span><span class="sxs-lookup"><span data-stu-id="b0c1b-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0c1b-104">Cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="b0c1b-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="b0c1b-105">Cluster autónomo</span><span class="sxs-lookup"><span data-stu-id="b0c1b-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="b0c1b-106">Para qualquer sistema moderno, Olá capacidade tooupgrade é um sucesso de longo prazo toohello chave do produto.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="b0c1b-107">Um cluster do Service Fabric do Azure é um recurso que é proprietário.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="b0c1b-108">Este artigo descreve como pode garantir que esse cluster Olá executa sempre as versões suportadas do código de Service Fabric e configurações.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="b0c1b-109">Versão de Service Fabric Olá do controlo que é executado no seu cluster</span><span class="sxs-lookup"><span data-stu-id="b0c1b-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="b0c1b-110">tooset atualiza o toodownload de cluster do Service Fabric quando a Microsoft disponibiliza uma nova versão, conjunto Olá **fabricClusterAutoupgradeEnabled** tootrue de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="b0c1b-111">tooselect uma versão suportada do Service Fabric que pretende que o seu toobe de cluster no conjunto Olá **fabricClusterAutoupgradeEnabled** toofalse de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="b0c1b-112">Certifique-se de que o cluster é sempre executada uma versão suportada do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="b0c1b-113">Quando a Microsoft announces versão Olá de uma nova versão de Service Fabric, versão anterior do Olá está marcado para fim de suporte após um mínimo de 60 dias a partir da data de Olá de anúncio de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="b0c1b-114">Novos lançamentos sejam anunciados [no blogue de equipa do Service Fabric Olá](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="b0c1b-115">nova versão de Olá é toochoose disponível nesse momento.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="b0c1b-116">Pode atualizar a versão nova do cluster toohello apenas se estiver a utilizar uma configuração de nó de estilo de produção, onde cada nó de Service Fabric está alocada numa máquina virtual ou físico separado.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="b0c1b-117">Se tiver um cluster de desenvolvimento, em que mais do que um nó de Service Fabric é numa única máquina física ou virtual, tem de voltar a criar cluster Olá com a versão nova Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="b0c1b-118">Dois fluxos de trabalho distintos podem atualizar a versão mais recente do cluster toohello ou uma versão suportada do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="b0c1b-119">Um fluxo de trabalho destina-se a clusters que têm a versão mais recente do conectividade toodownload Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="b0c1b-120">Olá outro fluxo de trabalho é para os clusters que não têm a versão de Service Fabric conectividade toodownload Olá mais recente.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="b0c1b-121">Atualizar clusters com o código mais recente do conectividade toodownload Olá e a configuração</span><span class="sxs-lookup"><span data-stu-id="b0c1b-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="b0c1b-122">Utilize estes passos tooupgrade a versão de tooa suportada do cluster se os nós do cluster tem conectividade Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="b0c1b-123">Para clusters com conectividade demasiado[http://download.microsoft.com](http://download.microsoft.com), Microsoft verifica periodicamente a existência de disponibilidade de Olá de novas versões de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="b0c1b-124">Quando estiver disponível uma nova versão de Service Fabric, Olá pacote é transferido localmente toohello cluster e aprovisionado para atualização.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="b0c1b-125">Além disso, cliente de Olá tooinform esta nova versão, o sistema Olá mostra um aviso de estado de funcionamento de explícita de cluster que é semelhante toohello seguintes:</span><span class="sxs-lookup"><span data-stu-id="b0c1b-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="b0c1b-126">"o suporte da versão [versão #] cluster atual Olá termina [Date]".</span><span class="sxs-lookup"><span data-stu-id="b0c1b-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="b0c1b-127">Depois do cluster de Olá está a executar a versão mais recente do Olá, aviso Olá passa ausente.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="b0c1b-128">Fluxo de trabalho de atualização de cluster</span><span class="sxs-lookup"><span data-stu-id="b0c1b-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="b0c1b-129">Depois de ver o aviso de estado de funcionamento do cluster Olá, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0c1b-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="b0c1b-130">Ligar toohello cluster a partir de qualquer computador que tenha máquinas Olá de tooall de acesso de administrador que estão listadas como nós num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="b0c1b-131">Olá que este script é executado no não ter toobe parte do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="b0c1b-132">Obter a lista de Olá das versões de Service Fabric que pode atualizar para o.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="b0c1b-133">Pode ser obtido um toothis semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="b0c1b-133">You should get an output similar toothis:</span></span>

    ![obter versões de recursos de infraestrutura][getfabversions]
3. <span data-ttu-id="b0c1b-135">Inicie uma versão disponível de tooan de atualização de cluster utilizando o [início ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) cmd do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="b0c1b-136">progresso de Olá toomonitor da atualização de Olá, pode utilizar o Service Fabric Explorer ou Olá executar seguinte comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="b0c1b-137">Se não forem satisfeitas as políticas de estado de funcionamento do cluster Olá, atualização Olá é revertida.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="b0c1b-138">políticas de estado de funcionamento personalizado toospecify para Olá **início ServiceFabricClusterUpgrade** comando, consulte a documentação para [início ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="b0c1b-139">Depois de corrigir os problemas de Olá que resultaram numa reversão Olá, inicie novamente a atualização Olá pelo seguinte Olá mesmos passos conforme descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="b0c1b-140">Atualizar clusters que tenham <U>sem conectividade</u> código mais recente do toodownload Olá e a configuração</span><span class="sxs-lookup"><span data-stu-id="b0c1b-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="b0c1b-141">Utilize estes passos tooupgrade a versão de tooa suportada do cluster se os nós do cluster não tem conectividade Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="b0c1b-142">Se estiver a executar um cluster que não é toohello ligado à Internet, terá toomonitor toolearn de blogue da equipa de Service Fabric de Olá sobre uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="b0c1b-143">sistema de Olá não mostra um tooalert de aviso do Estado de funcionamento de cluster de uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="b0c1b-144">Vs de aprovisionamento automático de aprovisionamento Manual</span><span class="sxs-lookup"><span data-stu-id="b0c1b-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="b0c1b-145">transferência automática de tooenable e o registo para a versão de código mais recente Olá, configurar o serviço de atualização do serviço de recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="b0c1b-146">Consulte toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro Olá [autónomo pacote](service-fabric-cluster-standalone-package-contents.md) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="b0c1b-147">Para o processo manual, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="b0c1b-148">Modificar o Olá tooset do cluster configuração seguinte propriedade toofalse antes de iniciar uma atualização da configuração.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="b0c1b-149">Consulte demasiado[início ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para detalhes de utilização.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="b0c1b-150">Certifique-se de que tooupdate 'clusterConfigurationVersion' no seu JSON antes de iniciar a atualização da configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="b0c1b-151">Fluxo de trabalho de atualização de cluster</span><span class="sxs-lookup"><span data-stu-id="b0c1b-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="b0c1b-152">Execute Get-ServiceFabricClusterUpgrade a partir de um de nós de Olá no cluster de Olá e tenha em atenção Olá TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="b0c1b-153">Seguinte Olá execução de um toolist de computador ligado à internet atualizar todas as versões compatíveis com a versão atual do Olá e transferir Olá correspondente do pacote de ligações de transferência associados Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="b0c1b-154">Ligar toohello cluster a partir de qualquer computador que tenha máquinas Olá de tooall de acesso de administrador que estão listadas como nós num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="b0c1b-155">máquina Olá que este script é executado no não tem toobe parte do cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="b0c1b-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="b0c1b-156">Copie o pacote de Olá transferido para o arquivo de imagens do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="b0c1b-157">Registe o pacote de Olá copiado.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="b0c1b-158">Inicie uma versão disponível de tooan atualização do cluster.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="b0c1b-159">Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer, ou pode executar Olá seguinte comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="b0c1b-160">Se não forem satisfeitas as políticas de estado de funcionamento do cluster Olá, atualização Olá é revertida.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="b0c1b-161">políticas de estado de funcionamento personalizado toospecify para Olá **início ServiceFabricClusterUpgrade** comando, consulte a documentação de Olá para [início ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="b0c1b-162">Depois de corrigir os problemas de Olá que resultaram numa reversão Olá, inicie novamente a atualização Olá pelo seguinte Olá mesmos passos conforme descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="b0c1b-163">Atualizar a configuração de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="b0c1b-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="b0c1b-164">Antes de iniciar a atualização da configuração de Olá, pode testar a sua nova json de configuração de cluster executando o script do powershell Olá no pacote de autónomo Olá.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="b0c1b-165">ou</span><span class="sxs-lookup"><span data-stu-id="b0c1b-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="b0c1b-166">Algumas configurações não podem ser atualizado, como pontos finais, nome do cluster, IP de nó, etc. Isto irá testar Olá novo cluster configuração json contra Olá antigo e gerar erros na janela do Powershell Olá, se existir qualquer problema.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="b0c1b-167">atualização de configuração de cluster de Olá tooupgrade, execute **início ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="b0c1b-168">atualização da configuração de Olá é processado domínio de atualização por domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="b0c1b-169">Atualização de configuração do certificado de cluster</span><span class="sxs-lookup"><span data-stu-id="b0c1b-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="b0c1b-170">Certificado de cluster é utilizado para autenticação entre nós de cluster, para que o rollover de certificado Olá devem ser efetuadas com cuidado extra porque falha irá bloquear a comunicação de Olá entre nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="b0c1b-171">Tecnicamente, são suportadas três opções:</span><span class="sxs-lookup"><span data-stu-id="b0c1b-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="b0c1b-172">Atualização do certificado único: é o caminho de atualização de Olá ' certificado de um site (primário) -> B do certificado (primário) -> certificado C (primário) ->... '.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="b0c1b-173">Duplo atualização do certificado: é o caminho de atualização de Olá ' certificado de um site (primário) -> certificado (principal) e B (secundário) -> B do certificado (primário) -> B do certificado (principal) e C (secundário) -> certificado C (primário) ->... '.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="b0c1b-174">Atualização do tipo de certificado: baseado na Thumbprint do certificado <> - certificado com base em CommonName configuração.</span><span class="sxs-lookup"><span data-stu-id="b0c1b-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="b0c1b-175">Por exemplo, o Thumbprint do certificado (principal) e Thumbprint B (secundário)-C. CommonName do certificado ></span><span class="sxs-lookup"><span data-stu-id="b0c1b-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b0c1b-176">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b0c1b-176">Next steps</span></span>
* <span data-ttu-id="b0c1b-177">Saiba como toocustomize algumas [definições de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="b0c1b-178">Saiba como demasiado[reduzir e ampliar o seu cluster](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="b0c1b-179">Saiba mais sobre [as atualizações de aplicações](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="b0c1b-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
