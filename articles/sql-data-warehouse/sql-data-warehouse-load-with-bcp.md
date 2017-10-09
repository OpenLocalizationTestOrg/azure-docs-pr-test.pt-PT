---
title: dados de tooload aaaUse bcp para o SQL Data Warehouse | Microsoft Docs
description: "Saiba o que é o bcp e como toouse-la para cenários do armazém de dados."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="4c326-103">Carregar dados com o bcp</span><span class="sxs-lookup"><span data-stu-id="4c326-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c326-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="4c326-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="4c326-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="4c326-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="4c326-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="4c326-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="4c326-107">BCP</span><span class="sxs-lookup"><span data-stu-id="4c326-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="4c326-108">**[BCP] [ bcp]**  é um utilitário de carregamento em massa da linha de comandos que lhe permite toocopy dados entre o SQL Server, ficheiros de dados e do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c326-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="4c326-109">Utilize o bcp tooimport grandes quantidades de linhas em tabelas de SQL do armazém de dados ou dados tooexport tabelas do SQL Server para ficheiros de dados.</span><span class="sxs-lookup"><span data-stu-id="4c326-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="4c326-110">Exceto quando utilizado com a opção de queryout Olá, bcp necessita de nenhum conhecimento de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4c326-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="4c326-111">o BCP é uma forma rápida e fácil toomove conjuntos de dados menores dentro e fora de uma base de dados do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c326-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="4c326-112">quantidade exata de Olá de dados que são recomendadas tooload/extração através do bcp dependerá de rede ligação toohello Datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c326-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="4c326-113">Geralmente, as tabelas de dimensões podem ser prontamente carregadas e extraídas com o bcp. No entanto, não é recomendada a utilização do bcp para carregar ou extrair grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="4c326-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="4c326-114">O Polybase é Olá recomendado ferramenta para carregar e extrair grandes volumes de dados como uma tarefa melhor tirar partido da arquitetura de processamento paralelo em grande escala de Olá do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4c326-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="4c326-115">O bcp permite:</span><span class="sxs-lookup"><span data-stu-id="4c326-115">With bcp you can:</span></span>

