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
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a>Orientações para definir os tipos de dados para tabelas no armazém de dados do SQL Server
Utilize estas recomendações toodefine tabela os tipos de dados que são compatíveis com o SQL Data Warehouse. Além disso toocompatibility, minimizando o tamanho de Olá dos tipos de dados melhora o desempenho de consulta.

Armazém de dados SQL suporta tipos de dados de Olá normalmente utilizada. Para obter uma lista dos tipos de dados de Olá suportado, consulte [tipos de dados](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) no Olá instrução CREATE TABLE. 


## <a name="minimize-row-length"></a>Minimizar o comprimento de linha
Minimizar o tamanho de Olá dos tipos de dados reduz o comprimento de linha Olá, o que conduz toobetter desempenho das consultas. Utilize Olá menor tipo de dados que funciona para os seus dados. 

- Evite definir colunas de carateres com um comprimento grande predefinido. Por exemplo, se o valor mais longo Olá é de 25 carateres, em seguida, defina a coluna como VARCHAR(25). 
- Evite utilizar [NVARCHAR] [ NVARCHAR] quando apenas precisam VARCHAR.
- Sempre que possível, utilize NVARCHAR(4000) ou VARCHAR(8000) em vez de nvarchar (Max) ou varchar (Max).

Se estiver a utilizar o Polybase tooload as tabelas, Olá definido da linha da tabela de Olá não pode exceder 1 MB. Quando uma linha com dados de comprimento variável excede 1 MB, pode carregar linha Olá com o BCP, mas não com o PolyBase.

## <a name="identify-unsupported-data-types"></a>Identificar os tipos de dados não suportado
Se estiver a migrar a base de dados de outra base de dados do SQL Server, poderá encontrar os tipos de dados que não são suportados no SQL Data Warehouse. Utilize esta consulta toodiscover não suportada os tipos de dados no seu esquema de SQL Server existente.

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a>Utilizar soluções para os tipos de dados não suportado

Olá lista seguinte mostra Olá tipos de dados que não suporta o SQL Data Warehouse e fornecem alternativas que pode utilizar em vez de Olá não suportado tipos de dados.

| Tipo de dados não suportado | Solução |
| --- | --- |
| [geometria][geometry] |[varbinary][varbinary] |
| [Geografia][geography] |[varbinary][varbinary] |
| [hierarchyid][hierarchyid] |[nvarchar][nvarchar](4000) |
| [imagem][ntext,text,image] |[varbinary][varbinary] |
| [texto][ntext,text,image] |[varchar][varchar] |
| [ntext][ntext,text,image] |[nvarchar][nvarchar] |
| [sql_variant][sql_variant] |Dividir coluna em várias colunas de tipo seguro. |
| [tabela][table] |Converta tootemporary tabelas. |
| [Timestamp][timestamp] |Rework código toouse [datetime2] [ datetime2] e `CURRENT_TIMESTAMP` função.  São suportadas constantes apenas como predefinições de fábrica, por conseguinte current_timestamp não pode ser definida como uma restrição default. Se precisar de toomigrate valores da versão de linha de uma coluna com tipo timestamp, em seguida, utilize [binário][BINARY](8) ou [VARBINARY][BINARY](8) para não nulo ou Valores da versão de linha nulo. |
| [XML][xml] |[varchar][varchar] |
| [tipo definido pelo utilizador][user defined types] |Converta o tipo de dados nativos de back-toohello sempre que possível. |
| valores predefinidos | Os valores predefinidos suportam literais e constantes apenas.  As expressões não determinística ou funções, tais como `GETDATE()` ou `CURRENT_TIMESTAMP`, não são suportadas. |


## <a name="next-steps"></a>Passos seguintes
toolearn mais, consulte:

- [Melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices]
- [Descrição geral da tabela][Overview]
- [Distribuição de uma tabela][Distribute]
- [A indexação de uma tabela][Index]
- [Uma tabela de criação de partições][Partition]
- [Manter as estatísticas da tabela][Statistics]
- [Tabelas temporárias][Temporary]

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
