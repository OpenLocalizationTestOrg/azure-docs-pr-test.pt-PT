---
title: "Memória aaaIn OLTP melhora o desempenho do SQL Server txn | Microsoft Docs"
description: "Adopt dentro da memória OLTP tooimprove transacional desempenho uma base de dados existente do SQL Server."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="05353-103">Utilização de memória OLTP tooimprove o desempenho da aplicação na base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="05353-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="05353-104">[OLTP na memória](sql-database-in-memory.md) podem ser utilizados tooimprove Olá desempenho do processamento de transações, a ingestão de dados e cenários de dados transitório, [Premium](sql-database-service-tiers.md) bases de dados do Azure SQL sem aumentar Olá escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="05353-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="05353-105">Saiba como [quórum duplica carga de trabalho de chave da base de dados ao reduzirem DTU por 70% com base de dados SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="05353-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="05353-106">Siga estes passos tooadopt OLTP dentro da memória na base de dados existente.</span><span class="sxs-lookup"><span data-stu-id="05353-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="05353-107">Passo 1: Certifique-se de que está a utilizar uma base de dados Premium</span><span class="sxs-lookup"><span data-stu-id="05353-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="05353-108">OLTP dentro da memória só é suportado em bases de dados Premium.</span><span class="sxs-lookup"><span data-stu-id="05353-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="05353-109">Dentro da memória é suportada se Olá devolveu o resultado é 1 (não 0):</span><span class="sxs-lookup"><span data-stu-id="05353-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="05353-110">*XTP* representa *Alpine processamento de transação*</span><span class="sxs-lookup"><span data-stu-id="05353-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="05353-111">Passo 2: Identificar objetos toomigrate tooIn memória OLTP</span><span class="sxs-lookup"><span data-stu-id="05353-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="05353-112">SSMS inclui um **descrição geral de análise do desempenho de transação** relatório que pode executar em relação a uma base de dados com uma carga de trabalho ativa.</span><span class="sxs-lookup"><span data-stu-id="05353-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="05353-113">relatório de Olá identifica as tabelas e procedimentos armazenados que sejam candidatas para a migração tooIn memória OLTP.</span><span class="sxs-lookup"><span data-stu-id="05353-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="05353-114">No SSMS, relatório de Olá toogenerate:</span><span class="sxs-lookup"><span data-stu-id="05353-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="05353-115">No Olá **Object Explorer**, clique com o botão direito do nó de base de dados.</span><span class="sxs-lookup"><span data-stu-id="05353-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="05353-116">Clique em **relatórios** > **relatórios padrão** > **descrição geral de análise do desempenho de transação**.</span><span class="sxs-lookup"><span data-stu-id="05353-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="05353-117">Para obter mais informações, consulte [Determining se uma tabela ou armazenados procedimento deve ser convertidos serem OLTP de memória tooIn](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="05353-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="05353-118">Passo 3: Criar uma base de dados de teste comparável</span><span class="sxs-lookup"><span data-stu-id="05353-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="05353-119">Suponhamos Olá relatório indica que a base de dados tem uma tabela que seria beneficiam de ser convertida tabela com otimização de memória de tooa.</span><span class="sxs-lookup"><span data-stu-id="05353-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="05353-120">Recomendamos que teste primeiro indicação de Olá tooconfirm ao testar.</span><span class="sxs-lookup"><span data-stu-id="05353-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="05353-121">Precisa de uma cópia de teste da sua base de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="05353-121">You need a test copy of your production database.</span></span> <span data-ttu-id="05353-122">Olá base de dados de teste deve ser em Olá service mesmo nível de como a base de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="05353-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="05353-123">tooease testar, otimizar a base de dados de teste da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="05353-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="05353-124">Liga a base de dados de teste de toohello, utilizando o SSMS.</span><span class="sxs-lookup"><span data-stu-id="05353-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="05353-125">tooavoid necessitar Olá opção WITH (SNAPSHOT) em consultas, defina a opção de base de dados de Olá conforme mostrado no Olá seguinte declaração de T-SQL:</span><span class="sxs-lookup"><span data-stu-id="05353-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="05353-126">Passo 4: Migrar tabelas</span><span class="sxs-lookup"><span data-stu-id="05353-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="05353-127">Tem de criar e preencher uma cópia com otimização de memória da tabela de Olá pretende tootest.</span><span class="sxs-lookup"><span data-stu-id="05353-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="05353-128">Pode criá-la utilizando:</span><span class="sxs-lookup"><span data-stu-id="05353-128">You can create it by using either:</span></span>

* <span data-ttu-id="05353-129">Olá à mão Assistente de otimização de memória no SSMS.</span><span class="sxs-lookup"><span data-stu-id="05353-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="05353-130">Manual de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="05353-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="05353-131">Assistente de otimização de memória no SSMS</span><span class="sxs-lookup"><span data-stu-id="05353-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="05353-132">toouse esta opção de migração:</span><span class="sxs-lookup"><span data-stu-id="05353-132">toouse this migration option:</span></span>

1. <span data-ttu-id="05353-133">Ligar a base de dados de teste de toohello com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="05353-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="05353-134">No Olá **Object Explorer**, faça duplo clique na tabela de Olá e, em seguida, clique em **Advisor de otimização de memória**.</span><span class="sxs-lookup"><span data-stu-id="05353-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="05353-135">Olá **tabela memória otimizador Advisor** é apresentado o assistente.</span><span class="sxs-lookup"><span data-stu-id="05353-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="05353-136">No Assistente de Olá, clique em **validação de migração** (ou Olá **seguinte** botão) toosee se a tabela de Olá tem quaisquer funcionalidades não suportadas que não são suportadas em tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="05353-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="05353-137">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="05353-137">For more information, see:</span></span>
   
   * <span data-ttu-id="05353-138">Olá *lista de verificação de otimização de memória* no [Advisor de otimização de memória](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="05353-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="05353-139">[As construções de Transact-SQL não suportadas pelo OLTP na memória](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="05353-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="05353-140">[Migrar tooIn memória OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="05353-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="05353-141">Se a tabela de Olá não tem nenhum funcionalidades não suportadas, advisor de Olá pode executar esquema real Olá e migração de dados para si.</span><span class="sxs-lookup"><span data-stu-id="05353-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="05353-142">Manual de T-SQL</span><span class="sxs-lookup"><span data-stu-id="05353-142">Manual T-SQL</span></span>
<span data-ttu-id="05353-143">toouse esta opção de migração:</span><span class="sxs-lookup"><span data-stu-id="05353-143">toouse this migration option:</span></span>

1. <span data-ttu-id="05353-144">Liga a base de dados de teste de tooyour utilizando o SSMS (ou um utilitário semelhante).</span><span class="sxs-lookup"><span data-stu-id="05353-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="05353-145">Obter o script T-SQL completado Olá para a tabela e seus índices.</span><span class="sxs-lookup"><span data-stu-id="05353-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="05353-146">No SSMS, clique no nó da tabela.</span><span class="sxs-lookup"><span data-stu-id="05353-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="05353-147">Clique em **Script tabela como** > **criar para** > **nova janela de consulta**.</span><span class="sxs-lookup"><span data-stu-id="05353-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="05353-148">Na janela de script de Olá, adicionar WITH (MEMORY_OPTIMIZED = ON) toohello instrução CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="05353-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="05353-149">Se existir um índice em cluster, alterá-la tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="05353-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="05353-150">Mudar o nome da tabela existente Olá utilizando SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="05353-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="05353-151">Crie Olá nova com otimização de memória cópia da tabela de Olá executando o script de CREATE TABLE editado.</span><span class="sxs-lookup"><span data-stu-id="05353-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="05353-152">Copie a tabela de otimização de memória do Olá dados tooyour utilizando INSERT... SELECIONE * PARA:</span><span class="sxs-lookup"><span data-stu-id="05353-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="05353-153">Passo 5 (opcional): Migrar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="05353-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="05353-154">funcionalidade de memória de Olá também pode modificar um procedimento armazenado para um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="05353-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="05353-155">Considerações de procedimentos armazenados compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="05353-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="05353-156">Um procedimento armazenado compilado nativamente tem de ter Olá opções na sua cláusula T-SQL com os seguintes:</span><span class="sxs-lookup"><span data-stu-id="05353-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="05353-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="05353-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="05353-158">SCHEMABINDING: tabelas significado Olá procedimento armazenado não podem ter as respetivas definições de coluna alteradas de qualquer forma que iria afetar o procedimento armazenado de Olá, a menos que largar o procedimento de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="05353-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="05353-159">Um módulo nativo tem de utilizar uma grande [em blocos ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para a gestão de transação.</span><span class="sxs-lookup"><span data-stu-id="05353-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="05353-160">Não há nenhuma função para uma transação começar explícita ou para ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="05353-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="05353-161">Se o seu código detetar uma violação de uma regra de negócio, pode terminar o bloco atomic de Olá com um [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrução.</span><span class="sxs-lookup"><span data-stu-id="05353-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="05353-162">CREATE PROCEDURE típico para compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="05353-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="05353-163">Normalmente, Olá T-SQL toocreate um procedimento armazenado compilado nativamente é semelhante toohello modelo os seguintes:</span><span class="sxs-lookup"><span data-stu-id="05353-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="05353-164">Para Olá TRANSACTION_ISOLATION_LEVEL, o INSTANTÂNEO é procedimento de valor para Olá compilado nativamente armazenado mais comuns Olá.</span><span class="sxs-lookup"><span data-stu-id="05353-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="05353-165">No entanto, um subconjunto de Olá outros valores também são suportados:</span><span class="sxs-lookup"><span data-stu-id="05353-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="05353-166">LEITURA REPETIDA</span><span class="sxs-lookup"><span data-stu-id="05353-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="05353-167">SERIALIZÁVEL</span><span class="sxs-lookup"><span data-stu-id="05353-167">SERIALIZABLE</span></span>
* <span data-ttu-id="05353-168">Olá valor de idioma deve estar presente na vista de sys.languages Olá.</span><span class="sxs-lookup"><span data-stu-id="05353-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="05353-169">Como toomigrate um procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="05353-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="05353-170">passos de migração de Olá são:</span><span class="sxs-lookup"><span data-stu-id="05353-170">hello migration steps are:</span></span>

1. <span data-ttu-id="05353-171">Obter Olá CREATE PROCEDURE script toohello regular interpretado procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="05353-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="05353-172">O modelo anterior do cabeçalho toomatch Olá de regravação.</span><span class="sxs-lookup"><span data-stu-id="05353-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="05353-173">Ascertain se o procedimento armazenado de Olá código T-SQL utiliza quaisquer funcionalidades que não são suportadas para procedimentos armazenados compilados nativamente.</span><span class="sxs-lookup"><span data-stu-id="05353-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="05353-174">Implementar soluções se necessário.</span><span class="sxs-lookup"><span data-stu-id="05353-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="05353-175">Para mais informações, consulte [problemas de migração para compilada nativamente procedimentos armazenados](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="05353-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="05353-176">Mudar o nome de procedimento armazenado de antigo Olá utilizando SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="05353-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="05353-177">Ou, basta REMOVÊ-la.</span><span class="sxs-lookup"><span data-stu-id="05353-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="05353-178">Execute o script Criar procedimento T-SQL editado.</span><span class="sxs-lookup"><span data-stu-id="05353-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="05353-179">Passo 6: Executar a carga de trabalho no teste</span><span class="sxs-lookup"><span data-stu-id="05353-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="05353-180">Execute uma carga de trabalho na sua base de dados de teste que é semelhante toohello a carga de trabalho é executado na sua base de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="05353-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="05353-181">Isto deve revelar ganhos de desempenho de Olá alcançado através da utilização da funcionalidade de memória de Olá para tabelas e procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="05353-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="05353-182">Atributos principais da carga de trabalho Olá são:</span><span class="sxs-lookup"><span data-stu-id="05353-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="05353-183">Número de ligações em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="05353-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="05353-184">Rácio de leitura/escrita.</span><span class="sxs-lookup"><span data-stu-id="05353-184">Read/write ratio.</span></span>

<span data-ttu-id="05353-185">tootailor e Olá executar a carga de trabalho de teste, considere a utilização da ferramenta de ostress.exe à mão de Olá, ilustrado na [aqui](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="05353-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="05353-186">Latência de rede toominimize, execute o teste no Olá mesma região geográfica do Azure onde a base de dados de Olá existe.</span><span class="sxs-lookup"><span data-stu-id="05353-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="05353-187">Passo 7: Monitorização de pós-implementação</span><span class="sxs-lookup"><span data-stu-id="05353-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="05353-188">Considere os efeitos de desempenho de Olá das suas implementações de dentro da memória na produção de monitorização:</span><span class="sxs-lookup"><span data-stu-id="05353-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="05353-189">[Monitorizar o armazenamento em memória](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="05353-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="05353-190">Monitorizar a Base de Dados SQL do Azure com vistas de gestão dinâmica (Monitoring Azure SQL Database using dynamic management views)</span><span class="sxs-lookup"><span data-stu-id="05353-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="05353-191">Ligações relacionadas</span><span class="sxs-lookup"><span data-stu-id="05353-191">Related links</span></span>
* [<span data-ttu-id="05353-192">OLTP (otimização de memória) de memória</span><span class="sxs-lookup"><span data-stu-id="05353-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="05353-193">TooNatively de introdução-compilado procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="05353-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="05353-194">Advisor de otimização de memória</span><span class="sxs-lookup"><span data-stu-id="05353-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

