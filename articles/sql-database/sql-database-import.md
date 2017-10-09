---
title: aaaImport um BACPAC ficheiro toocreate uma base de dados SQL do Azure | Microsoft Docs
description: Crie uma base de dados do SQL Server newAzure ao importar um ficheiro BACPAC.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="81cce-103">Importar um tooa de ficheiro BACPAC nova SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="81cce-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="81cce-104">Quando precisa de uma base de dados de um arquivo de tooimport ou quando a migrar de outra plataforma, pode importar o esquema de base de dados de Olá e dos dados de um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) ficheiro.</span><span class="sxs-lookup"><span data-stu-id="81cce-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="81cce-105">Um ficheiro BACPAC é um ficheiro ZIP com uma extensão BACPAC contendo Olá metadados e dados a partir de uma base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="81cce-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="81cce-106">Um ficheiro BACPAC pode ser importado a partir do blob storage do Azure (apenas armazenamento standard) ou a partir do armazenamento local numa localização no local.</span><span class="sxs-lookup"><span data-stu-id="81cce-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="81cce-107">velocidade de importação do toomaximize Olá, recomendamos que especifique um nível mais elevado serviço camada e o desempenho, tais como um P6 e, em seguida, dimensionar toodown conforme apropriado após a importação de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="81cce-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="81cce-108">Além disso, o nível de compatibilidade de base de dados de Olá após a importação de Olá baseia-se no nível de compatibilidade de Olá da base de dados de origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="81cce-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="81cce-109">Depois de migrar o tooAzure de base de dados da base de dados do SQL Server, pode escolher toooperate Olá da base de dados ao respetivo nível de compatibilidade atual (nível 100 da base de dados do Olá AdventureWorks2008R2) ou com um nível superior.</span><span class="sxs-lookup"><span data-stu-id="81cce-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="81cce-110">Para obter mais informações sobre implicações de Olá e as opções para utilizar uma base de dados a um nível de compatibilidade específicos, consulte [nível de compatibilidade de base de dados ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="81cce-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="81cce-111">Consulte também [configuração de um âmbito de base de dados de falha de ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obter informações sobre definições de nível de base de dados adicionais relacionados com toocompatibility níveis.</span><span class="sxs-lookup"><span data-stu-id="81cce-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="81cce-112">tooimport BACPAC tooa nova base de dados, tem primeiro de criar um servidor lógico da SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="81cce-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="81cce-113">Para um tutorial que mostra como toomigrate um SQL Server da base de dados tooAzure base de dados SQL utilizando SQLPackage, consulte [migrar uma base de dados do SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="81cce-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="81cce-114">Importar de um ficheiro BACPAC através do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="81cce-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="81cce-115">Este artigo fornece instruções para criar uma base de dados SQL do Azure a partir de um ficheiro BACPAC armazenado no blob storage do Azure utilizando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81cce-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="81cce-116">Importar através de Olá apenas o portal do Azure suporta a importação de um ficheiro BACPAC do armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="81cce-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="81cce-117">Olá, tooimport uma base de dados através do portal do Azure, a página Olá aberto para a base de dados e clique em **importação** na barra de ferramentas Olá.</span><span class="sxs-lookup"><span data-stu-id="81cce-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="81cce-118">Especifique a conta de armazenamento Olá e um contentor e selecione Olá BACPAC ficheiro pretende tooimport.</span><span class="sxs-lookup"><span data-stu-id="81cce-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="81cce-119">Selecione o tamanho da base de dados nova Olá Olá (normalmente Olá mesmo como origem) e fornecer as credenciais do SQL Server de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="81cce-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Importação de base de dados](./media/sql-database-import/import.png)

<span data-ttu-id="81cce-121">progresso Olá toomonitor Olá operação de importação, abra a página Olá Olá servidor lógico que contêm Olá da base de dados que está a ser importado.</span><span class="sxs-lookup"><span data-stu-id="81cce-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="81cce-122">Desloque para baixo demasiado**operações** e, em seguida, clique em **importar/exportar** histórico.</span><span class="sxs-lookup"><span data-stu-id="81cce-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="81cce-123">Monitorize o progresso de Olá de uma operação de importação</span><span class="sxs-lookup"><span data-stu-id="81cce-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="81cce-124">progresso Olá toomonitor Olá operação de importação, abra a página Olá Olá servidor lógico no qual Olá base de dados está a ser importado importado.</span><span class="sxs-lookup"><span data-stu-id="81cce-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="81cce-125">Desloque para baixo demasiado**operações** e, em seguida, clique em **importar/exportar** histórico.</span><span class="sxs-lookup"><span data-stu-id="81cce-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="81cce-126">![importar](./media/sql-database-import/import-history.png) ![Importar estado](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="81cce-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="81cce-127">base de dados do tooverify Olá estiver em direto no servidor de Olá, clique em **bases de dados SQL** e certifique-se de que é nova base de dados Olá **Online**.</span><span class="sxs-lookup"><span data-stu-id="81cce-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="81cce-128">Importar de um ficheiro BACPAC utilizando SQLPackage</span><span class="sxs-lookup"><span data-stu-id="81cce-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="81cce-129">tooimport SQL da base de dados utilizando Olá [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitário de linha de comandos, consulte [importar parâmetros e as propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="81cce-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="81cce-130">Olá SQLPackage utilitário é fornecido com versões mais recentes do Olá das [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou pode transferir a versão mais recente do Olá do [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente a partir de Olá Microsoft Centro de transferências.</span><span class="sxs-lookup"><span data-stu-id="81cce-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="81cce-131">Recomendamos a utilização de Olá de Olá SQLPackage utilitário para dimensionamento e desempenho na maioria dos ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="81cce-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="81cce-132">Para uma equipa de Consultadora de cliente do SQL Server a utilizar ficheiros BACPAC, consulte o blogue sobre como migrar [migrar a partir do SQL Server tooAzure base de dados SQL a utilizar ficheiros BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="81cce-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="81cce-133">Consulte Olá seguir SQLPackage comando para obter um exemplo de script como tooimport Olá **AdventureWorks2008R2** base de dados de armazenamento local tooan SQL Database do Azure servidor lógico, denominado **mynewserver20170403** neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="81cce-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="81cce-134">Este script mostra a criação de uma nova base de dados chamado Olá **myMigratedDatabase**, com uma camada de serviço de **Premium**e um objetivo do serviço de **P6**.</span><span class="sxs-lookup"><span data-stu-id="81cce-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="81cce-135">Altere estes valores como ambiente de tooyour adequado.</span><span class="sxs-lookup"><span data-stu-id="81cce-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importação de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="81cce-137">Um servidor lógico da Base de Dados SQL do Azure ouve na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="81cce-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="81cce-138">Se está a tentar efetuar tooconnect tooan SQL Database do Azure servidor lógico de dentro de uma firewall empresarial, esta porta tem de ser aberta na firewall da empresa Olá para toosuccessfully a ligação.</span><span class="sxs-lookup"><span data-stu-id="81cce-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="81cce-139">Este exemplo mostra como tooimport uma base de dados utilizando SqlPackage.exe com autenticação de Universal do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="81cce-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="81cce-140">Importar de um ficheiro BACPAC através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="81cce-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="81cce-141">Olá utilize [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit um toohello de pedido de base de dados de importação serviço SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="81cce-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="81cce-142">Consoante o tamanho da base de dados Olá, operação de importação de Olá pode demorar algum tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="81cce-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="81cce-143">Estado de Olá toocheck de Olá o pedido de importação, utilize Olá [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="81cce-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="81cce-144">Normalmente, isto a executar imediatamente após Olá pedido devolve **Estado: em curso**.</span><span class="sxs-lookup"><span data-stu-id="81cce-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="81cce-145">Quando vir **Estado: foi concluída com êxito** Olá importação estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="81cce-145">When you see **Status: Succeeded** hello import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="81cce-146">Para obter outro exemplo de script, consulte [importar uma base de dados de um ficheiro BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="81cce-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81cce-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="81cce-147">Next steps</span></span>
* <span data-ttu-id="81cce-148">toolearn como tooconnect tooand consultar uma base de dados importados do SQL Server, consulte [ligar tooSQL da base de dados com o SQL Server Management Studio e executar uma consulta de T-SQL de exemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="81cce-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="81cce-149">Para uma equipa de Consultadora de cliente do SQL Server a utilizar ficheiros BACPAC, consulte o blogue sobre como migrar [migrar a partir do SQL Server tooAzure base de dados SQL a utilizar ficheiros BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="81cce-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="81cce-150">Para ver um debate Olá completo do SQL Server da base de dados do processo de migração, incluindo as recomendações de desempenho, consulte [migrar um tooAzure de base de dados do SQL Server da base de dados do SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="81cce-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



