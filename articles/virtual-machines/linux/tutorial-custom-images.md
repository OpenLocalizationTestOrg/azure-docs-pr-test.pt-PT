---
title: "aaaCreate imagens VM personalizadas com Olá CLI do Azure | Microsoft Docs"
description: "Tutorial - criar uma imagem VM personalizada utilizando Olá CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="63811-103">Criar uma imagem personalizada da VM do Azure utilizando Olá CLI</span><span class="sxs-lookup"><span data-stu-id="63811-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="63811-104">São imagens personalizadas, como imagens do marketplace, mas que são criados por si.</span><span class="sxs-lookup"><span data-stu-id="63811-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="63811-105">Imagens personalizadas podem ser utilizados toobootstrap configurações, tais como o pré-carregamento de aplicações, configurações de aplicação e outras configurações de SO.</span><span class="sxs-lookup"><span data-stu-id="63811-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="63811-106">Neste tutorial, vai criar sua imagem personalizada de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="63811-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="63811-107">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="63811-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63811-108">Desaprovisionar e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="63811-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="63811-109">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="63811-109">Create a custom image</span></span>
> * <span data-ttu-id="63811-110">Criar uma VM a partir de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="63811-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="63811-111">Lista todas as imagens de Olá na sua subscrição</span><span class="sxs-lookup"><span data-stu-id="63811-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="63811-112">Eliminar uma imagem</span><span class="sxs-lookup"><span data-stu-id="63811-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="63811-113">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="63811-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="63811-114">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="63811-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="63811-115">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="63811-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="63811-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="63811-116">Before you begin</span></span>

<span data-ttu-id="63811-117">passos de Olá abaixo de detalhe como tootake uma VM existente e ative a imagem para um reutilizável personalizado que podem utilizar toocreate novas instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="63811-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="63811-118">exemplo de Olá toocomplete neste tutorial, tem de ter uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="63811-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="63811-119">Se for necessário, isto [script de exemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) pode criar uma por si.</span><span class="sxs-lookup"><span data-stu-id="63811-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="63811-120">Quando trabalhar com tutorial de Olá, substitua o grupo de recursos de Olá e VM nomes sempre que necessário.</span><span class="sxs-lookup"><span data-stu-id="63811-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="63811-121">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="63811-121">Create a custom image</span></span>

<span data-ttu-id="63811-122">toocreate uma imagem de uma máquina virtual, terá de tooprepare Olá VM ao desaprovisionamento, Desalocação e, em seguida, marcar Olá de VM de origem como generalizado.</span><span class="sxs-lookup"><span data-stu-id="63811-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="63811-123">Uma vez Olá que VM tenha sido preparada, pode criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="63811-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="63811-124">Desaprovisionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="63811-124">Deprovision hello VM</span></span> 

<span data-ttu-id="63811-125">Desaprovisionamento generaliza Olá VM ao remover informações específicas do computador.</span><span class="sxs-lookup"><span data-stu-id="63811-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="63811-126">Este generalização torna possível toodeploy várias VMs a partir de uma única imagem.</span><span class="sxs-lookup"><span data-stu-id="63811-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="63811-127">Durante o desaprovisionamento, nome de anfitrião Olá é reposto demasiado*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="63811-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="63811-128">Chaves de anfitrião do SSH, configurações de nameserver, palavra-passe raiz e concessões DHCP em cache também são eliminados.</span><span class="sxs-lookup"><span data-stu-id="63811-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="63811-129">Olá toodeprovision VM, utilize o agente de VM do Azure de Olá (waagent).</span><span class="sxs-lookup"><span data-stu-id="63811-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="63811-130">agente de VM do Azure Olá Olá VM está instalado e gere de aprovisionamento e interagir com Olá controlador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="63811-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="63811-131">Para obter mais informações, consulte Olá [guia de utilizador do agente Linux do Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="63811-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="63811-132">Ligar tooyour VM através de SSH e Olá de toodeprovision Olá executar comandos VM.</span><span class="sxs-lookup"><span data-stu-id="63811-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="63811-133">Com Olá `+user` argumento, a última conta de utilizador aprovisionado Olá e quaisquer dados associados também são eliminados.</span><span class="sxs-lookup"><span data-stu-id="63811-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="63811-134">Substitua o endereço IP do exemplo Olá pelo endereço IP público Olá da sua VM.</span><span class="sxs-lookup"><span data-stu-id="63811-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="63811-135">SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="63811-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="63811-136">Desaprovisionar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="63811-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="63811-137">Fechar a sessão SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="63811-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="63811-138">Desalocar e marcar Olá VM como generalizado</span><span class="sxs-lookup"><span data-stu-id="63811-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="63811-139">toocreate uma imagem, tem de Olá VM toobe desalocada.</span><span class="sxs-lookup"><span data-stu-id="63811-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="63811-140">Desalocar Olá VM utilizando [az vm desalocar](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="63811-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="63811-141">Por fim, definir o estado de Olá de Olá VM como generalizado com [az vm Generalizar](/cli//azure/vm#generalize) para Olá plataforma Azure confie Olá VM tenha sido generalizada.</span><span class="sxs-lookup"><span data-stu-id="63811-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="63811-142">Só pode criar uma imagem de uma VM generalizada.</span><span class="sxs-lookup"><span data-stu-id="63811-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="63811-143">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="63811-143">Create hello image</span></span>

<span data-ttu-id="63811-144">Agora pode criar uma imagem de VM de Olá utilizando [criar imagem az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="63811-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="63811-145">Olá exemplo seguinte cria uma imagem com o nome *myImage* de uma VM chamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="63811-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="63811-146">Criar as VMs da imagem de Olá</span><span class="sxs-lookup"><span data-stu-id="63811-146">Create VMs from hello image</span></span>

<span data-ttu-id="63811-147">Agora que tem uma imagem, pode criar uma ou mais VMs novas da utilização de imagem Olá [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="63811-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="63811-148">Olá exemplo seguinte cria uma VM chamada *myVMfromImage* imagem Olá com o nome do *myImage*.</span><span class="sxs-lookup"><span data-stu-id="63811-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="63811-149">Gestão de imagens</span><span class="sxs-lookup"><span data-stu-id="63811-149">Image management</span></span> 

<span data-ttu-id="63811-150">Seguem-se alguns exemplos de tarefas comuns de gestão de imagem e como toocomplete-los utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="63811-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="63811-151">Liste todas as imagens de por nome de um formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="63811-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="63811-152">Elimine uma imagem.</span><span class="sxs-lookup"><span data-stu-id="63811-152">Delete an image.</span></span> <span data-ttu-id="63811-153">Neste exemplo eliminações Olá imagem com o nome *myOldImage* de Olá *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="63811-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="63811-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="63811-154">Next steps</span></span>

<span data-ttu-id="63811-155">Neste tutorial, vai criar uma imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="63811-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="63811-156">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="63811-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63811-157">Desaprovisionar e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="63811-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="63811-158">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="63811-158">Create a custom image</span></span>
> * <span data-ttu-id="63811-159">Criar uma VM a partir de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="63811-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="63811-160">Lista todas as imagens de Olá na sua subscrição</span><span class="sxs-lookup"><span data-stu-id="63811-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="63811-161">Eliminar uma imagem</span><span class="sxs-lookup"><span data-stu-id="63811-161">Delete an image</span></span>

<span data-ttu-id="63811-162">Produzir toohello seguinte toolearn tutorial sobre máquinas virtuais altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="63811-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="63811-163">[Criar VMs de elevada](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="63811-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

