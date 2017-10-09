---
title: "aaaAzure CLI Script de exemplo - implementar Olá LAMP pilha num conjunto de dimensionamento Load-Balanced à Machin | Microsoft Docs"
description: "Utilize um Olá de toodeploy de extensão LAMP pilha de script personalizado numa carga = dimensionamento da máquina de virtual com balanceamento definida no Azure."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="e86c2-103">Implementar a pilha LAMP Olá num conjunto de dimensionamento da máquina de virtual com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="e86c2-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="e86c2-104">Este exemplo cria um conjunto de dimensionamento de máquina virtual e aplica-se de uma extensão que executa uma pilha de LAMP do script personalizado toodeploy Olá em cada máquina virtual num conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="e86c2-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="e86c2-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e86c2-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="e86c2-106">Ligar</span><span class="sxs-lookup"><span data-stu-id="e86c2-106">Connect</span></span>

<span data-ttu-id="e86c2-107">Utilize este toosee de código como definir tooconnect tooyour VMs e a escala.</span><span class="sxs-lookup"><span data-stu-id="e86c2-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e86c2-108">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="e86c2-108">Clean up deployment</span></span> 

<span data-ttu-id="e86c2-109">Execute Olá seguir o grupo de recursos do comando tooremove Olá, conjunto de dimensionamento de Olá e VMs e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e86c2-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e86c2-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="e86c2-110">Script explanation</span></span>

<span data-ttu-id="e86c2-111">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e86c2-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="e86c2-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="e86c2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e86c2-113">Comando</span><span class="sxs-lookup"><span data-stu-id="e86c2-113">Command</span></span> | <span data-ttu-id="e86c2-114">Notas</span><span class="sxs-lookup"><span data-stu-id="e86c2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e86c2-115">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="e86c2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e86c2-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e86c2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e86c2-117">Criar AZ vmss</span><span class="sxs-lookup"><span data-stu-id="e86c2-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="e86c2-118">Cria um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e86c2-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="e86c2-119">Criar regra de lb AZ de rede</span><span class="sxs-lookup"><span data-stu-id="e86c2-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e86c2-120">Adicionar um ponto final com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="e86c2-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="e86c2-121">conjunto de extensão de vmss AZ</span><span class="sxs-lookup"><span data-stu-id="e86c2-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="e86c2-122">Criar extensão Olá que executa o script personalizado Olá na implementação de uma VM</span><span class="sxs-lookup"><span data-stu-id="e86c2-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="e86c2-123">instâncias de atualização do vmss AZ</span><span class="sxs-lookup"><span data-stu-id="e86c2-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="e86c2-124">Executar script personalizado Olá em instâncias VM de Olá que foram implementadas antes de extensão de Olá foi aplicada toohello conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e86c2-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="e86c2-125">escala de vmss AZ</span><span class="sxs-lookup"><span data-stu-id="e86c2-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="e86c2-126">Aumentar verticalmente escala Olá definida adicionando mais instâncias VM.</span><span class="sxs-lookup"><span data-stu-id="e86c2-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="e86c2-127">script personalizado Olá é executado nestes quando estão implementadas.</span><span class="sxs-lookup"><span data-stu-id="e86c2-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="e86c2-128">lista de ip público de rede AZ</span><span class="sxs-lookup"><span data-stu-id="e86c2-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="e86c2-129">Obter os endereços IP de Olá de Olá VMs criadas pelo exemplo Olá.</span><span class="sxs-lookup"><span data-stu-id="e86c2-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="e86c2-130">Mostrar de lb AZ rede</span><span class="sxs-lookup"><span data-stu-id="e86c2-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="e86c2-131">Obter o front-end de Olá e back-end portas utilizadas pelo balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="e86c2-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e86c2-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e86c2-132">Next steps</span></span>

<span data-ttu-id="e86c2-133">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e86c2-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e86c2-134">Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e86c2-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
