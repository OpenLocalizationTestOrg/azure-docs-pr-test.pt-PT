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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="56520-104">Gerir a capacidade de computação no armazém de dados do Azure SQL (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="56520-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56520-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="56520-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="56520-106">Portal</span><span class="sxs-lookup"><span data-stu-id="56520-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="56520-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56520-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="56520-108">REST</span><span class="sxs-lookup"><span data-stu-id="56520-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="56520-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="56520-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="56520-110">Ver definições de DWU atuais</span><span class="sxs-lookup"><span data-stu-id="56520-110">View current DWU settings</span></span>
<span data-ttu-id="56520-111">tooview Olá atuais DWU definições para as bases de dados:</span><span class="sxs-lookup"><span data-stu-id="56520-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="56520-112">Abra o SQL Server Object Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="56520-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="56520-113">Ligar toohello principal da base de dados associada ao servidor de base de dados SQL lógico Olá.</span><span class="sxs-lookup"><span data-stu-id="56520-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="56520-114">Selecione a partir da vista de gestão dinâmica do Olá sys.database_service_objectives.</span><span class="sxs-lookup"><span data-stu-id="56520-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="56520-115">Segue-se um exemplo:</span><span class="sxs-lookup"><span data-stu-id="56520-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="56520-116">Dimensionar a computação</span><span class="sxs-lookup"><span data-stu-id="56520-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="56520-117">Olá toochange DWUs:</span><span class="sxs-lookup"><span data-stu-id="56520-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="56520-118">Ligar toohello principal da base de dados associada ao servidor lógico da base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="56520-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="56520-119">Olá utilize [ALTER DATABASE] [ ALTER DATABASE] instrução TSQL.</span><span class="sxs-lookup"><span data-stu-id="56520-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="56520-120">Olá exemplo a seguir define Olá serviço nível tooDW1000, objetivo, da base de dados Olá MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="56520-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="56520-121">Verificar progresso de estado e a operação de base de dados</span><span class="sxs-lookup"><span data-stu-id="56520-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="56520-122">Ligar toohello principal da base de dados associada ao servidor lógico da base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="56520-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="56520-123">Submeter o estado da base de dados da consulta toocheck</span><span class="sxs-lookup"><span data-stu-id="56520-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="56520-124">Consultar o estado de toocheck da operação de envio</span><span class="sxs-lookup"><span data-stu-id="56520-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="56520-125">Este DMV irá devolver informações sobre as várias operações de gestão no SQL Data Warehouse, tais como o estado de funcionamento e Olá de Olá da operação de Olá, que irá ser IN_PROGRESS ou foi concluída.</span><span class="sxs-lookup"><span data-stu-id="56520-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="56520-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="56520-126">Next steps</span></span>
<span data-ttu-id="56520-127">Para outras tarefas de gestão, consulte [descrição geral da gestão][Management overview].</span><span class="sxs-lookup"><span data-stu-id="56520-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
