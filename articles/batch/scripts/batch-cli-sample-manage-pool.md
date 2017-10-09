---
title: aaaAzure CLI Script de exemplo - Gerir agrupamentos no Batch | Microsoft Docs
description: Exemplo de Script da CLI do Azure - Gerir agrupamentos no Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="a2467-103">Gerir conjuntos do Azure Batch com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a2467-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="a2467-104">Estes scripts demonstra Algumas das ferramentas de Olá disponíveis no Olá CLI do Azure toocreate e gerir conjuntos de nós de computação no serviço do Azure Batch Olá.</span><span class="sxs-lookup"><span data-stu-id="a2467-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="a2467-105">comandos de Olá neste exemplo, criar máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2467-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="a2467-106">VMs em execução serão acumular conta tooyour de encargos.</span><span class="sxs-lookup"><span data-stu-id="a2467-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="a2467-107">toominimize estes custos, eliminar as VMs de Olá quando tiver terminado o exemplo de Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="a2467-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="a2467-108">Consulte [limpar agrupamentos](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="a2467-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="a2467-109">Conjuntos do batch podem ser configurados de duas formas, com uma configuração de serviços em nuvem (apenas Windows) ou uma configuração de Máquina Virtual (Windows e Linux).</span><span class="sxs-lookup"><span data-stu-id="a2467-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="a2467-110">scripts de exemplo de Olá abaixo mostram como toocreate agrupamentos com ambas as configurações.</span><span class="sxs-lookup"><span data-stu-id="a2467-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2467-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a2467-111">Prerequisites</span></span>

- <span data-ttu-id="a2467-112">Instalação Olá CLI do Azure, utilizando instruções Olá fornecidas Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se ainda não o tiver feito.</span><span class="sxs-lookup"><span data-stu-id="a2467-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="a2467-113">Se ainda não tiver um, crie uma conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="a2467-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="a2467-114">Consulte [criar uma conta do Batch com Olá CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="a2467-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="a2467-115">Se ainda não o ainda feito, configure toorun uma aplicação de uma tarefa de início.</span><span class="sxs-lookup"><span data-stu-id="a2467-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="a2467-116">Consulte [adicionar aplicações tooAzure Batch com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para um script de exemplo que cria uma aplicação e carrega um tooAzure do pacote de aplicação.</span><span class="sxs-lookup"><span data-stu-id="a2467-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="a2467-117">Conjunto com o script de exemplo de configuração de serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="a2467-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="a2467-118">Conjunto com o script de exemplo de configuração de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a2467-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="a2467-119">Limpar os agrupamentos</span><span class="sxs-lookup"><span data-stu-id="a2467-119">Clean up pools</span></span>

<span data-ttu-id="a2467-120">Depois de executar Olá acima script de exemplo, execute Olá conjuntos de Olá toodelete de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a2467-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="a2467-121">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="a2467-121">Script explanation</span></span>

<span data-ttu-id="a2467-122">Este script utiliza Olá os seguintes comandos toocreate e manipular conjuntos do Batch.</span><span class="sxs-lookup"><span data-stu-id="a2467-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="a2467-123">Cada comando na documentação do Olá tabela ligações toocommand específicos.</span><span class="sxs-lookup"><span data-stu-id="a2467-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="a2467-124">Comando</span><span class="sxs-lookup"><span data-stu-id="a2467-124">Command</span></span> | <span data-ttu-id="a2467-125">Notas</span><span class="sxs-lookup"><span data-stu-id="a2467-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2467-126">início de sessão de conta de batch de AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="a2467-127">Autenticar face a uma conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="a2467-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="a2467-128">lista de resumo de aplicações de batch de AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="a2467-129">Listar Olá aplicações disponíveis na Olá conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="a2467-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="a2467-130">Criar conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="a2467-131">Crie um conjunto de VMs.</span><span class="sxs-lookup"><span data-stu-id="a2467-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="a2467-132">conjunto de conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="a2467-133">Atualize propriedades de um conjunto.</span><span class="sxs-lookup"><span data-stu-id="a2467-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="a2467-134">lista de skus de agente de nó de conjunto de batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="a2467-135">Agente de listas de nó disponível SKUs e as informações da imagem.</span><span class="sxs-lookup"><span data-stu-id="a2467-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="a2467-136">redimensionamento de conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="a2467-137">Redimensionamento Olá número de VMs em execução no Olá especificado agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a2467-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="a2467-138">Mostrar de conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="a2467-139">Apresentar as propriedades de Olá de um conjunto.</span><span class="sxs-lookup"><span data-stu-id="a2467-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="a2467-140">eliminação de conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="a2467-141">Eliminar Olá especificado agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a2467-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="a2467-142">Ativar o dimensionamento automático de conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="a2467-143">Ativar o dimensionamento automático num agrupamento e aplicar uma fórmula.</span><span class="sxs-lookup"><span data-stu-id="a2467-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="a2467-144">desativar o dimensionamento automático de conjunto do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="a2467-145">Desative o dimensionamento automático num agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a2467-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="a2467-146">lista de nós de batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="a2467-147">Listar todas as nó de computação Olá Olá especificado agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a2467-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="a2467-148">reinício do nó AZ batch</span><span class="sxs-lookup"><span data-stu-id="a2467-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="a2467-149">Reinicie o nó de cálculo especificada de Olá.</span><span class="sxs-lookup"><span data-stu-id="a2467-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="a2467-150">eliminação de nó do batch AZ</span><span class="sxs-lookup"><span data-stu-id="a2467-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="a2467-151">Eliminar Olá listado nós de Olá especificado agrupamento.</span><span class="sxs-lookup"><span data-stu-id="a2467-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a2467-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a2467-152">Next steps</span></span>

<span data-ttu-id="a2467-153">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2467-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a2467-154">Exemplos de script de Batch CLI adicionais podem ser encontrados na Olá [documentação da CLI do Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2467-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

