---
title: aaaUpload um disco do Linux personalizado com o Azure CLI 2.0 | Microsoft Docs
description: "Criar e carregar um tooAzure de disco rígido virtual (VHD) utilizando o modelo de implementação do Resource Manager Olá e Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="0695e-103">Carregar e criar uma VM com Linux a partir do disco personalizado com Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0695e-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="0695e-104">Este artigo mostra-lhe como tooupload tooan um disco rígido virtual (VHD) storage do Azure da conta com Olá 2.0 de CLI do Azure e criar VMs com Linux a partir deste disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="0695e-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="0695e-105">Também pode executar estes passos com Olá [CLI do Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0695e-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0695e-106">Esta funcionalidade permite-lhe tooinstall e configurar um requisitos do Linux distro tooyour e, em seguida, utilizar essa VHD tooquickly criar máquinas de virtuais (VMs) do Azure.</span><span class="sxs-lookup"><span data-stu-id="0695e-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="0695e-107">Este tópico utiliza contas de armazenamento para hello VHDs finais, mas também pode fazer estes passos através de [discos geridos pelo](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="0695e-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="0695e-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="0695e-108">Quick commands</span></span>
<span data-ttu-id="0695e-109">Se precisar de tooquickly realizar tarefas Olá, Olá Olá de detalhes de secção a seguir base tooupload comandos tooAzure um VHD.</span><span class="sxs-lookup"><span data-stu-id="0695e-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="0695e-110">Mais informações e o contexto de cada passo pode ser encontrado rest Olá documento Olá, [Iniciar aqui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="0695e-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="0695e-111">Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0695e-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0695e-112">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="0695e-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0695e-113">Os nomes de parâmetros de exemplo incluídos `myResourceGroup`, `mystorageaccount`, e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="0695e-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="0695e-114">Em primeiro lugar, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0695e-115">Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `WestUs` localização:</span><span class="sxs-lookup"><span data-stu-id="0695e-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="0695e-116">Criar um toohold de conta de armazenamento de discos virtuais com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="0695e-117">Olá exemplo seguinte cria uma conta de armazenamento com o nome `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="0695e-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="0695e-118">Listar chaves de acesso de Olá para a sua conta de armazenamento com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="0695e-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="0695e-119">Tome nota do `key1`:</span><span class="sxs-lookup"><span data-stu-id="0695e-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="0695e-120">Criar um contentor na sua conta de armazenamento utilizando a chave de armazenamento Olá obtida com [criar contentor de armazenamento az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="0695e-121">Olá exemplo seguinte cria um contentor com o nome `mydisks` utilizando o valor de chave de armazenamento de Olá de `key1`:</span><span class="sxs-lookup"><span data-stu-id="0695e-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="0695e-122">Por fim, carregue o contentor de toohello do VHD que criou com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="0695e-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="0695e-123">Especifique o caminho local de Olá tooyour VHD em `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="0695e-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="0695e-124">Especifique Olá URI tooyour disco (`--image`) com [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0695e-125">Olá exemplo seguinte cria uma VM chamada `myVM` utilização de disco virtual Olá carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0695e-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="0695e-126">conta de armazenamento de destino Olá tem toobe Olá mesmo como onde o seu disco virtual para que carregou.</span><span class="sxs-lookup"><span data-stu-id="0695e-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="0695e-127">É também necessário toospecify ou responder a pedidos de, Olá todos os parâmetros adicionais necessários ao hello **az vm criar** comando tais como a rede virtual, o endereço IP público, o nome de utilizador e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="0695e-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="0695e-128">Pode ler mais sobre Olá [parâmetros disponíveis de Gestor de recursos do CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="0695e-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="0695e-129">Requisitos</span><span class="sxs-lookup"><span data-stu-id="0695e-129">Requirements</span></span>
<span data-ttu-id="0695e-130">Olá toocomplete os seguintes passos, tem de:</span><span class="sxs-lookup"><span data-stu-id="0695e-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="0695e-131">**Sistema de operativo Linux instalado num ficheiro. vhd** -instalar um [distribuição Linux aprovadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual Olá VHD formato.</span><span class="sxs-lookup"><span data-stu-id="0695e-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="0695e-132">Várias ferramentas existem toocreate uma VM e os VHD:</span><span class="sxs-lookup"><span data-stu-id="0695e-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="0695e-133">Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tendo cuidado toouse VHD como o formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="0695e-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="0695e-134">Se necessário, pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) utilizando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="0695e-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="0695e-135">Também pode utilizar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0695e-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0695e-136">formato VHDX mais recente Olá não é suportado no Azure.</span><span class="sxs-lookup"><span data-stu-id="0695e-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="0695e-137">Quando cria uma VM, especifique o VHD como formato Olá.</span><span class="sxs-lookup"><span data-stu-id="0695e-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="0695e-138">Se for necessário, pode converter VHDX discos tooVHD utilizando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou Olá [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0695e-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="0695e-139">Além disso, Azure não suporta o carregamento de VHDs dinâmicos, por isso terá de tooconvert essa toostatic discos VHDs antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="0695e-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="0695e-140">Pode utilizar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinâmicos durante o processo de Olá de carregamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0695e-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="0695e-141">VMs criadas a partir do seu disco personalizado tem de residir na Olá mesma conta de armazenamento como disco de Olá próprio</span><span class="sxs-lookup"><span data-stu-id="0695e-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="0695e-142">Criar toohold de conta e contentor de armazenamento do disco personalizado e VMs criadas</span><span class="sxs-lookup"><span data-stu-id="0695e-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="0695e-143">Depois de criar as suas VMs, pode eliminar em segurança o disco</span><span class="sxs-lookup"><span data-stu-id="0695e-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="0695e-144">Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0695e-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0695e-145">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="0695e-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0695e-146">Os nomes de parâmetros de exemplo incluídos `myResourceGroup`, `mystorageaccount`, e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="0695e-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="0695e-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="0695e-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="0695e-148">Preparar Olá disco toobe carregado</span><span class="sxs-lookup"><span data-stu-id="0695e-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="0695e-149">Azure suporta várias distribuições em Linux (consulte [distribuições aprovadas pelo](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="0695e-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="0695e-150">Olá seguintes artigos orientá-lo através do como tooprepare Olá várias distribuições em Linux que são suportadas no Azure:</span><span class="sxs-lookup"><span data-stu-id="0695e-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="0695e-151">**[Distribuições baseado em centOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0695e-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0695e-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0695e-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0695e-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0695e-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="0695e-157">**[Outras - distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="0695e-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="0695e-158">Consulte também Olá  **[Linux instalação notas](create-upload-generic.md#general-linux-installation-notes)**  para dicas mais gerais sobre preparar imagens de Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="0695e-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="0695e-159">Olá [plataforma Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs com o Linux apenas quando um dos Olá distribuições aprovadas pelo é utilizada com detalhes de configuração de Olá conforme especificado em versões suportadas em [Linux em aprovadas pelo Azure Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0695e-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="0695e-160">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0695e-160">Create a resource group</span></span>
<span data-ttu-id="0695e-161">Grupos de recursos logicamente reunir toosupport de recursos do Azure Olá todas as suas máquinas virtuais, tais como redes virtuais Olá e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0695e-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="0695e-162">Para grupos de recursos mais informações, consulte [descrição geral de grupos de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0695e-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0695e-163">Antes de carregar o seu disco personalizado e a criação de VMs, terá primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="0695e-164">Olá exemplo seguinte cria um grupo de recursos denominado `myResourceGroup` no Olá `westus` localização:</span><span class="sxs-lookup"><span data-stu-id="0695e-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="0695e-165">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0695e-165">Create a storage account</span></span>

<span data-ttu-id="0695e-166">Criar uma conta de armazenamento para o seu disco personalizado e VMs com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="0695e-167">Quaisquer VMs com discos não geridos que cria a partir do seu toobe necessidade de disco personalizado no Olá a mesma conta de armazenamento como esse disco.</span><span class="sxs-lookup"><span data-stu-id="0695e-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="0695e-168">Olá exemplo seguinte cria uma conta de armazenamento com o nome `mystorageaccount` no grupo de recursos de Olá que criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0695e-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="0695e-169">Lista de chaves de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0695e-169">List storage account keys</span></span>
<span data-ttu-id="0695e-170">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0695e-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="0695e-171">Estas chaves de acesso são utilizadas ao autenticar a conta do storage toohello, tais como toocarry operações de escrita.</span><span class="sxs-lookup"><span data-stu-id="0695e-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="0695e-172">Leia mais sobre [gerir acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0695e-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="0695e-173">Visualizar chaves de acesso de Olá com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="0695e-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="0695e-174">Ver as chaves de acesso Olá Olá conta de armazenamento que criou:</span><span class="sxs-lookup"><span data-stu-id="0695e-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="0695e-175">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="0695e-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="0695e-176">Tome nota do `key1` como pode utilizá-lo toointeract com a sua conta de armazenamento nos passos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="0695e-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="0695e-177">Criar um contentor de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0695e-177">Create a storage container</span></span>
<span data-ttu-id="0695e-178">No Olá mesma forma que criar diretórios diferentes toologically organizar o sistema de ficheiros local, criar contentores dentro de um tooorganize de conta de armazenamento aos discos.</span><span class="sxs-lookup"><span data-stu-id="0695e-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="0695e-179">Uma conta do storage pode conter qualquer número de contentores.</span><span class="sxs-lookup"><span data-stu-id="0695e-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="0695e-180">Criar um contentor com [criar contentor de armazenamento az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="0695e-181">Olá exemplo seguinte cria um contentor com o nome `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="0695e-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="0695e-182">Carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="0695e-182">Upload VHD</span></span>
<span data-ttu-id="0695e-183">Agora carregue o seu disco personalizado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="0695e-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="0695e-184">Carregar e armazenar o disco personalizado como um blob de página.</span><span class="sxs-lookup"><span data-stu-id="0695e-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="0695e-185">Especifique a chave de acesso, o contentor de Olá que criou no passo anterior Olá e, em seguida, Olá disco de personalizado toohello caminho no seu computador local:</span><span class="sxs-lookup"><span data-stu-id="0695e-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="0695e-186">Criar Olá VM</span><span class="sxs-lookup"><span data-stu-id="0695e-186">Create hello VM</span></span>
<span data-ttu-id="0695e-187">toocreate uma VM com os discos não geridos, especifique o disco do Olá URI tooyour (`--image`) com [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0695e-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0695e-188">Olá exemplo seguinte cria uma VM chamada `myVM` utilização de disco virtual Olá carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0695e-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="0695e-189">Especifique Olá `--image` parâmetro com [az vm criar](/cli/azure/vm#create) toopoint tooyour personalizado disco.</span><span class="sxs-lookup"><span data-stu-id="0695e-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="0695e-190">Certifique-se de que `--storage-account` correspondências Olá conta do storage onde está armazenado o seu disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="0695e-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="0695e-191">Não dispõe de toouse Olá mesmo contentor como Olá disco personalizado toostore as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="0695e-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="0695e-192">Certifique-se de que toocreate quaisquer contentores adicionais Olá igual forma ao hello passos anteriores antes de carregar o seu disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="0695e-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="0695e-193">Olá exemplo seguinte cria uma VM chamada `myVM` do seu disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="0695e-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="0695e-194">Ainda necessário toospecify, ou responder a pedidos de, Olá todos os parâmetros adicionais necessários ao hello **az vm criar** comando como o nome de utilizador e as chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="0695e-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="0695e-195">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0695e-195">Resource Manager template</span></span>
<span data-ttu-id="0695e-196">Modelos Azure Resource Manager são ficheiros JavaScript Object Notation (JSON) que definem o ambiente de Olá desejar toobuild.</span><span class="sxs-lookup"><span data-stu-id="0695e-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="0695e-197">modelos de Olá são divididos em toodifferent fornecedores de recursos, tais como a computação ou rede.</span><span class="sxs-lookup"><span data-stu-id="0695e-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="0695e-198">Pode utilizar os modelos existentes ou escrever os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="0695e-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="0695e-199">Leia mais sobre [utilizando o Gestor de recursos e modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0695e-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="0695e-200">Dentro do Olá `Microsoft.Compute/virtualMachines` fornecedor do seu modelo, tiver um `storageProfile` nó que contém os detalhes de configuração de Olá para a VM.</span><span class="sxs-lookup"><span data-stu-id="0695e-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="0695e-201">Olá dois parâmetros principal tooedit são Olá `image` e `vhd` URIs ponto disco personalizado tooyour e disco virtual a nova VM.</span><span class="sxs-lookup"><span data-stu-id="0695e-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="0695e-202">seguinte Olá mostra um exemplo de Olá JSON para utilizar um disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="0695e-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="0695e-203">Pode utilizar [este toocreate modelo existente uma VM a partir de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou leia sobre [criar os seus próprios modelos Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0695e-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="0695e-204">Assim que tiver um modelo configurado, utilize [criar a implementação do grupo az](/cli/azure/group/deployment#create) toocreate as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="0695e-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="0695e-205">Especifique o URI do seu modelo JSON de Olá com Olá `--template-uri` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="0695e-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="0695e-206">Se tiver um ficheiro JSON armazenado localmente no seu computador, pode utilizar Olá `--template-file` parâmetro em vez disso:</span><span class="sxs-lookup"><span data-stu-id="0695e-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="0695e-207">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0695e-207">Next steps</span></span>
<span data-ttu-id="0695e-208">Depois de ter preparado e carregado o disco virtual personalizado, pode ler mais sobre [utilizando o Gestor de recursos e modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0695e-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0695e-209">Também poderá demasiado[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs.</span><span class="sxs-lookup"><span data-stu-id="0695e-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="0695e-210">Se tiver aplicações em execução no seu VMs que precisa de tooaccess, lembre-se demasiado[abrir portas e os pontos finais](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0695e-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

