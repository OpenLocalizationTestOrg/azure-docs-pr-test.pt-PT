---
title: aaaCapture uma imagem de uma VM com Linux no Azure utilizando o CLI 2.0 | Microsoft Docs
description: "Capture uma imagem de toouse uma VM do Azure para implementações em massa com Olá Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="82e26-103">Como toocreate uma imagem de uma máquina virtual ou o VHD</span><span class="sxs-lookup"><span data-stu-id="82e26-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="82e26-104">toocreate várias cópias dos toouse máquina virtual (VM) no Azure, capturar uma imagem de Olá VM ou Olá VHD de SO.</span><span class="sxs-lookup"><span data-stu-id="82e26-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="82e26-105">toocreate uma imagem, tem de remover as informações de conta pessoal que torna mais segura toodeploy várias vezes.</span><span class="sxs-lookup"><span data-stu-id="82e26-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="82e26-106">Olá os seguintes passos desaprovisionar uma VM existente, Desalocação e criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="82e26-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="82e26-107">Pode utilizar esta imagem toocreate VMs em qualquer grupo de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="82e26-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="82e26-108">Se pretende toocreate uma cópia da sua VM do Linux existente para cópia de segurança ou de depuração ou carregar um VHD de Linux especializado de uma VM no local, consulte [carregar e criar uma VM com Linux a partir da imagem de disco personalizado](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="82e26-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="82e26-109">Também pode utilizar **Packer** toocreate a configuração personalizada.</span><span class="sxs-lookup"><span data-stu-id="82e26-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="82e26-110">Para obter mais informações sobre como utilizar Packer, consulte [como imagens de máquina virtual do toouse Packer toocreate Linux no Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="82e26-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="82e26-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="82e26-111">Before you begin</span></span>
<span data-ttu-id="82e26-112">Certifique-se de que cumpre Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="82e26-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="82e26-113">Precisa de uma VM do Azure criados no modelo de implementação Resource Manager Olá utilizando discos geridos.</span><span class="sxs-lookup"><span data-stu-id="82e26-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="82e26-114">Se ainda não criou uma VM com Linux, pode utilizar Olá [portal](quick-create-portal.md), Olá [CLI do Azure](quick-create-cli.md), ou [modelos do Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="82e26-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="82e26-115">Configure Olá VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="82e26-115">Configure hello VM as needed.</span></span> <span data-ttu-id="82e26-116">Por exemplo, [adicionar discos de dados](add-disk.md), aplicar atualizações e instalar aplicações.</span><span class="sxs-lookup"><span data-stu-id="82e26-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="82e26-117">Também precisa de toohave Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e de ter sessão iniciada utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="82e26-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="82e26-118">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="82e26-118">Quick commands</span></span>

<span data-ttu-id="82e26-119">Para uma versão simplificada neste tópico, para fins de teste, avaliar ou a saber mais sobre as VMs do Azure, consulte o artigo [criar uma imagem personalizada da VM do Azure utilizando Olá CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="82e26-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="82e26-120">Passo 1: Desaprovisionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="82e26-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="82e26-121">Desaprovisionar Olá VM, com o agente da VM do Azure de Olá, dados e ficheiros específicos do toodelete máquina.</span><span class="sxs-lookup"><span data-stu-id="82e26-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="82e26-122">Olá utilize `waagent` comando com Olá *-deprovision + utilizador* parâmetro na sua origem de VM com Linux.</span><span class="sxs-lookup"><span data-stu-id="82e26-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="82e26-123">Para obter mais informações, consulte Olá [guia de utilizador do agente Linux do Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="82e26-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="82e26-124">Ligar tooyour VM com Linux utilizando um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="82e26-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="82e26-125">Na janela SSH Olá, escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="82e26-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="82e26-126">Apenas execute este comando numa VM que pretende toocapture como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="82e26-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="82e26-127">Garante dessa imagem Olá é limpa de todas as informações confidenciais ou é adequada para a redistribuição.</span><span class="sxs-lookup"><span data-stu-id="82e26-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="82e26-128">Olá *+ utilizador* parâmetro também remove a última conta de utilizador aprovisionado Olá.</span><span class="sxs-lookup"><span data-stu-id="82e26-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="82e26-129">Se pretender que as credenciais da conta tookeep no Olá VM, utilize apenas *-deprovision* conta de utilizador de Olá tooleave no local.</span><span class="sxs-lookup"><span data-stu-id="82e26-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="82e26-130">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="82e26-130">Type **y** toocontinue.</span></span> <span data-ttu-id="82e26-131">Pode adicionar Olá **-forçar** parâmetro tooavoid este passo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="82e26-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="82e26-132">Após a conclusão do comando de Olá, escreva **sair**.</span><span class="sxs-lookup"><span data-stu-id="82e26-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="82e26-133">Este passo se fechar o cliente SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="82e26-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="82e26-134">Passo 2: Criar a imagem de VM</span><span class="sxs-lookup"><span data-stu-id="82e26-134">Step 2: Create VM image</span></span>
<span data-ttu-id="82e26-135">Utilize Olá de toomark Olá Azure CLI 2.0 VM como generalizado e capturar a imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="82e26-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="82e26-136">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="82e26-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="82e26-137">Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myVnet*, e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="82e26-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="82e26-138">Desalocar Olá VM desaprovisionada com [az vm desalocar](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="82e26-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="82e26-139">Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no grupo de recursos de Olá designado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="82e26-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="82e26-140">Olá marca VM como generalizado com [az vm Generalizar](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="82e26-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="82e26-141">Olá seguintes Olá Olá marcas de exemplo com o nome de VM *myVM* no grupo de recursos de Olá designado *myResourceGroup* como generalizado:</span><span class="sxs-lookup"><span data-stu-id="82e26-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="82e26-142">Agora criar uma imagem de recurso VM Olá com [criar imagem az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="82e26-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="82e26-143">Olá exemplo seguinte cria uma imagem com o nome *myImage* no grupo de recursos de Olá designado *myResourceGroup* com recurso VM de Olá designado *myVM*:</span><span class="sxs-lookup"><span data-stu-id="82e26-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="82e26-144">Olá imagem é criada na Olá mesmo grupo de recursos como a VM de origem.</span><span class="sxs-lookup"><span data-stu-id="82e26-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="82e26-145">Pode criar VMs em qualquer grupo de recursos na sua subscrição a partir desta imagem.</span><span class="sxs-lookup"><span data-stu-id="82e26-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="82e26-146">Numa perspetiva de gestão, pode ser útil toocreate um grupo de recursos específicos para os recursos da VM e imagens.</span><span class="sxs-lookup"><span data-stu-id="82e26-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="82e26-147">Passo 3: Criar uma VM da imagem de Olá capturada</span><span class="sxs-lookup"><span data-stu-id="82e26-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="82e26-148">Criar uma VM utilizando a imagem de Olá que criou com [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="82e26-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="82e26-149">Olá exemplo seguinte cria uma VM chamada *myVMDeployed* imagem Olá com o nome do *myImage*:</span><span class="sxs-lookup"><span data-stu-id="82e26-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="82e26-150">Criar Olá VM noutro grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="82e26-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="82e26-151">Pode criar VMs a partir de uma imagem em qualquer grupo de recursos na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="82e26-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="82e26-152">toocreate uma VM de um grupo de recursos diferente que imagem Olá, especifique a imagem de tooyour de ID de recurso completo de Olá.</span><span class="sxs-lookup"><span data-stu-id="82e26-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="82e26-153">Utilize [lista de imagens az](/cli/azure/image#list) tooview uma lista de imagens.</span><span class="sxs-lookup"><span data-stu-id="82e26-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="82e26-154">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="82e26-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="82e26-155">Olá exemplo seguinte utiliza [az vm criar](/cli/azure/vm#create) toocreate uma VM de um grupo de recursos diferente a imagem de origem Olá, especificando o ID de recurso de imagem de Olá:</span><span class="sxs-lookup"><span data-stu-id="82e26-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="82e26-156">Passo 4: Verificar a implementação de Olá</span><span class="sxs-lookup"><span data-stu-id="82e26-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="82e26-157">Agora SSH toohello máquina virtual é criada a implementação de Olá tooverify e utilizar o início Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="82e26-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="82e26-158">tooconnect através de SSH, localizar o endereço IP Olá ou o FQDN da sua VM com [mostrar de vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="82e26-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="82e26-159">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="82e26-159">Next steps</span></span>
<span data-ttu-id="82e26-160">Pode criar várias VMs a partir da imagem de VM de origem.</span><span class="sxs-lookup"><span data-stu-id="82e26-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="82e26-161">Se precisar de imagem de tooyour toomake alterações:</span><span class="sxs-lookup"><span data-stu-id="82e26-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="82e26-162">Crie uma VM a partir da imagem.</span><span class="sxs-lookup"><span data-stu-id="82e26-162">Create a VM from your image.</span></span>
- <span data-ttu-id="82e26-163">Fazer quaisquer atualizações ou alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="82e26-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="82e26-164">Siga Olá novamente passos toodeprovision, desalocar, generalize e criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="82e26-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="82e26-165">Utilize esta nova imagem para implementações futuras.</span><span class="sxs-lookup"><span data-stu-id="82e26-165">Use this new image for future deployments.</span></span> <span data-ttu-id="82e26-166">Se assim o desejar, elimine a imagem original Olá.</span><span class="sxs-lookup"><span data-stu-id="82e26-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="82e26-167">Para obter mais informações sobre gerir as VMs com Olá CLI, consulte [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82e26-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
