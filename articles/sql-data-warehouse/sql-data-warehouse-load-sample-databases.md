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
# <a name="load-sample-data-into-sql-data-warehouse"></a>Carregar dados de exemplo para o SQL Data Warehouse
Siga estes tooload passos simples e a base de dados de exemplo do Adventure Works de Olá de consulta. Estes scripts primeiro utilizam o sqlcmd toorun SQL que irá criar tabelas e vistas. Depois de criar tabelas, scripts de Olá irão utilizar dados de tooload bcp.  Se ainda não tiver sqlcmd e bcp instalado, siga estas ligações demasiado[instalar bcp] [ install bcp] e demasiado[instalar sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Carregar dados de exemplo
1. Transferir Olá [Scripts de exemplo Adventure Works para SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] ficheiro zip.
2. Extraia os ficheiros de Olá do diretório de tooa zip transferido na sua máquina local.
3. Editar Olá extraído ficheiro aw_create.bat e defina Olá seguir encontradas, Olá parte superior do ficheiro de Olá variáveis.  Ser tooleave se de que não são espaços em branco entre Olá "=" e o parâmetro de Olá.  Seguem-se exemplos de como poderão ver as suas edições.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. A partir de uma linha de comandos do Windows, execute aw_create.bat Olá editá-lo.  Lembre-se de que estão no diretório de olá onde guardou a versão de aw_create.bat editada.
   Este script será...
   
   * Remover Adventure Works tabelas ou vistas que já existem na base de dados
   * Criar Olá Adventure Works tabelas e vistas
   * Carregar a tabela cada Adventure Works com o bcp
   * Validar Olá contagens de linha para cada tabela Adventure Works
   * Recolher estatísticas em cada coluna para cada tabela Adventure Works

## <a name="query-sample-data"></a>Dados de exemplo de consulta
Assim que tiver carregar alguns dados de exemplo para o SQL Data Warehouse, pode rapidamente executar algumas consultas.  toorun uma consulta, ligar a base de dados do Adventure Works tooyour recentemente criado no armazém de dados do SQL do Azure utilizando o Visual Studio e SSDT, conforme descrito em Olá [consulta com o Visual Studio] [ query with Visual Studio] documento.

Exemplo de simples selecione instrução tooget todas as informações de Olá de funcionários Olá:

```sql
SELECT * FROM DimEmployee;
```

Exemplo de uma consulta mais complexa utilizando construções como toolook GROUP BY na quantidade total de Olá para todas as vendas em cada dia:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Exemplo de um SELECIONE com um toofilter de cláusula WHERE saída encomendas a partir de antes de uma determinada data:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Armazém de dados SQL suporta quase todas as construções de T-SQL que suporta o SQL Server.  Todas as diferenças estão documentadas na nossa [migre código] [ migrate code] documentação.

## <a name="next-steps"></a>Passos seguintes
Agora que já teve um tootry hipótese algumas consultas com dados de exemplo, verificar como demasiado[desenvolver][develop], [carregar][load], ou [ migrar] [ migrate] tooSQL do armazém de dados.

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
