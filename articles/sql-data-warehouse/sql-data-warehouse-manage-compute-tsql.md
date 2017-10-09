---
title: aaaPause, retomar, dimensionem com T-SQL no Azure SQL Data Warehouse | Microsoft Docs
description: Desempenho de tooscale Escalamento de tarefas de Transact-SQL (T-SQL) ao ajustar as DWUs. Reduzir os custos ao aumentar durante o pico.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Gerir a capacidade de computação no armazém de dados do Azure SQL (T-SQL)
> [!div class="op_single_selector"]
> * [Descrição geral](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Ver definições de DWU atuais
tooview Olá atuais DWU definições para as bases de dados:

1. Abra o SQL Server Object Explorer no Visual Studio.
2. Ligar toohello principal da base de dados associada ao servidor de base de dados SQL lógico Olá.
3. Selecione a partir da vista de gestão dinâmica do Olá sys.database_service_objectives. Segue-se um exemplo: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Dimensionar a computação
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Olá toochange DWUs:

1. Ligar toohello principal da base de dados associada ao servidor lógico da base de dados do SQL Server.
2. Olá utilize [ALTER DATABASE] [ ALTER DATABASE] instrução TSQL. Olá exemplo a seguir define Olá serviço nível tooDW1000, objetivo, da base de dados Olá MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Verificar progresso de estado e a operação de base de dados

1. Ligar toohello principal da base de dados associada ao servidor lógico da base de dados do SQL Server.
2. Submeter o estado da base de dados da consulta toocheck

```sql
SELECT *
FROM
sys.databases
```

3. Consultar o estado de toocheck da operação de envio

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Este DMV irá devolver informações sobre as várias operações de gestão no SQL Data Warehouse, tais como o estado de funcionamento e Olá de Olá da operação de Olá, que irá ser IN_PROGRESS ou foi concluída.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Passos seguintes
Para outras tarefas de gestão, consulte [descrição geral da gestão][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
