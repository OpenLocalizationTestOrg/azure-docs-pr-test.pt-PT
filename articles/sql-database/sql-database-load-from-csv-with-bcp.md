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
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Carregar dados de ficheiros CSV para a Base de Dados SQL do Azure (ficheiros simples)
Pode utilizar dados de tooimport Olá bcp utilitário da linha de comandos de um ficheiro CSV numa SQL Database do Azure.

## <a name="before-you-begin"></a>Antes de começar
### <a name="prerequisites"></a>Pré-requisitos
Olá toocomplete os passos neste artigo, tem de:

* Uma base de dados e um servidor lógico da Base de Dados SQL do Azure
* Olá da linha de comandos instalado o utilitário bcp
* Olá da linha de comandos instalado o utilitário sqlcmd

Pode transferir os utilitários bcp e sqlcmd a Olá de Olá [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dados no formato ASCII ou UTF-16
Se estiver a tentar este tutorial com os seus dados, estes têm de toouse Olá ASCII ou UTF-16 codificação, uma vez que o bcp não suporta UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Criar uma tabela de destino
Defina uma tabela na base de dados do SQL Server como tabela de destino Olá. Olá as colunas na tabela de Olá têm de corresponder dados toohello em cada linha do seu ficheiro de dados.

toocreate uma tabela, abra uma linha de comandos e utilize sqlcmd.exe toorun Olá os seguintes comandos:

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


## <a name="2-create-a-source-data-file"></a>2. Criar um ficheiro de dados de origem
Abra o bloco de notas e copie Olá seguintes linhas de dados para um novo ficheiro de texto e, em seguida, guarde este ficheiro tooyour diretório temporário local, c:\temp\dimdate2.txt.. Estes dados estão no formato ASCII.

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

(Opcional) tooexport os seus próprios dados da base de dados do SQL Server, abra uma linha de comandos e execute Olá os seguintes comandos. Substitua TableName, ServerName, DatabaseName, Username e Password pelas suas informações.

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Carregar dados de Olá
dados de Olá tooload, abra uma linha de comandos e execute Olá comando a seguir, substituindo os valores de Olá para o nome do servidor, nome da base de dados, nome de utilizador e palavra-passe pelas suas informações.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Utilize este Olá tooverify de comando dados foram carregados corretamente

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

resultados de Olá devem ter o seguinte aspeto:

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

## <a name="next-steps"></a>Passos seguintes
toomigrate uma base de dados do SQL Server, consulte [migração de base de dados do SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
