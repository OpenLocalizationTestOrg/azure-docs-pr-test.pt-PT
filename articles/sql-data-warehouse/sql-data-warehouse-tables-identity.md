---
title: "chaves de substituição de aaaCreate utilizando identidade | Microsoft Docs"
description: "Saiba como chaves de substituição de toocreate toouse identidade no seu tabelas."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="dbdaa-103">Criar chaves substituto através da utilização de identidade</span><span class="sxs-lookup"><span data-stu-id="dbdaa-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="dbdaa-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="dbdaa-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="dbdaa-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="dbdaa-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-107">[Index][Index]</span></span>
> * <span data-ttu-id="dbdaa-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="dbdaa-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="dbdaa-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="dbdaa-111">[Identidade][Identity]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="dbdaa-112">Muitos modelers de dados, como as chaves de substituto toocreate as respetivas tabelas quando estes modelos de armazém de dados de design.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="dbdaa-113">Pode utilizar tooachieve de propriedade de identidade Olá este objetivo simples e eficaz sem afetar o desempenho da carga.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="dbdaa-114">Começar com uma identidade</span><span class="sxs-lookup"><span data-stu-id="dbdaa-114">Get started with IDENTITY</span></span>
<span data-ttu-id="dbdaa-115">Pode definir uma tabela como ter a propriedade de identidade Olá ao primeiro criar tabela Olá utilizando sintaxe semelhante toohello a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="dbdaa-116">Em seguida, pode utilizar `INSERT..SELECT` tabela de Olá toopopulate.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="dbdaa-117">Comportamento</span><span class="sxs-lookup"><span data-stu-id="dbdaa-117">Behavior</span></span>
<span data-ttu-id="dbdaa-118">Olá propriedade de identidade é concebida tooscale enviados em todas as distribuições de Olá no armazém de dados de Olá sem afetar o desempenho da carga.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="dbdaa-119">Por conseguinte, implementação de Olá de identidade é dedicada a alcançar estes objetivos.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="dbdaa-120">Esta secção realça nuances Olá de Olá implementação toohelp compreende-las mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="dbdaa-121">Alocação de valores</span><span class="sxs-lookup"><span data-stu-id="dbdaa-121">Allocation of values</span></span>
<span data-ttu-id="dbdaa-122">Olá propriedade de identidade não garante a ordem de Olá no qual Olá são atribuídos valores de substituição, que reflete o comportamento de Olá do SQL Server e SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="dbdaa-123">No entanto, no Azure SQL Data Warehouse, mais pronunciada de ausência de Olá de uma garantia.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="dbdaa-124">Olá seguinte o exemplo é uma ilustração:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-124">hello following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="dbdaa-125">No Olá anterior exemplo, duas linhas landed distribuição 1.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="dbdaa-126">primeira linha de Olá tem um valor de substituição de 1 Olá na coluna `C1`, e a segunda linha de Olá tem um valor de substituição de 61 Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="dbdaa-127">Ambos estes valores foram gerados por Olá propriedade de identidade.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="dbdaa-128">No entanto, Olá dos valores de Olá não é contíguo.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="dbdaa-129">Este comportamento é propositado.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="dbdaa-130">Dados distorcidos</span><span class="sxs-lookup"><span data-stu-id="dbdaa-130">Skewed data</span></span> 
<span data-ttu-id="dbdaa-131">intervalo de Olá de valores para o tipo de dados de Olá são distribuídos uniformemente por distribuições Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="dbdaa-132">Se sofrerá de uma tabela distribuída a partir dos dados distorcidos, Olá, em seguida, intervalo de valores datatype toohello disponível pode ser esgotado prematuramente.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="dbdaa-133">Por exemplo, se todos os dados de Olá termina uma distribuição único, em seguida, eficazmente Olá tabela tem acesso tooonly sixtieth um dos valores de Olá Olá do tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="dbdaa-134">Por este motivo, Olá propriedade de identidade é limitado demasiado`INT` e `BIGINT` apenas tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="dbdaa-135">SELECIONAR... PARA</span><span class="sxs-lookup"><span data-stu-id="dbdaa-135">SELECT..INTO</span></span>
<span data-ttu-id="dbdaa-136">Quando uma coluna de identidade existente é selecionada para uma nova tabela, coluna nova Olá herda propriedade de identidade Olá, a menos que uma das Olá seguintes condições for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="dbdaa-137">instrução SELECT Olá contém uma associação.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="dbdaa-138">Múltiplas instruções SELECIONADAS são associadas através da utilização de União.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="dbdaa-139">a coluna de identidade Olá é listada mais do que uma vez na lista de SELEÇÃO de Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="dbdaa-140">a coluna de identidade Olá faz parte de uma expressão.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="dbdaa-141">Se qualquer um dos seguintes condições for VERDADEIRO, a coluna Olá é criada NOT NULL em vez de a herança de propriedade de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="dbdaa-142">CRIAR TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="dbdaa-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="dbdaa-143">Criar tabela AS SELECIONE (CTAS) forma Olá mesmo comportamento SQL Server que é descrito selecione... PARA.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="dbdaa-144">No entanto, não é possível especificar uma propriedade de identidade na definição de coluna Olá de Olá `CREATE TABLE` fazem parte da instrução Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="dbdaa-145">É também não é possível utilizar a função de identidade Olá no Olá `SELECT` fazem parte da Olá CTAS.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="dbdaa-146">toopopulate uma tabela, terá de toouse `CREATE TABLE` seguido de tabela de Olá toodefine `INSERT..SELECT` toopopulate-lo.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="dbdaa-147">Inserir explicitamente valores numa coluna de identidade</span><span class="sxs-lookup"><span data-stu-id="dbdaa-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="dbdaa-148">Suporta o SQL Data Warehouse `SET IDENTITY_INSERT <your table> ON|OFF` sintaxe.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="dbdaa-149">Pode utilizar valores de inserção de tooexplicitly esta sintaxe na coluna de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="dbdaa-150">Muitos modelers de dados como negativo predefinidas toouse para determinados valores de linhas na respetiva dimensões.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="dbdaa-151">Um exemplo é Olá -1 ou linha "membro desconhecido".</span><span class="sxs-lookup"><span data-stu-id="dbdaa-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="dbdaa-152">script seguinte Olá mostra como tooexplicitly adicionar esta linha utilizando IDENTITY_INSERT definir:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="dbdaa-153">Carregar dados para uma tabela com uma identidade</span><span class="sxs-lookup"><span data-stu-id="dbdaa-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="dbdaa-154">presença Olá Olá propriedade de identidade tem alguns códigos de carregamento de dados de tooyour implicações.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="dbdaa-155">Esta secção realça alguns padrões básicos para carregar dados para tabelas através da utilização de identidade.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="dbdaa-156">Carregar dados com o PolyBase</span><span class="sxs-lookup"><span data-stu-id="dbdaa-156">Load data with PolyBase</span></span>
<span data-ttu-id="dbdaa-157">dados de tooload numa tabela e gerar uma chave de substituição, utilizando a identidade, criar a tabela de Olá e, em seguida, utilizar INSERT... SELECIONE ou INSIRA... VALORES tooperform Olá carga.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="dbdaa-158">Olá exemplo seguinte realça padrão básico Olá:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-158">hello following example highlights hello basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="dbdaa-159">Não é possível toouse `CREATE TABLE AS SELECT` atualmente ao carregar dados para uma tabela com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="dbdaa-160">Para mais informações sobre como carregar dados utilizando a ferramenta do programa (BCP) de cópia em massa Olá, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="dbdaa-161">[Carregar com o PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="dbdaa-162">[O PolyBase melhores práticas][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="dbdaa-163">Carregar dados com o BCP</span><span class="sxs-lookup"><span data-stu-id="dbdaa-163">Load data with BCP</span></span>
<span data-ttu-id="dbdaa-164">BCP é uma ferramenta da linha de comandos que pode utilizar dados tooload para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="dbdaa-165">Um dos respetivos parâmetros (-I) controlos Olá comportamento do BCP ao carregar dados para uma tabela com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="dbdaa-166">Quando é especificado -I, valores Olá contidos no ficheiro de entrada Olá para a coluna de Olá com a identidade são retidos.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="dbdaa-167">Se for -I *não* especificado, em seguida, são ignorados valores Olá nesta coluna.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="dbdaa-168">Se a coluna de identidade Olá não estiver incluída, em seguida, Olá os dados são carregados como normal.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="dbdaa-169">valores de Olá são gerados de acordo com a política incremento e seed toohello da propriedade Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="dbdaa-170">Para mais informações sobre como carregar dados utilizando o BCP, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="dbdaa-171">[Carregar com o BCP][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-171">[Load with BCP][]</span></span>
- <span data-ttu-id="dbdaa-172">[BCP no MSDN][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="dbdaa-173">Vistas de catálogo</span><span class="sxs-lookup"><span data-stu-id="dbdaa-173">Catalog views</span></span>
<span data-ttu-id="dbdaa-174">Armazém de dados SQL suporta Olá `sys.identity_columns` vista de catálogo.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="dbdaa-175">Esta vista pode ser utilizado tooidentify uma coluna que tem a propriedade de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="dbdaa-176">toohelp compreender melhor o esquema de base de dados de Olá, este exemplo mostra como toointegrate `sys.identity_columns` com outras vistas de catálogo de sistema:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="dbdaa-177">Limitações</span><span class="sxs-lookup"><span data-stu-id="dbdaa-177">Limitations</span></span>
<span data-ttu-id="dbdaa-178">Não é possível utilizar Olá propriedade de identidade Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="dbdaa-179">Em que tipo de dados da coluna de Olá não é INT ou BIGINT</span><span class="sxs-lookup"><span data-stu-id="dbdaa-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="dbdaa-180">Em que a coluna de Olá também é Olá de distribuição de chaves</span><span class="sxs-lookup"><span data-stu-id="dbdaa-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="dbdaa-181">Em que a tabela de Olá é uma tabela externa</span><span class="sxs-lookup"><span data-stu-id="dbdaa-181">Where hello table is an external table</span></span> 

<span data-ttu-id="dbdaa-182">Olá funções relacionadas com os seguintes não é suportado no armazém de dados do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="dbdaa-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="dbdaa-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="dbdaa-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="dbdaa-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="dbdaa-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="dbdaa-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="dbdaa-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="dbdaa-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="dbdaa-190">Tarefas</span><span class="sxs-lookup"><span data-stu-id="dbdaa-190">Tasks</span></span>

<span data-ttu-id="dbdaa-191">Esta secção fornece algum código de exemplo pode utilizar tarefas comuns tooperform quando trabalha com colunas de identidade.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="dbdaa-192">C1 de coluna é Olá identidade no Olá todas as seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="dbdaa-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="dbdaa-193">Localizar o valor mais elevado de Olá alocado para uma tabela</span><span class="sxs-lookup"><span data-stu-id="dbdaa-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="dbdaa-194">Olá utilize `MAX()` função de valor de mais alto de toodetermine Olá atribuído a uma tabela distribuída:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="dbdaa-195">Localizar Olá seed e incrementação maiores para Olá propriedade de identidade</span><span class="sxs-lookup"><span data-stu-id="dbdaa-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="dbdaa-196">Pode utilizar Olá catálogo vistas toodiscover Olá identidade incremento e seed valores de configuração para uma tabela utilizando Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="dbdaa-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="dbdaa-197">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dbdaa-197">Next steps</span></span>

* <span data-ttu-id="dbdaa-198">toolearn mais informações sobre desenvolver as tabelas, consulte [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de índice][Index], [uma tabela de partição][Partition], e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="dbdaa-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="dbdaa-199">Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="dbdaa-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Carregar com o bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Carregar com o PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[O PolyBase melhores práticas]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP no MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
