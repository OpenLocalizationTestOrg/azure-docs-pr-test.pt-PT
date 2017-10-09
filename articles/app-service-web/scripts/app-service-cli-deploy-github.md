---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web com a implementação a partir do GitHub | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação web com a implementação a partir do GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="0ddae-103">Criar uma aplicação web com a implementação a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="0ddae-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="0ddae-104">Este script de exemplo cria uma aplicação web no App Service com os respetivos recursos relacionados e, em seguida, implementa o código de aplicação web a partir de um repositório do GitHub público (sem a implementação contínua).</span><span class="sxs-lookup"><span data-stu-id="0ddae-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="0ddae-105">Para implementação do GitHub com a implementação contínua, consulte [criar uma aplicação web com a implementação contínua do GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="0ddae-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0ddae-106">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0ddae-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0ddae-107">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="0ddae-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0ddae-108">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0ddae-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0ddae-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0ddae-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0ddae-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="0ddae-110">Script explanation</span></span> 

<span data-ttu-id="0ddae-111">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="0ddae-111">This script uses hello following commands.</span></span> <span data-ttu-id="0ddae-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="0ddae-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0ddae-113">Comando</span><span class="sxs-lookup"><span data-stu-id="0ddae-113">Command</span></span> | <span data-ttu-id="0ddae-114">Notas</span><span class="sxs-lookup"><span data-stu-id="0ddae-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0ddae-115">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="0ddae-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0ddae-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="0ddae-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0ddae-117">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="0ddae-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0ddae-118">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="0ddae-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0ddae-119">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="0ddae-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0ddae-120">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ddae-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0ddae-121">AZ webapp configuração da origem de implementação</span><span class="sxs-lookup"><span data-stu-id="0ddae-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="0ddae-122">Associa um repositório de Git ou Mercurial uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ddae-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="0ddae-123">Procurar de webapp AZ</span><span class="sxs-lookup"><span data-stu-id="0ddae-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="0ddae-124">Abra uma aplicação web do Azure num browser.</span><span class="sxs-lookup"><span data-stu-id="0ddae-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0ddae-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0ddae-125">Next steps</span></span>

<span data-ttu-id="0ddae-126">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0ddae-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0ddae-127">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0ddae-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
