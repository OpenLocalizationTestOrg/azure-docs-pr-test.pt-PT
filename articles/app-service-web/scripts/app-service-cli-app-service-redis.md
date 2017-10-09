---
title: "aaaAzure CLI Script de exemplo - ligar uma cache de redis do tooa de aplicações web | Microsoft Docs"
description: "Script CLI do Azure de exemplo - ligar uma cache de redis do tooa de aplicação web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="74aad-103">Ligar uma cache de redis do tooa de aplicação web</span><span class="sxs-lookup"><span data-stu-id="74aad-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="74aad-104">Neste cenário ficará a saber como toocreate um Azure redis cache e uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="74aad-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="74aad-105">Em seguida, vai ligar Olá redis cache toohello web app através das definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="74aad-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="74aad-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="74aad-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="74aad-107">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="74aad-107">Script explanation</span></span>

<span data-ttu-id="74aad-108">Este script utiliza Olá comandos relacionados todos os recursos e a cache de redis toocreate um grupo de recursos, a aplicação web, a seguir.</span><span class="sxs-lookup"><span data-stu-id="74aad-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="74aad-109">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="74aad-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="74aad-110">Comando</span><span class="sxs-lookup"><span data-stu-id="74aad-110">Command</span></span> | <span data-ttu-id="74aad-111">Notas</span><span class="sxs-lookup"><span data-stu-id="74aad-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74aad-112">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="74aad-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="74aad-113">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="74aad-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74aad-114">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="74aad-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="74aad-115">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="74aad-115">Creates an App Service plan.</span></span> <span data-ttu-id="74aad-116">Trata-se como um farm de servidores para a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="74aad-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="74aad-117">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="74aad-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="74aad-118">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="74aad-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="74aad-119">Criar AZ redis</span><span class="sxs-lookup"><span data-stu-id="74aad-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="74aad-120">Crie uma nova instância da Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="74aad-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="74aad-121">Este é onde os dados de Olá serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="74aad-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="74aad-122">AZ lista-as chaves de redis</span><span class="sxs-lookup"><span data-stu-id="74aad-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="74aad-123">Apresenta uma lista de chaves de acesso de Olá para a instância da cache de redis Olá.</span><span class="sxs-lookup"><span data-stu-id="74aad-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="74aad-124">AZ webapp configuração appsettings conjunto</span><span class="sxs-lookup"><span data-stu-id="74aad-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="74aad-125">Cria ou atualiza uma definição de aplicação para uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="74aad-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="74aad-126">As definições de aplicação são expostas como variáveis de ambiente para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="74aad-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74aad-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="74aad-127">Next steps</span></span>

<span data-ttu-id="74aad-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="74aad-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="74aad-129">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="74aad-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
