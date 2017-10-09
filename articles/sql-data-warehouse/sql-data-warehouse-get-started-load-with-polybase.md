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
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="a66c0-103">Carregar os dados com o PolyBase para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a66c0-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a66c0-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="a66c0-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="a66c0-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="a66c0-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="a66c0-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="a66c0-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="a66c0-107">BCP</span><span class="sxs-lookup"><span data-stu-id="a66c0-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="a66c0-108">Este tutorial mostra como dados de tooload para o SQL Data Warehouse, utilizando o AzCopy e o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="a66c0-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="a66c0-109">Quando terminar, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="a66c0-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="a66c0-110">Utilizar o AzCopy toocopy dados tooAzure blob storage</span><span class="sxs-lookup"><span data-stu-id="a66c0-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="a66c0-111">Criar objetos de base de dados dados de Olá toodefine</span><span class="sxs-lookup"><span data-stu-id="a66c0-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="a66c0-112">Executar uma consulta de T-SQL tooload Olá dados</span><span class="sxs-lookup"><span data-stu-id="a66c0-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a66c0-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a66c0-113">Prerequisites</span></span>
<span data-ttu-id="a66c0-114">toostep com este tutorial, terá de</span><span class="sxs-lookup"><span data-stu-id="a66c0-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="a66c0-115">Uma base de dados SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a66c0-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="a66c0-116">Uma conta de armazenamento do Azure do tipo Armazenamento Localmente Redundante Standard (Standard-LRS), Armazenamento Georredundante Standard (Standard-GRS) ou Armazenamento Georredundante Standard com Acesso de Leitura (Standard-RAGRS).</span><span class="sxs-lookup"><span data-stu-id="a66c0-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="a66c0-117">Utilitário de Linha de Comandos do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a66c0-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="a66c0-118">Transfira e instale Olá [versão mais recente do AzCopy] [ latest version of AzCopy] que é instalada com Olá ferramentas de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a66c0-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Ferramentas de Armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="a66c0-120">Passo 1: Adicionar armazenamento de BLOBs de tooAzure de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="a66c0-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="a66c0-121">Dados de tooload ordem, precisamos tooput alguns dados de exemplo para um armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a66c0-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="a66c0-122">Neste passo, vamos preencher um blob de Armazenamento do Azure com dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a66c0-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="a66c0-123">Mais tarde, utilizaremos PolyBase tooload estes dados de exemplo para a base de dados do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a66c0-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="a66c0-124">A.</span><span class="sxs-lookup"><span data-stu-id="a66c0-124">A.</span></span> <span data-ttu-id="a66c0-125">Preparar um ficheiro de texto de exemplo</span><span class="sxs-lookup"><span data-stu-id="a66c0-125">Prepare a sample text file</span></span>
<span data-ttu-id="a66c0-126">tooprepare um ficheiro de texto de exemplo:</span><span class="sxs-lookup"><span data-stu-id="a66c0-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="a66c0-127">Abra o bloco de notas e copie Olá seguintes linhas de dados para um novo ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a66c0-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="a66c0-128">Guarde este tooyour no diretório temporário local como Temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="a66c0-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="a66c0-129">B.</span><span class="sxs-lookup"><span data-stu-id="a66c0-129">B.</span></span> <span data-ttu-id="a66c0-130">Localizar o ponto final de serviço blob</span><span class="sxs-lookup"><span data-stu-id="a66c0-130">Find your blob service endpoint</span></span>
<span data-ttu-id="a66c0-131">toofind o ponto de final de serviço blob:</span><span class="sxs-lookup"><span data-stu-id="a66c0-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="a66c0-132">A partir do Portal do Azure de Olá selecione **procurar** > **contas do Storage**.</span><span class="sxs-lookup"><span data-stu-id="a66c0-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="a66c0-133">Clique em conta de armazenamento de Olá que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="a66c0-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="a66c0-134">No painel de conta de armazenamento de Olá, clique em Blobs</span><span class="sxs-lookup"><span data-stu-id="a66c0-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Clicar em Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="a66c0-136">Guarde o URL do seu ponto final de serviço blob para utilizar mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a66c0-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Ponto final de serviço blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="a66c0-138">C.</span><span class="sxs-lookup"><span data-stu-id="a66c0-138">C.</span></span> <span data-ttu-id="a66c0-139">Localizar a chave de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a66c0-139">Find your Azure storage key</span></span>
<span data-ttu-id="a66c0-140">toofind a chave de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="a66c0-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="a66c0-141">A partir do Portal do Azure Olá, selecione **procurar** > **contas do Storage**.</span><span class="sxs-lookup"><span data-stu-id="a66c0-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="a66c0-142">Clique na conta de armazenamento de Olá que pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="a66c0-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="a66c0-143">Selecione **Todas as definições** > **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="a66c0-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="a66c0-144">Clique em Olá cópia caixa toocopy um da sua área de transferência do acesso chaves toohello.</span><span class="sxs-lookup"><span data-stu-id="a66c0-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Copiar a chave de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="a66c0-146">D.</span><span class="sxs-lookup"><span data-stu-id="a66c0-146">D.</span></span> <span data-ttu-id="a66c0-147">Copie o armazenamento de BLOBs de tooAzure de ficheiros de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="a66c0-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="a66c0-148">toocopy o armazenamento de BLOBs de tooAzure de dados:</span><span class="sxs-lookup"><span data-stu-id="a66c0-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="a66c0-149">Abra uma linha de comandos e altere o diretório de instalação do diretórios toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a66c0-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="a66c0-150">Este comando altera toohello diretório de instalação predefinido num cliente Windows de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="a66c0-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="a66c0-151">Execute Olá seguintes comandos tooupload Olá ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a66c0-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="a66c0-152">Especifique o URL do ponto final de serviço blob para <blob service endpoint URL> e a chave da conta de armazenamento do Azure para <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="a66c0-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="a66c0-153">Consulte também [introdução ao utilitário de linha de comandos do AzCopy Olá][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="a66c0-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="a66c0-154">E.</span><span class="sxs-lookup"><span data-stu-id="a66c0-154">E.</span></span> <span data-ttu-id="a66c0-155">Explorar o contentor do armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="a66c0-155">Explore your blob storage container</span></span>
<span data-ttu-id="a66c0-156">ficheiro de Olá toosee carregado tooblob armazenamento:</span><span class="sxs-lookup"><span data-stu-id="a66c0-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="a66c0-157">Volte painel de serviço Blob tooyour.</span><span class="sxs-lookup"><span data-stu-id="a66c0-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="a66c0-158">Em Contentores, faça duplo clique em **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="a66c0-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="a66c0-159">tooexplore Olá caminho tooyour os dados, clique em pasta Olá **datedimension** e irá ver o ficheiro carregado **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="a66c0-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="a66c0-160">Clique em Propriedades de tooview, **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="a66c0-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="a66c0-161">Tenha em atenção que no painel de propriedades de Blob Olá, pode transferir ou eliminar o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Ver o blob de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="a66c0-163">Passo 2: Criar uma tabela externa de dados de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="a66c0-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="a66c0-164">Nesta secção, iremos criar uma tabela externa que define os dados de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="a66c0-165">O PolyBase utiliza dados de tooaccess tabelas externas no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a66c0-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="a66c0-166">Uma vez que os dados de Olá não são armazenados no SQL Data Warehouse, o PolyBase processa dados externos de toohello de autenticação utilizando uma credencial com âmbito de base de dados.</span><span class="sxs-lookup"><span data-stu-id="a66c0-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="a66c0-167">exemplo de Olá neste passo utiliza estas toocreate de instruções Transact-SQL uma tabela externa.</span><span class="sxs-lookup"><span data-stu-id="a66c0-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="a66c0-168">[Criar chave mestra (Transact-SQL)] [ Create Master Key (Transact-SQL)] credencial com âmbito segredo de Olá tooencrypt da base de dados.</span><span class="sxs-lookup"><span data-stu-id="a66c0-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="a66c0-169">[Criar Database Scoped Credential (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informações de autenticação para a sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a66c0-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="a66c0-170">[Criar origem de dados externa (Transact-SQL)] [ Create External Data Source (Transact-SQL)] localização de Olá toospecify do seu armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a66c0-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="a66c0-171">[Criar formato de ficheiro externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] formato de Olá toospecify dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="a66c0-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="a66c0-172">[Criar tabela externa (Transact-SQL)] [ Create External Table (Transact-SQL)] Olá, definição de tabela de Olá toospecify e a localização dos dados.</span><span class="sxs-lookup"><span data-stu-id="a66c0-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="a66c0-173">Execute esta consulta na base de dados SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a66c0-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="a66c0-174">Criará uma tabela externa com o nome DimDate2External no esquema dbo Olá que aponta toohello os dados de exemplo DimDate2.txt no armazenamento de Blobs do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


