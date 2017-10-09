---
title: "agrupamento elástico de SQL da base de dados SQL do Azure de exemplo mover aaaCLI | Microsoft Docs"
description: "Azure CLI exemplo script toomove uma base de dados SQL num agrupamento elástico de SQL"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a>Utilize o CLI toomove uma base de dados SQL do Azure num agrupamento elástico de SQL

Neste exemplo de script da CLI do Azure cria dois conjuntos elásticos e move de uma base de dados SQL do Azure de um agrupamento elástico de SQL para outro conjunto elástico de SQL e, em seguida, avança base de dados de Olá fora do nível de desempenho do conjunto elástico tooa única base de dados do Azure. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [servidor de sql AZ criar](https://docs.microsoft.com/cli/azure/sql/server#create) | Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico. |
| [criar conjuntos de elástico do sql AZ](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Cria um conjunto elástico no servidor lógico de Olá. |
| [Criar BD do sql AZ](https://docs.microsoft.com/cli/azure/sql/db#create) | Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado. |
| [atualização de base de dados do sql AZ](https://docs.microsoft.com/cli/azure/sql/db#update) | Atualiza as propriedades de base de dados ou move de uma base de dados para fora do ou entre conjuntos elásticos. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de base de dados do SQL adicionais podem ser encontrados na Olá [documentação da SQL Database do Azure](../sql-database-cli-samples.md).


