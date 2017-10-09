---
title: "do novo para a base de dados do SQL Server de exemplo-cópia-Azure aaaPowerShell | Microsoft Docs"
description: Azure PowerShell exemplo script toocopy um SQL Server da base de dados tooa novo servidor
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a>Utilizar o PowerShell toocopy um SQL Server da base de dados tooa novo servidor

Neste exemplo de script do PowerShell cria uma cópia da base de dados existente num servidor novo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a>Copiar um base de dados tooa novo servidor

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Novo AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado. |
| [Novo AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | Cria uma cópia da base de dados que utiliza o instantâneo de Olá em Olá hora atual. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).
