---
title: aaaVisualize dados do SQL Data Warehouse com o Power BI Microsoft Azure
description: Visualizar dados do SQL Data Warehouse com o Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="d4ff0-103">Visualizar dados com o Power BI</span><span class="sxs-lookup"><span data-stu-id="d4ff0-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4ff0-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="d4ff0-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="d4ff0-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d4ff0-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="d4ff0-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4ff0-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="d4ff0-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="d4ff0-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="d4ff0-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="d4ff0-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="d4ff0-109">Este tutorial mostra como toouse Power BI tooconnect tooSQL do armazém de dados e criar algumas visualizações básicas.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d4ff0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4ff0-110">Prerequisites</span></span>
<span data-ttu-id="d4ff0-111">toostep com este tutorial, precisa de:</span><span class="sxs-lookup"><span data-stu-id="d4ff0-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="d4ff0-112">Um SQL Data Warehouse pré-carregado com a base de dados do Olá AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="d4ff0-113">tooprovision esta, consulte [criar um SQL Data Warehouse] [ Create a SQL Data Warehouse] e escolha os dados de exemplo de Olá tooload.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="d4ff0-114">Se já tiver um armazém de dados, mas não tiver dados de exemplo, pode [carregar dados de exemplo manualmente][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="d4ff0-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="d4ff0-115">1. Ligar a base de dados tooyour</span><span class="sxs-lookup"><span data-stu-id="d4ff0-115">1. Connect tooyour database</span></span>
<span data-ttu-id="d4ff0-116">tooopen Power BI e ligar a base de dados do tooyour AdventureWorksDW:</span><span class="sxs-lookup"><span data-stu-id="d4ff0-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="d4ff0-117">Inicie sessão em Olá [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d4ff0-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="d4ff0-118">Clique em **Bases de dados SQL** e selecione a sua base de dados AdventureWorks do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Localizar a base de dados][1]
3. <span data-ttu-id="d4ff0-120">Clique no botão 'Abrir no Power BI' de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Botão do Power BI][2]
4. <span data-ttu-id="d4ff0-122">Agora, deverá ver a página de ligação de armazém de dados do SQL Server Olá apresentar o seu endereço de web de base de dados.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="d4ff0-123">Clique em seguinte.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-123">Click next.</span></span>
   
    ![Ligação ao Power BI][3]
5. <span data-ttu-id="d4ff0-125">Introduza o nome de utilizador do Azure SQL server e a palavra-passe e será a base de dados do SQL Data Warehouse tooyour completamente ligado.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Início de sessão no Power BI][4]
6. <span data-ttu-id="d4ff0-127">Assim que o se se inscreveu no Power BI, clique em conjunto de dados no painel esquerdo Olá Olá AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="d4ff0-128">Esta ação irá abrir a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-128">This will open hello database.</span></span>
   
    ![No Power BI, abrir AdventureWorksDW][5]

## <a name="2-create-a-report"></a><span data-ttu-id="d4ff0-130">2. Criar um relatório</span><span class="sxs-lookup"><span data-stu-id="d4ff0-130">2. Create a report</span></span>
<span data-ttu-id="d4ff0-131">Está agora prontos toouse Power BI tooanalyze os dados de exemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="d4ff0-132">análise de Olá tooperform, a AdventureWorksDW tem uma vista denominada AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="d4ff0-133">Esta vista contém algumas das métricas principais de Olá para analisar as vendas Olá da empresa Olá.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="d4ff0-134">toocreate um mapa do montante de vendas em conformidade com o código de toopostal, no painel direito de campos de Olá, clique em Olá tooexpand de vista AggregateSales-lo.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="d4ff0-135">Clique em Olá PostalCode e SalesAmount colunas tooselect-los.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![No Power BI, selecionar AggregateSales][6]
   
    <span data-ttu-id="d4ff0-137">O Power BI reconhece automaticamente estes dados geográficos e coloca-os num mapa para si.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mapa do Power BI][7]
2. <span data-ttu-id="d4ff0-139">Este passo cria um gráfico de barras que mostra a quantidade de vendas por receitas de cliente.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="d4ff0-140">toocreate este toohello aceda expandido vista AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="d4ff0-141">Clique no campo SalesAmount Olá.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="d4ff0-142">Arraste Olá receitas de cliente campo toohello esquerda e solte-o no eixo.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![No Power BI, selecionar eixo][8]
   
    <span data-ttu-id="d4ff0-144">Iremos movidos gráfico de barras Olá através de Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-144">We moved hello bar chart over hello left.</span></span>
   
    ![Barra do Power BI][9]
3. <span data-ttu-id="d4ff0-146">Este passo cria um gráfico de linhas que mostra o montante de vendas por data de encomenda.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="d4ff0-147">toocreate este toohello aceda expandido vista AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="d4ff0-148">Clique em SalesAmount e OrderDate.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="d4ff0-149">Na coluna visualizações de Olá clique ícone de gráfico de linhas de Olá; Este é o primeiro ícone de Olá na segunda linha de Olá em visualizações.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![No Power BI, selecionar gráfico de linhas][10]
   
    <span data-ttu-id="d4ff0-151">Tem agora um relatório que mostra as três visualizações diferentes dos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Linha do Power BI][11]

<span data-ttu-id="d4ff0-153">Pode guardar o seu progresso em qualquer altura, clicando em **Ficheiro** e selecionando **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d4ff0-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ff0-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d4ff0-154">Next steps</span></span>
<span data-ttu-id="d4ff0-155">Agora que iremos toowarm algum tempo cópias de segurança com dados de exemplo de Olá, consulte como demasiado[desenvolver][develop], [carregar][load], ou [ migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="d4ff0-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="d4ff0-156">Ou observe Olá [Web site do Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="d4ff0-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
