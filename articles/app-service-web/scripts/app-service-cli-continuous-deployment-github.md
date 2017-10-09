---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web com a implementação contínua do GitHub | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação web com a implementação contínua do GitHub"
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="96c2b-103">Criar uma aplicação web com a implementação contínua do GitHub</span><span class="sxs-lookup"><span data-stu-id="96c2b-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="96c2b-104">Este script de exemplo cria uma aplicação web no App Service com respetivos recursos relacionados e, em seguida, configura a implementação contínua provém de um repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="96c2b-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="96c2b-105">Para a implementação do GitHub sem a implementação contínua, consulte [criar uma aplicação web e implementar código a partir do GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="96c2b-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="96c2b-106">Neste exemplo, necessitará de:</span><span class="sxs-lookup"><span data-stu-id="96c2b-106">In this sample, you will need:</span></span>

* <span data-ttu-id="96c2b-107">Um repositório do GitHub com código da aplicação, que tem permissões administrativas.</span><span class="sxs-lookup"><span data-stu-id="96c2b-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="96c2b-108">A [pessoais acesso Token (TERESA)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para a sua conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="96c2b-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="96c2b-109">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="96c2b-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="96c2b-110">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="96c2b-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="96c2b-111">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="96c2b-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="96c2b-112">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="96c2b-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="96c2b-113">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="96c2b-113">Script explanation</span></span>

<span data-ttu-id="96c2b-114">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="96c2b-114">This script uses hello following commands.</span></span> <span data-ttu-id="96c2b-115">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="96c2b-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="96c2b-116">Comando</span><span class="sxs-lookup"><span data-stu-id="96c2b-116">Command</span></span> | <span data-ttu-id="96c2b-117">Notas</span><span class="sxs-lookup"><span data-stu-id="96c2b-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96c2b-118">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="96c2b-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="96c2b-119">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="96c2b-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="96c2b-120">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="96c2b-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="96c2b-121">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="96c2b-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="96c2b-122">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="96c2b-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="96c2b-123">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="96c2b-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="96c2b-124">AZ webapp configuração da origem de implementação</span><span class="sxs-lookup"><span data-stu-id="96c2b-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="96c2b-125">Associa um repositório de Git ou Mercurial uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="96c2b-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="96c2b-126">Procurar de webapp AZ</span><span class="sxs-lookup"><span data-stu-id="96c2b-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="96c2b-127">Abra uma aplicação web do Azure num browser.</span><span class="sxs-lookup"><span data-stu-id="96c2b-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96c2b-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="96c2b-128">Next steps</span></span>

<span data-ttu-id="96c2b-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96c2b-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="96c2b-130">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="96c2b-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
