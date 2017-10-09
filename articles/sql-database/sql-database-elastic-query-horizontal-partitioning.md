---
title: aaaReporting entre bases de dados de nuvem de escalamento horizontal | Microsoft Docs
description: "como tooset segurança elásticas consultas através de partições horizontais"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="fd8fd-103">Relatórios em bases de dados de nuvem de escalamento horizontal (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="fd8fd-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Consultar em partições horizontais][1]

<span data-ttu-id="fd8fd-105">Bases de dados em partição horizontal distribuam linhas por um dados expandido terminar camada.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="fd8fd-106">esquema de Olá é idêntica em todos os participantes bases de dados, também conhecidos como criação de partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="fd8fd-107">Utilizando uma consulta elástica, pode criar relatórios que abrangem todas as bases de dados numa base de dados em partição horizontal.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="fd8fd-108">Para uma introdução, consulte [Reporting entre bases de dados de nuvem de escalamento horizontal](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="fd8fd-109">Para bases de dados não-em partição horizontal, consulte [consulta em bases de dados de nuvem com diferentes esquemas](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd8fd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fd8fd-110">Prerequisites</span></span>
* <span data-ttu-id="fd8fd-111">Crie um mapa de partições horizontais com biblioteca de cliente de base de dados elástica Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="fd8fd-112">consulte [gestão de mapa de partições horizontais](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="fd8fd-113">Ou utilize a aplicação de exemplo de Olá no [começar a utilizar as ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="fd8fd-114">Em alternativa, consulte [existente Migrar bases de dados de bases de dados de saída tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="fd8fd-115">utilizador Olá precisa de ter permissão ALTER qualquer origem de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="fd8fd-116">Esta permissão está incluído com a permissão do Olá ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="fd8fd-117">As permissões de ALTER qualquer origem de dados externas são toohello toorefer necessários subjacente a origem de dados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="fd8fd-118">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="fd8fd-118">Overview</span></span>
<span data-ttu-id="fd8fd-119">Estas instruções criar representação de metadados de Olá da sua camada de dados fragmentados Olá consulta elástico da base de dados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="fd8fd-120">CRIAR CHAVE MESTRA</span><span class="sxs-lookup"><span data-stu-id="fd8fd-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="fd8fd-121">CRIAR UM ÂMBITO DE BASE DE DADOS CREDENCIAL</span><span class="sxs-lookup"><span data-stu-id="fd8fd-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="fd8fd-122">CRIAR ORIGEM DE DADOS EXTERNA</span><span class="sxs-lookup"><span data-stu-id="fd8fd-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="fd8fd-123">CRIAR TABELA EXTERNA</span><span class="sxs-lookup"><span data-stu-id="fd8fd-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="fd8fd-124">1.1 Criar chave mestra de base de dados no âmbito e as credenciais</span><span class="sxs-lookup"><span data-stu-id="fd8fd-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="fd8fd-125">credencial de Olá é utilizado pelo Olá consulta elástico tooconnect tooyour remoto as bases de dados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="fd8fd-126">Certifique-se de que Olá *"\<username\>"* não inclui quaisquer *"@servername"* sufixo.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="fd8fd-127">1.2 Criar origens de dados externas</span><span class="sxs-lookup"><span data-stu-id="fd8fd-127">1.2 Create external data sources</span></span>
<span data-ttu-id="fd8fd-128">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="fd8fd-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fd8fd-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="fd8fd-130">Obter a lista de Olá de origens de dados externas atual:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="fd8fd-131">origem de dados externa Olá referencia o mapa de partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-131">hello external data source references your shard map.</span></span> <span data-ttu-id="fd8fd-132">Uma consulta elástica, em seguida, utiliza a origem de dados externa Olá e Olá subjacente partições horizontais mapa tooenumerate Olá bases de dados que participam na camada de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="fd8fd-133">Olá mesmas credenciais são mapa de partições horizontais utilizadas tooread Olá e tooaccess Olá dados shards Olá durante o processamento de Olá de uma consulta elástico.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="fd8fd-134">1.3 criar tabelas externas</span><span class="sxs-lookup"><span data-stu-id="fd8fd-134">1.3 Create external tables</span></span>
<span data-ttu-id="fd8fd-135">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="fd8fd-136">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="fd8fd-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="fd8fd-137">Obter a lista de Olá de tabelas externas da base de dados atual Olá:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="fd8fd-138">tabelas externas toodrop:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="fd8fd-139">Observações</span><span class="sxs-lookup"><span data-stu-id="fd8fd-139">Remarks</span></span>
<span data-ttu-id="fd8fd-140">Olá dados\_cláusula origem define a origem de dados externa Olá (um mapa de partições horizontais) que é utilizada para a tabela externa Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="fd8fd-141">Olá esquema\_nome e o OBJETO\_cláusulas nome mapeiam uma tabela tooa de definição de tabela externa do Olá de um esquema diferente.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="fd8fd-142">Se for omitido, o esquema Olá do objeto remoto Olá é assumida toobe "dbo" e o respetivo nome é assumido o nome de tabela externa toobe toohello idênticos a ser definido.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="fd8fd-143">Isto é útil se Olá o nome da sua tabela remota já foi atribuído na base de dados de olá onde pretende tabela externa de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="fd8fd-144">Por exemplo, pretende toodefine tooget uma tabela externa uma vista de agregação de vistas de catálogo ou camada DMVs nos seus dados expandidos terminar.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="fd8fd-145">Uma vez que as vistas de catálogo e DMVs já existem localmente, não é possível utilizar os respetivos nomes para a definição de tabela externa Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="fd8fd-146">Em vez disso, utilize um nome diferente e utilizar a vista de catálogo a Olá ou Olá nome do DMV no Olá esquema\_nome e/ou OBJETO\_cláusulas de nome.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="fd8fd-147">(Consulte Exemplo Olá abaixo).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-147">(See hello example below.)</span></span> 

<span data-ttu-id="fd8fd-148">cláusula de distribuição Olá Especifica a distribuição de dados de Olá utilizada para esta tabela.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="fd8fd-149">processador de consultas Olá utiliza informações Olá fornecidas Olá distribuição cláusula toobuild Olá mais eficientes consulta planos.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="fd8fd-150">**A** significa dados horizontalmente estão particionados em bases de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="fd8fd-151">Olá, chave de criação de partições para distribuição de dados de Olá é Olá **< sharding_column_name >** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="fd8fd-152">**REPLICADO** significa que existem idênticas cópias da tabela de Olá em cada base de dados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="fd8fd-153">É o tooensure responsabilidade réplicas Olá são idênticas em bases de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="fd8fd-154">**ARREDONDAR\_Round ROBIN** significa nessa tabela Olá horizontalmente partições utilizando um método de distribuição de aplicações dependentes.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="fd8fd-155">**Referência de camada de dados**: DDL da tabela externa Olá refere-se a origem de dados externa tooan.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="fd8fd-156">origem de dados externa Olá Especifica um mapa de partições horizontais que disponibiliza tabela externa Olá Olá informações necessárias toolocate todas as bases de dados de Olá na sua camada de dados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="fd8fd-157">Considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="fd8fd-157">Security considerations</span></span>
<span data-ttu-id="fd8fd-158">Os utilizadores com a tabela externa do acesso toohello automaticamente obterem acesso toohello subjacente tabelas remotas sob credenciais de Olá especificado na definição de origem de dados externas Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="fd8fd-159">Evite indesejada elevação de privilégios através de credencial de Olá Olá externo da origem de dados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="fd8fd-160">Utilize GRANT ou REVOKE para uma tabela externa como se fosse uma tabela normal.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="fd8fd-161">Assim que definiu a sua origem de dados externos e as tabelas externas, agora pode utilizar o T-SQL completo sobre as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="fd8fd-162">Exemplo: consultar as bases de dados de particionadas horizontais</span><span class="sxs-lookup"><span data-stu-id="fd8fd-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="fd8fd-163">Olá seguinte consulta efetua uma junção de três vias entre armazéns, encomendas pendentes e linhas de ordem e utiliza vários agregados e um filtro seletivo.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="fd8fd-164">Pressupõe que (1) horizontal partições (fragmentação) e (2) se armazéns, as ordens de linhas de ordem, sendo pela coluna de id de armazém Olá, e essa consulta elástico Olá pode colocalizar Olá associações em shards Olá e processar Olá dispendiosas parte consulta Olá Olá shards em paralelo.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="fd8fd-165">Procedimento para execução remota de T-SQL armazenado: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="fd8fd-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="fd8fd-166">Consulta elástica também apresenta um procedimento armazenado que fornece acesso direto toohello shards.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="fd8fd-167">Olá procedimento armazenado é chamado [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) e podem ser utilizados tooexecute de procedimentos armazenados remoto ou um código de T-SQL em bases de dados remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="fd8fd-168">Demora Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="fd8fd-169">Nome da origem de dados (nvarchar): nome de Olá Olá externo da origem de dados do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="fd8fd-170">Consulta (nvarchar): Olá T-SQL consulta toobe executada em cada partição horizontal.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="fd8fd-171">Declaração de parâmetro (nvarchar) - opcional: de cadeia com as definições de tipo de dados para os parâmetros de Olá utilizadas no parâmetro de consulta Olá (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="fd8fd-172">Lista de valores de parâmetro - opcional: lista de valores separados por vírgulas de valores de parâmetros (por exemplo, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="fd8fd-173">Olá sp\_executar\_remota utiliza Olá fornecida Olá invocação parâmetros tooexecute Olá fornecido instrução T-SQL em bases de dados remoto Olá de origem de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="fd8fd-174">Utiliza credenciais Olá Olá dados externos origem tooconnect toohello shardmap Gestor da base de dados e as bases de dados remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="fd8fd-175">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="fd8fd-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="fd8fd-176">Conectividade de ferramentas</span><span class="sxs-lookup"><span data-stu-id="fd8fd-176">Connectivity for tools</span></span>
<span data-ttu-id="fd8fd-177">Utilizar regular tooconnect de cadeias de ligação do SQL Server da aplicação, dados e BI integração ferramentas toohello base de dados com as definições de tabela externa.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="fd8fd-178">Certifique-se de que o SQL Server é suportada como uma origem de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="fd8fd-179">Olá elástico consultar base de dados como qualquer outra ferramenta do SQL Server da base de dados ligada toohello de referência, em seguida e utilize as tabelas externas da sua aplicação ou a ferramenta como se estivessem tabelas locais.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="fd8fd-180">Melhores práticas</span><span class="sxs-lookup"><span data-stu-id="fd8fd-180">Best practices</span></span>
* <span data-ttu-id="fd8fd-181">Certifique-se de que a base de dados de ponto final de consulta elástico Olá foi indicado o base de dados do access toohello shardmap e todas as partições horizontais através de Olá firewalls de BD do SQL.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="fd8fd-182">Validar ou impor a distribuição de dados de Olá definida pela tabela externa Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="fd8fd-183">Se a distribuição de dados real é diferente da distribuição Olá especificada na definição de tabela, as suas consultas poderão produzir resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="fd8fd-184">Consulta elástica atualmente não efetuar a eliminação de partições horizontais quando predicados sobre a chave de fragmentação Olá permitiria-toosafely excluir determinadas shards de processamento.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="fd8fd-185">Consulta elástica funciona melhor para consultas onde é possível efetuar a maioria do cálculo de Olá shards Olá.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="fd8fd-186">Obter normalmente Olá melhor desempenho das consultas com predicados de filtro seletiva que pode ser avaliado em shards Olá ou associações através de Olá a criação de partições de chaves que podem ser executadas de forma a partição alinhada em todas as partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="fd8fd-187">Outros padrões de consulta podem precisar de grandes quantidades de tooload dos dados a partir do nó principal do Olá shards toohello e podem efetuar mal</span><span class="sxs-lookup"><span data-stu-id="fd8fd-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd8fd-188">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fd8fd-188">Next steps</span></span>

* <span data-ttu-id="fd8fd-189">Para obter uma descrição geral da consulta elástica, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="fd8fd-190">Para um tutorial de criação de partições vertical, consulte [introdução à consulta de base de dados em vários locais (criação de partições vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="fd8fd-191">Para consultas de sintaxe e exemplos de dados verticalmente particionadas, consulte [consultar verticalmente particionada dados)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="fd8fd-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="fd8fd-192">Para um tutorial horizontal criação de partições (fragmentação), consulte [como começar a consultar elástico (fragmentação) de partições horizontais](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd8fd-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="fd8fd-193">Consulte [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução de Transact-SQL num único remoto SQL Database do Azure ou um conjunto de bases de dados que servem como shards num esquema de partições horizontal.</span><span class="sxs-lookup"><span data-stu-id="fd8fd-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
