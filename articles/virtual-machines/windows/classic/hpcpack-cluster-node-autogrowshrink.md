---
title: "nós de cluster HPC Pack aaaAutoscale | Microsoft Docs"
description: "Automaticamente aumentar e diminuir o número de Olá de nós de computação de cluster HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="8ab05-103">Automaticamente aumentar e diminuir a recursos de cluster HPC Pack Olá no Azure de acordo com a carga de trabalho de cluster de toohello</span><span class="sxs-lookup"><span data-stu-id="8ab05-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="8ab05-104">Se implementar nós do Azure "rajada" no seu cluster HPC Pack ou criar um cluster HPC Pack em VMs do Azure, poderá pretender uma forma de automaticamente aumentar ou diminuir os recursos do cluster Olá como nós ou núcleos de acordo com a carga de trabalho Olá no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="8ab05-105">Dimensionar os recursos do cluster Olá desta forma permite-lhe toouse os recursos do Azure de forma mais eficiente e controlar os custos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="8ab05-106">Este artigo mostra-lhe duas formas de HPC Pack fornece recursos de computação tooautoscale:</span><span class="sxs-lookup"><span data-stu-id="8ab05-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="8ab05-107">Olá propriedade de cluster HPC Pack **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8ab05-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="8ab05-108">Olá **AzureAutoGrowShrink.ps1** script do HPC PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab05-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8ab05-109">Atualmente só automaticamente pode aumentar e diminuir a nós de computação de HPC Pack que estejam a executar um sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8ab05-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="8ab05-110">Definir a propriedade de cluster Olá AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="8ab05-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8ab05-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ab05-111">Prerequisites</span></span>

