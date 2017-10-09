---
title: ficheiros de dados de aaaLoad do ficheiro CSV para a SQL Database do Azure (bcp) | Microsoft Docs
description: Para um tamanho de dados de pequena, utiliza o bcp tooimport dados na base de dados do Azure SQL.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="77759-103">Carregar dados de ficheiros CSV para a Base de Dados SQL do Azure (ficheiros simples)</span><span class="sxs-lookup"><span data-stu-id="77759-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="77759-104">Pode utilizar dados de tooimport Olá bcp utilitário da linha de comandos de um ficheiro CSV numa SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="77759-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="77759-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="77759-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="77759-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77759-106">Prerequisites</span></span>
<span data-ttu-id="77759-107">Olá toocomplete os passos neste artigo, tem de:</span><span class="sxs-lookup"><span data-stu-id="77759-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="77759-108">Uma base de dados e um servidor lógico da Base de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="77759-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="77759-109">Olá da linha de comandos instalado o utilitário bcp</span><span class="sxs-lookup"><span data-stu-id="77759-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="77759-110">Olá da linha de comandos instalado o utilitário sqlcmd</span><span class="sxs-lookup"><span data-stu-id="77759-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="77759-111">Pode transferir os utilitários bcp e sqlcmd a Olá de Olá [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="77759-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="77759-112">Dados no formato ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="77759-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="77759-113">Se estiver a tentar este tutorial com os seus dados, estes têm de toouse Olá ASCII ou UTF-16 codificação, uma vez que o bcp não suporta UTF-8.</span><span class="sxs-lookup"><span data-stu-id="77759-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="77759-114">1. Criar uma tabela de destino</span><span class="sxs-lookup"><span data-stu-id="77759-114">1. Create a destination table</span></span>
<span data-ttu-id="77759-115">Defina uma tabela na base de dados do SQL Server como tabela de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="77759-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="77759-116">Olá as colunas na tabela de Olá têm de corresponder dados toohello em cada linha do seu ficheiro de dados.</span><span class="sxs-lookup"><span data-stu-id="77759-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="77759-117">toocreate uma tabela, abra uma linha de comandos e utilize sqlcmd.exe toorun Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="77759-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="77759-118">2. Criar um ficheiro de dados de origem</span><span class="sxs-lookup"><span data-stu-id="77759-118">2. Create a source data file</span></span>
<span data-ttu-id="77759-119">Abra o bloco de notas e copie Olá seguintes linhas de dados para um novo ficheiro de texto e, em seguida, guarde este ficheiro tooyour diretório temporário local, c:\temp\dimdate2.txt..</span><span class="sxs-lookup"><span data-stu-id="77759-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="77759-120">Estes dados estão no formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="77759-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="77759-121">(Opcional) tooexport os seus próprios dados da base de dados do SQL Server, abra uma linha de comandos e execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="77759-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="77759-122">Substitua TableName, ServerName, DatabaseName, Username e Password pelas suas informações.</span><span class="sxs-lookup"><span data-stu-id="77759-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="77759-123">3. Carregar dados de Olá</span><span class="sxs-lookup"><span data-stu-id="77759-123">3. Load hello data</span></span>
<span data-ttu-id="77759-124">dados de Olá tooload, abra uma linha de comandos e execute Olá comando a seguir, substituindo os valores de Olá para o nome do servidor, nome da base de dados, nome de utilizador e palavra-passe pelas suas informações.</span><span class="sxs-lookup"><span data-stu-id="77759-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="77759-125">Utilize este Olá tooverify de comando dados foram carregados corretamente</span><span class="sxs-lookup"><span data-stu-id="77759-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="77759-126">resultados de Olá devem ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="77759-126">hello results should look like this:</span></span>

| <span data-ttu-id="77759-127">DateId</span><span class="sxs-lookup"><span data-stu-id="77759-127">DateId</span></span> | <span data-ttu-id="77759-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="77759-128">CalendarQuarter</span></span> | <span data-ttu-id="77759-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="77759-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77759-130">20150101</span><span class="sxs-lookup"><span data-stu-id="77759-130">20150101</span></span> |<span data-ttu-id="77759-131">1</span><span class="sxs-lookup"><span data-stu-id="77759-131">1</span></span> |<span data-ttu-id="77759-132">3</span><span class="sxs-lookup"><span data-stu-id="77759-132">3</span></span> |
| <span data-ttu-id="77759-133">20150201</span><span class="sxs-lookup"><span data-stu-id="77759-133">20150201</span></span> |<span data-ttu-id="77759-134">1</span><span class="sxs-lookup"><span data-stu-id="77759-134">1</span></span> |<span data-ttu-id="77759-135">3</span><span class="sxs-lookup"><span data-stu-id="77759-135">3</span></span> |
| <span data-ttu-id="77759-136">20150301</span><span class="sxs-lookup"><span data-stu-id="77759-136">20150301</span></span> |<span data-ttu-id="77759-137">1</span><span class="sxs-lookup"><span data-stu-id="77759-137">1</span></span> |<span data-ttu-id="77759-138">3</span><span class="sxs-lookup"><span data-stu-id="77759-138">3</span></span> |
| <span data-ttu-id="77759-139">20150401</span><span class="sxs-lookup"><span data-stu-id="77759-139">20150401</span></span> |<span data-ttu-id="77759-140">2</span><span class="sxs-lookup"><span data-stu-id="77759-140">2</span></span> |<span data-ttu-id="77759-141">4</span><span class="sxs-lookup"><span data-stu-id="77759-141">4</span></span> |
| <span data-ttu-id="77759-142">20150501</span><span class="sxs-lookup"><span data-stu-id="77759-142">20150501</span></span> |<span data-ttu-id="77759-143">2</span><span class="sxs-lookup"><span data-stu-id="77759-143">2</span></span> |<span data-ttu-id="77759-144">4</span><span class="sxs-lookup"><span data-stu-id="77759-144">4</span></span> |
| <span data-ttu-id="77759-145">20150601</span><span class="sxs-lookup"><span data-stu-id="77759-145">20150601</span></span> |<span data-ttu-id="77759-146">2</span><span class="sxs-lookup"><span data-stu-id="77759-146">2</span></span> |<span data-ttu-id="77759-147">4</span><span class="sxs-lookup"><span data-stu-id="77759-147">4</span></span> |
| <span data-ttu-id="77759-148">20150701</span><span class="sxs-lookup"><span data-stu-id="77759-148">20150701</span></span> |<span data-ttu-id="77759-149">3</span><span class="sxs-lookup"><span data-stu-id="77759-149">3</span></span> |<span data-ttu-id="77759-150">1</span><span class="sxs-lookup"><span data-stu-id="77759-150">1</span></span> |
| <span data-ttu-id="77759-151">20150801</span><span class="sxs-lookup"><span data-stu-id="77759-151">20150801</span></span> |<span data-ttu-id="77759-152">3</span><span class="sxs-lookup"><span data-stu-id="77759-152">3</span></span> |<span data-ttu-id="77759-153">1</span><span class="sxs-lookup"><span data-stu-id="77759-153">1</span></span> |
| <span data-ttu-id="77759-154">20150801</span><span class="sxs-lookup"><span data-stu-id="77759-154">20150801</span></span> |<span data-ttu-id="77759-155">3</span><span class="sxs-lookup"><span data-stu-id="77759-155">3</span></span> |<span data-ttu-id="77759-156">1</span><span class="sxs-lookup"><span data-stu-id="77759-156">1</span></span> |
| <span data-ttu-id="77759-157">20151001</span><span class="sxs-lookup"><span data-stu-id="77759-157">20151001</span></span> |<span data-ttu-id="77759-158">4</span><span class="sxs-lookup"><span data-stu-id="77759-158">4</span></span> |<span data-ttu-id="77759-159">2</span><span class="sxs-lookup"><span data-stu-id="77759-159">2</span></span> |
| <span data-ttu-id="77759-160">20151101</span><span class="sxs-lookup"><span data-stu-id="77759-160">20151101</span></span> |<span data-ttu-id="77759-161">4</span><span class="sxs-lookup"><span data-stu-id="77759-161">4</span></span> |<span data-ttu-id="77759-162">2</span><span class="sxs-lookup"><span data-stu-id="77759-162">2</span></span> |
| <span data-ttu-id="77759-163">20151201</span><span class="sxs-lookup"><span data-stu-id="77759-163">20151201</span></span> |<span data-ttu-id="77759-164">4</span><span class="sxs-lookup"><span data-stu-id="77759-164">4</span></span> |<span data-ttu-id="77759-165">2</span><span class="sxs-lookup"><span data-stu-id="77759-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77759-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="77759-166">Next steps</span></span>
<span data-ttu-id="77759-167">toomigrate uma base de dados do SQL Server, consulte [migração de base de dados do SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="77759-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
