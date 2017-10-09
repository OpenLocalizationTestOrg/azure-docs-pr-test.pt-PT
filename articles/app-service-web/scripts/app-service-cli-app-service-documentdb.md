---
title: "aaaAzure CLI Script de exemplo - ligar um tooCosmos de aplicação web DB | Microsoft Docs"
description: "Script CLI do Azure de exemplo - ligar um tooCosmos de aplicação web DB"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="9e9ea-103">Ligar um tooCosmos de aplicação web DB</span><span class="sxs-lookup"><span data-stu-id="9e9ea-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="9e9ea-104">Neste cenário ficará a saber como toocreate uma conta de base de dados do Azure Cosmos e um Azure aplicação web.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="9e9ea-105">Em seguida, vai ligar a aplicação web Olá Cosmos DB toohello utilizando as definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9e9ea-106">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9e9ea-107">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9e9ea-108">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9e9ea-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9e9ea-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9e9ea-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9e9ea-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="9e9ea-110">Script explanation</span></span>

<span data-ttu-id="9e9ea-111">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, aplicação web, base de dados do Cosmos e relacionados todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="9e9ea-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e9ea-113">Comando</span><span class="sxs-lookup"><span data-stu-id="9e9ea-113">Command</span></span> | <span data-ttu-id="9e9ea-114">Notas</span><span class="sxs-lookup"><span data-stu-id="9e9ea-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e9ea-115">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="9e9ea-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9e9ea-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e9ea-117">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="9e9ea-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9e9ea-118">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-118">Creates an App Service plan.</span></span> <span data-ttu-id="9e9ea-119">Trata-se como um farm de servidores para a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9e9ea-120">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="9e9ea-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9e9ea-121">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9e9ea-122">Criar AZ cosmosdb</span><span class="sxs-lookup"><span data-stu-id="9e9ea-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="9e9ea-123">Cria uma conta de base de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="9e9ea-124">Este é onde os dados de Olá serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="9e9ea-125">AZ cosmosdb lista de chaves</span><span class="sxs-lookup"><span data-stu-id="9e9ea-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="9e9ea-126">Apresenta uma lista de chaves de acesso de Olá para Olá especificar conta de base de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="9e9ea-127">AZ webapp configuração appsettings conjunto</span><span class="sxs-lookup"><span data-stu-id="9e9ea-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="9e9ea-128">Cria ou atualiza uma definição de aplicação para uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="9e9ea-129">As definições de aplicação são expostas como variáveis de ambiente para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9e9ea-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e9ea-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9e9ea-130">Next steps</span></span>

<span data-ttu-id="9e9ea-131">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e9ea-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9e9ea-132">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9e9ea-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
