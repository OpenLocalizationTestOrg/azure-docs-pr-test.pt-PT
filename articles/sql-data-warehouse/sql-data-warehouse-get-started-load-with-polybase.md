---
title: "aaaPolyBase tutorial de armazém de dados SQL | Microsoft Docs"
description: "Saiba o que é PolyBase e como toouse-la para cenários do armazém de dados."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Carregar os dados com o PolyBase para o SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Este tutorial mostra como dados de tooload para o SQL Data Warehouse, utilizando o AzCopy e o PolyBase. Quando terminar, ficará a saber como:

* Utilizar o AzCopy toocopy dados tooAzure blob storage
* Criar objetos de base de dados dados de Olá toodefine
* Executar uma consulta de T-SQL tooload Olá dados

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toostep com este tutorial, terá de

* Uma base de dados SQL Data Warehouse.
* Uma conta de armazenamento do Azure do tipo Armazenamento Localmente Redundante Standard (Standard-LRS), Armazenamento Georredundante Standard (Standard-GRS) ou Armazenamento Georredundante Standard com Acesso de Leitura (Standard-RAGRS).
* Utilitário de Linha de Comandos do AzCopy. Transfira e instale Olá [versão mais recente do AzCopy] [ latest version of AzCopy] que é instalada com Olá ferramentas de armazenamento do Microsoft Azure.
  
    ![Ferramentas de Armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Passo 1: Adicionar armazenamento de BLOBs de tooAzure de dados de exemplo
Dados de tooload ordem, precisamos tooput alguns dados de exemplo para um armazenamento de Blobs do Azure. Neste passo, vamos preencher um blob de Armazenamento do Azure com dados de exemplo. Mais tarde, utilizaremos PolyBase tooload estes dados de exemplo para a base de dados do armazém de dados do SQL Server.

### <a name="a-prepare-a-sample-text-file"></a>A. Preparar um ficheiro de texto de exemplo
tooprepare um ficheiro de texto de exemplo:

1. Abra o bloco de notas e copie Olá seguintes linhas de dados para um novo ficheiro. Guarde este tooyour no diretório temporário local como Temp%\DimDate2.txt.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a>B. Localizar o ponto final de serviço blob
toofind o ponto de final de serviço blob:

1. A partir do Portal do Azure de Olá selecione **procurar** > **contas do Storage**.
2. Clique em conta de armazenamento de Olá que pretende toouse.
3. No painel de conta de armazenamento de Olá, clique em Blobs
   
    ![Clicar em Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Guarde o URL do seu ponto final de serviço blob para utilizar mais tarde.
   
    ![Ponto final de serviço blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Localizar a chave de armazenamento do Azure
toofind a chave de armazenamento do Azure:

1. A partir do Portal do Azure Olá, selecione **procurar** > **contas do Storage**.
2. Clique na conta de armazenamento de Olá que pretende toouse.
3. Selecione **Todas as definições** > **Chaves de acesso**.
4. Clique em Olá cópia caixa toocopy um da sua área de transferência do acesso chaves toohello.
   
    ![Copiar a chave de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Copie o armazenamento de BLOBs de tooAzure de ficheiros de exemplo de Olá
toocopy o armazenamento de BLOBs de tooAzure de dados:

1. Abra uma linha de comandos e altere o diretório de instalação do diretórios toohello AzCopy. Este comando altera toohello diretório de instalação predefinido num cliente Windows de 64 bits.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Execute Olá seguintes comandos tooupload Olá ficheiro. Especifique o URL do ponto final de serviço blob para <blob service endpoint URL> e a chave da conta de armazenamento do Azure para <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

Consulte também [introdução ao utilitário de linha de comandos do AzCopy Olá][Getting Started with hello AzCopy Command-Line Utility].

### <a name="e-explore-your-blob-storage-container"></a>E. Explorar o contentor do armazenamento de blobs
ficheiro de Olá toosee carregado tooblob armazenamento:

1. Volte painel de serviço Blob tooyour.
2. Em Contentores, faça duplo clique em **datacontainer**.
3. tooexplore Olá caminho tooyour os dados, clique em pasta Olá **datedimension** e irá ver o ficheiro carregado **DimDate2.txt**.
4. Clique em Propriedades de tooview, **DimDate2.txt**.
5. Tenha em atenção que no painel de propriedades de Blob Olá, pode transferir ou eliminar o ficheiro de Olá.
   
    ![Ver o blob de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Passo 2: Criar uma tabela externa de dados de exemplo de Olá
Nesta secção, iremos criar uma tabela externa que define os dados de exemplo de Olá.

O PolyBase utiliza dados de tooaccess tabelas externas no armazenamento de Blobs do Azure. Uma vez que os dados de Olá não são armazenados no SQL Data Warehouse, o PolyBase processa dados externos de toohello de autenticação utilizando uma credencial com âmbito de base de dados.

exemplo de Olá neste passo utiliza estas toocreate de instruções Transact-SQL uma tabela externa.

* [Criar chave mestra (Transact-SQL)] [ Create Master Key (Transact-SQL)] credencial com âmbito segredo de Olá tooencrypt da base de dados.
* [Criar Database Scoped Credential (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informações de autenticação para a sua conta de armazenamento do Azure.
* [Criar origem de dados externa (Transact-SQL)] [ Create External Data Source (Transact-SQL)] localização de Olá toospecify do seu armazenamento de Blobs do Azure.
* [Criar formato de ficheiro externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] formato de Olá toospecify dos seus dados.
* [Criar tabela externa (Transact-SQL)] [ Create External Table (Transact-SQL)] Olá, definição de tabela de Olá toospecify e a localização dos dados.

Execute esta consulta na base de dados SQL Data Warehouse. Criará uma tabela externa com o nome DimDate2External no esquema dbo Olá que aponta toohello os dados de exemplo DimDate2.txt no armazenamento de Blobs do Azure Olá.

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


No SQL Server Object Explorer no Visual Studio, pode ver o formato de ficheiro externo Olá origem de dados externa, tabela e Olá DimDate2External.

![Ver tabela externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Passo 3: carregar dados para o SQL Data Warehouse
Depois de criar tabela externa Olá, pode carregar dados de Olá para uma nova tabela ou inseri-los numa tabela existente.

* dados de Olá tooload numa nova tabela, execute Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução. Step-by-Olá nova tabela terá as colunas de Olá nomeadas na consulta de Olá. tipos de dados de Olá de colunas de Olá corresponderá tipos de dados de Olá na definição de tabela externa Olá.
* dados de Olá tooload para uma tabela existente, utilize Olá [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrução.

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Passo 4: criar estatísticas nos dados recentemente carregados
O SQL Data Warehouse não cria nem atualiza automaticamente as estatísticas. Por conseguinte, tooachieve desempenho de consulta elevado, é importante toocreate estatísticas em cada coluna de cada tabela após Olá carregar primeiro. Também é importante tooupdate estatísticas após alterações substanciais nos dados de Olá.

Este exemplo cria estatísticas de coluna única na nova tabela de DimDate2 Olá.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

toolearn mais, consulte [estatísticas][Statistics].  

## <a name="next-steps"></a>Passos seguintes
Consulte Olá [Guia do PolyBase] [ PolyBase guide] para obter informações adicionais que deve conhecer ao desenvolver uma solução que utiliza o PolyBase.

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
