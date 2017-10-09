---
<span data-ttu-id="184d1-101">Título: aaa "lesson de suplementar tutorial Azure Analysis Services: linhas detalhadas | Descrição da Microsoft Docs": descreve a forma como toocreate uma expressão de linhas de detalhe no Olá tutorial do Analysis Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="184d1-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="184d1-102">serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '</span><span class="sxs-lookup"><span data-stu-id="184d1-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="184d1-103">MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 05/26/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="184d1-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="184d1-104">Lição suplementar - Linhas Detalhadas</span><span class="sxs-lookup"><span data-stu-id="184d1-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="184d1-105">Este lesson suplementar, utiliza Olá DAX Editor toodefine uma expressão de linhas de detalhe personalizada.</span><span class="sxs-lookup"><span data-stu-id="184d1-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="184d1-106">Uma expressão de linhas de detalhe é uma propriedade numa medida, os utilizadores finais a fornecer mais informações sobre os resultados de Olá agregado de uma medida.</span><span class="sxs-lookup"><span data-stu-id="184d1-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="184d1-107">Estimado tempo toocomplete este lesson: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="184d1-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="184d1-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="184d1-108">Prerequisites</span></span>  
<span data-ttu-id="184d1-109">Este tópico de lição suplementar faz parte de um tutorial de modelação em tabela.</span><span class="sxs-lookup"><span data-stu-id="184d1-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="184d1-110">Antes de executar tarefas de Olá neste lesson suplementar, deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet vendas concluído.</span><span class="sxs-lookup"><span data-stu-id="184d1-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="184d1-111">O que fazer precisamos toosolve?</span><span class="sxs-lookup"><span data-stu-id="184d1-111">What do we need toosolve?</span></span>
<span data-ttu-id="184d1-112">Vamos ver detalhes de Olá do nosso medida InternetTotalSales, antes de adicionar uma expressão de linhas de detalhe.</span><span class="sxs-lookup"><span data-stu-id="184d1-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="184d1-113">No SSDT, clique em Olá **modelo** menu > **analisar no Excel** tooopen Excel e criar uma tabela dinâmica em branco.</span><span class="sxs-lookup"><span data-stu-id="184d1-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="184d1-114">No **campos PivotTable**, adicionar Olá **InternetTotalSales** medidas da tabela de FactInternetSales Olá demasiado**valores**, **CalendarYear**de Olá DimDate tabela demasiado**colunas**, e **EnglishCountryRegionName** demasiado**linhas**.</span><span class="sxs-lookup"><span data-stu-id="184d1-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="184d1-115">Nosso tabela dinâmica agora dá-nos resultados de agregados de medidas de InternetTotalSales Olá, regiões e ano.</span><span class="sxs-lookup"><span data-stu-id="184d1-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="184d1-117">Na tabela dinâmica Olá, faça duplo clique num valor de agregados de um ano e um nome de região.</span><span class="sxs-lookup"><span data-stu-id="184d1-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="184d1-118">Aqui iremos duplo clique no valor de Olá para a Austrália e Olá ano 2014.</span><span class="sxs-lookup"><span data-stu-id="184d1-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="184d1-119">É aberta uma nova folha de cálculo que contém dados, mas os dados não são úteis.</span><span class="sxs-lookup"><span data-stu-id="184d1-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="184d1-121">O que podemos pretende toosee aqui é uma tabela que contém as colunas e linhas de dados que contribuem para toohello agregado resultado da nossa medidas InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="184d1-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="184d1-122">toodo, que pode adicionar uma expressão de linhas de detalhe como uma propriedade de medida Olá.</span><span class="sxs-lookup"><span data-stu-id="184d1-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="184d1-123">Adicionar uma expressão de linhas detalhadas</span><span class="sxs-lookup"><span data-stu-id="184d1-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="184d1-124">toocreate uma expressão de linhas de detalhe</span><span class="sxs-lookup"><span data-stu-id="184d1-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="184d1-125">No SSDT, na grelha de medida da tabela FactInternetSales Olá, clique em Olá **InternetTotalSales** medidas.</span><span class="sxs-lookup"><span data-stu-id="184d1-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="184d1-126">No **propriedades** > **detalhe linhas expressão**, clique em Olá do Olá editor botão tooopen DAX Editor.</span><span class="sxs-lookup"><span data-stu-id="184d1-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="184d1-128">No Editor de DAX, introduza Olá seguintes expressão:</span><span class="sxs-lookup"><span data-stu-id="184d1-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="184d1-129">Esta expressão Especifica os nomes de colunas, e resultados de medida da tabela de FactInternetSales Olá e tabelas relacionadas são devolvidos quando um utilizador faz duplo clique num resultado numa tabela dinâmica ou relatório agregado.</span><span class="sxs-lookup"><span data-stu-id="184d1-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="184d1-130">Novamente no Excel, Eliminar folha Olá criada no passo 3, em seguida, faça duplo clique num valor agregado.</span><span class="sxs-lookup"><span data-stu-id="184d1-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="184d1-131">Neste momento, com uma propriedade de expressão de linhas de detalhe definida para a medida de Olá, uma nova folha abre-se que contêm dados muito mais útil.</span><span class="sxs-lookup"><span data-stu-id="184d1-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="184d1-133">Volte a implementar o modelo.</span><span class="sxs-lookup"><span data-stu-id="184d1-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="184d1-134">Veja Também</span><span class="sxs-lookup"><span data-stu-id="184d1-134">See Also</span></span>  
<span data-ttu-id="184d1-135">[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="184d1-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="184d1-136">Lição suplementar - Segurança dinâmica</span><span class="sxs-lookup"><span data-stu-id="184d1-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="184d1-137">Lição suplementar - Hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="184d1-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
