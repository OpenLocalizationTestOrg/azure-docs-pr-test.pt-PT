---
title: "aaaMigrate tooSQL sua solução do armazém de dados | Microsoft Docs"
description: "Orientações de migração para colocar a sua plataforma a solução tooAzure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="29f42-103">Migrar o tooAzure solução SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="29f42-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="29f42-104">Ver o que está envolvido num tooAzure de solução de base de dados do armazém de dados do SQL Server existente a migrar.</span><span class="sxs-lookup"><span data-stu-id="29f42-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="29f42-105">A carga de trabalho de perfil</span><span class="sxs-lookup"><span data-stu-id="29f42-105">Profile your workload</span></span>
<span data-ttu-id="29f42-106">Antes de migrar, quer toobe determinada que do armazém de dados do SQL Server é a solução certa do Olá para a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="29f42-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="29f42-107">SQL Data Warehouse é uma análise de tooperform sistema distribuída concebido dados de grandes dimensões.</span><span class="sxs-lookup"><span data-stu-id="29f42-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="29f42-108">Migrar tooSQL do armazém de dados requer algumas alterações de estrutura que não são demasiado difícil toounderstand mas poderão demorar algum tempo tooimplement.</span><span class="sxs-lookup"><span data-stu-id="29f42-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="29f42-109">Se a sua empresa precisar de um armazém de dados de classe empresarial, os benefícios de Olá merecem esforço Olá.</span><span class="sxs-lookup"><span data-stu-id="29f42-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="29f42-110">No entanto, se não precisa de energia Olá do SQL Data Warehouse, é mais económico toouse do SQL Server ou SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="29f42-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="29f42-111">Considere utilizar o SQL Data Warehouse quando tiver:</span><span class="sxs-lookup"><span data-stu-id="29f42-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="29f42-112">Ter um ou mais Terabytes de dados</span><span class="sxs-lookup"><span data-stu-id="29f42-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="29f42-113">Planear a análise de toorun em grandes quantidades de dados</span><span class="sxs-lookup"><span data-stu-id="29f42-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="29f42-114">Tem de Olá capacidade tooscale computação e armazenamento</span><span class="sxs-lookup"><span data-stu-id="29f42-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="29f42-115">Pretende que os custos de toosave por colocar em pausa recursos de computação quando não precisar deles.</span><span class="sxs-lookup"><span data-stu-id="29f42-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="29f42-116">Não utilize o SQL Data Warehouse para cargas de trabalho (OLTP) operacionais que tem:</span><span class="sxs-lookup"><span data-stu-id="29f42-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="29f42-117">Frequência alta lê e escreve</span><span class="sxs-lookup"><span data-stu-id="29f42-117">High frequency reads and writes</span></span>
- <span data-ttu-id="29f42-118">Grande número de singleton seleciona</span><span class="sxs-lookup"><span data-stu-id="29f42-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="29f42-119">Volumes elevados de inserções de linha única</span><span class="sxs-lookup"><span data-stu-id="29f42-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="29f42-120">Linha por linha tem de processar</span><span class="sxs-lookup"><span data-stu-id="29f42-120">Row by row processing needs</span></span>
- <span data-ttu-id="29f42-121">Formatos incompatíveis (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="29f42-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="29f42-122">Migração do plano de Olá</span><span class="sxs-lookup"><span data-stu-id="29f42-122">Plan hello migration</span></span>

<span data-ttu-id="29f42-123">Depois de decidir toomigrate um tooSQL de solução do armazém de dados existente, é importante tooplan migração de Olá antes da introdução.</span><span class="sxs-lookup"><span data-stu-id="29f42-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="29f42-124">Um objetivo de planeamento é tooensure os dados, esquemas de tabela, e código são compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="29f42-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="29f42-125">Existem algumas diferenças de compatibilidade toowork à volta entre o sistema atual e o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="29f42-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="29f42-126">Plus, a migrar grandes quantidades de dados tooAzure demora tempo.</span><span class="sxs-lookup"><span data-stu-id="29f42-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="29f42-127">Um planeamento cuidado expedites ao obter o tooAzure de dados.</span><span class="sxs-lookup"><span data-stu-id="29f42-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="29f42-128">Outro objetivo do planeamento é design toomake tooensure ajustes que a solução tira partido do desempenho de consulta elevado Olá que SQL Data Warehouse é concebido tooprovide.</span><span class="sxs-lookup"><span data-stu-id="29f42-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="29f42-129">Conceber armazéns de dados para a escala apresenta padrões de conceção diferentes e abordagens tradicionais, por isso, não são sempre Olá melhor.</span><span class="sxs-lookup"><span data-stu-id="29f42-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="29f42-130">Embora pode efetuar alguns ajustes de design após a migração, efetuar as alterações mais cedo no processo de Olá irá poupar tempo posteriormente.</span><span class="sxs-lookup"><span data-stu-id="29f42-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="29f42-131">tooperform uma migração com êxito, terá de toomigrate as esquemas de tabela, o seu código e os dados.</span><span class="sxs-lookup"><span data-stu-id="29f42-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="29f42-132">Para obter orientações sobre estes tópicos de migração, consulte:</span><span class="sxs-lookup"><span data-stu-id="29f42-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="29f42-133">Migrar as esquemas</span><span class="sxs-lookup"><span data-stu-id="29f42-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="29f42-134">Migrar o seu código</span><span class="sxs-lookup"><span data-stu-id="29f42-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="29f42-135">[Migrar os dados](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="29f42-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="29f42-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="29f42-136">Next steps</span></span>
<span data-ttu-id="29f42-137">Olá CAT (equipa de Consultadora dos clientes) também tem algumas excelente documentação de orientação do armazém de dados do SQL Server, que publicam através de blogues.</span><span class="sxs-lookup"><span data-stu-id="29f42-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="29f42-138">Observe respetivo artigo, [tooAzure de dados de migração do armazém de dados do SQL Server na prática] [ Migrating data tooAzure SQL Data Warehouse in practice] para orientações adicionais sobre a migração.</span><span class="sxs-lookup"><span data-stu-id="29f42-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
