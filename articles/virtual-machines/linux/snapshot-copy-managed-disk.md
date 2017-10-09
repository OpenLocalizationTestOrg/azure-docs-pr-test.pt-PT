---
title: "aaaCopy uma gerida do Azure em disco para Back cópias de segurança | Microsoft Docs"
description: "Saiba como toocreate emite uma cópia de um toouse de disco gerida do Azure para o disco voltar se ou a resolução de problemas."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="a118b-103">Criar uma cópia de um VHD armazenado como um disco gerida do Azure, utilizando instantâneos de gerido</span><span class="sxs-lookup"><span data-stu-id="a118b-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="a118b-104">Tirar um instantâneo de um disco de gerido para cópia de segurança ou criar um disco gerido a partir do instantâneo Olá e anexe-tootroubleshoot de máquina virtual de teste tooa.</span><span class="sxs-lookup"><span data-stu-id="a118b-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="a118b-105">Um instantâneo gerido é uma cópia completa ponto no tempo de um disco de geridos de VM.</span><span class="sxs-lookup"><span data-stu-id="a118b-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="a118b-106">Cria uma cópia só de leitura do seu VHD e, por predefinição, armazena-lo como um disco gerido Standard.</span><span class="sxs-lookup"><span data-stu-id="a118b-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="a118b-107">Para obter informações sobre preços, consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="a118b-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="a118b-108">Utilize o Olá tootake de 2.0 do Azure CLI do Azure portal ou Olá um instantâneo de Olá disco gerida.</span><span class="sxs-lookup"><span data-stu-id="a118b-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="a118b-109">Utilizar o Azure CLI 2.0 tootake um instantâneo</span><span class="sxs-lookup"><span data-stu-id="a118b-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="a118b-110">Olá seguinte exemplo requer Olá Azure CLI 2.0 instalado e registado na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a118b-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="a118b-111">Olá passos seguintes mostram como tooobtain e tirar um instantâneo de um SO gerido disco Olá `az snapshot create` comando com Olá `--source-disk` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a118b-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="a118b-112">Olá seguinte exemplo assume que há uma VM chamada `myVM` criado com um disco de SO gerido no Olá `myResourceGroup` grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a118b-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="a118b-113">saída de Olá deverá ter um aspeto semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="a118b-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="a118b-114">Utilizar tootake do portal do Azure, um instantâneo</span><span class="sxs-lookup"><span data-stu-id="a118b-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="a118b-115">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a118b-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a118b-116">A partir de Olá canto superior esquerdo, clique em **novo** e procure **instantâneo**.</span><span class="sxs-lookup"><span data-stu-id="a118b-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="a118b-117">No painel de instantâneo Olá, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a118b-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="a118b-118">Introduza um **nome** para instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="a118b-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="a118b-119">Selecione um existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de Olá de tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="a118b-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="a118b-120">Selecione um localização do datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="a118b-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="a118b-121">Para **disco de origem**, selecione Olá toosnapshot de disco gerido.</span><span class="sxs-lookup"><span data-stu-id="a118b-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="a118b-122">Selecione Olá **tipo de conta** instantâneo de Olá toouse toostore.</span><span class="sxs-lookup"><span data-stu-id="a118b-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="a118b-123">Recomendamos **Standard_LRS** , a menos que o ficheiro necessário armazenados num disco elevado desempenho.</span><span class="sxs-lookup"><span data-stu-id="a118b-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="a118b-124">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a118b-124">Click **Create**.</span></span>

<span data-ttu-id="a118b-125">Se planear toouse Olá instantâneo toocreate um disco gerido e ligá-lo uma VM que necessita de toobe elevado desempenho, utilize o parâmetro de Olá `--sku Premium_LRS` com Olá `az snapshot create` comando.</span><span class="sxs-lookup"><span data-stu-id="a118b-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="a118b-126">Esta ação cria o instantâneo de Olá, para que esta está armazenada como um disco de gerido para Premium.</span><span class="sxs-lookup"><span data-stu-id="a118b-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="a118b-127">Os discos Premium geridos melhor efetuar porque são unidades de estado sólido (SSDs), mas custo mais do que os discos padrão (HDDs).</span><span class="sxs-lookup"><span data-stu-id="a118b-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


