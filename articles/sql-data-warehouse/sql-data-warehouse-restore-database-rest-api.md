---
title: aaaRestore um Azure SQL Data Warehouse (REST API) | Microsoft Docs
description: Tarefas da REST API para restaurar um Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Restaurar um armazém de dados SQL do Azure (REST API)
> [!div class="op_single_selector"]
> * [Descrição geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Neste artigo, ficará a saber como toorestore um Azure SQL Data Warehouse, utilizando Olá REST API.

## <a name="before-you-begin"></a>Antes de começar
**Certifique-se a capacidade DTU.** Cada SQL Data Warehouse for alojado por um servidor de SQL Server (por exemplo, myserver.database.windows.net) tem uma quota DTU predefinido.  Antes de pode restaurar um SQL Data Warehouse, certifique-se que Olá que do SQL server tem suficiente restante quota de DTU para base de dados de Olá seja restaurado. toolearn como toocalculate DTU necessário ou toorequest DTU mais, consulte [pedir uma alteração de quota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restaurar uma base de dados do Active Directory ou em pausa
toorestore uma base de dados:

1. Obter a lista de Olá de pontos de restauro de base de dados utilizando a operação de pontos de restauro de base de dados de Get Olá.
2. Iniciar o restauro utilizando Olá [criar pedido de restauro de base de dados] [ Create database restore request] operação.
3. Controlar o estado de Olá do seu restauro utilizando Olá [base de dados de estado da operação] [ Database operation status] operação.

> [!NOTE]
> Depois de concluir o restauro de Olá, pode configurar a base de dados recuperada seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Restaurar uma base de dados eliminada
toorestore uma base de dados eliminada:

1. Lista todas as bases de dados eliminadas que possam ser restauradas utilizando Olá [lista que possam ser restaurada remover bases de dados] [ List restorable dropped databases] operação.
2. Detalhes do obter Olá para Olá eliminar base de dados toorestore utilizando Olá [Get que possam ser restaurada removido da base de dados] [ Get restorable dropped database] operação.
3. Iniciar o restauro utilizando Olá [criar pedido de restauro de base de dados] [ Create database restore request] operação.
4. Controlar o estado de Olá do seu restauro utilizando Olá [base de dados de estado da operação] [ Database operation status] operação.

> [!NOTE]
> tooconfigure a base de dados depois de concluir o restauro de Olá, consulte [configurar a base de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Passos seguintes
toolearn sobre as funcionalidades de continuidade de negócio Olá das edições do SQL Database do Azure, leia Olá [descrição geral da continuidade de negócio da linha de base de dados do Azure SQL][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
