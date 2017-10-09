---
<span data-ttu-id="afa38-101">Título: aaa "lesson tutorial do Azure Analysis Services 5: criar colunas calculadas | Descrição da Microsoft Docs": descreve a forma como toocreate calculada colunas do projeto tutorial do Olá Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="afa38-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="afa38-102">serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '</span><span class="sxs-lookup"><span data-stu-id="afa38-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="afa38-103">MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 06/01/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="afa38-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="afa38-104">Lição 5: Criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="afa38-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="afa38-105">Nesta lição, irá criar dados no seu modelo ao adicionar colunas calculadas.</span><span class="sxs-lookup"><span data-stu-id="afa38-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="afa38-106">Pode criar colunas calculadas (como colunas personalizadas) ao utilizar a obter dados, utilizando o Editor de consultas Olá ou posterior no designer como modelo o Olá fazer aqui.</span><span class="sxs-lookup"><span data-stu-id="afa38-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="afa38-107">toolearn mais, consulte [calculado colunas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="afa38-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="afa38-108">Pode criar cinco novas colunas calculadas em três tabelas diferentes.</span><span class="sxs-lookup"><span data-stu-id="afa38-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="afa38-109">passos de Olá são ligeiramente diferentes para cada tarefa, existem várias formas toocreate colunas a mostrar, renomeie-os e colocá-los em várias localizações numa tabela.</span><span class="sxs-lookup"><span data-stu-id="afa38-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="afa38-110">Nesta lição também usa pela primeira vez o Data Analysis Expressions (DAX).</span><span class="sxs-lookup"><span data-stu-id="afa38-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="afa38-111">DAX é uma linguagem especial para criar expressões de fórmulas altamente personalizáveis para modelos de tabela.</span><span class="sxs-lookup"><span data-stu-id="afa38-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="afa38-112">Neste tutorial, utilize toocreate calculado colunas, medidas e filtros de função DAX.</span><span class="sxs-lookup"><span data-stu-id="afa38-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="afa38-113">toolearn mais, consulte [DAX na criação de modelos em tabela](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="afa38-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="afa38-114">Estimado tempo toocomplete este lesson: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="afa38-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="afa38-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="afa38-115">Prerequisites</span></span>  
<span data-ttu-id="afa38-116">Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem.</span><span class="sxs-lookup"><span data-stu-id="afa38-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="afa38-117">Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="afa38-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="afa38-118">Criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="afa38-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="afa38-119">Criar uma coluna calculada de MonthCalendar na tabela de DimDate Olá</span><span class="sxs-lookup"><span data-stu-id="afa38-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="afa38-120">Clique em Olá **modelo** menu > **vista do modelo** > **vista de dados**.</span><span class="sxs-lookup"><span data-stu-id="afa38-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="afa38-121">Só é possível criar colunas calculadas utilizando o estruturador de modelo de Olá na vista de dados.</span><span class="sxs-lookup"><span data-stu-id="afa38-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="afa38-122">No estruturador de modelo de Olá, clique em Olá **DimDate** tabela (separador).</span><span class="sxs-lookup"><span data-stu-id="afa38-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="afa38-123">Contexto Olá **CalendarQuarter** cabeçalho da coluna e, em seguida, clique em **Inserir coluna**.</span><span class="sxs-lookup"><span data-stu-id="afa38-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="afa38-124">Uma nova coluna com o nome **1 de coluna calculada** é inserido toohello esquerda da vírgula Olá **trimestre de calendário** coluna.</span><span class="sxs-lookup"><span data-stu-id="afa38-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="afa38-125">Na barra de fórmulas Olá acima tabela Olá, escreva Olá seguinte fórmula DAX: Olá, ajuda a conclusão automática, escreva os nomes completamente qualificados de colunas e tabelas e listas Olá funções que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="afa38-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="afa38-126">Os valores, em seguida, são povoados para todas as linhas de Olá na coluna calculada Olá.</span><span class="sxs-lookup"><span data-stu-id="afa38-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="afa38-127">Se se deslocar para baixo através da tabela de Olá, verá linhas podem ter valores diferentes para esta coluna, com base nos dados de Olá em cada linha.</span><span class="sxs-lookup"><span data-stu-id="afa38-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="afa38-128">Mudar o nome desta coluna demasiado**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="afa38-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="afa38-130">coluna calculada de MonthCalendar Olá fornece um nome para o mês ordenável.</span><span class="sxs-lookup"><span data-stu-id="afa38-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="afa38-131">Criar uma DayOfWeek a coluna calculada na tabela de DimDate Olá</span><span class="sxs-lookup"><span data-stu-id="afa38-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="afa38-132">Com Olá **DimDate** tabela ainda ativo, clique em Olá **coluna** e, em seguida, clique em **Add Column**.</span><span class="sxs-lookup"><span data-stu-id="afa38-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="afa38-133">Na barra de fórmulas Olá, escreva Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="afa38-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="afa38-134">Quando tiver terminado a construção fórmula Olá, prima ENTER.</span><span class="sxs-lookup"><span data-stu-id="afa38-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="afa38-135">coluna nova Olá é adicionada toohello extremidade direita da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="afa38-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="afa38-136">Mudar o nome de coluna Olá demasiado**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="afa38-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="afa38-137">Clique no cabeçalho de coluna Olá e, em seguida, arraste coluna Olá entre Olá **EnglishDayNameOfWeek** coluna e Olá **DayNumberOfMonth** coluna.</span><span class="sxs-lookup"><span data-stu-id="afa38-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="afa38-138">Mover as colunas na tabela torna mais fácil toonavigate.</span><span class="sxs-lookup"><span data-stu-id="afa38-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="afa38-139">a coluna calculada da DayOfWeek Olá fornece um nome ordenável dia Olá da semana.</span><span class="sxs-lookup"><span data-stu-id="afa38-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="afa38-140">Criar uma coluna calculada ProductSubcategoryName na tabela de DimProduct Olá</span><span class="sxs-lookup"><span data-stu-id="afa38-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="afa38-141">No Olá **DimProduct** tabela, desloque-se toohello mais à direita da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="afa38-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="afa38-142">Nome da coluna do aviso Olá mais à direita **Add Column** (em itálico), clique no cabeçalho de coluna Olá.</span><span class="sxs-lookup"><span data-stu-id="afa38-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="afa38-143">Na barra de fórmulas Olá, escreva Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="afa38-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="afa38-144">Mudar o nome de coluna Olá demasiado**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="afa38-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="afa38-145">a coluna calculada da ProductSubcategoryName Olá é utilizado toocreate hierarquia na tabela de DimProduct Olá, incluindo os dados da coluna de EnglishProductSubcategoryName Olá na tabela de DimProductSubcategory Olá.</span><span class="sxs-lookup"><span data-stu-id="afa38-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="afa38-146">Hierarquias não podem abranger mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="afa38-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="afa38-147">Na lição 9, irá criar hierarquias.</span><span class="sxs-lookup"><span data-stu-id="afa38-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="afa38-148">Criar uma coluna calculada ProductCategoryName na tabela de DimProduct Olá</span><span class="sxs-lookup"><span data-stu-id="afa38-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="afa38-149">Com Olá **DimProduct** tabela ainda ativo, clique em Olá **coluna** e, em seguida, clique em **Add Column**.</span><span class="sxs-lookup"><span data-stu-id="afa38-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="afa38-150">Na barra de fórmulas Olá, escreva Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="afa38-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="afa38-151">Mudar o nome de coluna Olá demasiado**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="afa38-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="afa38-152">a coluna calculada da ProductCategoryName Olá é utilizado toocreate hierarquia na tabela de DimProduct Olá, incluindo os dados da coluna de EnglishProductCategoryName Olá na tabela de DimProductCategory Olá.</span><span class="sxs-lookup"><span data-stu-id="afa38-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="afa38-153">Hierarquias não podem abranger mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="afa38-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="afa38-154">Criar uma coluna calculada margem na tabela de FactInternetSales Olá</span><span class="sxs-lookup"><span data-stu-id="afa38-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="afa38-155">No estruturador de modelo de Olá, selecione Olá **FactInternetSales** tabela.</span><span class="sxs-lookup"><span data-stu-id="afa38-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="afa38-156">Criar uma nova coluna calculada entre Olá **SalesAmount** coluna e Olá **TaxAmt** coluna.</span><span class="sxs-lookup"><span data-stu-id="afa38-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="afa38-157">Na barra de fórmulas Olá, escreva Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="afa38-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="afa38-158">Mudar o nome de coluna Olá demasiado**margem**.</span><span class="sxs-lookup"><span data-stu-id="afa38-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="afa38-160">a coluna calculada da margem Olá é utilizado tooanalyze lucros margens para cada venda.</span><span class="sxs-lookup"><span data-stu-id="afa38-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="afa38-161">Passos seguintes?</span><span class="sxs-lookup"><span data-stu-id="afa38-161">What's next?</span></span>
<span data-ttu-id="afa38-162">[Lição 6: Criar medidas](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="afa38-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
