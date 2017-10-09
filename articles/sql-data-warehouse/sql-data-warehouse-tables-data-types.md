---
title: "aaaData de tipos de orientação - Azure SQL Data Warehouse | Microsoft Docs"
description: "Recomendações de tipos de dados de toodefine que são compatíveis com o SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="10ede-103">Orientações para definir os tipos de dados para tabelas no armazém de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="10ede-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="10ede-104">Utilize estas recomendações toodefine tabela os tipos de dados que são compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="10ede-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="10ede-105">Além disso toocompatibility, minimizando o tamanho de Olá dos tipos de dados melhora o desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="10ede-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="10ede-106">Armazém de dados SQL suporta tipos de dados de Olá normalmente utilizada.</span><span class="sxs-lookup"><span data-stu-id="10ede-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="10ede-107">Para obter uma lista dos tipos de dados de Olá suportado, consulte [tipos de dados](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) no Olá instrução CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="10ede-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="10ede-108">Minimizar o comprimento de linha</span><span class="sxs-lookup"><span data-stu-id="10ede-108">Minimize row length</span></span>
<span data-ttu-id="10ede-109">Minimizar o tamanho de Olá dos tipos de dados reduz o comprimento de linha Olá, o que conduz toobetter desempenho das consultas.</span><span class="sxs-lookup"><span data-stu-id="10ede-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="10ede-110">Utilize Olá menor tipo de dados que funciona para os seus dados.</span><span class="sxs-lookup"><span data-stu-id="10ede-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="10ede-111">Evite definir colunas de carateres com um comprimento grande predefinido.</span><span class="sxs-lookup"><span data-stu-id="10ede-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="10ede-112">Por exemplo, se o valor mais longo Olá é de 25 carateres, em seguida, defina a coluna como VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="10ede-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="10ede-113">Evite utilizar [NVARCHAR] [ NVARCHAR] quando apenas precisam VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="10ede-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="10ede-114">Sempre que possível, utilize NVARCHAR(4000) ou VARCHAR(8000) em vez de nvarchar (Max) ou varchar (Max).</span><span class="sxs-lookup"><span data-stu-id="10ede-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="10ede-115">Se estiver a utilizar o Polybase tooload as tabelas, Olá definido da linha da tabela de Olá não pode exceder 1 MB.</span><span class="sxs-lookup"><span data-stu-id="10ede-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="10ede-116">Quando uma linha com dados de comprimento variável excede 1 MB, pode carregar linha Olá com o BCP, mas não com o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="10ede-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="10ede-117">Identificar os tipos de dados não suportado</span><span class="sxs-lookup"><span data-stu-id="10ede-117">Identify unsupported data types</span></span>
<span data-ttu-id="10ede-118">Se estiver a migrar a base de dados de outra base de dados do SQL Server, poderá encontrar os tipos de dados que não são suportados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="10ede-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="10ede-119">Utilize esta consulta toodiscover não suportada os tipos de dados no seu esquema de SQL Server existente.</span><span class="sxs-lookup"><span data-stu-id="10ede-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="10ede-120"><a name="unsupported-data-types"></a>Utilizar soluções para os tipos de dados não suportado</span><span class="sxs-lookup"><span data-stu-id="10ede-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="10ede-121">Olá lista seguinte mostra Olá tipos de dados que não suporta o SQL Data Warehouse e fornecem alternativas que pode utilizar em vez de Olá não suportado tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="10ede-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="10ede-122">Tipo de dados não suportado</span><span class="sxs-lookup"><span data-stu-id="10ede-122">Unsupported data type</span></span> | <span data-ttu-id="10ede-123">Solução</span><span class="sxs-lookup"><span data-stu-id="10ede-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="10ede-124">[geometria][geometry]</span><span class="sxs-lookup"><span data-stu-id="10ede-124">[geometry][geometry]</span></span> |<span data-ttu-id="10ede-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="10ede-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="10ede-126">[Geografia][geography]</span><span class="sxs-lookup"><span data-stu-id="10ede-126">[geography][geography]</span></span> |<span data-ttu-id="10ede-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="10ede-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="10ede-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="10ede-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="10ede-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="10ede-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="10ede-130">[imagem][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="10ede-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="10ede-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="10ede-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="10ede-132">[texto][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="10ede-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="10ede-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="10ede-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="10ede-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="10ede-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="10ede-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="10ede-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="10ede-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="10ede-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="10ede-137">Dividir coluna em várias colunas de tipo seguro.</span><span class="sxs-lookup"><span data-stu-id="10ede-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="10ede-138">[tabela][table]</span><span class="sxs-lookup"><span data-stu-id="10ede-138">[table][table]</span></span> |<span data-ttu-id="10ede-139">Converta tootemporary tabelas.</span><span class="sxs-lookup"><span data-stu-id="10ede-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="10ede-140">[Timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="10ede-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="10ede-141">Rework código toouse [datetime2] [ datetime2] e `CURRENT_TIMESTAMP` função.</span><span class="sxs-lookup"><span data-stu-id="10ede-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="10ede-142">São suportadas constantes apenas como predefinições de fábrica, por conseguinte current_timestamp não pode ser definida como uma restrição default.</span><span class="sxs-lookup"><span data-stu-id="10ede-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="10ede-143">Se precisar de toomigrate valores da versão de linha de uma coluna com tipo timestamp, em seguida, utilize [binário][BINARY](8) ou [VARBINARY][BINARY](8) para não nulo ou Valores da versão de linha nulo.</span><span class="sxs-lookup"><span data-stu-id="10ede-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="10ede-144">[XML][xml]</span><span class="sxs-lookup"><span data-stu-id="10ede-144">[xml][xml]</span></span> |<span data-ttu-id="10ede-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="10ede-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="10ede-146">[tipo definido pelo utilizador][user defined types]</span><span class="sxs-lookup"><span data-stu-id="10ede-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="10ede-147">Converta o tipo de dados nativos de back-toohello sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="10ede-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="10ede-148">valores predefinidos</span><span class="sxs-lookup"><span data-stu-id="10ede-148">default values</span></span> | <span data-ttu-id="10ede-149">Os valores predefinidos suportam literais e constantes apenas.</span><span class="sxs-lookup"><span data-stu-id="10ede-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="10ede-150">As expressões não determinística ou funções, tais como `GETDATE()` ou `CURRENT_TIMESTAMP`, não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="10ede-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="10ede-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="10ede-151">Next steps</span></span>
<span data-ttu-id="10ede-152">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="10ede-152">toolearn more, see:</span></span>

- <span data-ttu-id="10ede-153">[Melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="10ede-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="10ede-154">[Descrição geral da tabela][Overview]</span><span class="sxs-lookup"><span data-stu-id="10ede-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="10ede-155">[Distribuição de uma tabela][Distribute]</span><span class="sxs-lookup"><span data-stu-id="10ede-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="10ede-156">[A indexação de uma tabela][Index]</span><span class="sxs-lookup"><span data-stu-id="10ede-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="10ede-157">[Uma tabela de criação de partições][Partition]</span><span class="sxs-lookup"><span data-stu-id="10ede-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="10ede-158">[Manter as estatísticas da tabela][Statistics]</span><span class="sxs-lookup"><span data-stu-id="10ede-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="10ede-159">[Tabelas temporárias][Temporary]</span><span class="sxs-lookup"><span data-stu-id="10ede-159">[Temporary Tables][Temporary]</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
