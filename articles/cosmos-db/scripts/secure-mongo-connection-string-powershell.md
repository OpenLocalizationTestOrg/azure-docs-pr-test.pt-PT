---
title: "aaaAzure cadeia de ligação de base de dados do Cosmos do PowerShell Get de Script do Azure para aplicações do MongoDB | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - cadeia de ligação de base de dados do Get Azure Cosmos para aplicações do MongoDB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d04502b8f59bb6f3cb8bec696595f962b479fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a>Obter uma cadeia de ligação de base de dados do Azure Cosmos para as aplicações de MongoDB utilizando o PowerShell

Este exemplo obtém uma cadeia de ligação de base de dados do Azure Cosmos para aplicações de MongoDB utilizando o PowerShell. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get hello MongoDB connection string from an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Novo AzureRmResource](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico. |
| [AzureRmResourceAction invocar](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | Invoca uma ação no Olá conta CosmosDB do Azure. |
| [Remove-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).

Exemplos de script do PowerShell de base de dados do Azure Cosmos adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do Azure Cosmos](../powershell-samples.md).
