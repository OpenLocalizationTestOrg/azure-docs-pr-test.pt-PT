---
title: "débito de contentor do CLI escala de Script do Azure Cosmos DB aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - escala Azure Cosmos DB contianer débito"
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
ms.openlocfilehash: b1a60feaf43f555a9f6ba20e5e0617f73521c0a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-hello-azure-cli"></a>Débito de contentor Azure Cosmos BD do dimensionamento utilizando Olá CLI do Azure

Este exemplo ajusta o débito de contentor para qualquer tipo de contentor do Azure Cosmos DB.  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

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
