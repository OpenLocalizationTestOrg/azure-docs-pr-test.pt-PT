---
title: "aaaAzure discos de dados ligados à máquina Virtual escala conjuntos | Microsoft Docs"
description: "Saiba como toouse ligado a discos de dados com conjuntos de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="2d319-103">Conjuntos de dimensionamento de VMs do Azure e discos de dados anexados</span><span class="sxs-lookup"><span data-stu-id="2d319-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="2d319-104">Agora, os [conjuntos de dimensionamento de máquinas virtuais](/azure/virtual-machine-scale-sets/) do Azure suportam máquinas virtuais com discos de dados anexados.</span><span class="sxs-lookup"><span data-stu-id="2d319-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="2d319-105">Os discos de dados podem ser definidos no perfil de armazenamento Olá para conjuntos de dimensionamento que foram criadas com discos gerida do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d319-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="2d319-106">Anteriormente hello apenas ligado diretamente as opções de armazenamento disponíveis com as VMs em conjuntos de dimensionamento foram unidade Olá SO e unidades temporários.</span><span class="sxs-lookup"><span data-stu-id="2d319-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="2d319-107">Quando cria um conjunto com discos de dados anexados definidos de dimensionamento, terá ainda de toomount e Olá formato discos de dentro de uma VM toouse-los (apenas como autónomo VMs do Azure).</span><span class="sxs-lookup"><span data-stu-id="2d319-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="2d319-108">Uma forma conveniente toodo trata toouse uma extensão de script personalizado que chama um script padrão toopartition e formatar a todos os discos de dados de Olá numa VM.</span><span class="sxs-lookup"><span data-stu-id="2d319-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="2d319-109">Criar um conjunto de dimensionamento com discos de dados anexados</span><span class="sxs-lookup"><span data-stu-id="2d319-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="2d319-110">Toocreate uma forma simples definir com discos ligados a uma escala é toouse Olá [CLI do Azure](https://github.com/Azure/azure-cli) _vmss criar_ comando.</span><span class="sxs-lookup"><span data-stu-id="2d319-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="2d319-111">Olá seguinte exemplo cria um grupo de recursos do Azure e um conjunto de dimensionamento VM de 10 Ubuntu VMs, cada um com discos de dados anexados 2, de 50 GB e 100 GB, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="2d319-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="2d319-112">Tenha em atenção que Olá _vmss criar_ comando predefinições determinados valores de configuração se não especificá-los.</span><span class="sxs-lookup"><span data-stu-id="2d319-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="2d319-113">toosee Olá opções disponíveis que pode substituir tente:</span><span class="sxs-lookup"><span data-stu-id="2d319-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="2d319-114">Outra forma toocreate, um conjunto com discos de dados anexados de dimensionamento é toodefine uma escala definida num modelo Azure Resource Manager, incluir uma _dataDisks_ secção Olá _storageProfile_e implementar Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="2d319-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="2d319-115">Olá 50 GB e 100 GB disco exemplo acima deverá ser definido como esta no modelo de Olá:</span><span class="sxs-lookup"><span data-stu-id="2d319-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="2d319-116">Pode ver um exemplo de toodeploy concluída, pronto de um modelo de conjunto de dimensionamento com um disco ligado definido aqui: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="2d319-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="2d319-117">Adicionar uma escala existentes do disco tooan de dados definido</span><span class="sxs-lookup"><span data-stu-id="2d319-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="2d319-118">Apenas pode anexar dados discos tooa conjunto de dimensionamento da que foi criado com [Azure geridos discos](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="2d319-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="2d319-119">Pode adicionar um dados disco tooa dimensionamento definido utilizando a CLI do Azure _anexar o disco de vmss az_ comando.</span><span class="sxs-lookup"><span data-stu-id="2d319-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="2d319-120">Certifique-se de que especifica um lun que não esteja já em utilização.</span><span class="sxs-lookup"><span data-stu-id="2d319-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="2d319-121">Olá seguinte CLI exemplo adiciona uma toolun de unidade de 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="2d319-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="2d319-122">Olá seguinte o exemplo do PowerShell adiciona um toolun de unidade de 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="2d319-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="2d319-123">Tamanhos VM diferentes têm limites diferentes em números de Olá de unidades anexados suportam.</span><span class="sxs-lookup"><span data-stu-id="2d319-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="2d319-124">Verifique Olá [características de tamanho de máquina virtual](../virtual-machines/windows/sizes.md) antes de adicionar um novo disco.</span><span class="sxs-lookup"><span data-stu-id="2d319-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="2d319-125">Também pode adicionar um disco ao adicionar um novo toohello de entrada _dataDisks_ propriedade no Olá _storageProfile_ de escala definido a definição e aplicar a alteração de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d319-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="2d319-126">tootest, encontrar uma definição de conjunto de dimensionamento existente no Olá [Explorador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2d319-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="2d319-127">Selecione _editar_ e adicione uma nova lista de toohello de disco de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="2d319-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="2d319-128">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="2d319-128">E.g.</span></span> <span data-ttu-id="2d319-129">utilizar o exemplo de Olá acima:</span><span class="sxs-lookup"><span data-stu-id="2d319-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="2d319-130">Em seguida, selecione _colocar_ tooapply Olá altera o conjunto de dimensionamento tooyour.</span><span class="sxs-lookup"><span data-stu-id="2d319-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="2d319-131">Este exemplo funciona desde que utilize um tamanho de VM que suporte mais do que dois discos de dados anexados.</span><span class="sxs-lookup"><span data-stu-id="2d319-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="2d319-132">Quando efetuar o conjunto de dimensionamento de tooa uma alteração da definição de como adicionar ou remover um disco de dados, que aplica-se as VMs de tooall recentemente criado, mas apenas se aplica tooexisting VMs se hello _upgradePolicy_ propriedade está definida demasiado "automática".</span><span class="sxs-lookup"><span data-stu-id="2d319-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="2d319-133">Se estiver definido demasiado "Manual", precisa de toomanually aplicar Olá novo modelo tooexisting VMs.</span><span class="sxs-lookup"><span data-stu-id="2d319-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="2d319-134">Pode fazer isto no portal de Olá, utilizando Olá _atualização AzureRmVmssInstance_ PowerShell comandos ou utilizando Olá _az vmss update-instâncias_ comando da CLI.</span><span class="sxs-lookup"><span data-stu-id="2d319-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="2d319-135">Adicionar conjunto de dimensionamento existente do tooan de discos de dados pré-preenchidos</span><span class="sxs-lookup"><span data-stu-id="2d319-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="2d319-136">Ao adicionar discos tooan existente conjunto de dimensionamento de modelo, por predefinição, o disco de Olá será sempre criado vazio.</span><span class="sxs-lookup"><span data-stu-id="2d319-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="2d319-137">Este cenário também inclui novas instâncias criadas pelo conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d319-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="2d319-138">Este comportamento é porque a definição de scaleset Olá tem um disco de dados vazio.</span><span class="sxs-lookup"><span data-stu-id="2d319-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="2d319-139">Na ordem toocreate dados pré-preenchidos unidades para um modelo de conjunto de dimensionamento existente, pode escolher uma das junto duas opções:</span><span class="sxs-lookup"><span data-stu-id="2d319-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="2d319-140">Copie dados de discos de dados do Olá instância 0 VM toohello no Olá outras VMs, executando um script personalizado.</span><span class="sxs-lookup"><span data-stu-id="2d319-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="2d319-141">Criar uma imagem gerida com o disco de SO de Olá plus disco de dados (com dados Olá necessário) e crie um novo scaleset com imagem Olá.</span><span class="sxs-lookup"><span data-stu-id="2d319-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="2d319-142">Desta forma, cada nova VM criada terá dados de um disco que é fornecido na definição de Olá de Olá scaleset.</span><span class="sxs-lookup"><span data-stu-id="2d319-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="2d319-143">Uma vez que esta definição irá referir-se a imagem de tooan com um disco de dados que tenha personalizado dados, cada máquina virtual no Olá scaleset será pensar automaticamente com estas alterações.</span><span class="sxs-lookup"><span data-stu-id="2d319-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="2d319-144">Olá toocreate de forma uma imagem personalizada pode ser encontrada aqui: [criar uma imagem gerida de uma VM generalizada no Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="2d319-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="2d319-145">Olá utilizador precisa de toocapture Olá instância 0 VM que tenha Olá dados necessários e, em seguida, utilizar essa vhd para a definição de imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d319-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="2d319-146">Remover um disco de dados de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="2d319-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="2d319-147">Pode remover um disco de dados de um conjunto de dimensionamento de VM com o comando _az vmss disk detach_ da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d319-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="2d319-148">Por exemplo Olá seguinte comando remove o Olá disco definido no lun 2:</span><span class="sxs-lookup"><span data-stu-id="2d319-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="2d319-149">Da mesma forma, pode também remover um disco de um conjunto ao remover uma entrada de Olá de dimensionamento _dataDisks_ propriedade no Olá _storageProfile_ e aplicar a alteração de Olá.</span><span class="sxs-lookup"><span data-stu-id="2d319-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="2d319-150">Notas adicionais</span><span class="sxs-lookup"><span data-stu-id="2d319-150">Additional notes</span></span>
<span data-ttu-id="2d319-151">Suporte para discos gerida do Azure e o dimensionamento definido discos de dados anexados está disponível numa versão de API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) ou posterior do Olá Microsoft. Compute API.</span><span class="sxs-lookup"><span data-stu-id="2d319-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="2d319-152">Na implementação inicial de Olá do suporte de disco ligado para conjuntos de dimensionamento, não é possível anexar ou desanexar os discos de dados do VMs individuais num conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="2d319-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="2d319-153">O suporte do portal do Azure para discos de dados anexados em conjuntos de dimensionamento é limitado inicialmente.</span><span class="sxs-lookup"><span data-stu-id="2d319-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="2d319-154">Dependendo dos requisitos, que pode utilizar os modelos do Azure, CLI, do PowerShell, SDKs e REST API toomanage discos ligados.</span><span class="sxs-lookup"><span data-stu-id="2d319-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