<span data-ttu-id="a66c0-175">No SQL Server Object Explorer no Visual Studio, pode ver o formato de ficheiro externo Olá origem de dados externa, tabela e Olá DimDate2External.</span><span class="sxs-lookup"><span data-stu-id="a66c0-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Ver tabela externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="a66c0-177">Passo 3: carregar dados para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a66c0-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="a66c0-178">Depois de criar tabela externa Olá, pode carregar dados de Olá para uma nova tabela ou inseri-los numa tabela existente.</span><span class="sxs-lookup"><span data-stu-id="a66c0-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="a66c0-179">dados de Olá tooload numa nova tabela, execute Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="a66c0-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="a66c0-180">Step-by-Olá nova tabela terá as colunas de Olá nomeadas na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="a66c0-181">tipos de dados de Olá de colunas de Olá corresponderá tipos de dados de Olá na definição de tabela externa Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="a66c0-182">dados de Olá tooload para uma tabela existente, utilize Olá [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="a66c0-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="a66c0-183">Passo 4: criar estatísticas nos dados recentemente carregados</span><span class="sxs-lookup"><span data-stu-id="a66c0-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="a66c0-184">O SQL Data Warehouse não cria nem atualiza automaticamente as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="a66c0-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="a66c0-185">Por conseguinte, tooachieve desempenho de consulta elevado, é importante toocreate estatísticas em cada coluna de cada tabela após Olá carregar primeiro.</span><span class="sxs-lookup"><span data-stu-id="a66c0-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="a66c0-186">Também é importante tooupdate estatísticas após alterações substanciais nos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="a66c0-187">Este exemplo cria estatísticas de coluna única na nova tabela de DimDate2 Olá.</span><span class="sxs-lookup"><span data-stu-id="a66c0-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="a66c0-188">toolearn mais, consulte [estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="a66c0-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a66c0-189">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a66c0-189">Next steps</span></span>
<span data-ttu-id="a66c0-190">Consulte Olá [Guia do PolyBase] [ PolyBase guide] para obter informações adicionais que deve conhecer ao desenvolver uma solução que utiliza o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="a66c0-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

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
