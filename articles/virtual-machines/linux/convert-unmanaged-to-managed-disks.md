---
title: "aaaConvert máquina virtual com Linux no Azure de não discos discos toomanaged - discos gerida do Azure | Microsoft Docs"
description: "Como tooconvert uma VM com Linux a partir de discos não gerido toomanaged discos utilizando o Azure CLI 2.0 no modelo de implementação do Resource Manager Olá"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="dfa17-103">Converter uma máquina virtual Linux de discos de toomanaged discos não gerido</span><span class="sxs-lookup"><span data-stu-id="dfa17-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="dfa17-104">Se tiver existentes máquinas de virtuais de Linux (VMs) que utilizam discos não geridos, pode converter Olá VMs toouse gerido discos através de Olá [Azure geridos discos](../windows/managed-disks-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="dfa17-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="dfa17-105">Este processo converte o disco de Olá SO e discos de dados anexados.</span><span class="sxs-lookup"><span data-stu-id="dfa17-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="dfa17-106">Este artigo mostra como tooconvert VMs utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfa17-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="dfa17-107">Se precisar de tooinstall ou atualizá-lo, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dfa17-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="dfa17-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="dfa17-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="dfa17-109">Converter a VMs de instância única</span><span class="sxs-lookup"><span data-stu-id="dfa17-109">Convert single-instance VMs</span></span>
<span data-ttu-id="dfa17-110">Esta secção abrange como tooconvert single-instance as VMs do Azure de não discos toomanaged discos.</span><span class="sxs-lookup"><span data-stu-id="dfa17-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="dfa17-111">(Se as suas VMs num conjunto de disponibilidade, consulte o secção seguinte Olá.) Pode utilizar este processo tooconvert Olá VMs do premium (SSD) não gerido discos toopremium gerido discos ou de standard (HDD) não geridos discos toostandard gerido discos.</span><span class="sxs-lookup"><span data-stu-id="dfa17-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="dfa17-112">Desalocar Olá VM utilizando [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dfa17-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dfa17-113">Olá exemplo seguinte deallocates Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dfa17-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="dfa17-114">Converta os discos de toomanaged VM de Olá utilizando [converter az vm](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="dfa17-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="dfa17-115">Olá seguir o processo converte Olá VM com o nome `myVM`, incluindo disco Olá SO e discos de dados:</span><span class="sxs-lookup"><span data-stu-id="dfa17-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="dfa17-116">Iniciar Olá VM após a discos de toomanaged de conversão de Olá utilizando [início de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dfa17-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dfa17-117">Olá seguir iniciado o exemplo Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="dfa17-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="dfa17-118">Converter VMs num conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="dfa17-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="dfa17-119">Se Olá VMs que pretende que sejam tooconvert toomanaged discos estão num conjunto de disponibilidade, terá primeiro tooconvert Olá disponibilidade conjunto tooa gerido conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="dfa17-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="dfa17-120">Todas as VMs no conjunto de disponibilidade de Olá tem de ser desalocadas antes de converter o conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa17-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="dfa17-121">Tooconvert plano todos os discos de toomanaged VMs depois de disponibilidade de Olá definir próprio foi convertida tooa gerido conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="dfa17-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="dfa17-122">Em seguida, iniciar todas as VMs de Olá e continuar a funcionar como normal.</span><span class="sxs-lookup"><span data-stu-id="dfa17-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="dfa17-123">Lista todas as VMs num conjunto através de disponibilidade [lista de conjunto de disponibilidade de vm az](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="dfa17-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="dfa17-124">Olá exemplo seguinte apresenta uma lista de todas as VMs no conjunto nomeada de disponibilidade de Olá `myAvailabilitySet` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dfa17-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="dfa17-125">Desalocar todas as VMs de Olá utilizando [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dfa17-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dfa17-126">Olá exemplo seguinte deallocates Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dfa17-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="dfa17-127">Converter o conjunto através de disponibilidade de Olá [converter o conjunto de disponibilidade az vm](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="dfa17-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="dfa17-128">Olá exemplo seguinte converte conjunto nomeada de disponibilidade de Olá `myAvailabilitySet` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dfa17-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="dfa17-129">Converter a todos os discos de toomanaged de VMs de Olá utilizando [converter az vm](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="dfa17-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="dfa17-130">Olá seguir o processo converte Olá VM com o nome `myVM`, incluindo disco Olá SO e discos de dados:</span><span class="sxs-lookup"><span data-stu-id="dfa17-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="dfa17-131">Iniciar todas as VMs de Olá após discos de toomanaged de conversão de Olá utilizando [início de vm az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dfa17-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dfa17-132">Olá seguir iniciado o exemplo Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dfa17-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="dfa17-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dfa17-133">Next steps</span></span>
<span data-ttu-id="dfa17-134">Para obter mais informações sobre as opções de armazenamento, consulte [descrição geral do Azure gerida discos](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfa17-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
