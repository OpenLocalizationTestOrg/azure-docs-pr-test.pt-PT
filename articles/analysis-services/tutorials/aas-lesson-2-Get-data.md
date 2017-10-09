---
<span data-ttu-id="17e7a-101">Título: aaa "lesson tutorial do Azure Analysis Services 2: obter dados | Descrição da Microsoft Docs": descreve a forma como tooget e importar dados Olá projeto tutorial Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="17e7a-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="17e7a-102">serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '</span><span class="sxs-lookup"><span data-stu-id="17e7a-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="17e7a-103">MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 06/01/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="17e7a-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="17e7a-104">Lição 2: Obter dados</span><span class="sxs-lookup"><span data-stu-id="17e7a-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="17e7a-105">Este lesson, utilize obter dados no SSDT tooconnect toohello AdventureWorksDW2014 exemplo da base de dados, selecione os dados, pré-visualização e filtro e, em seguida, importar para a sua área de trabalho do modelo.</span><span class="sxs-lookup"><span data-stu-id="17e7a-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="17e7a-106">Através de Obter dados, pode importar dados de uma ampla variedade de origens: Base de Dados SQL do Azure, Oracle, Sybase, OData Feed, Teradata, ficheiros e muito mais.</span><span class="sxs-lookup"><span data-stu-id="17e7a-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="17e7a-107">Os dados também podem ser consultados através de uma expressão de fórmula Power Query M.</span><span class="sxs-lookup"><span data-stu-id="17e7a-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="17e7a-108">Estimado tempo toocomplete este lesson: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="17e7a-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="17e7a-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="17e7a-109">Prerequisites</span></span>  
<span data-ttu-id="17e7a-110">Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem.</span><span class="sxs-lookup"><span data-stu-id="17e7a-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="17e7a-111">Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 1: criar um novo projeto de modelo em tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="17e7a-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="17e7a-112">Criar uma ligação</span><span class="sxs-lookup"><span data-stu-id="17e7a-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="17e7a-113">toocreate uma base de dados de toohello AdventureWorksDW2014 de ligação</span><span class="sxs-lookup"><span data-stu-id="17e7a-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="17e7a-114">No Explorador de modelos de tabela, clique com botão direito do rato em **Origens de dados** > **Importar a partir de origens de dados**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="17e7a-115">Isto inicia obter dados, o que orienta-o origem de dados de tooa ligação.</span><span class="sxs-lookup"><span data-stu-id="17e7a-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="17e7a-116">Se não vir Explorador do modelo de tabela, no **Explorador de soluções**, faça duplo clique em **Model.bim** modelo de Olá tooopen no estruturador de Olá.</span><span class="sxs-lookup"><span data-stu-id="17e7a-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="17e7a-118">Em Obter dados, clique em **Base de dados** > **Base de dados do SQL Server** > **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="17e7a-119">No Olá **base de dados do SQL Server** caixa de diálogo, em **servidor**, escreva o nome de hello do servidor de olá onde instalou a base de dados de Olá AdventureWorksDW2014 e, em seguida, clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="17e7a-120">Quando lhe forem pedidas credenciais tooenter, precisa de credenciais de Olá toospecify Analysis Services utiliza tooconnect toohello origem de dados quando importar e processar dados.</span><span class="sxs-lookup"><span data-stu-id="17e7a-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="17e7a-121">No **Modo de representação**, selecione **Representar a conta**, insira as credenciais e, em seguida, clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="17e7a-122">É recomendado que utilizar uma conta em que a palavra-passe de Olá não expira.</span><span class="sxs-lookup"><span data-stu-id="17e7a-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="17e7a-124">A utilização de uma conta de utilizador do Windows e a palavra-passe fornece o método mais seguro do Olá ligação tooa da origem de dados.</span><span class="sxs-lookup"><span data-stu-id="17e7a-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="17e7a-125">No navegador, selecione Olá **AdventureWorksDW2014** da base de dados e, em seguida, clique em **OK**. Esta ação cria a base de dados do Olá ligação toohello.</span><span class="sxs-lookup"><span data-stu-id="17e7a-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="17e7a-126">No navegador, selecione Olá a caixa de verificação para Olá seguintes tabelas: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="17e7a-128">Depois de clicar em OK, é aberto o Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="17e7a-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="17e7a-129">Na secção seguinte, Olá, selecione apenas os dados de Olá pretende tooimport.</span><span class="sxs-lookup"><span data-stu-id="17e7a-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="17e7a-130">Filtrar dados da tabela Olá</span><span class="sxs-lookup"><span data-stu-id="17e7a-130">Filter hello table data</span></span>  
<span data-ttu-id="17e7a-131">As tabelas na base de dados de exemplo Olá AdventureWorksDW2014 têm dados que não não necessário tooinclude no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="17e7a-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="17e7a-132">Sempre que possível, quer toofilter enviados dados desnecessários toosave no-memória espaço utilizado pelo modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="17e7a-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="17e7a-133">Filtrar alguns dos colunas Olá de tabelas, de modo não a importados para o Olá área de trabalho da base de dados ou base de dados de modelo de Olá depois foi implementada.</span><span class="sxs-lookup"><span data-stu-id="17e7a-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="17e7a-134">dados da tabela Olá toofilter antes de importar</span><span class="sxs-lookup"><span data-stu-id="17e7a-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="17e7a-135">No Editor de consultas, selecione Olá **DimCustomer** tabela.</span><span class="sxs-lookup"><span data-stu-id="17e7a-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="17e7a-136">É apresentada uma vista da tabela de DimCustomer Olá na origem de dados Olá (AdventureWorksDWQ2014 exemplo base de dados).</span><span class="sxs-lookup"><span data-stu-id="17e7a-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="17e7a-137">Multisseleção (Ctrl + clique) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation** e, em seguida, clique com botão direito do rato e clique em **Remover colunas**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="17e7a-139">Uma vez que Olá os valores para estas colunas não são relevantes tooInternet análise de vendas, há tooimport sem necessidade destas colunas.</span><span class="sxs-lookup"><span data-stu-id="17e7a-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="17e7a-140">A eliminação de colunas desnecessárias torna seu modelo menor e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="17e7a-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="17e7a-141">Filtre Olá restantes tabelas removendo Olá colunas de cada tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="17e7a-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="17e7a-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="17e7a-142">**DimDate**</span></span>
    
      |<span data-ttu-id="17e7a-143">Coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="17e7a-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="17e7a-144">DateKey</span></span>|  
      |<span data-ttu-id="17e7a-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="17e7a-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="17e7a-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="17e7a-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="17e7a-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="17e7a-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="17e7a-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="17e7a-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="17e7a-150">Coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="17e7a-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="17e7a-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="17e7a-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="17e7a-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="17e7a-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="17e7a-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="17e7a-155">Coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="17e7a-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="17e7a-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="17e7a-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="17e7a-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="17e7a-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="17e7a-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="17e7a-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="17e7a-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="17e7a-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="17e7a-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="17e7a-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="17e7a-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="17e7a-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="17e7a-167">Coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="17e7a-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="17e7a-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="17e7a-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="17e7a-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="17e7a-171">Coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="17e7a-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="17e7a-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="17e7a-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="17e7a-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="17e7a-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="17e7a-175">Coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="17e7a-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="17e7a-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="17e7a-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="17e7a-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="17e7a-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="17e7a-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="17e7a-179"><a name="Import"></a>Importar as tabelas de Olá selecionado e dados da coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="17e7a-180">Agora que já pré-visualizado e filtrados dados desnecessários, pode importar rest Olá dos dados de Olá que pretender.</span><span class="sxs-lookup"><span data-stu-id="17e7a-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="17e7a-181">Assistente de Olá importa dados de tabela de Olá juntamente com quaisquer relações entre tabelas.</span><span class="sxs-lookup"><span data-stu-id="17e7a-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="17e7a-182">Novas tabelas e colunas são criadas no modelo de Olá e não é possível importar dados que lhe filtrado.</span><span class="sxs-lookup"><span data-stu-id="17e7a-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="17e7a-183">Olá tooimport selecionar tabelas e os dados da coluna</span><span class="sxs-lookup"><span data-stu-id="17e7a-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="17e7a-184">Examine as suas seleções.</span><span class="sxs-lookup"><span data-stu-id="17e7a-184">Review your selections.</span></span> <span data-ttu-id="17e7a-185">Se tudo estiver correto, clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="17e7a-186">caixa de diálogo de processamento de dados de Olá mostra o estado de Olá dos dados que está a ser importados da sua origem de dados para a base de dados da área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="17e7a-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="17e7a-188">Clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="17e7a-189">Guardar o seu projeto de modelo</span><span class="sxs-lookup"><span data-stu-id="17e7a-189">Save your model project</span></span>  
<span data-ttu-id="17e7a-190">É importante toofrequently guardar o seu projeto de modelo.</span><span class="sxs-lookup"><span data-stu-id="17e7a-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="17e7a-191">projeto de modelo de Olá toosave</span><span class="sxs-lookup"><span data-stu-id="17e7a-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="17e7a-192">Clique em **Ficheiro** > **Guardar tudo**.</span><span class="sxs-lookup"><span data-stu-id="17e7a-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="17e7a-193">Passos seguintes?</span><span class="sxs-lookup"><span data-stu-id="17e7a-193">What's next?</span></span>
<span data-ttu-id="17e7a-194">[Lição 3: Marcar como tabela de datas](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="17e7a-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
