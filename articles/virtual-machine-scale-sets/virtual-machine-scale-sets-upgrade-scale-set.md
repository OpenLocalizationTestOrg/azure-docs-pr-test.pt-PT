---
title: "conjunto de um dimensionamento de máquina virtual do Azure aaaUpgrade | Microsoft Docs"
description: "Atualizar um conjunto de dimensionamento da máquina virtual do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="bccbb-103">Atualizar um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bccbb-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="bccbb-104">Este artigo descreve como pode implementar um SO atualização tooan máquina virtual do Azure conjunto de dimensionamento sem qualquer período de inatividade.</span><span class="sxs-lookup"><span data-stu-id="bccbb-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="bccbb-105">Neste contexto, uma atualização de SO envolve alterar versão Olá ou SKU do Olá SO ou alterar Olá URI de uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="bccbb-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="bccbb-106">A atualização sem meios de período de indisponibilidade atualizar máquinas virtuais uma a uma hora ou em grupos (por exemplo, um domínio de falhas numa altura) em vez de ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="bccbb-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="bccbb-107">Ao fazê-lo, pode manter executar quaisquer máquinas virtuais que não estão a ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="bccbb-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="bccbb-108">tooavoid ambiguidade, vamos distinguir quatro tipos de atualização de SO poderá tooperform:</span><span class="sxs-lookup"><span data-stu-id="bccbb-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="bccbb-109">Alterar a versão de Olá ou SKU de uma imagem de plataforma.</span><span class="sxs-lookup"><span data-stu-id="bccbb-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="bccbb-110">Por exemplo, a alteração Ubuntu versão 14.04.2-LTS de 14.04.201506100 too14.04.201507060 ou alterar Olá Ubuntu 15.10/mais recente SKU too16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="bccbb-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="bccbb-111">Este cenário é descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="bccbb-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="bccbb-112">A alteração Olá URI que aponta tooa nova versão de uma imagem personalizada que criou (**propriedades** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **imagem** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="bccbb-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="bccbb-113">Este cenário é descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="bccbb-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="bccbb-114">A alteração Olá a referência da imagem de um conjunto de dimensionamento que foi criada utilizando discos de gerida do Azure.</span><span class="sxs-lookup"><span data-stu-id="bccbb-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="bccbb-115">Aplicação de patches Olá SO a partir de uma máquina virtual (exemplos deste incluem a instalação de um patch de segurança e executar o Windows Update).</span><span class="sxs-lookup"><span data-stu-id="bccbb-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="bccbb-116">Este cenário é suportado, mas não abrangido neste artigo.</span><span class="sxs-lookup"><span data-stu-id="bccbb-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="bccbb-117">Conjuntos de dimensionamento de máquina virtual que são implementados como parte de um [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster não são abrangidos aqui.</span><span class="sxs-lookup"><span data-stu-id="bccbb-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="bccbb-118">Consulte [Patch de SO de Windows no seu cluster do Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) para obter mais informações sobre a aplicação de patches de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bccbb-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="bccbb-119">Olá básico Olá de sequência de tarefas para alterar versão de SO/SKU de uma imagem de plataforma ou Olá URI de uma imagem personalizada procura da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="bccbb-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="bccbb-120">Obter o modelo de conjunto de dimensionamento de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="bccbb-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="bccbb-121">Alterar versão do Olá, SKU, a referência da imagem ou o valor no modelo de Olá URI.</span><span class="sxs-lookup"><span data-stu-id="bccbb-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="bccbb-122">Atualize o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="bccbb-122">Update hello model.</span></span>
4. <span data-ttu-id="bccbb-123">Fazer uma *manualUpgrade* chamar Olá máquinas de virtuais num conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="bccbb-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="bccbb-124">Este passo só é relevante se *upgradePolicy* estiver definido demasiado**Manual** no seu dimensionamento definido.</span><span class="sxs-lookup"><span data-stu-id="bccbb-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="bccbb-125">Se estiver definido demasiado**automática**, todas as máquinas de virtuais Olá sejam atualizadas em simultâneo, fazendo com que um período de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="bccbb-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="bccbb-126">Com estas informações em mente, vamos ver como foi possível atualizar a versão de Olá de um conjunto no PowerShell e utilizando Olá REST API de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="bccbb-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="bccbb-127">Estes exemplos abrangem Olá maiúsculas e minúsculas de uma imagem de plataforma, mas este artigo fornece informações suficientes para lhe tooadapt esta imagem personalizada do tooa de processo.</span><span class="sxs-lookup"><span data-stu-id="bccbb-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="bccbb-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bccbb-128">PowerShell</span></span>
<span data-ttu-id="bccbb-129">Neste exemplo de atualizações de um conjunto de dimensionamento de máquina virtual do Windows (criar toohello nova versão 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="bccbb-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="bccbb-130">Depois de atualizar o modelo de Olá, faz uma instância de máquina virtual de um de atualização de cada vez.</span><span class="sxs-lookup"><span data-stu-id="bccbb-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="bccbb-131">Se estiver a atualizar o Olá URI para uma imagem personalizada em vez de alterar uma versão de imagem de plataforma, substitua Olá "Definir Olá nova versão" Olá, linha com um comando que irá atualizar a imagem de origem URI.</span><span class="sxs-lookup"><span data-stu-id="bccbb-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="bccbb-132">Por exemplo, se o conjunto de dimensionamento de Olá foi criado sem utilizar discos gerida do Azure, atualização Olá seria este aspeto:</span><span class="sxs-lookup"><span data-stu-id="bccbb-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="bccbb-133">Se uma imagem personalizada baseada em conjunto de dimensionamento foi criada utilizando discos gerida do Azure, em seguida, a referência da imagem Olá seria atualizada.</span><span class="sxs-lookup"><span data-stu-id="bccbb-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="bccbb-134">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bccbb-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="bccbb-135">Olá REST API</span><span class="sxs-lookup"><span data-stu-id="bccbb-135">hello REST API</span></span>
<span data-ttu-id="bccbb-136">Seguem-se alguns exemplos de Python que utilizam a API REST da Azure de Olá tooroll fora de uma atualização de versão do SO.</span><span class="sxs-lookup"><span data-stu-id="bccbb-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="bccbb-137">Utilizam ambos lightweight Olá [azurerm](https://pypi.python.org/pypi/azurerm) biblioteca de API REST da Azure wrapper funções toodo uma ação obter numa escala de Olá definir modelo, seguido de um PUT com um modelo atualizado.</span><span class="sxs-lookup"><span data-stu-id="bccbb-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="bccbb-138">Podem também ver vistas de instâncias de máquina virtual tooidentify Olá máquinas virtuais por domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="bccbb-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="bccbb-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="bccbb-139">Vmssupgrade</span></span>
 <span data-ttu-id="bccbb-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) é um script de Python que tenha utilizado tooroll terminar um tooa de atualização de SO em execução de dimensionamento da máquina virtual definir um domínio de atualização de cada vez.</span><span class="sxs-lookup"><span data-stu-id="bccbb-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Script de Vmssupgrade para escolher um domínio de atualização ou máquinas virtuais](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="bccbb-142">Este script permite-lhe escolher tooupdate de máquinas virtuais específicas ou especificar um domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="bccbb-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="bccbb-143">Suporta a alteração de uma versão de imagem de plataforma ou alterar Olá URI de uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="bccbb-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="bccbb-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="bccbb-144">Vmsseditor</span></span>
<span data-ttu-id="bccbb-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) é um editor para fins gerais para conjuntos de dimensionamento de máquina virtual que mostra a virtual máquina de estado como um heatmap em que uma linha representa um domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="bccbb-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="bccbb-146">Entre outras coisas, pode atualizar o modelo de Olá para um conjunto de dimensionamento com uma nova versão, o SKU ou o URI de imagem personalizada e, em seguida, escolha tooupgrade de domínios de falhas.</span><span class="sxs-lookup"><span data-stu-id="bccbb-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="bccbb-147">Ao fazê-lo, todas as máquinas de virtuais Olá nesse domínio de atualização são toohello atualizado novo modelo.</span><span class="sxs-lookup"><span data-stu-id="bccbb-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="bccbb-148">Em alternativa, pode efetuar uma atualização sem interrupção, com base no tamanho do lote Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="bccbb-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="bccbb-149">Olá seguinte captura de ecrã mostra um modelo de um conjunto para Ubuntu 14.04-2LTS versão 14.04.201507060 de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="bccbb-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="bccbb-150">Muitas mais opções foram adicionadas toothis ferramenta desde que foi tirada nesta captura de ecrã.</span><span class="sxs-lookup"><span data-stu-id="bccbb-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Modelo de Vmsseditor de um conjunto para Ubuntu 14.04-2LTS de dimensionamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="bccbb-152">Depois de clicar em **atualizar** e, em seguida, **obter detalhes**, máquinas virtuais no UD 0 Iniciar tooupdate.</span><span class="sxs-lookup"><span data-stu-id="bccbb-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor que mostra atualização em curso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

