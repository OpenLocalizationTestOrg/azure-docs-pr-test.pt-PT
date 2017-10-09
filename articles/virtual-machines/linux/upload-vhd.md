---
title: aaaUpload ou copiar uma VM com Linux personalizada com o Azure CLI 2.0 | Microsoft Docs
description: "Carregar ou copiar uma máquina virtual personalizada utilizando o modelo de implementação do Resource Manager Olá e Olá Azure CLI 2.0"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="bb1b2-103">Criar uma VM com Linux a partir do disco personalizado com Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bb1b2-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="bb1b2-104">Este artigo mostra como tooupload um disco de rígido virtual (VHD) personalizado ou copie um um VHD existente no Azure e criar novas Linux de máquinas virtuais (VMs) do disco personalizado Olá.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="bb1b2-105">Pode instalar e configurar um requisitos do Linux distro tooyour e, em seguida, utilizar essa VHD tooquickly criar uma nova máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="bb1b2-106">Se pretender toocreate várias VMs a partir do seu disco personalizado, deve criar uma imagem do seu VM ou o VHD.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="bb1b2-107">Para obter mais informações, consulte [criar uma imagem personalizada da VM do Azure utilizando Olá CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="bb1b2-108">Tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-108">You have two options:</span></span>
* [<span data-ttu-id="bb1b2-109">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="bb1b2-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="bb1b2-110">Copiar uma VM do Azure existente</span><span class="sxs-lookup"><span data-stu-id="bb1b2-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="bb1b2-111">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="bb1b2-111">Quick commands</span></span>

<span data-ttu-id="bb1b2-112">Ao criar uma nova VM utilizando [az vm criar](/cli/azure/vm#create) partir de um disco personalizado ou especializado **anexar** disco Olá (– anexar--disco do SO) em vez de especificar uma imagem personalizada ou marketplace (– imagem).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="bb1b2-113">Olá exemplo seguinte cria uma VM chamada *myVM* através de Olá de gerido com o nome do disco *myManagedDisk* criadas a partir do seu VHD personalizado:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="bb1b2-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="bb1b2-114">Requirements</span></span>
<span data-ttu-id="bb1b2-115">Olá toocomplete os seguintes passos, tem de:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="bb1b2-116">Uma máquina virtual de Linux que tenha sido preparada para utilização no Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="bb1b2-117">Olá [preparar Olá VM](#prepare-the-vm) secção deste artigo abrange como toofind distro informações específicas sobre como instalar Olá agente Linux do Azure (waagent) que é necessária para Olá VM toowork corretamente no Azure e para toobe capaz de tooconnect tooit utilizando SSH.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="bb1b2-118">ficheiro VHD Olá existente de um [distribuição Linux aprovadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtual no formato VHD Olá.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="bb1b2-119">Várias ferramentas existem toocreate uma VM e os VHD:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="bb1b2-120">Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tendo cuidado toouse VHD como o formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="bb1b2-121">Se necessário, pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) utilizando **qemu img converter**.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="bb1b2-122">Também pode utilizar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="bb1b2-123">formato VHDX mais recente Olá não é suportado no Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="bb1b2-124">Quando cria uma VM, especifique o VHD como formato Olá.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="bb1b2-125">Se for necessário, pode converter VHDX discos tooVHD utilizando [qemu img converter](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou Olá [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="bb1b2-126">Além disso, Azure não suporta o carregamento de VHDs dinâmicos, por isso terá de tooconvert essa toostatic discos VHDs antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="bb1b2-127">Pode utilizar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert discos dinâmicos durante o processo de Olá de carregamento tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="bb1b2-128">Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="bb1b2-129">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="bb1b2-130">Os nomes de parâmetros de exemplo incluídos *myResourceGroup*, *mystorageaccount*, e *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="bb1b2-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="bb1b2-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="bb1b2-132">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="bb1b2-132">Prepare hello VM</span></span>

<span data-ttu-id="bb1b2-133">Azure suporta várias distribuições em Linux (consulte [distribuições aprovadas pelo](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="bb1b2-134">Olá seguintes artigos orientá-lo através do como tooprepare Olá várias distribuições em Linux que são suportadas no Azure:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="bb1b2-135">Distribuições baseado em centOS</span><span class="sxs-lookup"><span data-stu-id="bb1b2-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bb1b2-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="bb1b2-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bb1b2-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="bb1b2-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bb1b2-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="bb1b2-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bb1b2-139">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="bb1b2-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bb1b2-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="bb1b2-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bb1b2-141">Outras - distribuições não aprovadas</span><span class="sxs-lookup"><span data-stu-id="bb1b2-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="bb1b2-142">Consulte também Olá [Linux instalação notas](create-upload-generic.md#general-linux-installation-notes) para dicas mais gerais sobre preparar imagens de Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="bb1b2-143">Olá [plataforma Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs com o Linux apenas quando um dos Olá distribuições aprovadas pelo é utilizada com detalhes de configuração de Olá conforme especificado em versões suportadas em [Linux em aprovadas pelo Azure Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="bb1b2-144">Opção 1: Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="bb1b2-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="bb1b2-145">Pode carregar um VHD personalizado que tem de ser executado num computador local ou que tenha exportado a partir de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="bb1b2-146">toouse Olá VHD toocreate uma nova VM do Azure, necessita de tooupload Olá VHD tooa armazenamento conta e criar um disco gerido a partir de Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="bb1b2-147">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bb1b2-147">Create a resource group</span></span>

<span data-ttu-id="bb1b2-148">Antes de carregar o seu disco personalizado e a criação de VMs, terá primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="bb1b2-149">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização: [descrição geral do Azure gerida discos](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bb1b2-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="bb1b2-150">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb1b2-150">Create a storage account</span></span>

<span data-ttu-id="bb1b2-151">Criar uma conta de armazenamento para o seu disco personalizado e VMs com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="bb1b2-152">Olá exemplo seguinte cria uma conta de armazenamento com o nome *mystorageaccount* no grupo de recursos de Olá que criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="bb1b2-153">Lista de chaves de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb1b2-153">List storage account keys</span></span>
<span data-ttu-id="bb1b2-154">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="bb1b2-155">Estas chaves de acesso são utilizadas ao autenticar a conta do storage toohello, como as devidas operações de escrita.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="bb1b2-156">Leia mais sobre [gerir acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="bb1b2-157">Visualizar chaves de acesso de Olá com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="bb1b2-158">Ver as chaves de acesso Olá Olá conta de armazenamento que criou:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="bb1b2-159">saída de Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="bb1b2-160">Tome nota do **chave1** como pode utilizá-lo toointeract com a sua conta de armazenamento nos passos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="bb1b2-161">Criar um contentor de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb1b2-161">Create a storage container</span></span>
<span data-ttu-id="bb1b2-162">No Olá mesma forma que criar diretórios diferentes toologically organizar o sistema de ficheiros local, criar contentores dentro de um tooorganize de conta de armazenamento aos discos.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="bb1b2-163">Uma conta do storage pode conter qualquer número de contentores.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="bb1b2-164">Criar um contentor com [criar contentor de armazenamento az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="bb1b2-165">Olá exemplo seguinte cria um contentor com o nome *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="bb1b2-166">Carregar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="bb1b2-166">Upload hello VHD</span></span>
<span data-ttu-id="bb1b2-167">Agora carregue o seu disco personalizado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="bb1b2-168">Carregar e armazenar o disco personalizado como um blob de página.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="bb1b2-169">Especifique a chave de acesso, o contentor de Olá que criou no passo anterior Olá e, em seguida, Olá disco de personalizado toohello caminho no seu computador local:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="bb1b2-170">Carregamento Olá VHD poderá demorar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="bb1b2-171">Criar um disco gerido</span><span class="sxs-lookup"><span data-stu-id="bb1b2-171">Create a managed disk</span></span>


<span data-ttu-id="bb1b2-172">Criar um disco gerido da utilização de VHD Olá [criar disco de az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="bb1b2-173">Olá exemplo seguinte cria um disco gerido com o nome *myManagedDisk* de Olá VHD que carregou tooyour com o nome de conta de armazenamento e um contentor:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="bb1b2-174">Opção 2: Copiar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="bb1b2-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="bb1b2-175">Também pode criar Olá VM personalizada no Azure e, em seguida, disco de SO de Olá de cópia e anexe-tooa nova VM toocreate outra cópia.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="bb1b2-176">Isto é adequado para fins de teste, mas se pretender toouse uma VM do Azure existente como modelo Olá para várias novas VMs, realmente deve criar um **imagem** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="bb1b2-177">Para obter mais informações sobre como criar uma imagem de VM do Azure existente, consulte [criar uma imagem personalizada da VM do Azure utilizando Olá CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="bb1b2-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="bb1b2-178">Criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="bb1b2-178">Create a snapshot</span></span>

<span data-ttu-id="bb1b2-179">Este exemplo cria um instantâneo de uma VM chamada *myVM* no grupo de recursos *myResourceGroup* e cria um instantâneo com o nome *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="bb1b2-180">Criar disco Olá de gerido</span><span class="sxs-lookup"><span data-stu-id="bb1b2-180">Create hello managed disk</span></span>

<span data-ttu-id="bb1b2-181">Crie um novo disco gerido a partir do instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="bb1b2-182">Obter ID de Olá de instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="bb1b2-183">Neste exemplo, é denominado instantâneo Olá *osDiskSnapshot* e está a ser Olá *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="bb1b2-184">Crie disco Olá de gerido.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-184">Create hello managed disk.</span></span> <span data-ttu-id="bb1b2-185">Neste exemplo, vamos criar um disco gerido com o nome *myManagedDisk* do nosso instantâneo, que é 128 GB de tamanho no armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="bb1b2-186">Criar Olá VM</span><span class="sxs-lookup"><span data-stu-id="bb1b2-186">Create hello VM</span></span>

<span data-ttu-id="bb1b2-187">Agora, crie a VM com [az vm criar](/cli/azure/vm#create) e anexe (– anexar--disco do SO) Olá disco como disco de SO de Olá de gerido.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="bb1b2-188">Olá exemplo seguinte cria uma VM chamada *myNewVM* através de Olá de gerido criado a partir do seu carregado VHD do disco:</span><span class="sxs-lookup"><span data-stu-id="bb1b2-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="bb1b2-189">Deve ser capaz de tooSSH para Olá VM utilizando credenciais de Olá de Olá de VM de origem.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb1b2-190">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bb1b2-190">Next steps</span></span>
<span data-ttu-id="bb1b2-191">Depois de ter preparado e carregado o disco virtual personalizado, pode ler mais sobre [utilizando o Gestor de recursos e modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="bb1b2-192">Também poderá demasiado[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs.</span><span class="sxs-lookup"><span data-stu-id="bb1b2-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="bb1b2-193">Se tiver aplicações em execução no seu VMs que precisa de tooaccess, lembre-se demasiado[abrir portas e os pontos finais](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bb1b2-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

