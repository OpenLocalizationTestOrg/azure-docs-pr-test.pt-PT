---
title: aaaCapture uma imagem de uma VM com Linux | Microsoft Docs
description: "Saiba como toocapture uma imagem de uma baseado em Linux máquina virtual do Azure (VM) é criado com o modelo de implementação clássica Olá."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="9e24a-103">Como toocapture uma máquina virtual de Linux clássica como uma imagem</span><span class="sxs-lookup"><span data-stu-id="9e24a-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9e24a-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9e24a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9e24a-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="9e24a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="9e24a-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="9e24a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9e24a-107">Saiba como demasiado[executar estes passos, utilizando o modelo do Resource Manager Olá](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e24a-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9e24a-108">Este artigo mostra como toocapture clássica do Azure máquinas virtuais (VMS) com o Linux como um toocreate imagem outras máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9e24a-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="9e24a-109">Esta imagem inclui o disco do SO Olá e discos de dados ligada toohello VM.</span><span class="sxs-lookup"><span data-stu-id="9e24a-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="9e24a-110">Não inclui a configuração de rede, por isso terá de tooconfigure que quando cria Olá outro VM da imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="9e24a-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="9e24a-111">Arquivos de Azure Olá imagem em **imagens**, juntamente com quaisquer imagens carregar.</span><span class="sxs-lookup"><span data-stu-id="9e24a-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="9e24a-112">Para obter mais informações sobre imagens, consulte [sobre imagens de Máquina Virtual no Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="9e24a-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e24a-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="9e24a-113">Before you begin</span></span>
<span data-ttu-id="9e24a-114">Estes passos partem do princípio de que já criou uma VM do Azure utilizando o modelo de implementação clássica Olá e sistema de operativo Olá configurada, incluindo anexar qualquer discos de dados.</span><span class="sxs-lookup"><span data-stu-id="9e24a-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="9e24a-115">Se precisar de toocreate uma VM, leia [como tooCreate uma Máquina Virtual Linux][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="9e24a-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="9e24a-116">Capturar a máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="9e24a-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="9e24a-117">[Ligar toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) utilizando um cliente SSH à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="9e24a-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="9e24a-118">Na janela SSH Olá, escreva Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="9e24a-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="9e24a-119">o resultado da Olá `waagent` pode variar devido às ligeiramente dependendo da versão de Olá deste utilitário:</span><span class="sxs-lookup"><span data-stu-id="9e24a-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="9e24a-120">Olá comando anterior tentativas de sistema de Olá tooclean e torná-lo adequado para reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="9e24a-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="9e24a-121">Esta operação efetua Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="9e24a-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="9e24a-122">Remove as chaves de anfitrião do SSH (se Provisioning.RegenerateSshHostKeyPair 'y' no ficheiro de configuração de Olá)</span><span class="sxs-lookup"><span data-stu-id="9e24a-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="9e24a-123">Limpa configuração nameserver /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="9e24a-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="9e24a-124">Remove Olá `root` palavra-passe de utilizador do etc/sombra de volumes (se Provisioning.DeleteRootPassword 'y' no ficheiro de configuração de Olá)</span><span class="sxs-lookup"><span data-stu-id="9e24a-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="9e24a-125">Remove as concessões de cliente DHCP em cache</span><span class="sxs-lookup"><span data-stu-id="9e24a-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="9e24a-126">Reposições toolocalhost.localdomain de nome de anfitrião</span><span class="sxs-lookup"><span data-stu-id="9e24a-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="9e24a-127">Elimina Olá último aprovisionado conta de utilizador (obtida /var/lib/waagent) **e dados associados**.</span><span class="sxs-lookup"><span data-stu-id="9e24a-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9e24a-128">Desaprovisionamento elimina os ficheiros e dados demasiado "generalize" Olá imagem.</span><span class="sxs-lookup"><span data-stu-id="9e24a-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="9e24a-129">Apenas execute este comando numa VM que pretende toocapture como um novo modelo de imagem.</span><span class="sxs-lookup"><span data-stu-id="9e24a-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="9e24a-130">Garante dessa imagem Olá é limpa de todas as informações confidenciais ou é adequada para as partes de toothird redistribuição.</span><span class="sxs-lookup"><span data-stu-id="9e24a-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="9e24a-131">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9e24a-131">Type **y** toocontinue.</span></span> <span data-ttu-id="9e24a-132">Pode adicionar Olá `-force` parâmetro tooavoid este passo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="9e24a-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="9e24a-133">Tipo **saída** cliente do tooclose Olá SSH.</span><span class="sxs-lookup"><span data-stu-id="9e24a-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9e24a-134">Olá restantes passos partem do princípio que já tem [instalado Olá CLI do Azure](../../../cli-install-nodejs.md) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="9e24a-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="9e24a-135">Também pode ser feito Olá todos os seguintes passos no Olá [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e24a-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="9e24a-136">A partir do computador cliente, abra CLI do Azure e o início de sessão tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e24a-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="9e24a-137">Para obter mais informações, leia o artigo [ligar tooan subscrição do Azure a partir de Olá CLI do Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9e24a-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="9e24a-138">No portal do Azure Olá, inicie sessão no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="9e24a-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="9e24a-139">Certifique-se de que estejam no modo de gestão do serviço:</span><span class="sxs-lookup"><span data-stu-id="9e24a-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="9e24a-140">Encerre Olá VM que já está a ser desaprovisionada.</span><span class="sxs-lookup"><span data-stu-id="9e24a-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="9e24a-141">Olá exemplo seguinte encerra Olá VM com o nome `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9e24a-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="9e24a-142">Se for necessário, pode ver uma lista Olá todas as VMs criados na sua subscrição através da utilização`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="9e24a-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="9e24a-143">Se estiver a utilizar Olá portal do Azure, selecione Olá VM e clique em **parar** encerrar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9e24a-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="9e24a-144">Quando Olá VM estiver parada, capture a imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="9e24a-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="9e24a-145">Olá seguintes capturas do exemplo Olá VM com o nome `myVM` e cria uma imagem generalizada com o nome `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="9e24a-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="9e24a-146">Olá `-t` subcomando eliminações Olá máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="9e24a-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e24a-147">No portal do Azure Olá, pode capturar uma imagem selecionando **imagem** a partir do menu do hub de Olá.</span><span class="sxs-lookup"><span data-stu-id="9e24a-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="9e24a-148">Terá de Olá toosupply seguintes informações para a imagem de Olá: nome, grupo de recursos, localização, tipo de sistema operativo e caminho do blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9e24a-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="9e24a-149">nova imagem de Olá está agora disponível na lista de Olá de imagens que pode ser tooconfigure de utilizada qualquer nova VM.</span><span class="sxs-lookup"><span data-stu-id="9e24a-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="9e24a-150">Pode vê-la com o comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="9e24a-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="9e24a-151">No Olá [portal do Azure](http://portal.azure.com), nova imagem de Olá aparece no Olá **imagens da VM (clássica)** que pertence toohello **computação** serviços.</span><span class="sxs-lookup"><span data-stu-id="9e24a-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="9e24a-152">Pode aceder ao **imagens da VM (clássica)** clicando _mais serviços_ na parte inferior de Olá de Olá Azure service lista e, em seguida, procura no Olá **computação** serviços.</span><span class="sxs-lookup"><span data-stu-id="9e24a-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Captura de imagens com êxito](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="9e24a-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9e24a-154">Next steps</span></span>
<span data-ttu-id="9e24a-155">imagem de Olá está pronto toobe utilizado toocreate VMs.</span><span class="sxs-lookup"><span data-stu-id="9e24a-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="9e24a-156">Pode utilizar o comando da CLI do Azure de Olá `azure vm create` e nome da imagem de alimentação Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="9e24a-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="9e24a-157">Para obter mais informações, consulte [Using Olá CLI do Azure com o modelo de implementação clássica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9e24a-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="9e24a-158">Em alternativa, utilize Olá [portal do Azure](http://portal.azure.com) toocreate uma VM personalizada utilizando Olá **imagem** método e Olá a seleção da imagem que criou.</span><span class="sxs-lookup"><span data-stu-id="9e24a-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="9e24a-159">Para obter mais informações, consulte [como tooCreate uma VM personalizada][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="9e24a-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="9e24a-160">**Consulte também:** [guia de utilizador do agente Linux do Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9e24a-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
