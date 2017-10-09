---
title: "exemplo de aaaCLI dimensiona uma SQL elástica conjunto-SQL Database do Azure | Microsoft Docs"
description: "Azure CLI exemplo script tooscale um agrupamento elástico de SQL no SQL Database do Azure"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a>Utilize o CLI tooscale um agrupamento elástico de SQL no SQL Database do Azure

Neste exemplo de script da CLI do Azure cria conjuntos elásticos SQL, move agrupados bases de dados e níveis de desempenho do conjunto elástico é alterado. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, servidor lógico, base de dados SQL e as regras de firewall. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [servidor de sql AZ criar](https://docs.microsoft.com/cli/azure/sql/server#create) | Cria um servidor lógico que anfitriões Olá base de dados SQL. |
| [criar conjuntos de elástico do sql AZ](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Cria um conjunto de bases de dados elásticas no servidor lógico de Olá. |
| [Criar BD do sql AZ](https://docs.microsoft.com/cli/azure/sql/db#create) | Cria Olá base de dados SQL no servidor lógico de Olá. |
| [atualização de conjuntos elásticos sql AZ](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | As atualizações de um conjunto de bases de dados elásticas, neste Olá de alterações de exemplo atribuída eDTU. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de base de dados do SQL adicionais podem ser encontrados na Olá [documentação da SQL Database do Azure](../sql-database-cli-samples.md).
