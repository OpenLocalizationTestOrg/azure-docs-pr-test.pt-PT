---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web e implementar o código do repositório de Git local | Microsoft Docs"
description: "Exemplo de Script do CLI do Azure - criar uma aplicação web e implementar o código do repositório de Git local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="da7d4-103">Criar uma aplicação web e implementar o código do repositório de Git local</span><span class="sxs-lookup"><span data-stu-id="da7d4-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="da7d4-104">Este script de exemplo cria uma aplicação web no App Service com os respetivos recursos relacionados e, em seguida, implementa o código de aplicação web num repositório de Git local.</span><span class="sxs-lookup"><span data-stu-id="da7d4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="da7d4-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="da7d4-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="da7d4-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="da7d4-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="da7d4-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="da7d4-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="da7d4-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="da7d4-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="da7d4-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="da7d4-109">Script explanation</span></span>

<span data-ttu-id="da7d4-110">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="da7d4-110">This script uses hello following commands.</span></span> <span data-ttu-id="da7d4-111">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="da7d4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="da7d4-112">Comando</span><span class="sxs-lookup"><span data-stu-id="da7d4-112">Command</span></span> | <span data-ttu-id="da7d4-113">Notas</span><span class="sxs-lookup"><span data-stu-id="da7d4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="da7d4-114">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="da7d4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="da7d4-115">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="da7d4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="da7d4-116">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="da7d4-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="da7d4-117">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="da7d4-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="da7d4-118">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="da7d4-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="da7d4-119">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="da7d4-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="da7d4-120">utilizador AZ webapp implementação definido</span><span class="sxs-lookup"><span data-stu-id="da7d4-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="da7d4-121">Define as credenciais de implementação de nível de conta de Olá para serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="da7d4-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="da7d4-122">origem de implementação webapp com AZ-config-local-git</span><span class="sxs-lookup"><span data-stu-id="da7d4-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="da7d4-123">Cria uma configuração de controlo de origem para um repositório de Git local.</span><span class="sxs-lookup"><span data-stu-id="da7d4-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="da7d4-124">Procurar de webapp AZ</span><span class="sxs-lookup"><span data-stu-id="da7d4-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="da7d4-125">Abra uma aplicação web do Azure num browser.</span><span class="sxs-lookup"><span data-stu-id="da7d4-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="da7d4-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="da7d4-126">Next steps</span></span>

<span data-ttu-id="da7d4-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da7d4-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="da7d4-128">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="da7d4-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
