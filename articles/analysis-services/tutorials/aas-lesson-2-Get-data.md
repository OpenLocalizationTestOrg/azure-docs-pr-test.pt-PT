---
Título: aaa "lesson tutorial do Azure Analysis Services 2: obter dados | Descrição da Microsoft Docs": descreve a forma como tooget e importar dados Olá projeto tutorial Azure Analysis Services. serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '

MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 06/01/2017 Author: owend
---

# <a name="lesson-2-get-data"></a>Lição 2: Obter dados

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Este lesson, utilize obter dados no SSDT tooconnect toohello AdventureWorksDW2014 exemplo da base de dados, selecione os dados, pré-visualização e filtro e, em seguida, importar para a sua área de trabalho do modelo.  
  
Através de Obter dados, pode importar dados de uma ampla variedade de origens: Base de Dados SQL do Azure, Oracle, Sybase, OData Feed, Teradata, ficheiros e muito mais. Os dados também podem ser consultados através de uma expressão de fórmula Power Query M.
  
Estimado tempo toocomplete este lesson: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem. Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 1: criar um novo projeto de modelo em tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma ligação  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate uma base de dados de toohello AdventureWorksDW2014 de ligação  
  
1.  No Explorador de modelos de tabela, clique com botão direito do rato em **Origens de dados** > **Importar a partir de origens de dados**.  
  
    Isto inicia obter dados, o que orienta-o origem de dados de tooa ligação. Se não vir Explorador do modelo de tabela, no **Explorador de soluções**, faça duplo clique em **Model.bim** modelo de Olá tooopen no estruturador de Olá. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  Em Obter dados, clique em **Base de dados** > **Base de dados do SQL Server** > **Ligar**.  
  
3.  No Olá **base de dados do SQL Server** caixa de diálogo, em **servidor**, escreva o nome de hello do servidor de olá onde instalou a base de dados de Olá AdventureWorksDW2014 e, em seguida, clique em **Connect**.  

4.  Quando lhe forem pedidas credenciais tooenter, precisa de credenciais de Olá toospecify Analysis Services utiliza tooconnect toohello origem de dados quando importar e processar dados. No **Modo de representação**, selecione **Representar a conta**, insira as credenciais e, em seguida, clique em **Ligar**. É recomendado que utilizar uma conta em que a palavra-passe de Olá não expira.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > A utilização de uma conta de utilizador do Windows e a palavra-passe fornece o método mais seguro do Olá ligação tooa da origem de dados.
  
5.  No navegador, selecione Olá **AdventureWorksDW2014** da base de dados e, em seguida, clique em **OK**. Esta ação cria a base de dados do Olá ligação toohello. 
  
6.  No navegador, selecione Olá a caixa de verificação para Olá seguintes tabelas: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Depois de clicar em OK, é aberto o Editor de consultas. Na secção seguinte, Olá, selecione apenas os dados de Olá pretende tooimport.

  
## <a name="filter-hello-table-data"></a>Filtrar dados da tabela Olá  
As tabelas na base de dados de exemplo Olá AdventureWorksDW2014 têm dados que não não necessário tooinclude no seu modelo. Sempre que possível, quer toofilter enviados dados desnecessários toosave no-memória espaço utilizado pelo modelo de Olá. Filtrar alguns dos colunas Olá de tabelas, de modo não a importados para o Olá área de trabalho da base de dados ou base de dados de modelo de Olá depois foi implementada. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>dados da tabela Olá toofilter antes de importar  
  
1.  No Editor de consultas, selecione Olá **DimCustomer** tabela. É apresentada uma vista da tabela de DimCustomer Olá na origem de dados Olá (AdventureWorksDWQ2014 exemplo base de dados). 
  
2.  Multisseleção (Ctrl + clique) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation** e, em seguida, clique com botão direito do rato e clique em **Remover colunas**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Uma vez que Olá os valores para estas colunas não são relevantes tooInternet análise de vendas, há tooimport sem necessidade destas colunas. A eliminação de colunas desnecessárias torna seu modelo menor e mais eficiente.  
  
4.  Filtre Olá restantes tabelas removendo Olá colunas de cada tabela a seguir:  
    
    **DimDate**
    
      |Coluna|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Coluna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Coluna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Coluna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Coluna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Coluna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Importar as tabelas de Olá selecionado e dados da coluna  
Agora que já pré-visualizado e filtrados dados desnecessários, pode importar rest Olá dos dados de Olá que pretender. Assistente de Olá importa dados de tabela de Olá juntamente com quaisquer relações entre tabelas. Novas tabelas e colunas são criadas no modelo de Olá e não é possível importar dados que lhe filtrado.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>Olá tooimport selecionar tabelas e os dados da coluna  
  
1.  Examine as suas seleções. Se tudo estiver correto, clique em **Importar**. caixa de diálogo de processamento de dados de Olá mostra o estado de Olá dos dados que está a ser importados da sua origem de dados para a base de dados da área de trabalho.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Clique em **Fechar**.  

  
## <a name="save-your-model-project"></a>Guardar o seu projeto de modelo  
É importante toofrequently guardar o seu projeto de modelo.  
  
#### <a name="toosave-hello-model-project"></a>projeto de modelo de Olá toosave  
  
-   Clique em **Ficheiro** > **Guardar tudo**.  
  
## <a name="whats-next"></a>Passos seguintes?
[Lição 3: Marcar como tabela de datas](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
