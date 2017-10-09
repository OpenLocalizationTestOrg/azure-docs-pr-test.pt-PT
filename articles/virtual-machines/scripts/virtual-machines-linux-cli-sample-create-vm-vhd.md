---
title: aaaAzure CLI Script de exemplo - criar uma VM com um VHD | Microsoft Docs
description: "Script CLI do Azure de exemplo - criar uma VM utilizando um disco rígido virtual."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="b9037-103">Criar uma VM com um disco rígido virtual</span><span class="sxs-lookup"><span data-stu-id="b9037-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="b9037-104">Este exemplo cria uma máquina virtual utilizando um VHD.</span><span class="sxs-lookup"><span data-stu-id="b9037-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="b9037-105">Cria um grupo de recursos, uma conta do storage e um contentor, em seguida, cria uma VM através do carregamento de contentor de toohello Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="b9037-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="b9037-106">Substitui Olá ssh pública da chave com a chave pública para que tenha acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b9037-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="b9037-107">Irá precisar de um VHD de arranque.</span><span class="sxs-lookup"><span data-stu-id="b9037-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="b9037-108">Pode transferir Olá VHD que utilizámos do https://azclisamples.blob.core.windows.net/vhds/sample.vhd ou utilizar o seu próprio VHD.</span><span class="sxs-lookup"><span data-stu-id="b9037-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="b9037-109">script de Olá procura `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="b9037-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b9037-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b9037-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b9037-111">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="b9037-111">Clean up deployment</span></span> 

<span data-ttu-id="b9037-112">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9037-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="b9037-113">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="b9037-113">Script explanation</span></span>

<span data-ttu-id="b9037-114">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b9037-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="b9037-115">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="b9037-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b9037-116">Comando</span><span class="sxs-lookup"><span data-stu-id="b9037-116">Command</span></span> | <span data-ttu-id="b9037-117">Notas</span><span class="sxs-lookup"><span data-stu-id="b9037-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b9037-118">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="b9037-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b9037-119">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b9037-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b9037-120">lista de contas de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="b9037-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="b9037-121">Apresenta uma lista de contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b9037-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="b9037-122">verificação de conta de armazenamento de AZ-name</span><span class="sxs-lookup"><span data-stu-id="b9037-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="b9037-123">Verifica se um nome de conta de armazenamento é válido e que já não existe</span><span class="sxs-lookup"><span data-stu-id="b9037-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="b9037-124">lista de chaves de conta de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="b9037-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="b9037-125">Apresenta uma lista de chaves Olá contas do storage</span><span class="sxs-lookup"><span data-stu-id="b9037-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="b9037-126">blob de armazenamento AZ existe</span><span class="sxs-lookup"><span data-stu-id="b9037-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="b9037-127">Verifica a existência de blob Olá</span><span class="sxs-lookup"><span data-stu-id="b9037-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="b9037-128">Criar contentor de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="b9037-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="b9037-129">Cria um contentor numa conta do storage.</span><span class="sxs-lookup"><span data-stu-id="b9037-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="b9037-130">carregamento de blob de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="b9037-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="b9037-131">Cria um blob no contentor de Olá, carregamento Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="b9037-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="b9037-132">lista de vm AZ</span><span class="sxs-lookup"><span data-stu-id="b9037-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="b9037-133">Utilizado com `--query` Verifique se o nome da VM Olá está em utilização.</span><span class="sxs-lookup"><span data-stu-id="b9037-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="b9037-134">Criar AZ vm</span><span class="sxs-lookup"><span data-stu-id="b9037-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="b9037-135">Cria Olá máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="b9037-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="b9037-136">AZ vm acesso conjunto linux-utilizador</span><span class="sxs-lookup"><span data-stu-id="b9037-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="b9037-137">Repõe Olá SSH toogive chave Olá atual utilizador acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b9037-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="b9037-138">AZ vm lista--endereços ip</span><span class="sxs-lookup"><span data-stu-id="b9037-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="b9037-139">Obtém o endereço IP Olá Olá VM que foi criado.</span><span class="sxs-lookup"><span data-stu-id="b9037-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9037-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b9037-140">Next steps</span></span>

<span data-ttu-id="b9037-141">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9037-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b9037-142">Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9037-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
