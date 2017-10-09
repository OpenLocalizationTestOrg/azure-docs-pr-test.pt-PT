---
title: grupos de aaaManage das bases de dados SQL do Azure | Microsoft Docs
description: "Percorrer a criação e gestão de uma tarefa elástica."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="d5a25-103">Criar e gerir expandido terminar as bases de dados de SQL do Azure utilizando as tarefas elásticas (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="d5a25-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="d5a25-104">**As tarefas de base de dados elásticas** simplificar a gestão de grupos de bases de dados ao executar operações administrativas como alterações de esquema, gestão de credenciais, as atualizações de dados de referência, recolha de dados de desempenho ou telemetria de inquilino (cliente) coleção.</span><span class="sxs-lookup"><span data-stu-id="d5a25-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="d5a25-105">As tarefas de base de dados elásticas está atualmente disponível através de Olá portal do Azure e os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5a25-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="d5a25-106">No entanto, Olá funcionalidade reduzida do Azure analisa portal limitada tooexecution em todas as bases de dados num [conjunto elástico (pré-visualização)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="d5a25-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="d5a25-107">conjunto de funcionalidades adicionais tooaccess e a execução de scripts entre um grupo de bases de dados, incluindo uma coleção personalizado ou um ID de partição horizontal (criado utilizando [biblioteca de clientes de base de dados elástica](sql-database-elastic-scale-introduction.md)), consulte [criar e gerir as tarefas através do PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d5a25-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="d5a25-108">Para obter mais informações sobre tarefas, consulte [descrição geral de tarefas de bases de dados elásticas](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5a25-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d5a25-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5a25-109">Prerequisites</span></span>
* <span data-ttu-id="d5a25-110">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5a25-110">An Azure subscription.</span></span> <span data-ttu-id="d5a25-111">Para uma versão de avaliação gratuita, consulte [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5a25-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d5a25-112">Um conjunto elástico.</span><span class="sxs-lookup"><span data-stu-id="d5a25-112">An elastic pool.</span></span> <span data-ttu-id="d5a25-113">Consulte [sobre conjuntos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="d5a25-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="d5a25-114">Instalação de componentes do serviço de tarefa de bases de dados elásticas.</span><span class="sxs-lookup"><span data-stu-id="d5a25-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="d5a25-115">Consulte [instalar o serviço de tarefas de bases de dados elásticas Olá](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="d5a25-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="d5a25-116">Criar tarefas</span><span class="sxs-lookup"><span data-stu-id="d5a25-116">Creating jobs</span></span>
1. <span data-ttu-id="d5a25-117">Utilizar Olá [portal do Azure](https://portal.azure.com), de um conjunto de trabalho de bases de dados elásticas existente, clique em **criar tarefa**.</span><span class="sxs-lookup"><span data-stu-id="d5a25-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="d5a25-118">Escreva Olá nome de utilizador e palavra-passe de administrador de bases de dados de Olá (criado durante a instalação de tarefas) para a base de dados de controlo de tarefas Olá (armazenamento de metadados para as tarefas).</span><span class="sxs-lookup"><span data-stu-id="d5a25-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Tarefa de Olá nome, escreva ou cole no código e clique em executar][1]
3. <span data-ttu-id="d5a25-120">No Olá **criar tarefa** painel, escreva um nome para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="d5a25-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="d5a25-121">Escreva Olá nome e palavra-passe tooconnect toohello destino bases de dados com permissões suficientes para toosucceed de execução do script.</span><span class="sxs-lookup"><span data-stu-id="d5a25-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="d5a25-122">Cole ou escreva no script de Olá T-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5a25-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="d5a25-123">Clique em **guardar** e, em seguida, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="d5a25-123">Click **Save** and then click **Run**.</span></span>
   
    ![Criar tarefas e executar][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="d5a25-125">Executar tarefas de idempotent</span><span class="sxs-lookup"><span data-stu-id="d5a25-125">Run idempotent jobs</span></span>
<span data-ttu-id="d5a25-126">Quando executar um script face a um conjunto de bases de dados, tem de ser se de que o script de Olá idempotent.</span><span class="sxs-lookup"><span data-stu-id="d5a25-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="d5a25-127">Ou seja, Olá script deve ser capaz de toorun várias vezes, mesmo que não conseguiu antes de um estado incompleto.</span><span class="sxs-lookup"><span data-stu-id="d5a25-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="d5a25-128">Por exemplo, um script falha, a tarefa de Olá será automaticamente repetida até ter êxito (dentro dos limites como tentativas de Olá lógica irá eventualmente cessar Olá repetir).</span><span class="sxs-lookup"><span data-stu-id="d5a25-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="d5a25-129">Olá forma toodo isto toouse Olá uma cláusula "Se existe" e eliminar qualquer instância encontrada antes de criar um novo objeto.</span><span class="sxs-lookup"><span data-stu-id="d5a25-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="d5a25-130">Um exemplo é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="d5a25-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="d5a25-131">Em alternativa, utilize uma cláusula "Se não existe" antes de criar uma nova instância:</span><span class="sxs-lookup"><span data-stu-id="d5a25-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="d5a25-132">Este script, em seguida, atualiza tabela Olá criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5a25-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="d5a25-133">A verificar o estado da tarefa</span><span class="sxs-lookup"><span data-stu-id="d5a25-133">Checking job status</span></span>
<span data-ttu-id="d5a25-134">Depois de uma tarefa foi iniciada, poder verificar o progresso da mesma.</span><span class="sxs-lookup"><span data-stu-id="d5a25-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="d5a25-135">Na página do conjunto elástico Olá, clique em **gerir tarefas**.</span><span class="sxs-lookup"><span data-stu-id="d5a25-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Clique em "Gerir tarefas"][2]
2. <span data-ttu-id="d5a25-137">Clique em Olá nome (a) de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="d5a25-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="d5a25-138">Olá **estado** pode ser "Concluída" ou "Falha".</span><span class="sxs-lookup"><span data-stu-id="d5a25-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="d5a25-139">Detalhes da tarefa de Olá aparecem (b) com a data e hora de criação e em execução.</span><span class="sxs-lookup"><span data-stu-id="d5a25-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="d5a25-140">lista de Olá (c) abaixo Olá que mostra o progresso de Olá de script de Olá em relação a cada base de dados no agrupamento de Olá, fornecer os detalhes de data e hora.</span><span class="sxs-lookup"><span data-stu-id="d5a25-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![A verificação de uma tarefa concluída][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="d5a25-142">A verificação de tarefas com falha</span><span class="sxs-lookup"><span data-stu-id="d5a25-142">Checking failed jobs</span></span>
<span data-ttu-id="d5a25-143">Se uma tarefa falhar, pode encontrar um registo sua execução.</span><span class="sxs-lookup"><span data-stu-id="d5a25-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="d5a25-144">Clique no nome de Olá de Olá falha na tarefa toosee os respetivos detalhes.</span><span class="sxs-lookup"><span data-stu-id="d5a25-144">Click hello name of hello failed job toosee its details.</span></span>

![Uma tarefa de verificação][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


