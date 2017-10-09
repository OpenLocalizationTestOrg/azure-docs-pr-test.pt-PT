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
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a>Utilize o CLI toomonitor e dimensionar uma base de dados SQL

Neste exemplo de script da CLI do Azure dimensiona um nível de desempenho diferentes do tooa de base de dados SQL do Azure único depois de consultar as informações de tamanho da base de dados de Olá Olá. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

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
| [servidor de sql AZ criar](https://docs.microsoft.com/cli/azure/sql/server#create) | Cria um servidor lógico que aloja uma base de dados. |
| [base de dados de sql AZ Mostrar-utilização](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | Mostra informações de utilização de tamanho de Olá para uma base de dados. |
| [atualização de base de dados do sql AZ](https://docs.microsoft.com/cli/azure/sql/db#update) | Atualiza as propriedades de base de dados (por exemplo, Olá camada ou desempenho de nível de serviço) ou uma base de dados é movido para fora do ou entre conjuntos elásticos. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de base de dados do SQL adicionais podem ser encontrados na Olá [documentação da SQL Database do Azure](../sql-database-cli-samples.md).