* <span data-ttu-id="4c326-116">Utilize um utilitário de linha de comandos simples tooload de dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4c326-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="4c326-117">Utilize dados de tooextract um utilitário de linha de comandos simples do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4c326-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="4c326-118">Este tutorial irá mostrar-lhe como:</span><span class="sxs-lookup"><span data-stu-id="4c326-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="4c326-119">Importar dados para uma tabela com o bcp de Olá no comando</span><span class="sxs-lookup"><span data-stu-id="4c326-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="4c326-120">Exportar dados de um tabela uisng Olá de saída do bcp comando</span><span class="sxs-lookup"><span data-stu-id="4c326-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4c326-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c326-121">Prerequisites</span></span>
<span data-ttu-id="4c326-122">toostep com este tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="4c326-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="4c326-123">Uma base de dados SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4c326-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="4c326-124">Olá linha de comandos instalado o utilitário bcp</span><span class="sxs-lookup"><span data-stu-id="4c326-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="4c326-125">Olá utilitário de linha de comandos SQLCMD instalado</span><span class="sxs-lookup"><span data-stu-id="4c326-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="4c326-126">Pode transferir os utilitários bcp e sqlcmd a Olá de Olá [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="4c326-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="4c326-127">Importar dados para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4c326-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="4c326-128">Neste tutorial, irá criar uma tabela no Azure SQL Data Warehouse e importar dados para a tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="4c326-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="4c326-129">Passo 1: criar uma tabela no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4c326-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="4c326-130">A partir de uma linha de comandos, utilize o sqlcmd toorun Olá toocreate consulta uma tabela a seguir na sua instância:</span><span class="sxs-lookup"><span data-stu-id="4c326-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> <span data-ttu-id="4c326-131">Consulte [descrição geral da tabela] [ Table Overview] ou [sintaxe CREATE TABLE] [ CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e Olá  opções disponíveis na cláusula WITH de Olá.</span><span class="sxs-lookup"><span data-stu-id="4c326-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="4c326-132">Passo 2: criar um ficheiro de dados de origem</span><span class="sxs-lookup"><span data-stu-id="4c326-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="4c326-133">Abra o bloco de notas e copie Olá seguintes linhas de dados para um novo ficheiro de texto e, em seguida, guarde este ficheiro tooyour diretório temporário local, c:\temp\dimdate2.txt..</span><span class="sxs-lookup"><span data-stu-id="4c326-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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

> [!NOTE]
> <span data-ttu-id="4c326-134">É importante tooremember que bcp.exe não suporta a codificação de ficheiro Olá UTF-8.</span><span class="sxs-lookup"><span data-stu-id="4c326-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="4c326-135">Utilize ficheiros ASCII ou ficheiros codificados com UTF-16 ao utilizar bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="4c326-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="4c326-136">Passo 3: Ligar e importar dados de Olá</span><span class="sxs-lookup"><span data-stu-id="4c326-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="4c326-137">Utilizar o bcp, pode ligar e importar dados de Olá utilizando Olá os seguintes valores de substituição Olá comando conforme adequado:</span><span class="sxs-lookup"><span data-stu-id="4c326-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="4c326-138">Pode verificar Olá dados foram carregados, executando Olá seguinte consulta com o sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="4c326-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="4c326-139">Isto deverá devolver Olá os seguintes resultados:</span><span class="sxs-lookup"><span data-stu-id="4c326-139">This should return hello following results:</span></span>

| <span data-ttu-id="4c326-140">DateId</span><span class="sxs-lookup"><span data-stu-id="4c326-140">DateId</span></span> | <span data-ttu-id="4c326-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="4c326-141">CalendarQuarter</span></span> | <span data-ttu-id="4c326-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="4c326-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c326-143">20150101</span><span class="sxs-lookup"><span data-stu-id="4c326-143">20150101</span></span> |<span data-ttu-id="4c326-144">1</span><span class="sxs-lookup"><span data-stu-id="4c326-144">1</span></span> |<span data-ttu-id="4c326-145">3</span><span class="sxs-lookup"><span data-stu-id="4c326-145">3</span></span> |
| <span data-ttu-id="4c326-146">20150201</span><span class="sxs-lookup"><span data-stu-id="4c326-146">20150201</span></span> |<span data-ttu-id="4c326-147">1</span><span class="sxs-lookup"><span data-stu-id="4c326-147">1</span></span> |<span data-ttu-id="4c326-148">3</span><span class="sxs-lookup"><span data-stu-id="4c326-148">3</span></span> |
| <span data-ttu-id="4c326-149">20150301</span><span class="sxs-lookup"><span data-stu-id="4c326-149">20150301</span></span> |<span data-ttu-id="4c326-150">1</span><span class="sxs-lookup"><span data-stu-id="4c326-150">1</span></span> |<span data-ttu-id="4c326-151">3</span><span class="sxs-lookup"><span data-stu-id="4c326-151">3</span></span> |
| <span data-ttu-id="4c326-152">20150401</span><span class="sxs-lookup"><span data-stu-id="4c326-152">20150401</span></span> |<span data-ttu-id="4c326-153">2</span><span class="sxs-lookup"><span data-stu-id="4c326-153">2</span></span> |<span data-ttu-id="4c326-154">4</span><span class="sxs-lookup"><span data-stu-id="4c326-154">4</span></span> |
| <span data-ttu-id="4c326-155">20150501</span><span class="sxs-lookup"><span data-stu-id="4c326-155">20150501</span></span> |<span data-ttu-id="4c326-156">2</span><span class="sxs-lookup"><span data-stu-id="4c326-156">2</span></span> |<span data-ttu-id="4c326-157">4</span><span class="sxs-lookup"><span data-stu-id="4c326-157">4</span></span> |
| <span data-ttu-id="4c326-158">20150601</span><span class="sxs-lookup"><span data-stu-id="4c326-158">20150601</span></span> |<span data-ttu-id="4c326-159">2</span><span class="sxs-lookup"><span data-stu-id="4c326-159">2</span></span> |<span data-ttu-id="4c326-160">4</span><span class="sxs-lookup"><span data-stu-id="4c326-160">4</span></span> |
| <span data-ttu-id="4c326-161">20150701</span><span class="sxs-lookup"><span data-stu-id="4c326-161">20150701</span></span> |<span data-ttu-id="4c326-162">3</span><span class="sxs-lookup"><span data-stu-id="4c326-162">3</span></span> |<span data-ttu-id="4c326-163">1</span><span class="sxs-lookup"><span data-stu-id="4c326-163">1</span></span> |
| <span data-ttu-id="4c326-164">20150801</span><span class="sxs-lookup"><span data-stu-id="4c326-164">20150801</span></span> |<span data-ttu-id="4c326-165">3</span><span class="sxs-lookup"><span data-stu-id="4c326-165">3</span></span> |<span data-ttu-id="4c326-166">1</span><span class="sxs-lookup"><span data-stu-id="4c326-166">1</span></span> |
| <span data-ttu-id="4c326-167">20150801</span><span class="sxs-lookup"><span data-stu-id="4c326-167">20150801</span></span> |<span data-ttu-id="4c326-168">3</span><span class="sxs-lookup"><span data-stu-id="4c326-168">3</span></span> |<span data-ttu-id="4c326-169">1</span><span class="sxs-lookup"><span data-stu-id="4c326-169">1</span></span> |
| <span data-ttu-id="4c326-170">20151001</span><span class="sxs-lookup"><span data-stu-id="4c326-170">20151001</span></span> |<span data-ttu-id="4c326-171">4</span><span class="sxs-lookup"><span data-stu-id="4c326-171">4</span></span> |<span data-ttu-id="4c326-172">2</span><span class="sxs-lookup"><span data-stu-id="4c326-172">2</span></span> |
| <span data-ttu-id="4c326-173">20151101</span><span class="sxs-lookup"><span data-stu-id="4c326-173">20151101</span></span> |<span data-ttu-id="4c326-174">4</span><span class="sxs-lookup"><span data-stu-id="4c326-174">4</span></span> |<span data-ttu-id="4c326-175">2</span><span class="sxs-lookup"><span data-stu-id="4c326-175">2</span></span> |
| <span data-ttu-id="4c326-176">20151201</span><span class="sxs-lookup"><span data-stu-id="4c326-176">20151201</span></span> |<span data-ttu-id="4c326-177">4</span><span class="sxs-lookup"><span data-stu-id="4c326-177">4</span></span> |<span data-ttu-id="4c326-178">2</span><span class="sxs-lookup"><span data-stu-id="4c326-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="4c326-179">Passo 4: criar Estatísticas nos dados recentemente carregados</span><span class="sxs-lookup"><span data-stu-id="4c326-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="4c326-180">O Azure SQL Data Warehouse ainda não suporta a criação ou atualização automática de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="4c326-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="4c326-181">Na ordem tooget Olá melhor desempenho das consultas, é importante que sejam criadas estatísticas em todas as colunas de todas as tabelas após o primeiro carregamento de Olá ou ocorrerem quaisquer alterações substanciais nos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="4c326-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="4c326-182">Para obter uma explicação detalhada das estatísticas, consulte Olá [estatísticas] [ Statistics] tópico, no grupo de tópicos desenvolver de Olá.</span><span class="sxs-lookup"><span data-stu-id="4c326-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="4c326-183">Segue-se um breve exemplo de como estatísticas toocreate Olá tabela carregada neste exemplo</span><span class="sxs-lookup"><span data-stu-id="4c326-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="4c326-184">Execute Olá seguintes instruções CREATE STATISTICS de uma linha de comandos sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="4c326-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="4c326-185">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4c326-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="4c326-186">Neste tutorial, irá criar um ficheiro de dados a partir de uma tabela do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4c326-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="4c326-187">Vamos exportar os dados de Olá que criámos acima tooa novo ficheiro de dados denominado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="4c326-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="4c326-188">Passo 1: Exportar dados de Olá</span><span class="sxs-lookup"><span data-stu-id="4c326-188">Step 1: Export hello data</span></span>
<span data-ttu-id="4c326-189">Utilizar o utilitário bcp de Olá, pode ligar e exportar dados com Olá os seguintes valores de substituição Olá comando conforme adequado:</span><span class="sxs-lookup"><span data-stu-id="4c326-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="4c326-190">Pode verificar Olá dados foram exportados corretamente ao abrir Olá novo ficheiro.</span><span class="sxs-lookup"><span data-stu-id="4c326-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="4c326-191">dados de Olá no ficheiro de Olá devem corresponder ao texto Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="4c326-191">hello data in hello file should match hello text below:</span></span>

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

> [!NOTE]
> <span data-ttu-id="4c326-192">Toohello natureza dos sistemas distribuídos, devido a ordem dos dados Olá não pode ser Olá mesmo em bases de dados do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c326-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="4c326-193">Outra opção consiste toouse Olá **queryout** função do bcp toowrite uma consulta extrair em vez de exportar a tabela inteira Olá.</span><span class="sxs-lookup"><span data-stu-id="4c326-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4c326-194">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4c326-194">Next steps</span></span>
<span data-ttu-id="4c326-195">Para obter uma descrição geral do carregamento, veja [Load data into SQL Data Warehouse (Carregar dados para o SQL Data Warehouse)][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4c326-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="4c326-196">Para obter mais sugestões de desenvolvimento, veja [SQL Data Warehouse development overview (Descrição geral do desenvolvimento no SQL Data Warehouse)][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="4c326-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
