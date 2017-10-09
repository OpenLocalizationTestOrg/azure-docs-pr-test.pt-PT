---
title: aaaDownload um VHD de Linux a partir do Azure | Microsoft Docs
description: "Transfira um VHD de Linux utilizando Olá CLI do Azure e Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="1055d-103">Transferir um VHD de Linux a partir do Azure</span><span class="sxs-lookup"><span data-stu-id="1055d-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="1055d-104">Neste artigo, saiba como toodownload um [Linux de disco rígido virtual (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ficheiro a partir do Azure com Olá CLI do Azure e o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1055d-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="1055d-105">Máquinas virtuais (VMs) em utilização do Azure [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como um toostore implementado um sistema operativo, aplicações e dados.</span><span class="sxs-lookup"><span data-stu-id="1055d-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="1055d-106">Todas as VMs do Azure de ter, pelo menos, dois discos – um disco de sistema operativo Windows e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="1055d-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="1055d-107">disco do sistema operativo Olá for criado inicialmente a partir de uma imagem e o disco do sistema operativo Olá e imagem Olá são VHDs armazenados na conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1055d-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="1055d-108">Máquinas virtuais podem ter também um ou mais discos de dados, que também são armazenados como VHDs.</span><span class="sxs-lookup"><span data-stu-id="1055d-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="1055d-109">Se ainda não o fez, instale [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="1055d-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="1055d-110">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="1055d-110">Stop hello VM</span></span>

<span data-ttu-id="1055d-111">Não é possível transferir um VHD a partir do Azure se está ligado tooa VM a executar.</span><span class="sxs-lookup"><span data-stu-id="1055d-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="1055d-112">É necessário toodownload VM de Olá toostop um VHD.</span><span class="sxs-lookup"><span data-stu-id="1055d-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="1055d-113">Se quiser toouse um VHD como um [imagem](tutorial-custom-images.md) toocreate outras VMs com novos discos, tem de toodeprovision e generalizar o sistema de operativo Olá contido no Olá de ficheiros e parar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1055d-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="1055d-114">Olá toouse VHD como um disco para uma nova instância de uma VM existente ou o disco de dados, apenas terá toostop e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1055d-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="1055d-115">toouse Olá VHD como uma imagem toocreate outras VMs, conclua estes passos:</span><span class="sxs-lookup"><span data-stu-id="1055d-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="1055d-116">Utilizar o SSH, o nome da conta Olá e o endereço IP público de Olá do Olá VM tooconnect tooit e desaprovisioná-lo.</span><span class="sxs-lookup"><span data-stu-id="1055d-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="1055d-117">Olá + utilizador parâmetro também remove a última conta de utilizador aprovisionado Olá.</span><span class="sxs-lookup"><span data-stu-id="1055d-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="1055d-118">Se estiver baking as credenciais da conta na toohello VM, deixe terminar este + parâmetro de utilizador.</span><span class="sxs-lookup"><span data-stu-id="1055d-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="1055d-119">Olá exemplo a seguir remove última conta de utilizador aprovisionado Olá:</span><span class="sxs-lookup"><span data-stu-id="1055d-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="1055d-120">Inicie sessão no tooyour a conta do Azure com [início de sessão az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1055d-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="1055d-121">Pare e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1055d-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="1055d-122">Generalize Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1055d-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="1055d-123">Olá toouse VHD como um disco para uma nova instância de uma VM existente ou o disco de dados, conclua estes passos:</span><span class="sxs-lookup"><span data-stu-id="1055d-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="1055d-124">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1055d-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="1055d-125">No menu do Hub de Olá, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="1055d-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="1055d-126">Selecione Olá VM Olá lista.</span><span class="sxs-lookup"><span data-stu-id="1055d-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="1055d-127">No painel Olá Olá VM, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="1055d-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Parar VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="1055d-129">Gerar SAS URL</span><span class="sxs-lookup"><span data-stu-id="1055d-129">Generate SAS URL</span></span>

<span data-ttu-id="1055d-130">ficheiro VHD de Olá toodownload, terá de toogenerate um [assinatura de acesso partilhado (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="1055d-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="1055d-131">Quando é gerado, o URL de Olá uma hora de expiração é atribuída toohello URL.</span><span class="sxs-lookup"><span data-stu-id="1055d-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="1055d-132">Olá menu do painel Olá Olá VM, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="1055d-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="1055d-133">Selecione o disco do sistema operativo Olá para Olá VM e, em seguida, clique em **exportar**.</span><span class="sxs-lookup"><span data-stu-id="1055d-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="1055d-134">Clique em **gerar URL**.</span><span class="sxs-lookup"><span data-stu-id="1055d-134">Click **Generate URL**.</span></span>

    ![Gerar URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="1055d-136">Transferir o VHD</span><span class="sxs-lookup"><span data-stu-id="1055d-136">Download VHD</span></span>

1.  <span data-ttu-id="1055d-137">Em Olá URL que foi gerado, clique em ficheiro VHD de Olá de transferência.</span><span class="sxs-lookup"><span data-stu-id="1055d-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Transferir o VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="1055d-139">Poderá ser necessário tooclick **guardar** na transferência do Olá browser toostart Olá.</span><span class="sxs-lookup"><span data-stu-id="1055d-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="1055d-140">nome do Olá predefinido para o ficheiro VHD Olá é *abcd*.</span><span class="sxs-lookup"><span data-stu-id="1055d-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Clique em Guardar no browser Olá](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="1055d-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1055d-142">Next steps</span></span>

- <span data-ttu-id="1055d-143">Saiba como demasiado[carregar e criar uma VM com Linux a partir do disco personalizado com Olá Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1055d-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="1055d-144">[Gerir Olá de discos do Azure CLI do Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1055d-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

