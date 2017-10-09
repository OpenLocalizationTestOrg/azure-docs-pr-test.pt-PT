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
# <a name="load-data-with-bcp"></a>Carregar dados com o bcp
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[BCP] [ bcp]**  é um utilitário de carregamento em massa da linha de comandos que lhe permite toocopy dados entre o SQL Server, ficheiros de dados e do armazém de dados do SQL Server. Utilize o bcp tooimport grandes quantidades de linhas em tabelas de SQL do armazém de dados ou dados tooexport tabelas do SQL Server para ficheiros de dados. Exceto quando utilizado com a opção de queryout Olá, bcp necessita de nenhum conhecimento de Transact-SQL.

o BCP é uma forma rápida e fácil toomove conjuntos de dados menores dentro e fora de uma base de dados do armazém de dados do SQL Server. quantidade exata de Olá de dados que são recomendadas tooload/extração através do bcp dependerá de rede ligação toohello Datacenter do Azure.  Geralmente, as tabelas de dimensões podem ser prontamente carregadas e extraídas com o bcp. No entanto, não é recomendada a utilização do bcp para carregar ou extrair grandes volumes de dados.  O Polybase é Olá recomendado ferramenta para carregar e extrair grandes volumes de dados como uma tarefa melhor tirar partido da arquitetura de processamento paralelo em grande escala de Olá do SQL Data Warehouse.

O bcp permite:

* Utilize um utilitário de linha de comandos simples tooload de dados para o SQL Data Warehouse.
* Utilize dados de tooextract um utilitário de linha de comandos simples do SQL Data Warehouse.

Este tutorial irá mostrar-lhe como:

* Importar dados para uma tabela com o bcp de Olá no comando
* Exportar dados de um tabela uisng Olá de saída do bcp comando

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toostep com este tutorial, precisa de:

* Uma base de dados SQL Data Warehouse
* Olá linha de comandos instalado o utilitário bcp
* Olá utilitário de linha de comandos SQLCMD instalado

> [!NOTE]
> Pode transferir os utilitários bcp e sqlcmd a Olá de Olá [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Importar dados para o SQL Data Warehouse
Neste tutorial, irá criar uma tabela no Azure SQL Data Warehouse e importar dados para a tabela de Olá.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Passo 1: criar uma tabela no Azure SQL Data Warehouse
A partir de uma linha de comandos, utilize o sqlcmd toorun Olá toocreate consulta uma tabela a seguir na sua instância:

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
> Consulte [descrição geral da tabela] [ Table Overview] ou [sintaxe CREATE TABLE] [ CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e Olá  opções disponíveis na cláusula WITH de Olá.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Passo 2: criar um ficheiro de dados de origem
Abra o bloco de notas e copie Olá seguintes linhas de dados para um novo ficheiro de texto e, em seguida, guarde este ficheiro tooyour diretório temporário local, c:\temp\dimdate2.txt..

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
> É importante tooremember que bcp.exe não suporta a codificação de ficheiro Olá UTF-8. Utilize ficheiros ASCII ou ficheiros codificados com UTF-16 ao utilizar bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Passo 3: Ligar e importar dados de Olá
Utilizar o bcp, pode ligar e importar dados de Olá utilizando Olá os seguintes valores de substituição Olá comando conforme adequado:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Pode verificar Olá dados foram carregados, executando Olá seguinte consulta com o sqlcmd:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Isto deverá devolver Olá os seguintes resultados:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Passo 4: criar Estatísticas nos dados recentemente carregados
O Azure SQL Data Warehouse ainda não suporta a criação ou atualização automática de estatísticas. Na ordem tooget Olá melhor desempenho das consultas, é importante que sejam criadas estatísticas em todas as colunas de todas as tabelas após o primeiro carregamento de Olá ou ocorrerem quaisquer alterações substanciais nos dados de Olá. Para obter uma explicação detalhada das estatísticas, consulte Olá [estatísticas] [ Statistics] tópico, no grupo de tópicos desenvolver de Olá. Segue-se um breve exemplo de como estatísticas toocreate Olá tabela carregada neste exemplo

Execute Olá seguintes instruções CREATE STATISTICS de uma linha de comandos sqlcmd:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Exportar dados do SQL Data Warehouse
Neste tutorial, irá criar um ficheiro de dados a partir de uma tabela do SQL Data Warehouse. Vamos exportar os dados de Olá que criámos acima tooa novo ficheiro de dados denominado DimDate2_export.txt.

### <a name="step-1-export-hello-data"></a>Passo 1: Exportar dados de Olá
Utilizar o utilitário bcp de Olá, pode ligar e exportar dados com Olá os seguintes valores de substituição Olá comando conforme adequado:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Pode verificar Olá dados foram exportados corretamente ao abrir Olá novo ficheiro. dados de Olá no ficheiro de Olá devem corresponder ao texto Olá abaixo:

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
> Toohello natureza dos sistemas distribuídos, devido a ordem dos dados Olá não pode ser Olá mesmo em bases de dados do armazém de dados do SQL Server. Outra opção consiste toouse Olá **queryout** função do bcp toowrite uma consulta extrair em vez de exportar a tabela inteira Olá.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Para obter uma descrição geral do carregamento, veja [Load data into SQL Data Warehouse (Carregar dados para o SQL Data Warehouse)][Load data into SQL Data Warehouse].
Para obter mais sugestões de desenvolvimento, veja [SQL Data Warehouse development overview (Descrição geral do desenvolvimento no SQL Data Warehouse)][SQL Data Warehouse development overview].

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
