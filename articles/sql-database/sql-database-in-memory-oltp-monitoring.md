---
title: "armazenamento de dentro da memória XTP aaaMonitor | Microsoft Docs"
description: "Monitor de armazenamento de dentro da memória XTP e estimativa utilizam, capacidade; Resolva o erro de capacidade 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="8b3f5-103">Monitorizar o Armazenamento OLTP Dentro da Memória</span><span class="sxs-lookup"><span data-stu-id="8b3f5-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="8b3f5-104">Quando utilizar [OLTP na memória](sql-database-in-memory.md), dados em tabelas com otimização de memória e variáveis de tabela residem no armazenamento do OLTP dentro da memória.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="8b3f5-105">Cada escalão de serviço Premium tem um tamanho de armazenamento de OLTP na memória máximo, o que é descrito da Olá [artigo escalões de serviço de base de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="8b3f5-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="8b3f5-106">Depois deste limite for excedido, insira e atualizar operações poderão começam a falhar (com o erro 41823).</span><span class="sxs-lookup"><span data-stu-id="8b3f5-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="8b3f5-107">Nesse momento será necessário tooeither eliminar dados tooreclaim de memória ou atualizar o escalão de desempenho de Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="8b3f5-108">Determinar se a dados se encaixa na extremidade de armazenamento em memória Olá</span><span class="sxs-lookup"><span data-stu-id="8b3f5-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="8b3f5-109">Determinar a extremidade de armazenamento Olá: consulte Olá [artigo escalões de serviço de base de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para caps de armazenamento Olá das camadas de serviços de Premium Olá diferentes.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="8b3f5-110">Estimar os requisitos para uma tabela com otimização de memória funciona Olá mesmo de memória de uma forma para o SQL Server faz na SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="8b3f5-111">Demorar alguns minutos tooreview nesse tópico [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b3f5-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="8b3f5-112">Tenha em atenção que a tabela de Olá e linhas de variável de tabela, bem como índices, contam para o tamanho de dados de utilizador máximo Olá.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="8b3f5-113">Além disso, ALTER TABLE tem suficiente toocreate sala de uma nova versão da tabela inteira Olá e seus índices.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="8b3f5-114">Monitorização e alertas</span><span class="sxs-lookup"><span data-stu-id="8b3f5-114">Monitoring and alerting</span></span>
<span data-ttu-id="8b3f5-115">Pode monitorizar a utilização de memória de armazenamento como uma percentagem do Olá [extremidade de armazenamento para o escalão de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) no Olá Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="8b3f5-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="8b3f5-116">No painel da base de dados de Olá, localize a caixa de utilização de recursos de Olá e clique em Editar.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="8b3f5-117">Em seguida, selecione a métrica de Olá `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="8b3f5-118">tooadd um alerta, clique em Olá utilização de recursos caixa tooopen Olá métrica painel, em seguida, clique em Adicionar alerta.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="8b3f5-119">Ou utilize a seguinte consulta tooshow Olá de memória a utilização do armazenamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="8b3f5-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="8b3f5-120">Corrija situações de memória esgotada - erro 41823</span><span class="sxs-lookup"><span data-stu-id="8b3f5-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="8b3f5-121">Resultados de execução-memória esgotada em operações de inserção, ATUALIZAÇÃO e criar a falhar com a mensagem de erro 41823.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="8b3f5-122">Mensagem de erro 41823 indica que as tabelas com otimização de memória de Olá e variáveis de tabela excedeu o tamanho máximo Olá.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="8b3f5-123">tooresolve este erro é:</span><span class="sxs-lookup"><span data-stu-id="8b3f5-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="8b3f5-124">Eliminar dados de tabelas com otimização de memória de Olá, potencialmente descarregar tootraditional de dados de Olá, com base em disco tabelas; ou,</span><span class="sxs-lookup"><span data-stu-id="8b3f5-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="8b3f5-125">Atualizar tooone de camada de serviço Olá com armazenamento suficiente na memória para os dados de Olá terá tookeep em tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="8b3f5-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b3f5-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8b3f5-126">Next steps</span></span>
<span data-ttu-id="8b3f5-127">Para monitorizar orientações, consulte [monitorização SQL Database do Azure utilizar as vistas de gestão dinâmica](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="8b3f5-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
