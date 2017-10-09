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
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Consultar em bases de dados de nuvem com diferentes esquemas (pré-visualização)
![Consultar em tabelas de bases de dados diferentes][1]

Verticalmente particionada bases de dados utilizam conjuntos diferentes de tabelas de bases de dados diferentes. Isto significa que o esquema dessa Olá é diferente em bases de dados diferentes. Por exemplo, todas as tabelas de inventário são numa base de dados enquanto todas as tabelas relacionadas com a gestão de contas numa segunda base de dados. 

## <a name="prerequisites"></a>Pré-requisitos
* utilizador Olá precisa de ter permissão ALTER qualquer origem de dados externa. Esta permissão está incluído com a permissão do Olá ALTER DATABASE.
* As permissões de ALTER qualquer origem de dados externas são toohello toorefer necessários subjacente a origem de dados.

## <a name="overview"></a>Descrição geral

> [!NOTE]
> Ao contrário com criação de partições horizontais, estas instruções DDL depende da definição de uma camada de dados com um mapa de partições horizontais através da biblioteca de clientes de base de dados elástica Olá.
>

1. [CRIAR CHAVE MESTRA](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CRIAR UM ÂMBITO DE BASE DE DADOS CREDENCIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CRIAR ORIGEM DE DADOS EXTERNA](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CRIAR TABELA EXTERNA](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Criar chave mestra de base de dados no âmbito e as credenciais
credencial de Olá é utilizado pelo Olá consulta elástico tooconnect tooyour remoto as bases de dados.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Certifique-se de que Olá `<username>` não inclui quaisquer **"@servername"** sufixo. 
>

## <a name="create-external-data-sources"></a>Criar origens de dados externas
Sintaxe:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> parâmetro de tipo Olá tem de ser definido demasiado**RDBMS**. 
>

### <a name="example"></a>Exemplo
Olá exemplo a seguir ilustra utilização Olá Olá instrução CREATE para origens de dados externas. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

lista de Olá tooretrieve atual externo de origens de dados: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Tabelas externas
Sintaxe:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Exemplo
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

Olá seguinte exemplo mostra como tooretrieve Olá a lista de tabelas externas da base de dados atual Olá: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Observações
Consulta elástica expande Olá existente tabela externa sintaxe toodefine tabelas externas que utilizam as origens de dados externas do tipo RDBMS. Uma definição de tabela externa para a criação de partições vertical abrange Olá os seguintes aspetos: 

* **Esquema**: DDL da tabela externa Olá define um esquema que podem utilizar as suas consultas. esquema de Olá fornecido na sua definição de tabela externa tem de esquema de Olá toomatch das tabelas de Olá no Olá base de dados remota armazenar dados real Olá. 
* **Referência de base de dados remota**: DDL da tabela externa Olá refere-se a origem de dados externa tooan. origem de dados externa Olá Especifica o nome de servidor lógico de Olá e nome de base de dados de Olá base de dados remota onde Olá tabela real dados são armazenados. 

Tabelas externas do Olá sintaxe toocreate conforme descrito na secção anterior Olá a utilizar uma origem de dados externo, é o seguinte: 

cláusula DATA_SOURCE Olá define a origem de dados externa hello (ou seja, Olá remota da base de dados em caso de criação de partições vertical) que é utilizada para a tabela externa Olá.  

cláusulas SCHEMA_NAME e OBJECT_NAME Olá fornecem Olá capacidade toomap Olá tabela externa definição tooa tabela de um esquema diferente na base de dados remota Olá ou tooa tabela com um nome diferente, respetivamente. Isto é útil se pretender que toodefine uma vista de catálogo tooa de tabela externa ou DMV na sua base de dados remota - ou quaisquer outra situação em que o nome de tabela remota Olá já foi atribuído localmente.  

Olá seguinte instrução DDL ignora uma definição de tabela externa existentes do catálogo local Olá. Não afetam a base de dados remota Olá. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Permissões de tabela externa CREATE/DROP**: são necessárias permissões de ALTER qualquer origem de dados externa para a tabela externa DDL que também é necessário toorefer toohello origem de dados subjacente.  

## <a name="security-considerations"></a>Considerações de segurança
Os utilizadores com a tabela externa do acesso toohello automaticamente obterem acesso toohello subjacente tabelas remotas sob credenciais de Olá especificado na definição de origem de dados externas Olá. Cuidadosamente deve gerir acesso toohello externo tabela tooavoid indesejado elevação de privilégios através de credencial de Olá Olá externo da origem de dados, ordem. Permissões normais do SQL Server podem ser utilizado tooGRANT ou tabela externa do REVOGAR acesso tooan como se fosse uma tabela normal.  

## <a name="example-querying-vertically-partitioned-databases"></a>Exemplo: consultar verticalmente particionada bases de dados
Olá seguinte consulta executa uma associação de três vias entre duas tabelas locais Olá sobre encomendas pendentes e linhas de ordem e tabela remota Olá para os clientes. Este é um exemplo de Olá referência dados caso de utilização da consulta elástico: 

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
Pode utilizar tooconnect de cadeias de ligação do SQL Server regular sua toodatabases de ferramentas de integração de BI e os dados no servidor de base de dados SQL Olá que tenha consulta elástica ativada e tabelas externas definidas. Certifique-se de que o SQL Server é suportada como uma origem de dados para a ferramenta. Em seguida, consulte a base de dados de consulta elástico toohello e as respetivas tabelas externas, tal como quaisquer outro do SQL Server da base de dados que seria se ligar toowith a ferramenta. 

## <a name="best-practices"></a>Melhores práticas
* Certifique-se de que a base de dados de ponto final de consulta elástico Olá foi indicado acesso toohello remota da base de dados ao permitir o acesso para serviços do Azure na sua configuração de firewall da BD do SQL. Certifique-se também essa credencial Olá fornecido nos dados externos Olá a definição de origem pode iniciar com êxito na base de dados remoto Olá e tem Olá permissões tooaccess Olá remoto tabela.  
* Consulta elástica funciona melhor para consultas onde a maioria do cálculo de Olá pode ser efetuada em bases de dados remoto Olá. Normalmente, obter Olá melhor desempenho das consultas com predicados de filtro seletiva que pode ser avaliado em bases de dados remoto Olá ou associações que podem ser efetuadas na base de dados remota Olá completamente. Outros padrões de consulta podem precisar de grandes quantidades de tooload dos dados da base de dados remoto Olá e podem efetuar mal. 

## <a name="next-steps"></a>Passos seguintes

* Para obter uma descrição geral da consulta elástica, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).
* Para um tutorial de criação de partições vertical, consulte [introdução à consulta de base de dados em vários locais (criação de partições vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Para um tutorial horizontal criação de partições (fragmentação), consulte [como começar a consultar elástico (fragmentação) de partições horizontais](sql-database-elastic-query-getting-started.md).
* Para consultas de sintaxe e exemplos de dados particionadas horizontalmente, consulte [consultar horizontalmente particionada dados)](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução de Transact-SQL num único remoto SQL Database do Azure ou um conjunto de bases de dados que servem como shards num esquema de partições horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
