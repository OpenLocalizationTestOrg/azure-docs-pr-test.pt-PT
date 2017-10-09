---
title: "aaaCreate uma função do Azure que liga tooan Storage do Azure | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma função do Azure que liga tooan Storage do Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="b19c2-103">Integrar a aplicação de função na conta do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="b19c2-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="b19c2-104">Este script de exemplo cria uma aplicação de função e a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b19c2-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b19c2-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b19c2-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b19c2-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="b19c2-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b19c2-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b19c2-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b19c2-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b19c2-108">Sample script</span></span>

<span data-ttu-id="b19c2-109">Este exemplo cria uma aplicação de função do Azure e adiciona a definição de aplicação de tooan ligação cadeia Olá armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b19c2-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="b19c2-110">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="b19c2-110">Clean up deployment</span></span>

<span data-ttu-id="b19c2-111">Depois de executar o script de exemplo Olá, Olá seguinte comando pode ser utilizado tooremove grupo de recursos de Olá, do serviço de aplicações aplicação e todos os recursos relacionados:</span><span class="sxs-lookup"><span data-stu-id="b19c2-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b19c2-112">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="b19c2-112">Script explanation</span></span>

<span data-ttu-id="b19c2-113">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="b19c2-113">This script uses hello following commands.</span></span> <span data-ttu-id="b19c2-114">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="b19c2-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b19c2-115">Comando</span><span class="sxs-lookup"><span data-stu-id="b19c2-115">Command</span></span> | <span data-ttu-id="b19c2-116">Notas</span><span class="sxs-lookup"><span data-stu-id="b19c2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b19c2-117">início de sessão AZ</span><span class="sxs-lookup"><span data-stu-id="b19c2-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="b19c2-118">TooAzure de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="b19c2-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="b19c2-119">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="b19c2-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b19c2-120">Criar um grupo de recursos com a localização</span><span class="sxs-lookup"><span data-stu-id="b19c2-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="b19c2-121">criar conta de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="b19c2-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="b19c2-122">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b19c2-122">Create a storage account</span></span> |
| [<span data-ttu-id="b19c2-123">Criar AZ functionapp</span><span class="sxs-lookup"><span data-stu-id="b19c2-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b19c2-124">Criar uma nova aplicação de função</span><span class="sxs-lookup"><span data-stu-id="b19c2-124">Create a new function app</span></span> |
| [<span data-ttu-id="b19c2-125">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="b19c2-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b19c2-126">Limpeza</span><span class="sxs-lookup"><span data-stu-id="b19c2-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b19c2-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b19c2-127">Next steps</span></span>

<span data-ttu-id="b19c2-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b19c2-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b19c2-129">Exemplos de script CLI de funções do Azure adicionais podem ser encontrados na Olá [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b19c2-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
