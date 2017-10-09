---
title: amostras de aaaAzure CLI tooscale uma base de dados do Azure para o servidor de MySQL | Microsoft Docs
description: "Este script de exemplo do CLI dimensiona de base de dados do Azure para o nível de desempenho diferentes MySQL servidor tooa depois de consultar as métricas de Olá."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="10cc3-103">Monitorizar e dimensionar uma base de dados do Azure para o servidor de MySQL utilizando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="10cc3-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="10cc3-104">Este script de exemplo do CLI dimensiona uma única base de dados do Azure para o nível de desempenho diferentes MySQL servidor tooa depois de consultar as métricas de Olá.</span><span class="sxs-lookup"><span data-stu-id="10cc3-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="10cc3-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="10cc3-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="10cc3-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="10cc3-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="10cc3-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10cc3-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="10cc3-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="10cc3-108">Sample script</span></span>
<span data-ttu-id="10cc3-109">Este script de exemplo, altere Olá realçado linhas toocustomize Olá admin nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="10cc3-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="10cc3-110">Substitua o id de subscrição de Olá utilizado nos comandos de monitor de az Olá com o seu id de subscrição.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="10cc3-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="10cc3-111">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="10cc3-111">Clean up deployment</span></span>
<span data-ttu-id="10cc3-112">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="10cc3-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="10cc3-113">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="10cc3-113">Script explanation</span></span>
<span data-ttu-id="10cc3-114">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="10cc3-114">This script uses hello following commands.</span></span> <span data-ttu-id="10cc3-115">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="10cc3-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="10cc3-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="10cc3-116">**Command**</span></span> | <span data-ttu-id="10cc3-117">**Notas**</span><span class="sxs-lookup"><span data-stu-id="10cc3-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="10cc3-118">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="10cc3-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="10cc3-119">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="10cc3-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="10cc3-120">Criar servidor do AZ mysql</span><span class="sxs-lookup"><span data-stu-id="10cc3-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="10cc3-121">Cria um servidor de MySQL aloja Olá bases de dados.</span><span class="sxs-lookup"><span data-stu-id="10cc3-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="10cc3-122">lista de métricas de monitor AZ</span><span class="sxs-lookup"><span data-stu-id="10cc3-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="10cc3-123">Olá métrico valor da lista de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="10cc3-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="10cc3-124">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="10cc3-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="10cc3-125">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="10cc3-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10cc3-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="10cc3-126">Next steps</span></span>
- <span data-ttu-id="10cc3-127">Leia mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="10cc3-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="10cc3-128">Tente scripts adicionais: [amostras da CLI do Azure para a base de dados do Azure para MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="10cc3-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="10cc3-129">Para obter mais informações sobre como aumentar, consulte [escalões de serviço](../concepts-service-tiers.md) e [unidades de armazenamento e computação unidades](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="10cc3-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
