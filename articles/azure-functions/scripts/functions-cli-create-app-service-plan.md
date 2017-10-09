---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação de função num plano do serviço de aplicações | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação de função num plano do serviço de aplicações"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="c5bfe-103">Criar uma aplicação de função num plano do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="c5bfe-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="c5bfe-104">Este script de exemplo cria uma aplicação de função do Azure, que é um contentor para as suas funções.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="c5bfe-105">Olá aplicação de função é criada utilizando um plano de serviço aplicacional dedicado, o que significa que os recursos do servidor estão sempre ativos.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c5bfe-106">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c5bfe-107">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c5bfe-108">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c5bfe-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c5bfe-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c5bfe-109">Sample script</span></span>

<span data-ttu-id="c5bfe-110">Este script cria uma aplicação de função do Azure utilizando um dedicado [plano do App Service](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="c5bfe-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c5bfe-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="c5bfe-111">Script explanation</span></span>

<span data-ttu-id="c5bfe-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="c5bfe-113">Este script utiliza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c5bfe-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="c5bfe-114">Comando</span><span class="sxs-lookup"><span data-stu-id="c5bfe-114">Command</span></span> | <span data-ttu-id="c5bfe-115">Notas</span><span class="sxs-lookup"><span data-stu-id="c5bfe-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c5bfe-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="c5bfe-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c5bfe-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c5bfe-118">criar conta de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="c5bfe-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="c5bfe-119">Cria uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="c5bfe-120">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="c5bfe-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="c5bfe-121">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c5bfe-122">Criar AZ functionapp</span><span class="sxs-lookup"><span data-stu-id="c5bfe-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="c5bfe-123">Cria uma aplicação de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bfe-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c5bfe-124">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c5bfe-124">Next steps</span></span>

<span data-ttu-id="c5bfe-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5bfe-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c5bfe-126">Exemplos de script CLI de funções do Azure adicionais podem ser encontrados na Olá [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c5bfe-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
