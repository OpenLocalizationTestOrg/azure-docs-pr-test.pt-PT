---
title: "aaaGet começar a utilizar consultas de base de dados em vários locais (criação de partições vertical) | Microsoft Docs"
description: "forma como consulta de base de dados elástica toouse com particionada verticalmente bases de dados"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Começar a utilizar consultas de base de dados em vários locais (criação de partições vertical) (pré-visualização)
A consulta de base de dados elásticas (pré-visualização) para a SQL Database do Azure permite-lhe consultas de T-SQL toorun que abrangem várias bases de dados a utilizar um ponto de ligação única. Este tópico aplica-se demasiado[verticalmente particionada bases de dados](sql-database-elastic-query-vertical-partitioning.md).  

Quando concluído, irá: Saiba como tooconfigure e utilizar uma SQL Database do Azure tooperform consulta que o intervalo de várias bases de dados relacionados. 

Para obter mais informações sobre a funcionalidade de consulta de base de dados elástica Olá, veja [descrição geral de consulta de base de dados elástica do SQL Database do Azure](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Pré-requisitos

Precisa de ter permissão ALTER qualquer origem de dados externa. Esta permissão está incluído com a permissão do Olá ALTER DATABASE. As permissões de ALTER qualquer origem de dados externas são toohello toorefer necessários subjacente a origem de dados.

## <a name="create-hello-sample-databases"></a>Criar Olá bases de dados de exemplo
toostart com, precisamos toocreate duas bases de dados, **clientes** e **ordens**, Olá no mesmo ou lógica num servidor diferente.   

Executar Olá seguindo as consultas do Olá **ordens** Olá toocreate de base de dados **OrderInformation** tabela e a entrada de dados de exemplo de Olá. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Agora, execute a seguinte consulta no Olá **clientes** Olá toocreate de base de dados **CustomerInformation** tabela e a entrada de dados de exemplo de Olá. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Criar objetos de base de dados
### <a name="database-scoped-master-key-and-credentials"></a>Chave mestra do âmbito e as credenciais da base de dados
1. Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.
2. Ligar toohello ordens da base de dados e execute os seguintes comandos T-SQL de Olá:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Olá "nomedeutilizador" e "password" devem ser Olá nome de utilizador e palavra-passe utilizada toologin na base de dados de clientes de Olá.
    A autenticação utilizando o Azure Active Directory com consultas elásticas não é atualmente suportada.

### <a name="external-data-sources"></a>Origens de dados externas
toocreate uma origem de dados externos, execute os seguintes comandos na base de dados do Olá as ordens de Olá: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Tabelas externas
Crie uma tabela externa em Olá ordens base de dados, que corresponde à definição de Olá da tabela de CustomerInformation Olá:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Executar uma consulta de T-SQL da base de dados elástica de exemplo
Assim que definiu a origem de dados externos e as tabelas externas pode agora utilizar tooquery T-SQL as tabelas externas. Execute esta consulta na base de dados do Olá ordens: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Custo
Atualmente, a funcionalidade de consulta de base de dados elástica Olá está incluída no custo Olá da base de dados SQL do Azure.  

Para obter informações sobre preços, consulte [preços da SQL Database](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Passos seguintes

* Para obter uma descrição geral da consulta elástica, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).
* Para consultas de sintaxe e exemplos de dados verticalmente particionadas, consulte [consultar verticalmente particionada dados)](sql-database-elastic-query-vertical-partitioning.md)
* Para um tutorial horizontal criação de partições (fragmentação), consulte [como começar a consultar elástico (fragmentação) de partições horizontais](sql-database-elastic-query-getting-started.md).
* Para consultas de sintaxe e exemplos de dados particionadas horizontalmente, consulte [consultar horizontalmente particionada dados)](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução de Transact-SQL num único remoto SQL Database do Azure ou um conjunto de bases de dados que servem como shards num esquema de partições horizontal.