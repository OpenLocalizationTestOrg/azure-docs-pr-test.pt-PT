---
title: bases de dados com outro esquema de aaaQuery na nuvem | Microsoft Docs
description: "como tooset cópias de segurança entre bases de dados de consultas através de partições verticais"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="fecbe-103">Consultar em bases de dados de nuvem com diferentes esquemas (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="fecbe-103">Query across cloud databases with different schemas (preview)</span></span>
![Consultar em tabelas de bases de dados diferentes][1]

<span data-ttu-id="fecbe-105">Verticalmente particionada bases de dados utilizam conjuntos diferentes de tabelas de bases de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="fecbe-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="fecbe-106">Isto significa que o esquema dessa Olá é diferente em bases de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="fecbe-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="fecbe-107">Por exemplo, todas as tabelas de inventário são numa base de dados enquanto todas as tabelas relacionadas com a gestão de contas numa segunda base de dados.</span><span class="sxs-lookup"><span data-stu-id="fecbe-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fecbe-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fecbe-108">Prerequisites</span></span>
* <span data-ttu-id="fecbe-109">utilizador Olá precisa de ter permissão ALTER qualquer origem de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fecbe-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="fecbe-110">Esta permissão está incluído com a permissão do Olá ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="fecbe-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="fecbe-111">As permissões de ALTER qualquer origem de dados externas são toohello toorefer necessários subjacente a origem de dados.</span><span class="sxs-lookup"><span data-stu-id="fecbe-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="fecbe-112">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="fecbe-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="fecbe-113">Ao contrário com criação de partições horizontais, estas instruções DDL depende da definição de uma camada de dados com um mapa de partições horizontais através da biblioteca de clientes de base de dados elástica Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="fecbe-114">CRIAR CHAVE MESTRA</span><span class="sxs-lookup"><span data-stu-id="fecbe-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="fecbe-115">CRIAR UM ÂMBITO DE BASE DE DADOS CREDENCIAL</span><span class="sxs-lookup"><span data-stu-id="fecbe-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="fecbe-116">CRIAR ORIGEM DE DADOS EXTERNA</span><span class="sxs-lookup"><span data-stu-id="fecbe-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="fecbe-117">CRIAR TABELA EXTERNA</span><span class="sxs-lookup"><span data-stu-id="fecbe-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="fecbe-118">Criar chave mestra de base de dados no âmbito e as credenciais</span><span class="sxs-lookup"><span data-stu-id="fecbe-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="fecbe-119">credencial de Olá é utilizado pelo Olá consulta elástico tooconnect tooyour remoto as bases de dados.</span><span class="sxs-lookup"><span data-stu-id="fecbe-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="fecbe-120">Certifique-se de que Olá `<username>` não inclui quaisquer **"@servername"** sufixo.</span><span class="sxs-lookup"><span data-stu-id="fecbe-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="fecbe-121">Criar origens de dados externas</span><span class="sxs-lookup"><span data-stu-id="fecbe-121">Create external data sources</span></span>
<span data-ttu-id="fecbe-122">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="fecbe-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="fecbe-123">parâmetro de tipo Olá tem de ser definido demasiado**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="fecbe-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="fecbe-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fecbe-124">Example</span></span>
<span data-ttu-id="fecbe-125">Olá exemplo a seguir ilustra utilização Olá Olá instrução CREATE para origens de dados externas.</span><span class="sxs-lookup"><span data-stu-id="fecbe-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="fecbe-126">lista de Olá tooretrieve atual externo de origens de dados:</span><span class="sxs-lookup"><span data-stu-id="fecbe-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="fecbe-127">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="fecbe-127">External Tables</span></span>
<span data-ttu-id="fecbe-128">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="fecbe-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="fecbe-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fecbe-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="fecbe-130">Olá seguinte exemplo mostra como tooretrieve Olá a lista de tabelas externas da base de dados atual Olá:</span><span class="sxs-lookup"><span data-stu-id="fecbe-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="fecbe-131">Observações</span><span class="sxs-lookup"><span data-stu-id="fecbe-131">Remarks</span></span>
<span data-ttu-id="fecbe-132">Consulta elástica expande Olá existente tabela externa sintaxe toodefine tabelas externas que utilizam as origens de dados externas do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="fecbe-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="fecbe-133">Uma definição de tabela externa para a criação de partições vertical abrange Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="fecbe-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="fecbe-134">**Esquema**: DDL da tabela externa Olá define um esquema que podem utilizar as suas consultas.</span><span class="sxs-lookup"><span data-stu-id="fecbe-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="fecbe-135">esquema de Olá fornecido na sua definição de tabela externa tem de esquema de Olá toomatch das tabelas de Olá no Olá base de dados remota armazenar dados real Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="fecbe-136">**Referência de base de dados remota**: DDL da tabela externa Olá refere-se a origem de dados externa tooan.</span><span class="sxs-lookup"><span data-stu-id="fecbe-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="fecbe-137">origem de dados externa Olá Especifica o nome de servidor lógico de Olá e nome de base de dados de Olá base de dados remota onde Olá tabela real dados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="fecbe-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="fecbe-138">Tabelas externas do Olá sintaxe toocreate conforme descrito na secção anterior Olá a utilizar uma origem de dados externo, é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fecbe-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="fecbe-139">cláusula DATA_SOURCE Olá define a origem de dados externa hello (ou seja, Olá remota da base de dados em caso de criação de partições vertical) que é utilizada para a tabela externa Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="fecbe-140">cláusulas SCHEMA_NAME e OBJECT_NAME Olá fornecem Olá capacidade toomap Olá tabela externa definição tooa tabela de um esquema diferente na base de dados remota Olá ou tooa tabela com um nome diferente, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="fecbe-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="fecbe-141">Isto é útil se pretender que toodefine uma vista de catálogo tooa de tabela externa ou DMV na sua base de dados remota - ou quaisquer outra situação em que o nome de tabela remota Olá já foi atribuído localmente.</span><span class="sxs-lookup"><span data-stu-id="fecbe-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="fecbe-142">Olá seguinte instrução DDL ignora uma definição de tabela externa existentes do catálogo local Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="fecbe-143">Não afetam a base de dados remota Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="fecbe-144">**Permissões de tabela externa CREATE/DROP**: são necessárias permissões de ALTER qualquer origem de dados externa para a tabela externa DDL que também é necessário toorefer toohello origem de dados subjacente.</span><span class="sxs-lookup"><span data-stu-id="fecbe-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="fecbe-145">Considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="fecbe-145">Security considerations</span></span>
<span data-ttu-id="fecbe-146">Os utilizadores com a tabela externa do acesso toohello automaticamente obterem acesso toohello subjacente tabelas remotas sob credenciais de Olá especificado na definição de origem de dados externas Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="fecbe-147">Cuidadosamente deve gerir acesso toohello externo tabela tooavoid indesejado elevação de privilégios através de credencial de Olá Olá externo da origem de dados, ordem.</span><span class="sxs-lookup"><span data-stu-id="fecbe-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="fecbe-148">Permissões normais do SQL Server podem ser utilizado tooGRANT ou tabela externa do REVOGAR acesso tooan como se fosse uma tabela normal.</span><span class="sxs-lookup"><span data-stu-id="fecbe-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="fecbe-149">Exemplo: consultar verticalmente particionada bases de dados</span><span class="sxs-lookup"><span data-stu-id="fecbe-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="fecbe-150">Olá seguinte consulta executa uma associação de três vias entre duas tabelas locais Olá sobre encomendas pendentes e linhas de ordem e tabela remota Olá para os clientes.</span><span class="sxs-lookup"><span data-stu-id="fecbe-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="fecbe-151">Este é um exemplo de Olá referência dados caso de utilização da consulta elástico:</span><span class="sxs-lookup"><span data-stu-id="fecbe-151">This is an example of hello reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="fecbe-152">Procedimento para execução remota de T-SQL armazenado: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="fecbe-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="fecbe-153">Consulta elástica também apresenta um procedimento armazenado que fornece acesso direto toohello shards.</span><span class="sxs-lookup"><span data-stu-id="fecbe-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="fecbe-154">Olá procedimento armazenado é chamado [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) e podem ser utilizados tooexecute de procedimentos armazenados remoto ou um código de T-SQL em bases de dados remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="fecbe-155">Demora Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fecbe-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="fecbe-156">Nome da origem de dados (nvarchar): nome de Olá Olá externo da origem de dados do tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="fecbe-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="fecbe-157">Consulta (nvarchar): Olá T-SQL consulta toobe executada em cada partição horizontal.</span><span class="sxs-lookup"><span data-stu-id="fecbe-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="fecbe-158">Declaração de parâmetro (nvarchar) - opcional: de cadeia com as definições de tipo de dados para os parâmetros de Olá utilizadas no parâmetro de consulta Olá (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="fecbe-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="fecbe-159">Lista de valores de parâmetro - opcional: lista de valores separados por vírgulas de valores de parâmetros (por exemplo, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="fecbe-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="fecbe-160">Olá sp\_executar\_remota utiliza Olá fornecida Olá invocação parâmetros tooexecute Olá fornecido instrução T-SQL em bases de dados remoto Olá de origem de dados externa.</span><span class="sxs-lookup"><span data-stu-id="fecbe-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="fecbe-161">Utiliza credenciais Olá Olá dados externos origem tooconnect toohello shardmap Gestor da base de dados e as bases de dados remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="fecbe-162">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="fecbe-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="fecbe-163">Conectividade de ferramentas</span><span class="sxs-lookup"><span data-stu-id="fecbe-163">Connectivity for tools</span></span>
<span data-ttu-id="fecbe-164">Pode utilizar tooconnect de cadeias de ligação do SQL Server regular sua toodatabases de ferramentas de integração de BI e os dados no servidor de base de dados SQL Olá que tenha consulta elástica ativada e tabelas externas definidas.</span><span class="sxs-lookup"><span data-stu-id="fecbe-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="fecbe-165">Certifique-se de que o SQL Server é suportada como uma origem de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="fecbe-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="fecbe-166">Em seguida, consulte a base de dados de consulta elástico toohello e as respetivas tabelas externas, tal como quaisquer outro do SQL Server da base de dados que seria se ligar toowith a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="fecbe-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="fecbe-167">Melhores práticas</span><span class="sxs-lookup"><span data-stu-id="fecbe-167">Best practices</span></span>
* <span data-ttu-id="fecbe-168">Certifique-se de que a base de dados de ponto final de consulta elástico Olá foi indicado acesso toohello remota da base de dados ao permitir o acesso para serviços do Azure na sua configuração de firewall da BD do SQL.</span><span class="sxs-lookup"><span data-stu-id="fecbe-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="fecbe-169">Certifique-se também essa credencial Olá fornecido nos dados externos Olá a definição de origem pode iniciar com êxito na base de dados remoto Olá e tem Olá permissões tooaccess Olá remoto tabela.</span><span class="sxs-lookup"><span data-stu-id="fecbe-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="fecbe-170">Consulta elástica funciona melhor para consultas onde a maioria do cálculo de Olá pode ser efetuada em bases de dados remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="fecbe-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="fecbe-171">Normalmente, obter Olá melhor desempenho das consultas com predicados de filtro seletiva que pode ser avaliado em bases de dados remoto Olá ou associações que podem ser efetuadas na base de dados remota Olá completamente.</span><span class="sxs-lookup"><span data-stu-id="fecbe-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="fecbe-172">Outros padrões de consulta podem precisar de grandes quantidades de tooload dos dados da base de dados remoto Olá e podem efetuar mal.</span><span class="sxs-lookup"><span data-stu-id="fecbe-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fecbe-173">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fecbe-173">Next steps</span></span>

* <span data-ttu-id="fecbe-174">Para obter uma descrição geral da consulta elástica, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fecbe-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="fecbe-175">Para um tutorial de criação de partições vertical, consulte [introdução à consulta de base de dados em vários locais (criação de partições vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="fecbe-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="fecbe-176">Para um tutorial horizontal criação de partições (fragmentação), consulte [como começar a consultar elástico (fragmentação) de partições horizontais](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fecbe-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="fecbe-177">Para consultas de sintaxe e exemplos de dados particionadas horizontalmente, consulte [consultar horizontalmente particionada dados)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="fecbe-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="fecbe-178">Consulte [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução de Transact-SQL num único remoto SQL Database do Azure ou um conjunto de bases de dados que servem como shards num esquema de partições horizontal.</span><span class="sxs-lookup"><span data-stu-id="fecbe-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
