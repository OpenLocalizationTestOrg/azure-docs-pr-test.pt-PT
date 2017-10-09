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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="52473-103">Restaurar um armazém de dados SQL do Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="52473-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="52473-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="52473-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="52473-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="52473-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="52473-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="52473-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="52473-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="52473-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="52473-108">Neste artigo, ficará a saber como toorestore um Azure SQL Server do armazém de dados com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52473-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="52473-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="52473-109">Before you begin</span></span>
<span data-ttu-id="52473-110">**Certifique-se a capacidade DTU.**</span><span class="sxs-lookup"><span data-stu-id="52473-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="52473-111">Cada SQL Data Warehouse for alojado por um servidor de SQL Server (por exemplo, myserver.database.windows.net) tem uma quota DTU predefinido.</span><span class="sxs-lookup"><span data-stu-id="52473-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="52473-112">Antes de pode restaurar um SQL Data Warehouse, certifique-se que Olá que do SQL server tem suficiente restante quota de DTU para base de dados de Olá seja restaurado.</span><span class="sxs-lookup"><span data-stu-id="52473-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="52473-113">toolearn como toocalculate DTU necessário ou toorequest DTU mais, consulte [pedir uma alteração de quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="52473-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="52473-114">Instalar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="52473-114">Install PowerShell</span></span>
<span data-ttu-id="52473-115">Na ordem toouse Azure PowerShell com o SQL Data Warehouse, terá de tooinstall do Azure PowerShell 1.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="52473-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="52473-116">Pode verificar a sua versão, executando **Get-Module - ListAvailable-Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="52473-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="52473-117">versão mais recente Olá pode ser instalado na [instalador de plataforma Web Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="52473-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="52473-118">Para obter mais informações sobre como instalar a versão mais recente Olá, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="52473-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="52473-119">Restaurar uma base de dados do Active Directory ou em pausa</span><span class="sxs-lookup"><span data-stu-id="52473-119">Restore an active or paused database</span></span>
<span data-ttu-id="52473-120">uma base de dados a partir de um instantâneo de toorestore utilizar Olá [restauro-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52473-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="52473-121">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52473-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="52473-122">Lista de todas as subscrições de Olá associadas à sua conta e ligar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="52473-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="52473-123">Selecione a subscrição de Olá que contém Olá toobe de base de dados restaurada.</span><span class="sxs-lookup"><span data-stu-id="52473-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="52473-124">Olá lista restaurar pontos da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="52473-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="52473-125">Escolha o ponto de restauro de Olá pretendido utilizando Olá RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="52473-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="52473-126">Restaure o ponto de restauro do Olá da base de dados toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="52473-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="52473-127">Certifique-se de que a base de dados de Olá restaurada está online.</span><span class="sxs-lookup"><span data-stu-id="52473-127">Verify that hello restored database is online.</span></span>

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
> <span data-ttu-id="52473-128">Depois de concluir o restauro de Olá, pode configurar a base de dados recuperada seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="52473-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="52473-129">Restaurar uma base de dados eliminada</span><span class="sxs-lookup"><span data-stu-id="52473-129">Restore a deleted database</span></span>
<span data-ttu-id="52473-130">toorestore uma base de dados eliminada, utilize Olá [restauro-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="52473-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="52473-131">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52473-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="52473-132">Lista de todas as subscrições de Olá associadas à sua conta e ligar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="52473-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="52473-133">Eliminar a subscrição de Olá SELECT que contém Olá toobe de base de dados restaurada.</span><span class="sxs-lookup"><span data-stu-id="52473-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="52473-134">Obter a base de dados de Olá específico eliminado.</span><span class="sxs-lookup"><span data-stu-id="52473-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="52473-135">Restaure a base de dados de Olá eliminado.</span><span class="sxs-lookup"><span data-stu-id="52473-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="52473-136">Certifique-se de que a base de dados de Olá restaurada está online.</span><span class="sxs-lookup"><span data-stu-id="52473-136">Verify that hello restored database is online.</span></span>

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
> <span data-ttu-id="52473-137">Depois de concluir o restauro de Olá, pode configurar a base de dados recuperada seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="52473-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="52473-138">Restaurar a partir de uma região geográfica do Azure</span><span class="sxs-lookup"><span data-stu-id="52473-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="52473-139">toorecover uma base de dados, utilize Olá [restauro-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="52473-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="52473-140">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52473-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="52473-141">Lista de todas as subscrições de Olá associadas à sua conta e ligar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="52473-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="52473-142">Selecione a subscrição de Olá que contém Olá toobe de base de dados restaurada.</span><span class="sxs-lookup"><span data-stu-id="52473-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="52473-143">Obter Olá base de dados toorecover.</span><span class="sxs-lookup"><span data-stu-id="52473-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="52473-144">Crie pedido de recuperação de Olá da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="52473-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="52473-145">Verifique o estado de Olá da base de dados de georreplicação-restaurada Olá.</span><span class="sxs-lookup"><span data-stu-id="52473-145">Verify hello status of hello geo-restored database.</span></span>

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
> <span data-ttu-id="52473-146">tooconfigure a base de dados depois de concluir o restauro de Olá, consulte [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="52473-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="52473-147">base de dados recuperada Olá será TDE-ativada se a base de dados de origem de Olá é TDE-ativado.</span><span class="sxs-lookup"><span data-stu-id="52473-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52473-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="52473-148">Next steps</span></span>
<span data-ttu-id="52473-149">toolearn sobre as funcionalidades de continuidade de negócio Olá das edições do SQL Database do Azure, leia Olá [descrição geral da continuidade de negócio da linha de base de dados do Azure SQL][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="52473-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
