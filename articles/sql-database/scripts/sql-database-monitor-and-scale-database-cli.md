---
title: "a base de dados SQL do Azure de exemplo-monitor escala único aaaCLI | Microsoft Docs"
description: Toomonitor de script de exemplo CLI do Azure e dimensionar uma base de dados SQL do Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="70bae-103">Utilize o CLI toomonitor e dimensionar uma base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="70bae-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="70bae-104">Neste exemplo de script da CLI do Azure dimensiona um nível de desempenho diferentes do tooa de base de dados SQL do Azure único depois de consultar as informações de tamanho da base de dados de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="70bae-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="70bae-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="70bae-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="70bae-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="70bae-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="70bae-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="70bae-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="70bae-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="70bae-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="70bae-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="70bae-109">Clean up deployment</span></span>

<span data-ttu-id="70bae-110">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="70bae-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="70bae-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="70bae-111">Script explanation</span></span>

<span data-ttu-id="70bae-112">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="70bae-112">This script uses hello following commands.</span></span> <span data-ttu-id="70bae-113">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="70bae-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="70bae-114">Comando</span><span class="sxs-lookup"><span data-stu-id="70bae-114">Command</span></span> | <span data-ttu-id="70bae-115">Notas</span><span class="sxs-lookup"><span data-stu-id="70bae-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="70bae-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="70bae-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="70bae-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="70bae-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="70bae-118">servidor de sql AZ criar</span><span class="sxs-lookup"><span data-stu-id="70bae-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="70bae-119">Cria um servidor lógico que aloja uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="70bae-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="70bae-120">base de dados de sql AZ Mostrar-utilização</span><span class="sxs-lookup"><span data-stu-id="70bae-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="70bae-121">Mostra informações de utilização de tamanho de Olá para uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="70bae-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="70bae-122">atualização de base de dados do sql AZ</span><span class="sxs-lookup"><span data-stu-id="70bae-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="70bae-123">Atualiza as propriedades de base de dados (por exemplo, Olá camada ou desempenho de nível de serviço) ou uma base de dados é movido para fora do ou entre conjuntos elásticos.</span><span class="sxs-lookup"><span data-stu-id="70bae-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="70bae-124">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="70bae-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="70bae-125">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="70bae-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="70bae-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="70bae-126">Next steps</span></span>

<span data-ttu-id="70bae-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="70bae-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="70bae-128">Exemplos de script CLI de base de dados do SQL adicionais podem ser encontrados na Olá [documentação da SQL Database do Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="70bae-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
