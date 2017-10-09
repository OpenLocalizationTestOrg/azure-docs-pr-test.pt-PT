---
title: "aaaConnect tooAzure do armazém de dados do SQL Server - VSTS | Microsoft Docs"
description: Consultar o SQL Data Warehouse com o Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="79fa6-103">Ligar tooSQL do armazém de dados com o Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="79fa6-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79fa6-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="79fa6-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="79fa6-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="79fa6-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="79fa6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79fa6-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="79fa6-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="79fa6-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="79fa6-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="79fa6-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="79fa6-109">Utilize o Visual Studio tooquery Azure SQL Data Warehouse em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="79fa6-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="79fa6-110">Este método utiliza a extensão do SQL Server Data Tools (SSDT) Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79fa6-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="79fa6-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79fa6-111">Prerequisites</span></span>
<span data-ttu-id="79fa6-112">toouse neste tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="79fa6-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="79fa6-113">Um SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="79fa6-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="79fa6-114">toocreate um, consulte [criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="79fa6-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="79fa6-115">SSDT para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79fa6-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="79fa6-116">Se tiver o Visual Studio, provavelmente já os tem.</span><span class="sxs-lookup"><span data-stu-id="79fa6-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="79fa6-117">Para obter instruções e opções de instalação, veja [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT] (Instalar o Visual Studio e o SSDT).</span><span class="sxs-lookup"><span data-stu-id="79fa6-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="79fa6-118">Olá nome de servidor SQL completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="79fa6-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="79fa6-119">toofind esta, consulte [ligar tooSQL do armazém de dados][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="79fa6-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="79fa6-120">1. Ligar tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="79fa6-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="79fa6-121">Abra o Visual Studio 2013 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="79fa6-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="79fa6-122">Abra o SQL Server Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="79fa6-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="79fa6-123">toodo este, selecione **vista** > **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server Object Explorer][1]
3. <span data-ttu-id="79fa6-125">Clique em Olá **adicionar SQL Server** ícone.</span><span class="sxs-lookup"><span data-stu-id="79fa6-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Adicionar SQL Server][2]
4. <span data-ttu-id="79fa6-127">Preencha os campos de Olá na janela de tooServer Olá ligar.</span><span class="sxs-lookup"><span data-stu-id="79fa6-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Ligar tooServer][3]
   
   * <span data-ttu-id="79fa6-129">**Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-129">**Server name**.</span></span> <span data-ttu-id="79fa6-130">Introduza Olá **nome do servidor** que identificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="79fa6-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="79fa6-131">**Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-131">**Authentication**.</span></span> <span data-ttu-id="79fa6-132">Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="79fa6-133">**Nome de Utilizador** e **Palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-133">**User Name** and **Password**.</span></span> <span data-ttu-id="79fa6-134">Introduza o nome de utilizador e a palavra-passe, se a Autenticação do SQL Server tiver sido selecionada acima.</span><span class="sxs-lookup"><span data-stu-id="79fa6-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="79fa6-135">Clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-135">Click **Connect**.</span></span>
5. <span data-ttu-id="79fa6-136">tooexplore, expanda o servidor de SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="79fa6-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="79fa6-137">Pode ver as bases de dados de Olá associadas ao servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="79fa6-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="79fa6-138">Expanda AdventureWorksDW tabelas de Olá toosee na sua base de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="79fa6-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorar AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="79fa6-140">2. Executar uma consulta de exemplo</span><span class="sxs-lookup"><span data-stu-id="79fa6-140">2. Run a sample query</span></span>
<span data-ttu-id="79fa6-141">Agora que uma ligação foi estabelecida tooyour base de dados, vamos escrever uma consulta.</span><span class="sxs-lookup"><span data-stu-id="79fa6-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="79fa6-142">Clique com o botão direito do rato na base de dados no SQL Server Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="79fa6-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="79fa6-143">Selecione **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="79fa6-143">Select **New Query**.</span></span> <span data-ttu-id="79fa6-144">É aberta uma nova janela de consulta.</span><span class="sxs-lookup"><span data-stu-id="79fa6-144">A new query window opens.</span></span>
   
    ![Nova consulta][5]
3. <span data-ttu-id="79fa6-146">Copie esta consulta TSQL para a janela de consulta Olá:</span><span class="sxs-lookup"><span data-stu-id="79fa6-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="79fa6-147">Execute consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="79fa6-147">Run hello query.</span></span> <span data-ttu-id="79fa6-148">toodo, clique seta de Olá verde ou utilize Olá seguir atalho: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="79fa6-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Executar consulta][6]
5. <span data-ttu-id="79fa6-150">Observe os resultados da consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="79fa6-150">Look at hello query results.</span></span> <span data-ttu-id="79fa6-151">Neste exemplo, a tabela do Olá FactInternetSales tem 60398 linhas.</span><span class="sxs-lookup"><span data-stu-id="79fa6-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados da consulta][7]

## <a name="next-steps"></a><span data-ttu-id="79fa6-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="79fa6-153">Next steps</span></span>
<span data-ttu-id="79fa6-154">Agora que pode ligar e consultar, experimente [visualizar Olá dados com o PowerBI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="79fa6-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="79fa6-155">tooconfigure o ambiente para a autenticação do Azure Active Directory, consulte [autenticar tooSQL do armazém de dados][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="79fa6-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