* <span data-ttu-id="8ab05-112">**HPC Pack 2012 R2 Update 2 ou posterior cluster** -nó principal do cluster Olá pode ser implementado no local ou numa VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="8ab05-113">Consulte [configurar um cluster de híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget começar a utilizar um nó principal no local e nós do Azure "rajada".</span><span class="sxs-lookup"><span data-stu-id="8ab05-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="8ab05-114">Consulte Olá [script de implementação de HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly implementar um cluster HPC Pack em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="8ab05-115">**Para um cluster com um nó principal no Azure (modelo de implementação do Resource Manager)** - a partir de HPC Pack 2016, autenticação de certificado de uma aplicação do Azure Active Directory é utilizada para a crescer automaticamente e reduzir o cluster VMs implementadas utilizando O Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ab05-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="8ab05-116">Configure um certificado da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="8ab05-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="8ab05-117">Após a implementação de cluster, se liguem ao nó principal do ambiente de trabalho remoto tooone.</span><span class="sxs-lookup"><span data-stu-id="8ab05-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="8ab05-118">Carregar o nó principal do Olá certificado (formato PFX com chave privada) tooeach e instale tooCert:\LocalMachine\My e Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="8ab05-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="8ab05-119">Inicie o Azure PowerShell como administrador e execute Olá os seguintes comandos num nó principal:</span><span class="sxs-lookup"><span data-stu-id="8ab05-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="8ab05-120">Se a sua conta está em mais do que um inquilino do Azure Active Directory ou a subscrição do Azure, pode executar o seguinte Olá comando inquilino correto do tooselect Olá e de subscrição:</span><span class="sxs-lookup"><span data-stu-id="8ab05-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="8ab05-121">Executar Olá os seguintes comandos tooview Olá atualmente selecionadas inquilino e de subscrição:</span><span class="sxs-lookup"><span data-stu-id="8ab05-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="8ab05-122">Execute o seguinte script de Olá</span><span class="sxs-lookup"><span data-stu-id="8ab05-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="8ab05-123">onde</span><span class="sxs-lookup"><span data-stu-id="8ab05-123">where</span></span>

    <span data-ttu-id="8ab05-124">**DisplayName** -nome de apresentação da aplicação Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="8ab05-125">Se a aplicação Olá não existir, será criado no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ab05-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="8ab05-126">**Home page** -Olá home page da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="8ab05-127">Pode configurar um URL fictício, tal como em Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="8ab05-128">**IdentifierUri** -identificador da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="8ab05-129">Pode configurar um URL fictício, tal como em Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="8ab05-130">**CertificateThumbprint** -Thumbprint do certificado de Olá instalado no nó principal do Olá no passo 1.</span><span class="sxs-lookup"><span data-stu-id="8ab05-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="8ab05-131">**TenantId** -ID do seu Azure Active Directory de inquilino.</span><span class="sxs-lookup"><span data-stu-id="8ab05-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="8ab05-132">Pode obter Olá ID do inquilino a partir do portal do Azure Active Directory Olá **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="8ab05-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="8ab05-133">Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="8ab05-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="8ab05-134">**Para um cluster com um nó principal no Azure (modelo de implementação clássica)** - se utilizar o cluster Olá de toocreate script Olá HPC Pack IaaS implementação no modelo de implementação clássica Olá, ativar Olá **AutoGrowShrink** cluster propriedade definindo a opção de AutoGrowShrink Olá no ficheiro de configuração de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="8ab05-135">Para obter mais informações, consulte a documentação de Olá que acompanha Olá [transferências de script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="8ab05-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="8ab05-136">Em alternativa, ativar Olá **AutoGrowShrink** propriedade cluster depois de implementar o cluster de Olá utilizando o HPC PowerShell comandos descrito Olá secção a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ab05-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="8ab05-137">tooprepare para tal, primeiro Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8ab05-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="8ab05-138">Configure um certificado de gestão do Azure no nó principal Olá e nas Olá subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="8ab05-139">Para uma implementação de teste, pode utilizar Olá predefinido Microsoft HPC Azure certificado autoassinado que instala o pacote HPC no nó principal Olá e, em seguida, carregue esse tooyour certificado de subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="8ab05-140">Para opções e passos, consulte Olá [orientações de biblioteca do TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ab05-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="8ab05-141">Executar **regedit** no nó principal Olá, aceda tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e adicione um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="8ab05-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="8ab05-142">Definir o nome do valor Olá demasiado "ThumbPrint" e valor dados toohello thumbprint do certificado de Olá no passo 1.</span><span class="sxs-lookup"><span data-stu-id="8ab05-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="8ab05-143">Propriedade do HPC PowerShell comandos tooset Olá AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="8ab05-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="8ab05-144">Seguem-se tooset de comandos do HPC PowerShell exemplo **AutoGrowShrink** e tootune respetivo comportamento com parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="8ab05-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="8ab05-145">Consulte [AutoGrowShrink parâmetros](#AutoGrowShrink-parameters) posteriormente neste artigo para a lista completa de Olá das definições.</span><span class="sxs-lookup"><span data-stu-id="8ab05-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="8ab05-146">toorun estes comandos, inicie o HPC PowerShell no nó principal do cluster Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="8ab05-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="8ab05-147">**Olá tooenable AutoGrowShrink propriedade**</span><span class="sxs-lookup"><span data-stu-id="8ab05-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="8ab05-148">**Olá toodisable AutoGrowShrink propriedade**</span><span class="sxs-lookup"><span data-stu-id="8ab05-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="8ab05-149">**Olá toochange aumente o intervalo em minutos**</span><span class="sxs-lookup"><span data-stu-id="8ab05-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="8ab05-150">**Olá toochange diminuir o intervalo em minutos**</span><span class="sxs-lookup"><span data-stu-id="8ab05-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="8ab05-151">**configuração de atual Olá tooview de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8ab05-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="8ab05-152">**grupos de nó tooexclude do AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8ab05-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="8ab05-153">Este parâmetro é suportado a partir de 2016 do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="8ab05-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="8ab05-154">Parâmetros de AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="8ab05-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="8ab05-155">Olá seguem-se AutoGrowShrink parâmetros que pode modificar utilizando Olá **conjunto HpcClusterProperty** comando.</span><span class="sxs-lookup"><span data-stu-id="8ab05-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="8ab05-156">**EnableGrowShrink** - mudar tooenable ou desativar Olá **AutoGrowShrink** propriedade.</span><span class="sxs-lookup"><span data-stu-id="8ab05-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="8ab05-157">**ParamSweepTasksPerCore** -número de varrimento paramétrico tarefas toogrow um núcleo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="8ab05-158">predefinição de Olá é toogrow um núcleo por tarefa.</span><span class="sxs-lookup"><span data-stu-id="8ab05-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8ab05-159">Alterações de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** demasiado**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="8ab05-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="8ab05-160">-Baseia-se no tipo de recurso de tarefa Olá e pode ser nó, socket ou core.</span><span class="sxs-lookup"><span data-stu-id="8ab05-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="8ab05-161">**GrowThreshold** -limiar de aumento automático do tootrigger tarefas em fila.</span><span class="sxs-lookup"><span data-stu-id="8ab05-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="8ab05-162">predefinição de Olá é 1, o que significa que o se existirem 1 ou mais tarefas no Olá em fila de estado, aumentar automaticamente nós.</span><span class="sxs-lookup"><span data-stu-id="8ab05-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="8ab05-163">**GrowInterval** -intervalo de aumento automático do tootrigger minutos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="8ab05-164">intervalo de Olá predefinido é 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="8ab05-165">**ShrinkInterval** -intervalo em minutos tootrigger automática reduzir.</span><span class="sxs-lookup"><span data-stu-id="8ab05-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="8ab05-166">intervalo de predefinido de Olá é de 5 minutos. |</span><span class="sxs-lookup"><span data-stu-id="8ab05-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="8ab05-167">**ShrinkIdleTimes** -número de nós de Olá verificações contínua tooshrink tooindicate está inativo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="8ab05-168">predefinição de Olá é 3 vezes.</span><span class="sxs-lookup"><span data-stu-id="8ab05-168">hello default is 3 times.</span></span> <span data-ttu-id="8ab05-169">Por exemplo, se hello **ShrinkInterval** é de 5 minutos, HPC Pack verifica se o nó de Olá está inativo a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="8ab05-170">Se nós de Olá num estado inativo Olá depois 3 contínua verifica (15 minutos), pacote HPC diminui nesse nó.</span><span class="sxs-lookup"><span data-stu-id="8ab05-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="8ab05-171">**ExtraNodesGrowRatio** -percentagem adicional de nós toogrow para tarefas de Interface de passagem de mensagens (MPI).</span><span class="sxs-lookup"><span data-stu-id="8ab05-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="8ab05-172">valor predefinido de Olá é 1, o que significa que o pacote HPC cresce nós % 1 para tarefas MPI.</span><span class="sxs-lookup"><span data-stu-id="8ab05-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="8ab05-173">**GrowByMin** -se a política de aumento automático Olá baseia-se nos recursos de Olá mínimo necessários para a tarefa de Olá tooindicate de comutador.</span><span class="sxs-lookup"><span data-stu-id="8ab05-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="8ab05-174">Olá predefinição é false, o que significa que o pacote HPC cresce nós para as tarefas com base nos recursos de máximo de Olá necessários para as tarefas de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="8ab05-175">**SoaJobGrowThreshold** -limiar de entrada SOA pedidos tootrigger Olá automática aumentar o processo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="8ab05-176">valor predefinido de Olá é 50000.</span><span class="sxs-lookup"><span data-stu-id="8ab05-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8ab05-177">Este parâmetro é suportado a partir de HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="8ab05-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="8ab05-178">**SoaRequestsPerCore** -número de SOA recebido pedidos toogrow um núcleo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="8ab05-179">valor predefinido de Olá é de 20000.</span><span class="sxs-lookup"><span data-stu-id="8ab05-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8ab05-180">Este parâmetro é suportado a partir de HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="8ab05-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="8ab05-181">**ExcludeNodeGroups** – especificado de nós no Olá grupos de nó automaticamente aumentar e diminuir.</span><span class="sxs-lookup"><span data-stu-id="8ab05-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8ab05-182">Este parâmetro é suportado a partir de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="8ab05-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="8ab05-183">Exemplo MPI</span><span class="sxs-lookup"><span data-stu-id="8ab05-183">MPI example</span></span>
<span data-ttu-id="8ab05-184">Por predefinição HPC Pack crescimentos de 1% nós adicionais para os trabalhos MPI (**ExtraNodesGrowRatio** está definido too1).</span><span class="sxs-lookup"><span data-stu-id="8ab05-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="8ab05-185">motivo Olá é que MPI pode necessitar de vários nós e tarefa Olá só pode ser executada quando todos os nós estão prontos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="8ab05-186">Quando Azure é iniciado nós, ocasionalmente, um nó pode ter mais tempo toostart que outros, fazendo com que outras toobe nós inativo enquanto aguardam que tooget esse nó pronto.</span><span class="sxs-lookup"><span data-stu-id="8ab05-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="8ab05-187">Incrementando nós adicionais, HPC Pack reduz o tempo de espera este recurso e, potencialmente, guarda os custos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="8ab05-188">percentagem de Olá tooincrease de nós adicionais para trabalhos MPI (por exemplo, too10%), execute um comando semelhante ao</span><span class="sxs-lookup"><span data-stu-id="8ab05-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="8ab05-189">Exemplo SOA</span><span class="sxs-lookup"><span data-stu-id="8ab05-189">SOA example</span></span>
<span data-ttu-id="8ab05-190">Por predefinição, **SoaJobGrowThreshold** está definido too50000 e **SoaRequestsPerCore** está definido too200000.</span><span class="sxs-lookup"><span data-stu-id="8ab05-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="8ab05-191">Se submeter uma tarefa SOA com 70000 pedidos, existe uma tarefa em fila e os pedidos recebidos são 70000.</span><span class="sxs-lookup"><span data-stu-id="8ab05-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="8ab05-192">Neste caso, o HPC Pack cresce 1 núcleo Olá colocados em fila de tarefas e para pedidos recebidos, cresce (70000 50000) / core 20000 = 1, no total crescimentos de 2 núcleos para esta tarefa SOA.</span><span class="sxs-lookup"><span data-stu-id="8ab05-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="8ab05-193">Executar script de AzureAutoGrowShrink.ps1 Olá</span><span class="sxs-lookup"><span data-stu-id="8ab05-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8ab05-194">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ab05-194">Prerequisites</span></span>

* <span data-ttu-id="8ab05-195">**HPC Pack 2012 R2 Update 1 ou posterior cluster** - hello **AzureAutoGrowShrink.ps1** script está instalado na pasta bin Olá % CCP_HOME %.</span><span class="sxs-lookup"><span data-stu-id="8ab05-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="8ab05-196">nó principal do cluster Olá pode ser implementado no local ou numa VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="8ab05-197">Consulte [configurar um cluster de híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget começar a utilizar um nó principal no local e nós do Azure "rajada".</span><span class="sxs-lookup"><span data-stu-id="8ab05-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="8ab05-198">Consulte Olá [script de implementação de HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly implementar um cluster HPC Pack em VMs do Azure ou utilize um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="8ab05-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="8ab05-199">**O Azure PowerShell 1.4.0** -script Olá depende atualmente esta versão específica do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ab05-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="8ab05-200">**Para um cluster com o Azure burst nós** -executar script de Olá num computador cliente onde o HPC Pack está instalado, ou no nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="8ab05-201">Se em execução num computador cliente, certifique-se de que definiu Olá $env variável: nó principal do CCP_SCHEDULER toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="8ab05-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="8ab05-202">Olá do Azure "rajada" nós têm de ser adicionados toohello cluster, mas podem estar a ser Olá Estado não implementadas.</span><span class="sxs-lookup"><span data-stu-id="8ab05-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="8ab05-203">**Para um cluster implementado em VMs do Azure (modelo de implementação do Resource Manager)** -num cluster de VMs do Azure implementadas no modelo de implementação do Resource Manager Olá, o script de Olá suporta dois métodos de autenticação do Azure: a iniciar sessão tooyour conta do Azure script de Olá toorun sempre (executando `Login-AzureRmAccount`, ou configurar um tooauthenticate principal de serviço com um certificado.</span><span class="sxs-lookup"><span data-stu-id="8ab05-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="8ab05-204">Pacote HPC fornece o script de Olá **ConfigARMAutoGrowShrinkCert.ps** toocreate um principal de serviço com o certificado.</span><span class="sxs-lookup"><span data-stu-id="8ab05-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="8ab05-205">script de Olá cria uma aplicação do Azure Active Directory (Azure AD) e um principal de serviço e atribui o principal de serviço de toohello de função de contribuinte de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="8ab05-206">script de Olá toorun, inicie o Azure PowerShell como administrador e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8ab05-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="8ab05-207">Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="8ab05-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="8ab05-208">**Para um cluster implementado em VMs do Azure (modelo de implementação clássica)** -execute o script de Olá no nó principal do Olá VM, porque depende de Olá **início HpcIaaSNode.ps1** e **Stop-HpcIaaSNode.ps1**scripts que são instaladas não existe.</span><span class="sxs-lookup"><span data-stu-id="8ab05-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="8ab05-209">Esses scripts adicionalmente requerem um certificado de gestão do Azure ou publicar o ficheiro de definições (consulte [cluster de nós de computação de gerir num pacote HPC no Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="8ab05-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="8ab05-210">Certifique-se de que todos os Olá nó VMs terá já foram adicionadas toohello cluster de computação.</span><span class="sxs-lookup"><span data-stu-id="8ab05-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="8ab05-211">Estes poderão Olá estado parado.</span><span class="sxs-lookup"><span data-stu-id="8ab05-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="8ab05-212">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="8ab05-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="8ab05-213">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8ab05-213">Parameters</span></span>
* <span data-ttu-id="8ab05-214">**NodeTemplates** -nomes de Olá nó modelos toodefine Olá âmbito Olá nós toogrow e diminuir.</span><span class="sxs-lookup"><span data-stu-id="8ab05-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="8ab05-215">Se não for especificado (valor predefinido de Olá é @()), todos os nós no Olá **AzureNodes** grupo de nós estão no âmbito quando **NodeType** tem um valor de AzureNodes e todos os nós no Olá **ComputeNodes** grupo de nós estão no âmbito quando **NodeType** tem um valor de ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="8ab05-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="8ab05-216">**JobTemplates** -nomes de Olá âmbito de Olá toodefine modelos para Olá nós toogrow da tarefa.</span><span class="sxs-lookup"><span data-stu-id="8ab05-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="8ab05-217">**NodeType** - Olá o tipo de nó toogrow e diminuir.</span><span class="sxs-lookup"><span data-stu-id="8ab05-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="8ab05-218">Os valores suportados são:</span><span class="sxs-lookup"><span data-stu-id="8ab05-218">Supported values are:</span></span>

  * <span data-ttu-id="8ab05-219">**AzureNodes** – para nós do Azure PaaS (rajada) no local ou cluster do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="8ab05-220">**ComputeNodes** – para o nó de computação VMs apenas um cluster do IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab05-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="8ab05-221">**NumOfQueuedJobsPerNodeToGrow** -número de tarefas em fila necessários toogrow um nó.</span><span class="sxs-lookup"><span data-stu-id="8ab05-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="8ab05-222">**NumOfQueuedJobsToGrowThreshold** -Olá limiar diversas Olá toostart de tarefas em fila aumentar o processo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="8ab05-223">**NumOfActiveQueuedTasksPerNodeToGrow** -número de Olá das tarefas em fila Active Directory necessários toogrow um nó.</span><span class="sxs-lookup"><span data-stu-id="8ab05-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="8ab05-224">Se **NumOfQueuedJobsPerNodeToGrow** for especificado com um valor maior que 0, este parâmetro será ignorado.</span><span class="sxs-lookup"><span data-stu-id="8ab05-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="8ab05-225">**NumOfActiveQueuedTasksToGrowThreshold** -Olá limiar diversas Olá do Active Directory tarefas em fila toostart aumentar o processo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="8ab05-226">**NumOfInitialNodesToGrow** - hello inicial número mínimo de nós toogrow se todos os nós de Olá no âmbito são **implementadas não** ou **parado (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="8ab05-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="8ab05-227">**GrowCheckIntervalMins** -intervalo de Olá em minutos entre verifica toogrow.</span><span class="sxs-lookup"><span data-stu-id="8ab05-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="8ab05-228">**ShrinkCheckIntervalMins** -intervalo de Olá em minutos entre verifica tooshrink.</span><span class="sxs-lookup"><span data-stu-id="8ab05-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="8ab05-229">**ShrinkCheckIdleTimes** -Olá número de verificações de operação de encolhimento contínua (separados por **ShrinkCheckIntervalMins**) nós de Olá tooindicate estão inativos.</span><span class="sxs-lookup"><span data-stu-id="8ab05-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="8ab05-230">**UseLastConfigurations** -Olá configurações anteriores guardadas no ficheiro de argumento Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="8ab05-231">**ArgFile**- Olá nome Olá argumento ficheiro utilizado toosave e atualizar o script de Olá Olá configurações toorun.</span><span class="sxs-lookup"><span data-stu-id="8ab05-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="8ab05-232">**LogFilePrefix** -nome de prefixo Olá Olá do ficheiro de registo.</span><span class="sxs-lookup"><span data-stu-id="8ab05-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="8ab05-233">Pode especificar um caminho.</span><span class="sxs-lookup"><span data-stu-id="8ab05-233">You can specify a path.</span></span> <span data-ttu-id="8ab05-234">Por predefinição o registo Olá é escrito toohello atual diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8ab05-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="8ab05-235">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="8ab05-235">Example 1</span></span>
<span data-ttu-id="8ab05-236">Olá exemplo a seguir configura Olá Azure burst nós implementados com o modelo predefinido de AzureNode toogrow e reduzir automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8ab05-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="8ab05-237">Se todos os nós inicialmente no Olá **implementadas não** Estado, pelo menos 3 nós são iniciados.</span><span class="sxs-lookup"><span data-stu-id="8ab05-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="8ab05-238">Se o número de Olá de tarefas em fila exceder 8, o script Olá inicia nós até que o respetivo número excede o rácio de Olá de tarefas em fila a **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="8ab05-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="8ab05-239">Se um nó for encontrado toobe inativo em 3 vezes consecutivas de inatividade, está parado.</span><span class="sxs-lookup"><span data-stu-id="8ab05-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="8ab05-240">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="8ab05-240">Example 2</span></span>
<span data-ttu-id="8ab05-241">Olá exemplo a seguir configura Olá Azure implementadas com Olá modelo predefinido de ComputeNode toogrow de VMs de nó de computação e reduzir automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8ab05-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="8ab05-242">tarefas de Olá configuradas pelo modelo de tarefa Olá predefinido definem âmbito de Olá da carga de trabalho no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ab05-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="8ab05-243">Se todos os nós de Olá inicialmente são parados, pelo menos 5 nós são iniciados.</span><span class="sxs-lookup"><span data-stu-id="8ab05-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="8ab05-244">Se o número de Olá do Active Directory tarefas em fila exceder 15, o script Olá inicia nós até que o respetivo número excede rácio Olá do Active Directory tarefas em fila demasiado**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="8ab05-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="8ab05-245">Se um nó for encontrado toobe inativo em 10 vezes consecutivas de inatividade, está parado.</span><span class="sxs-lookup"><span data-stu-id="8ab05-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
