---
Título: aaa "lesson tutorial do Azure Analysis Services 5: criar colunas calculadas | Descrição da Microsoft Docs": descreve a forma como toocreate calculada colunas do projeto tutorial do Olá Azure Analysis Services. serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '

MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 06/01/2017 Author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Lição 5: Criar colunas calculadas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, irá criar dados no seu modelo ao adicionar colunas calculadas. Pode criar colunas calculadas (como colunas personalizadas) ao utilizar a obter dados, utilizando o Editor de consultas Olá ou posterior no designer como modelo o Olá fazer aqui. toolearn mais, consulte [calculado colunas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Pode criar cinco novas colunas calculadas em três tabelas diferentes. passos de Olá são ligeiramente diferentes para cada tarefa, existem várias formas toocreate colunas a mostrar, renomeie-os e colocá-los em várias localizações numa tabela.  

Nesta lição também usa pela primeira vez o Data Analysis Expressions (DAX). DAX é uma linguagem especial para criar expressões de fórmulas altamente personalizáveis para modelos de tabela. Neste tutorial, utilize toocreate calculado colunas, medidas e filtros de função DAX. toolearn mais, consulte [DAX na criação de modelos em tabela](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Estimado tempo toocomplete este lesson: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem. Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Criar colunas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Criar uma coluna calculada de MonthCalendar na tabela de DimDate Olá  
  
1.  Clique em Olá **modelo** menu > **vista do modelo** > **vista de dados**.  
  
    Só é possível criar colunas calculadas utilizando o estruturador de modelo de Olá na vista de dados.  
  
2.  No estruturador de modelo de Olá, clique em Olá **DimDate** tabela (separador).  
  
3.  Contexto Olá **CalendarQuarter** cabeçalho da coluna e, em seguida, clique em **Inserir coluna**.  
  
    Uma nova coluna com o nome **1 de coluna calculada** é inserido toohello esquerda da vírgula Olá **trimestre de calendário** coluna.  
  
4.  Na barra de fórmulas Olá acima tabela Olá, escreva Olá seguinte fórmula DAX: Olá, ajuda a conclusão automática, escreva os nomes completamente qualificados de colunas e tabelas e listas Olá funções que estão disponíveis.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Os valores, em seguida, são povoados para todas as linhas de Olá na coluna calculada Olá. Se se deslocar para baixo através da tabela de Olá, verá linhas podem ter valores diferentes para esta coluna, com base nos dados de Olá em cada linha.    
  
5.  Mudar o nome desta coluna demasiado**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
coluna calculada de MonthCalendar Olá fornece um nome para o mês ordenável.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Criar uma DayOfWeek a coluna calculada na tabela de DimDate Olá  
  
1.  Com Olá **DimDate** tabela ainda ativo, clique em Olá **coluna** e, em seguida, clique em **Add Column**.  
  
2.  Na barra de fórmulas Olá, escreva Olá seguinte fórmula:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Quando tiver terminado a construção fórmula Olá, prima ENTER. coluna nova Olá é adicionada toohello extremidade direita da tabela de Olá.  
  
3.  Mudar o nome de coluna Olá demasiado**DayOfWeek**.  
  
4.  Clique no cabeçalho de coluna Olá e, em seguida, arraste coluna Olá entre Olá **EnglishDayNameOfWeek** coluna e Olá **DayNumberOfMonth** coluna.  
  
    > [!TIP]  
    > Mover as colunas na tabela torna mais fácil toonavigate.  
  
a coluna calculada da DayOfWeek Olá fornece um nome ordenável dia Olá da semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Criar uma coluna calculada ProductSubcategoryName na tabela de DimProduct Olá  
  
  
1.  No Olá **DimProduct** tabela, desloque-se toohello mais à direita da tabela de Olá. Nome da coluna do aviso Olá mais à direita **Add Column** (em itálico), clique no cabeçalho de coluna Olá.  
  
2.  Na barra de fórmulas Olá, escreva Olá seguinte fórmula:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Mudar o nome de coluna Olá demasiado**ProductSubcategoryName**.  
  
a coluna calculada da ProductSubcategoryName Olá é utilizado toocreate hierarquia na tabela de DimProduct Olá, incluindo os dados da coluna de EnglishProductSubcategoryName Olá na tabela de DimProductSubcategory Olá. Hierarquias não podem abranger mais de uma tabela. Na lição 9, irá criar hierarquias.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Criar uma coluna calculada ProductCategoryName na tabela de DimProduct Olá  
  
1.  Com Olá **DimProduct** tabela ainda ativo, clique em Olá **coluna** e, em seguida, clique em **Add Column**.  
  
2.  Na barra de fórmulas Olá, escreva Olá seguinte fórmula:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Mudar o nome de coluna Olá demasiado**ProductCategoryName**.  
  
a coluna calculada da ProductCategoryName Olá é utilizado toocreate hierarquia na tabela de DimProduct Olá, incluindo os dados da coluna de EnglishProductCategoryName Olá na tabela de DimProductCategory Olá. Hierarquias não podem abranger mais de uma tabela.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Criar uma coluna calculada margem na tabela de FactInternetSales Olá  
  
1.  No estruturador de modelo de Olá, selecione Olá **FactInternetSales** tabela.  
  
2.  Criar uma nova coluna calculada entre Olá **SalesAmount** coluna e Olá **TaxAmt** coluna.  
  
3.  Na barra de fórmulas Olá, escreva Olá seguinte fórmula:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Mudar o nome de coluna Olá demasiado**margem**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    a coluna calculada da margem Olá é utilizado tooanalyze lucros margens para cada venda.  
  
## <a name="whats-next"></a>Passos seguintes?
[Lição 6: Criar medidas](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
