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
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Relatórios em bases de dados de nuvem de escalamento horizontal (pré-visualização)
![Consultar em partições horizontais][1]

Bases de dados em partição horizontal distribuam linhas por um dados expandido terminar camada. esquema de Olá é idêntica em todos os participantes bases de dados, também conhecidos como criação de partições horizontais. Utilizando uma consulta elástica, pode criar relatórios que abrangem todas as bases de dados numa base de dados em partição horizontal.

Para uma introdução, consulte [Reporting entre bases de dados de nuvem de escalamento horizontal](sql-database-elastic-query-getting-started.md).

Para bases de dados não-em partição horizontal, consulte [consulta em bases de dados de nuvem com diferentes esquemas](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Crie um mapa de partições horizontais com biblioteca de cliente de base de dados elástica Olá. consulte [gestão de mapa de partições horizontais](sql-database-elastic-scale-shard-map-management.md). Ou utilize a aplicação de exemplo de Olá no [começar a utilizar as ferramentas de base de dados elástica](sql-database-elastic-scale-get-started.md).
* Em alternativa, consulte [existente Migrar bases de dados de bases de dados de saída tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).
* utilizador Olá precisa de ter permissão ALTER qualquer origem de dados externa. Esta permissão está incluído com a permissão do Olá ALTER DATABASE.
* As permissões de ALTER qualquer origem de dados externas são toohello toorefer necessários subjacente a origem de dados.

## <a name="overview"></a>Descrição geral
Estas instruções criar representação de metadados de Olá da sua camada de dados fragmentados Olá consulta elástico da base de dados. 

1. [CRIAR CHAVE MESTRA](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CRIAR UM ÂMBITO DE BASE DE DADOS CREDENCIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CRIAR ORIGEM DE DADOS EXTERNA](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CRIAR TABELA EXTERNA](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 Criar chave mestra de base de dados no âmbito e as credenciais
credencial de Olá é utilizado pelo Olá consulta elástico tooconnect tooyour remoto as bases de dados.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Certifique-se de que Olá *"\<username\>"* não inclui quaisquer *"@servername"* sufixo. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 Criar origens de dados externas
Sintaxe:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Exemplo
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Obter a lista de Olá de origens de dados externas atual: 

    select * from sys.external_data_sources; 

origem de dados externa Olá referencia o mapa de partições horizontais. Uma consulta elástica, em seguida, utiliza a origem de dados externa Olá e Olá subjacente partições horizontais mapa tooenumerate Olá bases de dados que participam na camada de dados de Olá. Olá mesmas credenciais são mapa de partições horizontais utilizadas tooread Olá e tooaccess Olá dados shards Olá durante o processamento de Olá de uma consulta elástico. 

## <a name="13-create-external-tables"></a>1.3 criar tabelas externas
Sintaxe:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Exemplo**

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

Obter a lista de Olá de tabelas externas da base de dados atual Olá: 

    SELECT * from sys.external_tables; 

tabelas externas toodrop:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Observações
Olá dados\_cláusula origem define a origem de dados externa Olá (um mapa de partições horizontais) que é utilizada para a tabela externa Olá.  

Olá esquema\_nome e o OBJETO\_cláusulas nome mapeiam uma tabela tooa de definição de tabela externa do Olá de um esquema diferente. Se for omitido, o esquema Olá do objeto remoto Olá é assumida toobe "dbo" e o respetivo nome é assumido o nome de tabela externa toobe toohello idênticos a ser definido. Isto é útil se Olá o nome da sua tabela remota já foi atribuído na base de dados de olá onde pretende tabela externa de Olá toocreate. Por exemplo, pretende toodefine tooget uma tabela externa uma vista de agregação de vistas de catálogo ou camada DMVs nos seus dados expandidos terminar. Uma vez que as vistas de catálogo e DMVs já existem localmente, não é possível utilizar os respetivos nomes para a definição de tabela externa Olá. Em vez disso, utilize um nome diferente e utilizar a vista de catálogo a Olá ou Olá nome do DMV no Olá esquema\_nome e/ou OBJETO\_cláusulas de nome. (Consulte Exemplo Olá abaixo). 

cláusula de distribuição Olá Especifica a distribuição de dados de Olá utilizada para esta tabela. processador de consultas Olá utiliza informações Olá fornecidas Olá distribuição cláusula toobuild Olá mais eficientes consulta planos.  

1. **A** significa dados horizontalmente estão particionados em bases de dados de Olá. Olá, chave de criação de partições para distribuição de dados de Olá é Olá **< sharding_column_name >** parâmetro.
2. **REPLICADO** significa que existem idênticas cópias da tabela de Olá em cada base de dados. É o tooensure responsabilidade réplicas Olá são idênticas em bases de dados de Olá.
3. **ARREDONDAR\_Round ROBIN** significa nessa tabela Olá horizontalmente partições utilizando um método de distribuição de aplicações dependentes. 

**Referência de camada de dados**: DDL da tabela externa Olá refere-se a origem de dados externa tooan. origem de dados externa Olá Especifica um mapa de partições horizontais que disponibiliza tabela externa Olá Olá informações necessárias toolocate todas as bases de dados de Olá na sua camada de dados. 

### <a name="security-considerations"></a>Considerações de segurança
Os utilizadores com a tabela externa do acesso toohello automaticamente obterem acesso toohello subjacente tabelas remotas sob credenciais de Olá especificado na definição de origem de dados externas Olá. Evite indesejada elevação de privilégios através de credencial de Olá Olá externo da origem de dados. Utilize GRANT ou REVOKE para uma tabela externa como se fosse uma tabela normal.  

Assim que definiu a sua origem de dados externos e as tabelas externas, agora pode utilizar o T-SQL completo sobre as tabelas externas.

## <a name="example-querying-horizontal-partitioned-databases"></a>Exemplo: consultar as bases de dados de particionadas horizontais
Olá seguinte consulta efetua uma junção de três vias entre armazéns, encomendas pendentes e linhas de ordem e utiliza vários agregados e um filtro seletivo. Pressupõe que (1) horizontal partições (fragmentação) e (2) se armazéns, as ordens de linhas de ordem, sendo pela coluna de id de armazém Olá, e essa consulta elástico Olá pode colocalizar Olá associações em shards Olá e processar Olá dispendiosas parte consulta Olá Olá shards em paralelo. 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Procedimento para execução remota de T-SQL armazenado: sp\_execute_remote
Consulta elástica também apresenta um procedimento armazenado que fornece acesso direto toohello shards. Olá procedimento armazenado é chamado [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) e podem ser utilizados tooexecute de procedimentos armazenados remoto ou um código de T-SQL em bases de dados remoto Olá. Demora Olá os seguintes parâmetros: 

* Nome da origem de dados (nvarchar): nome de Olá Olá externo da origem de dados do tipo RDBMS. 
* Consulta (nvarchar): Olá T-SQL consulta toobe executada em cada partição horizontal. 
* Declaração de parâmetro (nvarchar) - opcional: de cadeia com as definições de tipo de dados para os parâmetros de Olá utilizadas no parâmetro de consulta Olá (como sp_executesql). 
* Lista de valores de parâmetro - opcional: lista de valores separados por vírgulas de valores de parâmetros (por exemplo, sp_executesql).

Olá sp\_executar\_remota utiliza Olá fornecida Olá invocação parâmetros tooexecute Olá fornecido instrução T-SQL em bases de dados remoto Olá de origem de dados externa. Utiliza credenciais Olá Olá dados externos origem tooconnect toohello shardmap Gestor da base de dados e as bases de dados remoto Olá.  

Exemplo: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Conectividade de ferramentas
Utilizar regular tooconnect de cadeias de ligação do SQL Server da aplicação, dados e BI integração ferramentas toohello base de dados com as definições de tabela externa. Certifique-se de que o SQL Server é suportada como uma origem de dados para a ferramenta. Olá elástico consultar base de dados como qualquer outra ferramenta do SQL Server da base de dados ligada toohello de referência, em seguida e utilize as tabelas externas da sua aplicação ou a ferramenta como se estivessem tabelas locais. 

## <a name="best-practices"></a>Melhores práticas
* Certifique-se de que a base de dados de ponto final de consulta elástico Olá foi indicado o base de dados do access toohello shardmap e todas as partições horizontais através de Olá firewalls de BD do SQL.  
* Validar ou impor a distribuição de dados de Olá definida pela tabela externa Olá. Se a distribuição de dados real é diferente da distribuição Olá especificada na definição de tabela, as suas consultas poderão produzir resultados inesperados. 
* Consulta elástica atualmente não efetuar a eliminação de partições horizontais quando predicados sobre a chave de fragmentação Olá permitiria-toosafely excluir determinadas shards de processamento.
* Consulta elástica funciona melhor para consultas onde é possível efetuar a maioria do cálculo de Olá shards Olá. Obter normalmente Olá melhor desempenho das consultas com predicados de filtro seletiva que pode ser avaliado em shards Olá ou associações através de Olá a criação de partições de chaves que podem ser executadas de forma a partição alinhada em todas as partições horizontais. Outros padrões de consulta podem precisar de grandes quantidades de tooload dos dados a partir do nó principal do Olá shards toohello e podem efetuar mal

## <a name="next-steps"></a>Passos seguintes

* Para obter uma descrição geral da consulta elástica, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).
* Para um tutorial de criação de partições vertical, consulte [introdução à consulta de base de dados em vários locais (criação de partições vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Para consultas de sintaxe e exemplos de dados verticalmente particionadas, consulte [consultar verticalmente particionada dados)](sql-database-elastic-query-vertical-partitioning.md)
* Para um tutorial horizontal criação de partições (fragmentação), consulte [como começar a consultar elástico (fragmentação) de partições horizontais](sql-database-elastic-query-getting-started.md).
* Consulte [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução de Transact-SQL num único remoto SQL Database do Azure ou um conjunto de bases de dados que servem como shards num esquema de partições horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
