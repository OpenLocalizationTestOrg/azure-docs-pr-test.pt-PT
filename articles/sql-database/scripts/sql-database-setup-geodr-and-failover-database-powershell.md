---
title: "aaaPowerShell exemplo-ativo georreplicação-replicação-única base de dados SQL do Azure | Microsoft Docs"
description: "Azure tooset de script de exemplo do PowerShell segurança georreplicação ativa para uma base de dados SQL do Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a>Utilizar o PowerShell tooconfigure georreplicação ativa para uma base de dados SQL do Azure

Neste exemplo de script do PowerShell configura a georreplicação ativa para uma base de dados SQL do Azure e a ativação pós-falha tooa réplica secundária de Olá SQL database do Azure.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a>Scripts de exemplo

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Novo AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico. |
| [Novo-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | Cria um conjunto elástico dentro de um servidor lógico. |
| [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) | Atualiza as propriedades de base de dados ou move de uma base de dados para fora do ou entre conjuntos elásticos. |
| [Novo AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| Cria uma base de dados secundária para uma base de dados existente e começa a replicação de dados. |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)| Obtém um ou mais bases de dados. |
| [Conjunto AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| Comutadores uma ativação pós-falha primário tooinitiate de toobe de base de dados secundária.|
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | Obtém as ligações de georreplicação Olá entre uma base de dados do SQL do Azure e um grupo de recursos ou do SQL Server. |
| [Remover AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | Termina a replicação de dados entre uma base de dados SQL e Olá especificado base de dados secundária. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).
