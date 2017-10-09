---
title: aaaRestore um Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
description: Tarefas do PowerShell para restaurar um Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Restaurar um armazém de dados SQL do Azure (PowerShell)
> [!div class="op_single_selector"]
> * [Descrição geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Neste artigo, ficará a saber como toorestore um Azure SQL Server do armazém de dados com o PowerShell.

## <a name="before-you-begin"></a>Antes de começar
**Certifique-se a capacidade DTU.** Cada SQL Data Warehouse for alojado por um servidor de SQL Server (por exemplo, myserver.database.windows.net) tem uma quota DTU predefinido.  Antes de pode restaurar um SQL Data Warehouse, certifique-se que Olá que do SQL server tem suficiente restante quota de DTU para base de dados de Olá seja restaurado. toolearn como toocalculate DTU necessário ou toorequest DTU mais, consulte [pedir uma alteração de quota DTU][Request a DTU quota change].

### <a name="install-powershell"></a>Instalar o PowerShell
Na ordem toouse Azure PowerShell com o SQL Data Warehouse, terá de tooinstall do Azure PowerShell 1.0 ou superior.  Pode verificar a sua versão, executando **Get-Module - ListAvailable-Name AzureRM**.  versão mais recente Olá pode ser instalado na [instalador de plataforma Web Microsoft][Microsoft Web Platform Installer].  Para obter mais informações sobre como instalar a versão mais recente Olá, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Restaurar uma base de dados do Active Directory ou em pausa
uma base de dados a partir de um instantâneo de toorestore utilizar Olá [restauro-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet do PowerShell.

1. Abra o Windows PowerShell.
2. Lista de todas as subscrições de Olá associadas à sua conta e ligar tooyour conta do Azure.
3. Selecione a subscrição de Olá que contém Olá toobe de base de dados restaurada.
4. Olá lista restaurar pontos da base de dados de Olá.
5. Escolha o ponto de restauro de Olá pretendido utilizando Olá RestorePointCreationDate.
6. Restaure o ponto de restauro do Olá da base de dados toohello assim o desejar.
7. Certifique-se de que a base de dados de Olá restaurada está online.

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> Depois de concluir o restauro de Olá, pode configurar a base de dados recuperada seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Restaurar uma base de dados eliminada
toorestore uma base de dados eliminada, utilize Olá [restauro-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Abra o Windows PowerShell.
2. Lista de todas as subscrições de Olá associadas à sua conta e ligar tooyour conta do Azure.
3. Eliminar a subscrição de Olá SELECT que contém Olá toobe de base de dados restaurada.
4. Obter a base de dados de Olá específico eliminado.
5. Restaure a base de dados de Olá eliminado.
6. Certifique-se de que a base de dados de Olá restaurada está online.

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> Depois de concluir o restauro de Olá, pode configurar a base de dados recuperada seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Restaurar a partir de uma região geográfica do Azure
toorecover uma base de dados, utilize Olá [restauro-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Abra o Windows PowerShell.
2. Lista de todas as subscrições de Olá associadas à sua conta e ligar tooyour conta do Azure.
3. Selecione a subscrição de Olá que contém Olá toobe de base de dados restaurada.
4. Obter Olá base de dados toorecover.
5. Crie pedido de recuperação de Olá da base de dados de Olá.
6. Verifique o estado de Olá da base de dados de georreplicação-restaurada Olá.

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> tooconfigure a base de dados depois de concluir o restauro de Olá, consulte [configurar a base de dados após a recuperação][Configure your database after recovery].
> 
> 

base de dados recuperada Olá será TDE-ativada se a base de dados de origem de Olá é TDE-ativado.

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
