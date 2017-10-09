---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web do ASP.NET Core num contentor Docker | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação web do ASP.NET Core num contentor Docker"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="817b2-103">Criar uma aplicação web do ASP.NET Core num contentor Docker</span><span class="sxs-lookup"><span data-stu-id="817b2-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="817b2-104">Neste cenário, ficará a saber como toocreate um grupo de recursos, a aplicação do Linux plano e a aplicação web service e implementar uma aplicação ASP.NET Core utilizar um contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="817b2-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="817b2-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="817b2-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="817b2-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="817b2-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="817b2-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="817b2-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="817b2-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="817b2-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="817b2-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="817b2-109">Script explanation</span></span>

<span data-ttu-id="817b2-110">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, web aplicação e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="817b2-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="817b2-111">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="817b2-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="817b2-112">Comando</span><span class="sxs-lookup"><span data-stu-id="817b2-112">Command</span></span> | <span data-ttu-id="817b2-113">Notas</span><span class="sxs-lookup"><span data-stu-id="817b2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="817b2-114">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="817b2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="817b2-115">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="817b2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="817b2-116">Criar plano de serviço aplicacional AZ</span><span class="sxs-lookup"><span data-stu-id="817b2-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="817b2-117">Cria um plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="817b2-117">Creates an App Service plan.</span></span> <span data-ttu-id="817b2-118">Trata-se como um farm de servidores para a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="817b2-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="817b2-119">Criar AZ webapp</span><span class="sxs-lookup"><span data-stu-id="817b2-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="817b2-120">Cria uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="817b2-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="817b2-121">conjunto de contentor de configuração do AZ webapp</span><span class="sxs-lookup"><span data-stu-id="817b2-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="817b2-122">Define o contentor de Docker Olá para aplicação de web do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="817b2-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="817b2-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="817b2-123">Next steps</span></span>

<span data-ttu-id="817b2-124">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="817b2-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="817b2-125">Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="817b2-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
