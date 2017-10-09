---
title: dados de exemplo aaaLoad para o SQL Data Warehouse | Microsoft Docs
description: Carregar dados de exemplo para o SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="d352a-103">Carregar dados de exemplo para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d352a-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="d352a-104">Siga estes tooload passos simples e a base de dados de exemplo do Adventure Works de Olá de consulta.</span><span class="sxs-lookup"><span data-stu-id="d352a-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="d352a-105">Estes scripts primeiro utilizam o sqlcmd toorun SQL que irá criar tabelas e vistas.</span><span class="sxs-lookup"><span data-stu-id="d352a-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="d352a-106">Depois de criar tabelas, scripts de Olá irão utilizar dados de tooload bcp.</span><span class="sxs-lookup"><span data-stu-id="d352a-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="d352a-107">Se ainda não tiver sqlcmd e bcp instalado, siga estas ligações demasiado[instalar bcp] [ install bcp] e demasiado[instalar sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="d352a-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="d352a-108">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="d352a-108">Load sample data</span></span>
1. <span data-ttu-id="d352a-109">Transferir Olá [Scripts de exemplo Adventure Works para SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] ficheiro zip.</span><span class="sxs-lookup"><span data-stu-id="d352a-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="d352a-110">Extraia os ficheiros de Olá do diretório de tooa zip transferido na sua máquina local.</span><span class="sxs-lookup"><span data-stu-id="d352a-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="d352a-111">Editar Olá extraído ficheiro aw_create.bat e defina Olá seguir encontradas, Olá parte superior do ficheiro de Olá variáveis.</span><span class="sxs-lookup"><span data-stu-id="d352a-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="d352a-112">Ser tooleave se de que não são espaços em branco entre Olá "=" e o parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d352a-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="d352a-113">Seguem-se exemplos de como poderão ver as suas edições.</span><span class="sxs-lookup"><span data-stu-id="d352a-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="d352a-114">A partir de uma linha de comandos do Windows, execute aw_create.bat Olá editá-lo.</span><span class="sxs-lookup"><span data-stu-id="d352a-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="d352a-115">Lembre-se de que estão no diretório de olá onde guardou a versão de aw_create.bat editada.</span><span class="sxs-lookup"><span data-stu-id="d352a-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="d352a-116">Este script será...</span><span class="sxs-lookup"><span data-stu-id="d352a-116">This script will...</span></span>
   
   * <span data-ttu-id="d352a-117">Remover Adventure Works tabelas ou vistas que já existem na base de dados</span><span class="sxs-lookup"><span data-stu-id="d352a-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="d352a-118">Criar Olá Adventure Works tabelas e vistas</span><span class="sxs-lookup"><span data-stu-id="d352a-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="d352a-119">Carregar a tabela cada Adventure Works com o bcp</span><span class="sxs-lookup"><span data-stu-id="d352a-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="d352a-120">Validar Olá contagens de linha para cada tabela Adventure Works</span><span class="sxs-lookup"><span data-stu-id="d352a-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="d352a-121">Recolher estatísticas em cada coluna para cada tabela Adventure Works</span><span class="sxs-lookup"><span data-stu-id="d352a-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="d352a-122">Dados de exemplo de consulta</span><span class="sxs-lookup"><span data-stu-id="d352a-122">Query sample data</span></span>
<span data-ttu-id="d352a-123">Assim que tiver carregar alguns dados de exemplo para o SQL Data Warehouse, pode rapidamente executar algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="d352a-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="d352a-124">toorun uma consulta, ligar a base de dados do Adventure Works tooyour recentemente criado no armazém de dados do SQL do Azure utilizando o Visual Studio e SSDT, conforme descrito em Olá [consulta com o Visual Studio] [ query with Visual Studio] documento.</span><span class="sxs-lookup"><span data-stu-id="d352a-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="d352a-125">Exemplo de simples selecione instrução tooget todas as informações de Olá de funcionários Olá:</span><span class="sxs-lookup"><span data-stu-id="d352a-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="d352a-126">Exemplo de uma consulta mais complexa utilizando construções como toolook GROUP BY na quantidade total de Olá para todas as vendas em cada dia:</span><span class="sxs-lookup"><span data-stu-id="d352a-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="d352a-127">Exemplo de um SELECIONE com um toofilter de cláusula WHERE saída encomendas a partir de antes de uma determinada data:</span><span class="sxs-lookup"><span data-stu-id="d352a-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="d352a-128">Armazém de dados SQL suporta quase todas as construções de T-SQL que suporta o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d352a-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="d352a-129">Todas as diferenças estão documentadas na nossa [migre código] [ migrate code] documentação.</span><span class="sxs-lookup"><span data-stu-id="d352a-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d352a-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d352a-130">Next steps</span></span>
<span data-ttu-id="d352a-131">Agora que já teve um tootry hipótese algumas consultas com dados de exemplo, verificar como demasiado[desenvolver][develop], [carregar][load], ou [ migrar] [ migrate] tooSQL do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="d352a-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
