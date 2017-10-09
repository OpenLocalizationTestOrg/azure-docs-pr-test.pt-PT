---
title: um Cluster de ACS de escala aaaAzure CLI Script de exemplo - | Microsoft Docs
description: Exemplo de Script do CLI do Azure - escala um Cluster de ACS
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contentores, Microsserviços, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 1e07518fc2ca67476d9ef64bb22d75f848a37e43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="c538e-104">Dimensionar um Cluster do serviço de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="c538e-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="c538e-105">Este exemplo escalas e o serviço de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="c538e-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c538e-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c538e-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="c538e-107">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="c538e-107">Clean up deployment</span></span> 

<span data-ttu-id="c538e-108">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c538e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c538e-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="c538e-109">Script explanation</span></span>

<span data-ttu-id="c538e-110">Este script utiliza Olá após a implementação de Olá toocreate de comandos.</span><span class="sxs-lookup"><span data-stu-id="c538e-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="c538e-111">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="c538e-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c538e-112">Comando</span><span class="sxs-lookup"><span data-stu-id="c538e-112">Command</span></span> | <span data-ttu-id="c538e-113">Notas</span><span class="sxs-lookup"><span data-stu-id="c538e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c538e-114">escala de acs AZ</span><span class="sxs-lookup"><span data-stu-id="c538e-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="c538e-115">Dimensione um cluster de ACS.</span><span class="sxs-lookup"><span data-stu-id="c538e-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c538e-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c538e-116">Next steps</span></span>

<span data-ttu-id="c538e-117">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c538e-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c538e-118">Exemplos de script CLI de serviço de contentor do Azure adicionais podem ser encontrados na Olá [documentação do serviço de contentor Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c538e-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

