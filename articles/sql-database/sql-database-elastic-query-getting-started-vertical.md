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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="c4bcf-103">Começar a utilizar consultas de base de dados em vários locais (criação de partições vertical) (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="c4bcf-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="c4bcf-104">A consulta de base de dados elásticas (pré-visualização) para a SQL Database do Azure permite-lhe consultas de T-SQL toorun que abrangem várias bases de dados a utilizar um ponto de ligação única.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="c4bcf-105">Este tópico aplica-se demasiado[verticalmente particionada bases de dados](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="c4bcf-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="c4bcf-106">Quando concluído, irá: Saiba como tooconfigure e utilizar uma SQL Database do Azure tooperform consulta que o intervalo de várias bases de dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="c4bcf-107">Para obter mais informações sobre a funcionalidade de consulta de base de dados elástica Olá, veja [descrição geral de consulta de base de dados elástica do SQL Database do Azure](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4bcf-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c4bcf-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4bcf-108">Prerequisites</span></span>

<span data-ttu-id="c4bcf-109">Precisa de ter permissão ALTER qualquer origem de dados externa.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="c4bcf-110">Esta permissão está incluído com a permissão do Olá ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="c4bcf-111">As permissões de ALTER qualquer origem de dados externas são toohello toorefer necessários subjacente a origem de dados.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="c4bcf-112">Criar Olá bases de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="c4bcf-112">Create hello sample databases</span></span>
<span data-ttu-id="c4bcf-113">toostart com, precisamos toocreate duas bases de dados, **clientes** e **ordens**, Olá no mesmo ou lógica num servidor diferente.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="c4bcf-114">Executar Olá seguindo as consultas do Olá **ordens** Olá toocreate de base de dados **OrderInformation** tabela e a entrada de dados de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="c4bcf-115">Agora, execute a seguinte consulta no Olá **clientes** Olá toocreate de base de dados **CustomerInformation** tabela e a entrada de dados de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="c4bcf-116">Criar objetos de base de dados</span><span class="sxs-lookup"><span data-stu-id="c4bcf-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="c4bcf-117">Chave mestra do âmbito e as credenciais da base de dados</span><span class="sxs-lookup"><span data-stu-id="c4bcf-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="c4bcf-118">Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="c4bcf-119">Ligar toohello ordens da base de dados e execute os seguintes comandos T-SQL de Olá:</span><span class="sxs-lookup"><span data-stu-id="c4bcf-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="c4bcf-120">Olá "nomedeutilizador" e "password" devem ser Olá nome de utilizador e palavra-passe utilizada toologin na base de dados de clientes de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="c4bcf-121">A autenticação utilizando o Azure Active Directory com consultas elásticas não é atualmente suportada.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="c4bcf-122">Origens de dados externas</span><span class="sxs-lookup"><span data-stu-id="c4bcf-122">External data sources</span></span>
<span data-ttu-id="c4bcf-123">toocreate uma origem de dados externos, execute os seguintes comandos na base de dados do Olá as ordens de Olá:</span><span class="sxs-lookup"><span data-stu-id="c4bcf-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="c4bcf-124">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="c4bcf-124">External tables</span></span>
<span data-ttu-id="c4bcf-125">Crie uma tabela externa em Olá ordens base de dados, que corresponde à definição de Olá da tabela de CustomerInformation Olá:</span><span class="sxs-lookup"><span data-stu-id="c4bcf-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="c4bcf-126">Executar uma consulta de T-SQL da base de dados elástica de exemplo</span><span class="sxs-lookup"><span data-stu-id="c4bcf-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="c4bcf-127">Assim que definiu a origem de dados externos e as tabelas externas pode agora utilizar tooquery T-SQL as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="c4bcf-128">Execute esta consulta na base de dados do Olá ordens:</span><span class="sxs-lookup"><span data-stu-id="c4bcf-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="c4bcf-129">Custo</span><span class="sxs-lookup"><span data-stu-id="c4bcf-129">Cost</span></span>
<span data-ttu-id="c4bcf-130">Atualmente, a funcionalidade de consulta de base de dados elástica Olá está incluída no custo Olá da base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="c4bcf-131">Para obter informações sobre preços, consulte [preços da SQL Database](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="c4bcf-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c4bcf-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c4bcf-132">Next steps</span></span>

* <span data-ttu-id="c4bcf-133">Para obter uma descrição geral da consulta elástica, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4bcf-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c4bcf-134">Para consultas de sintaxe e exemplos de dados verticalmente particionadas, consulte [consultar verticalmente particionada dados)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c4bcf-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="c4bcf-135">Para um tutorial horizontal criação de partições (fragmentação), consulte [como começar a consultar elástico (fragmentação) de partições horizontais](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4bcf-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="c4bcf-136">Para consultas de sintaxe e exemplos de dados particionadas horizontalmente, consulte [consultar horizontalmente particionada dados)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c4bcf-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c4bcf-137">Consulte [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução de Transact-SQL num único remoto SQL Database do Azure ou um conjunto de bases de dados que servem como shards num esquema de partições horizontal.</span><span class="sxs-lookup"><span data-stu-id="c4bcf-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>