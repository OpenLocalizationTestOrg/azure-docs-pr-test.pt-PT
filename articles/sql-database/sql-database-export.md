---
title: aaaExport um ficheiro BACPAC de tooa de base de dados SQL do Azure | Microsoft Docs
description: "Exportar um ficheiro de tooa da base de dados do SQL do Azure BACPAC utilizando Olá Portal do Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Exportar um ficheiro de BACPAC de tooa de base de dados SQL do Azure

Quando precisar de tooexport uma base de dados para arquivar ou para mover tooanother plataforma, pode exportar tooa de esquema e os dados da base de dados Olá [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) ficheiro. Um ficheiro BACPAC é um ficheiro ZIP com uma extensão BACPAC contendo Olá metadados e dados a partir de uma base de dados do SQL Server. Um ficheiro BACPAC pode ser armazenado no blob storage do Azure ou no armazenamento local numa localização no local e posteriormente importado para o SQL Database do Azure ou para uma instalação do SQL Server no local. 

> [!IMPORTANT] 
> Azure base de dados de SQL automatizada exportar foi reformada no dia 1 de Março de 2017. Pode utilizar [retenção de cópias de segurança de longa duração](sql-database-long-term-retention.md
) ou [da automatização do Azure](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) através do PowerShell em conformidade com a agenda de tooa à sua escolha tooperiodically bases de dados SQL de arquivo. Para um exemplo de Olá transferir [script do PowerShell de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) a partir do Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Considerações ao exportar uma base de dados SQL do Azure

* Exportação de toobe uma forma consistente, tem de garantir um nenhuma atividade de escrita está a ocorrer durante a exportação de hello, ou que lhe são exportar de um [cópia de uma forma consistente](sql-database-copy.md) da base de dados SQL do Azure.
* Se estiver a exportar tooblob armazenamento, o tamanho máximo do Olá de um ficheiro BACPAC é 200 GB. tooarchive um ficheiro BACPAC maior, exporte toolocal armazenamento.
* Não é suportada a exportar um BACPAC file tooAzure premium storage através de métodos de Olá abordados neste artigo.
* Se a operação de exportação Olá da SQL Database do Azure exceder 20 horas, pode ser cancelada. desempenho de tooincrease durante a exportação, pode:
  * Temporariamente aumente o nível de serviço.
  * Cessar todos de leitura e escrita atividade durante a exportação de Olá.
  * Utilize um [índice em cluster](https://msdn.microsoft.com/library/ms190457.aspx) com valores não nulos em todas as tabelas grandes. Sem os índices em cluster, uma exportação poderá falhar se demora mais de 6-12 horas. Isto acontece porque necessita de serviço de exportação de Olá toocomplete uma tabela análise tootry tooexport tabela inteira. Toodetermine uma boa forma, se as tabelas estão otimizadas para exportação é toorun **DBCC SHOW_STATISTICS** e certifique-se de que Olá *RANGE_HI_KEY* não seja nulo e o valor tem um bom distribuição. Para obter mais informações, consulte [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> BACPACs não são toobe pretendido utilizada para operações de cópia de segurança e restauro. Base de dados SQL do Azure cria automaticamente cópias de segurança para cada base de dados do utilizador. Para obter mais informações, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md) e [cópias de segurança da base de dados SQL](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Exportar ficheiro BACPAC tooa utilizando Olá portal do Azure

Olá tooexport utilizando uma base de dados [portal do Azure](https://portal.azure.com), abra a página Olá da base de dados e clique em **exportar** na barra de ferramentas Olá. Especifique o nome de ficheiro do Olá BACPAC, forneça Olá conta de armazenamento do Azure e um contentor de exportação de Olá e fornecer Olá credenciais tooconnect toohello origem da base de dados.  

![Exportação de base de dados](./media/sql-database-export/database-export.png)

progresso de Olá toomonitor de Olá operação de exportação, abra a página Olá Olá servidor lógico que contêm Olá da base de dados que está a ser exportado. Desloque para baixo demasiado**operações** e, em seguida, clique em **importar/exportar** histórico.

![Exportar histórico](./media/sql-database-export/export-history.png)
![exportar o estado do histórico](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Exportar ficheiro BACPAC tooa utilizando Olá SQLPackage utilitário

tooexport SQL da base de dados utilizando Olá [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitário de linha de comandos, consulte [exportar parâmetros e as propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Olá SQLPackage utilitário é fornecido com versões mais recentes do Olá das [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou pode transferir a versão mais recente do Olá do [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente a partir de Olá Microsoft Centro de transferências.

Recomendamos a utilização de Olá de Olá SQLPackage utilitário para dimensionamento e desempenho na maioria dos ambientes de produção. Para uma equipa de Consultadora de cliente do SQL Server a utilizar ficheiros BACPAC, consulte o blogue sobre como migrar [migrar a partir do SQL Server tooAzure base de dados SQL a utilizar ficheiros BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Este exemplo mostra como tooexport uma base de dados utilizando SqlPackage.exe com autenticação de Universal do Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Exportar ficheiro BACPAC tooa utilizando o SQL Server Management Studio (SSMS)

versões mais recentes do Olá do SQL Server Management Studio também fornecem um assistente tooexport um ficheiro BACPAC tooa SQL Database do Azure. Consulte Olá [exportar uma aplicação de camada de dados](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Exportar tooa BACPAC ficheiro com o PowerShell

Olá utilize [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit um toohello de pedido de base de dados de exportação serviço SQL Database do Azure. Consoante o tamanho da base de dados Olá, operação de exportação de Olá pode demorar algum tempo toocomplete.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

Estado de Olá toocheck de Olá solicitação de exportação, utilize Olá [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Normalmente, isto a executar imediatamente após Olá pedido devolve **Estado: em curso**. Quando vir **Estado: foi concluída com êxito** exportação Olá está concluída.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Passos seguintes

* toolearn sobre retenção de cópias de segurança de longa duração de uma cópia de segurança de base de dados SQL do Azure como uma alternativa tooexported uma base de dados para efeitos de arquivo, consulte [retenção de cópias de segurança de longa duração](sql-database-long-term-retention.md).
- Para uma equipa de Consultadora de cliente do SQL Server a utilizar ficheiros BACPAC, consulte o blogue sobre como migrar [migrar a partir do SQL Server tooAzure base de dados SQL a utilizar ficheiros BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* toolearn sobre como importar um BACPAC tooa do SQL Server da base de dados, consulte [importar uma base de dados do SQL Server de tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn sobre como exportar um BACPAC de uma base de dados do SQL Server, consulte [exportar uma aplicação de camada de dados](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) e [migrar a sua primeira base de dados](sql-database-migrate-your-sql-server-database.md).
* Se estiver a exportação do SQL Server como um tooAzure de toomigration prelude base de dados SQL, consulte o artigo [migrar um tooAzure de base de dados do SQL Server da base de dados do SQL Server](sql-database-cloud-migrate.md).
