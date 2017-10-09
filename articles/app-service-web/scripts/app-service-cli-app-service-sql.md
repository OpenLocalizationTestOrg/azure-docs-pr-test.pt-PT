---
title: "aaaAzure CLI Script de exemplo - ligar uma base de dados SQL de tooa de aplicação do web | Microsoft Docs"
description: "Script CLI do Azure de exemplo - ligar uma base de dados SQL de tooa de aplicação do web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="62af6-103">Ligar uma base de dados SQL de tooa de aplicação do web</span><span class="sxs-lookup"><span data-stu-id="62af6-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="62af6-104">Neste cenário ficará a saber como toocreate uma base de dados SQL do Azure e um Azure aplicação web.</span><span class="sxs-lookup"><span data-stu-id="62af6-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="62af6-105">Em seguida, vai ligar Olá SQL da base de dados toohello web app através das definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="62af6-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="62af6-106">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="62af6-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="62af6-107">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="62af6-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="62af6-108">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62af6-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="62af6-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="62af6-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="62af6-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="62af6-110">Script explanation</span></span>

<span data-ttu-id="62af6-111">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, aplicação web, base de dados SQL e recursos de todos os relacionados.</span><span class="sxs-lookup"><span data-stu-id="62af6-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="62af6-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="62af6-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="62af6-113">Comando</span><span class="sxs-lookup"><span data-stu-id="62af6-113">Command</span></span> | <span data-ttu-id="62af6-114">Notas</span><span class="sxs-lookup"><span data-stu-id="62af6-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62af6-115">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="62af6-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62af6-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="62af6-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62af6-117">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="62af6-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="62af6-118">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="62af6-118">Creates an App Service plan.</span></span> <span data-ttu-id="62af6-119">Trata-se como um farm de servidores para a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="62af6-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="62af6-120">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="62af6-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="62af6-121">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="62af6-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="62af6-122">servidor de sql AZ criar</span><span class="sxs-lookup"><span data-stu-id="62af6-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="62af6-123">Cria um servidor de base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="62af6-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="62af6-124">Criar BD do sql AZ</span><span class="sxs-lookup"><span data-stu-id="62af6-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="62af6-125">Cria uma nova base de dados com hello do servidor de base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="62af6-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="62af6-126">AZ webapp configuração appsettings conjunto</span><span class="sxs-lookup"><span data-stu-id="62af6-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="62af6-127">Cria ou atualiza uma definição de aplicação para uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="62af6-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="62af6-128">As definições de aplicação são expostas como variáveis de ambiente para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="62af6-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62af6-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="62af6-129">Next steps</span></span>

<span data-ttu-id="62af6-130">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62af6-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62af6-131">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="62af6-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
