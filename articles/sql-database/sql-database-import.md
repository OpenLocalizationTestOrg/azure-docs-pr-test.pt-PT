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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Importar um tooa de ficheiro BACPAC nova SQL Database do Azure

Quando precisa de uma base de dados de um arquivo de tooimport ou quando a migrar de outra plataforma, pode importar o esquema de base de dados de Olá e dos dados de um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) ficheiro. Um ficheiro BACPAC é um ficheiro ZIP com uma extensão BACPAC contendo Olá metadados e dados a partir de uma base de dados do SQL Server. Um ficheiro BACPAC pode ser importado a partir do blob storage do Azure (apenas armazenamento standard) ou a partir do armazenamento local numa localização no local. velocidade de importação do toomaximize Olá, recomendamos que especifique um nível mais elevado serviço camada e o desempenho, tais como um P6 e, em seguida, dimensionar toodown conforme apropriado após a importação de Olá é efetuada com êxito. Além disso, o nível de compatibilidade de base de dados de Olá após a importação de Olá baseia-se no nível de compatibilidade de Olá da base de dados de origem de Olá. 

> [!IMPORTANT] 
> Depois de migrar o tooAzure de base de dados da base de dados do SQL Server, pode escolher toooperate Olá da base de dados ao respetivo nível de compatibilidade atual (nível 100 da base de dados do Olá AdventureWorks2008R2) ou com um nível superior. Para obter mais informações sobre implicações de Olá e as opções para utilizar uma base de dados a um nível de compatibilidade específicos, consulte [nível de compatibilidade de base de dados ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Consulte também [configuração de um âmbito de base de dados de falha de ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obter informações sobre definições de nível de base de dados adicionais relacionados com toocompatibility níveis.   >

> [!NOTE]
> tooimport BACPAC tooa nova base de dados, tem primeiro de criar um servidor lógico da SQL Database do Azure. Para um tutorial que mostra como toomigrate um SQL Server da base de dados tooAzure base de dados SQL utilizando SQLPackage, consulte [migrar uma base de dados do SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importar de um ficheiro BACPAC através do portal do Azure

Este artigo fornece instruções para criar uma base de dados SQL do Azure a partir de um ficheiro BACPAC armazenado no blob storage do Azure utilizando Olá [portal do Azure](https://portal.azure.com). Importar através de Olá apenas o portal do Azure suporta a importação de um ficheiro BACPAC do armazenamento de Blobs do Azure.

Olá, tooimport uma base de dados através do portal do Azure, a página Olá aberto para a base de dados e clique em **importação** na barra de ferramentas Olá. Especifique a conta de armazenamento Olá e um contentor e selecione Olá BACPAC ficheiro pretende tooimport. Selecione o tamanho da base de dados nova Olá Olá (normalmente Olá mesmo como origem) e fornecer as credenciais do SQL Server de destino Olá.  

   ![Importação de base de dados](./media/sql-database-import/import.png)

progresso Olá toomonitor Olá operação de importação, abra a página Olá Olá servidor lógico que contêm Olá da base de dados que está a ser importado. Desloque para baixo demasiado**operações** e, em seguida, clique em **importar/exportar** histórico.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Monitorize o progresso de Olá de uma operação de importação

progresso Olá toomonitor Olá operação de importação, abra a página Olá Olá servidor lógico no qual Olá base de dados está a ser importado importado. Desloque para baixo demasiado**operações** e, em seguida, clique em **importar/exportar** histórico.
   
   ![importar](./media/sql-database-import/import-history.png) ![Importar estado](./media/sql-database-import/import-status.png)

base de dados do tooverify Olá estiver em direto no servidor de Olá, clique em **bases de dados SQL** e certifique-se de que é nova base de dados Olá **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importar de um ficheiro BACPAC utilizando SQLPackage

tooimport SQL da base de dados utilizando Olá [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitário de linha de comandos, consulte [importar parâmetros e as propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Olá SQLPackage utilitário é fornecido com versões mais recentes do Olá das [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou pode transferir a versão mais recente do Olá do [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente a partir de Olá Microsoft Centro de transferências.

Recomendamos a utilização de Olá de Olá SQLPackage utilitário para dimensionamento e desempenho na maioria dos ambientes de produção. Para uma equipa de Consultadora de cliente do SQL Server a utilizar ficheiros BACPAC, consulte o blogue sobre como migrar [migrar a partir do SQL Server tooAzure base de dados SQL a utilizar ficheiros BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Consulte Olá seguir SQLPackage comando para obter um exemplo de script como tooimport Olá **AdventureWorks2008R2** base de dados de armazenamento local tooan SQL Database do Azure servidor lógico, denominado **mynewserver20170403** neste exemplo. Este script mostra a criação de uma nova base de dados chamado Olá **myMigratedDatabase**, com uma camada de serviço de **Premium**e um objetivo do serviço de **P6**. Altere estes valores como ambiente de tooyour adequado.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importação de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Um servidor lógico da Base de Dados SQL do Azure ouve na porta 1433. Se está a tentar efetuar tooconnect tooan SQL Database do Azure servidor lógico de dentro de uma firewall empresarial, esta porta tem de ser aberta na firewall da empresa Olá para toosuccessfully a ligação.
>

Este exemplo mostra como tooimport uma base de dados utilizando SqlPackage.exe com autenticação de Universal do Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importar de um ficheiro BACPAC através do PowerShell

Olá utilize [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit um toohello de pedido de base de dados de importação serviço SQL Database do Azure. Consoante o tamanho da base de dados Olá, operação de importação de Olá pode demorar algum tempo toocomplete.

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

Estado de Olá toocheck de Olá o pedido de importação, utilize Olá [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Normalmente, isto a executar imediatamente após Olá pedido devolve **Estado: em curso**. Quando vir **Estado: foi concluída com êxito** Olá importação estiver concluída.

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
Para obter outro exemplo de script, consulte [importar uma base de dados de um ficheiro BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Passos seguintes
* toolearn como tooconnect tooand consultar uma base de dados importados do SQL Server, consulte [ligar tooSQL da base de dados com o SQL Server Management Studio e executar uma consulta de T-SQL de exemplo](sql-database-connect-query-ssms.md).
* Para uma equipa de Consultadora de cliente do SQL Server a utilizar ficheiros BACPAC, consulte o blogue sobre como migrar [migrar a partir do SQL Server tooAzure base de dados SQL a utilizar ficheiros BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Para ver um debate Olá completo do SQL Server da base de dados do processo de migração, incluindo as recomendações de desempenho, consulte [migrar um tooAzure de base de dados do SQL Server da base de dados do SQL Server](sql-database-cloud-migrate.md).



