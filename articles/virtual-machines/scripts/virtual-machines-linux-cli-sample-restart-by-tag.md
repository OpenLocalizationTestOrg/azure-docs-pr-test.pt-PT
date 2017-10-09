---
title: aaaAzure CLI Script de exemplo - VMs reiniciar | Microsoft Docs
description: "Exemplo de Script CLI do Azure - reinício VMs por tag e ID"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="e2e43-103">Reinício de VMs</span><span class="sxs-lookup"><span data-stu-id="e2e43-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="e2e43-104">Este exemplo mostra algumas formas tooget algumas VMs e reiniciá-las.</span><span class="sxs-lookup"><span data-stu-id="e2e43-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="e2e43-105">Olá reinicia primeiro todas as VMs de Olá no grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2e43-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="e2e43-106">Olá segundo obtém Olá etiquetados VMs utilizando `az resouce list` filtra toohello recursos que são as VMs e reinicia esses VMs.</span><span class="sxs-lookup"><span data-stu-id="e2e43-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="e2e43-107">Este exemplo funciona numa shell de deteção.</span><span class="sxs-lookup"><span data-stu-id="e2e43-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="e2e43-108">Para opções sobre a execução de scripts da CLI do Azure num cliente Windows, consulte [Olá CLI do Azure a executar no Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="e2e43-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="e2e43-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e2e43-109">Sample script</span></span>

<span data-ttu-id="e2e43-110">exemplo de Olá tem três scripts.</span><span class="sxs-lookup"><span data-stu-id="e2e43-110">hello sample has three scripts.</span></span>
<span data-ttu-id="e2e43-111">Olá máquinas de virtuais de Olá aprovisiona um primeiro.</span><span class="sxs-lookup"><span data-stu-id="e2e43-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="e2e43-112">Utiliza a opção de não-aguardar Olá pelo comando Olá devolve sem aguardar a resposta de cada toobe VM aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="e2e43-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="e2e43-113">Olá aguarda segundo Olá VMs toobe totalmente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="e2e43-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="e2e43-114">script terceiro Olá reiniciado todas as VMs de Olá que tenham sido aprovisionadas e, em seguida, Olá apenas etiquetados VMs.</span><span class="sxs-lookup"><span data-stu-id="e2e43-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="e2e43-115">Aprovisionar Olá VMs</span><span class="sxs-lookup"><span data-stu-id="e2e43-115">Provision hello VMs</span></span>

<span data-ttu-id="e2e43-116">Este script cria um grupo de recursos e, em seguida, cria três toorestart de VMs.</span><span class="sxs-lookup"><span data-stu-id="e2e43-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="e2e43-117">Dois dos mesmos são etiquetados.</span><span class="sxs-lookup"><span data-stu-id="e2e43-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="e2e43-118">Wait</span><span class="sxs-lookup"><span data-stu-id="e2e43-118">Wait</span></span>

<span data-ttu-id="e2e43-119">Este script verifica-se no estado de aprovisionamento cada 20 segundos até que todos os três VMs são aprovisionadas ou um deles falha tooprovision de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2e43-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="e2e43-120">Reiniciar Olá VMs</span><span class="sxs-lookup"><span data-stu-id="e2e43-120">Restart hello VMs</span></span>

<span data-ttu-id="e2e43-121">Este script reiniciado todas as VMs de Olá no grupo de recursos de Olá e, em seguida, reinicia-apenas Olá etiquetado VMs.</span><span class="sxs-lookup"><span data-stu-id="e2e43-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e2e43-122">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="e2e43-122">Clean up deployment</span></span> 

<span data-ttu-id="e2e43-123">Depois de executar o script de exemplo Olá, Olá os seguintes comandos pode ser utilizados tooremove Olá os grupos de recursos, VMs e recursos relacionados todos os.</span><span class="sxs-lookup"><span data-stu-id="e2e43-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e2e43-124">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="e2e43-124">Script explanation</span></span>

<span data-ttu-id="e2e43-125">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e2e43-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="e2e43-126">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="e2e43-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e2e43-127">Comando</span><span class="sxs-lookup"><span data-stu-id="e2e43-127">Command</span></span> | <span data-ttu-id="e2e43-128">Notas</span><span class="sxs-lookup"><span data-stu-id="e2e43-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e2e43-129">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="e2e43-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e2e43-130">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e2e43-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e2e43-131">Criar AZ vm</span><span class="sxs-lookup"><span data-stu-id="e2e43-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="e2e43-132">Cria Olá máquinas de virtuais.</span><span class="sxs-lookup"><span data-stu-id="e2e43-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="e2e43-133">lista de vm AZ</span><span class="sxs-lookup"><span data-stu-id="e2e43-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="e2e43-134">Utilizado com `--query` tooensure Olá VMs são aprovisionados antes de reiniciá-los e, em seguida, tooget Olá IDs de Olá VMs toorestart-los.</span><span class="sxs-lookup"><span data-stu-id="e2e43-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="e2e43-135">lista de recursos de AZ</span><span class="sxs-lookup"><span data-stu-id="e2e43-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="e2e43-136">Utilizado com `--query` tooget Olá IDs de VMs de Olá utilizar Olá tag.</span><span class="sxs-lookup"><span data-stu-id="e2e43-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="e2e43-137">reinício de vm AZ</span><span class="sxs-lookup"><span data-stu-id="e2e43-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="e2e43-138">Reinicia Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="e2e43-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="e2e43-139">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="e2e43-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e2e43-140">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="e2e43-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e2e43-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e2e43-141">Next steps</span></span>

<span data-ttu-id="e2e43-142">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2e43-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e2e43-143">Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2e43-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
