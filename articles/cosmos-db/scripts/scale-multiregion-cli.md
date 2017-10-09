---
title: "replicação de CLI Script-Multiregion aaaAzure para a base de dados do Azure Cosmos | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - Multiregion replicação para a base de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: e3590303ed3bda9eca1046bf62fff6b61333156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-hello-azure-cli"></a>Replicar uma conta de base de dados de base de dados do Azure Cosmos em várias regiões e configurar as prioridades de ativação pós-falha utilizando Olá CLI do Azure

Este exemplo replica qualquer tipo de conta de base de dados de base de dados do Azure Cosmos em várias regiões e configura as prioridades de ativação pós-falha utilizando Olá CLI do Azure.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [atualização de cosmosdb AZ](https://docs.microsoft.com/cli/azure/cosmosdb#update) | Atualiza uma conta de base de dados do Azure Cosmos. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/group#delete) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script da CLI do Azure Cosmos DB adicionais podem ser encontrados na Olá [documentação da CLI do Azure Cosmos DB](../cli-samples.md).
