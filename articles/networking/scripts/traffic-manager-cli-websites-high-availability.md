---
title: "aaaAzure CLI Script de exemplo - encaminhar o tráfego para elevada disponibilidade de aplicações | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - encaminhar o tráfego para elevada disponibilidade de aplicações"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="07f21-103">Encaminhar o tráfego para elevada disponibilidade de aplicações</span><span class="sxs-lookup"><span data-stu-id="07f21-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="07f21-104">Este script cria um grupo de recursos, dois planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos finais Gestor de tráfego.</span><span class="sxs-lookup"><span data-stu-id="07f21-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="07f21-105">Gestor de tráfego direciona o tráfego toohello aplicação uma região como região primária Olá e região secundária toohello quando a aplicação Olá na região primária Olá não está disponível.</span><span class="sxs-lookup"><span data-stu-id="07f21-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="07f21-106">Antes de executar o script de Olá, tem de alterar Olá MyWebApp, MyWebAppL1 e MyWebAppL2 valores toounique valores em todo o Azure.</span><span class="sxs-lookup"><span data-stu-id="07f21-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="07f21-107">Depois de executar o script de Olá, pode aceder à aplicação Olá na região primária de Olá com Olá URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="07f21-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="07f21-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="07f21-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="07f21-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="07f21-109">Clean up deployment</span></span> 

<span data-ttu-id="07f21-110">Depois de executar o script de exemplo Olá, Olá siga pode ser utilizado tooremove grupo de recursos de Olá, do serviço de aplicações aplicação e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="07f21-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="07f21-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="07f21-111">Script explanation</span></span>

<span data-ttu-id="07f21-112">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, de aplicação web, de perfil do Gestor de tráfego e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="07f21-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="07f21-113">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="07f21-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="07f21-114">Comando</span><span class="sxs-lookup"><span data-stu-id="07f21-114">Command</span></span> | <span data-ttu-id="07f21-115">Notas</span><span class="sxs-lookup"><span data-stu-id="07f21-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07f21-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="07f21-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="07f21-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="07f21-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="07f21-118">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="07f21-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="07f21-119">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="07f21-119">Creates an App Service plan.</span></span> <span data-ttu-id="07f21-120">Trata-se como um farm de servidores para a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="07f21-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="07f21-121">criar web de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="07f21-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="07f21-122">Cria uma aplicação web do Azure dentro Olá plano do App Service.</span><span class="sxs-lookup"><span data-stu-id="07f21-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="07f21-123">Criar perfil de Gestor de tráfego de rede AZ</span><span class="sxs-lookup"><span data-stu-id="07f21-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="07f21-124">Cria um perfil do Traffic Manager do Azure.</span><span class="sxs-lookup"><span data-stu-id="07f21-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="07f21-125">criar o ponto final do Gestor de tráfego de rede AZ</span><span class="sxs-lookup"><span data-stu-id="07f21-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="07f21-126">Adiciona um ponto final tooan perfil do Traffic Manager do Azure.</span><span class="sxs-lookup"><span data-stu-id="07f21-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07f21-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="07f21-127">Next steps</span></span>

<span data-ttu-id="07f21-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07f21-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="07f21-129">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [redes do Azure documentação](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="07f21-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
