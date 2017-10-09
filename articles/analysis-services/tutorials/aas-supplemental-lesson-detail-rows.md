---
Título: aaa "lesson de suplementar tutorial Azure Analysis Services: linhas detalhadas | Descrição da Microsoft Docs": descreve a forma como toocreate uma expressão de linhas de detalhe no Olá tutorial do Analysis Services do Azure.
serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '

MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 05/26/2017 Author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Lição suplementar - Linhas Detalhadas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Este lesson suplementar, utiliza Olá DAX Editor toodefine uma expressão de linhas de detalhe personalizada. Uma expressão de linhas de detalhe é uma propriedade numa medida, os utilizadores finais a fornecer mais informações sobre os resultados de Olá agregado de uma medida. 
  
Estimado tempo toocomplete este lesson: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico de lição suplementar faz parte de um tutorial de modelação em tabela. Antes de executar tarefas de Olá neste lesson suplementar, deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet vendas concluído.  
  
## <a name="what-do-we-need-toosolve"></a>O que fazer precisamos toosolve?
Vamos ver detalhes de Olá do nosso medida InternetTotalSales, antes de adicionar uma expressão de linhas de detalhe.

1.  No SSDT, clique em Olá **modelo** menu > **analisar no Excel** tooopen Excel e criar uma tabela dinâmica em branco.
  
2.  No **campos PivotTable**, adicionar Olá **InternetTotalSales** medidas da tabela de FactInternetSales Olá demasiado**valores**, **CalendarYear**de Olá DimDate tabela demasiado**colunas**, e **EnglishCountryRegionName** demasiado**linhas**. Nosso tabela dinâmica agora dá-nos resultados de agregados de medidas de InternetTotalSales Olá, regiões e ano. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Na tabela dinâmica Olá, faça duplo clique num valor de agregados de um ano e um nome de região. Aqui iremos duplo clique no valor de Olá para a Austrália e Olá ano 2014. É aberta uma nova folha de cálculo que contém dados, mas os dados não são úteis.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
O que podemos pretende toosee aqui é uma tabela que contém as colunas e linhas de dados que contribuem para toohello agregado resultado da nossa medidas InternetTotalSales. toodo, que pode adicionar uma expressão de linhas de detalhe como uma propriedade de medida Olá.

## <a name="add-a-detail-rows-expression"></a>Adicionar uma expressão de linhas detalhadas

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate uma expressão de linhas de detalhe 
  
1. No SSDT, na grelha de medida da tabela FactInternetSales Olá, clique em Olá **InternetTotalSales** medidas. 

2. No **propriedades** > **detalhe linhas expressão**, clique em Olá do Olá editor botão tooopen DAX Editor.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. No Editor de DAX, introduza Olá seguintes expressão:

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

    Esta expressão Especifica os nomes de colunas, e resultados de medida da tabela de FactInternetSales Olá e tabelas relacionadas são devolvidos quando um utilizador faz duplo clique num resultado numa tabela dinâmica ou relatório agregado.

4. Novamente no Excel, Eliminar folha Olá criada no passo 3, em seguida, faça duplo clique num valor agregado. Neste momento, com uma propriedade de expressão de linhas de detalhe definida para a medida de Olá, uma nova folha abre-se que contêm dados muito mais útil.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Volte a implementar o modelo.

  
## <a name="see-also"></a>Veja Também  
[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Lição suplementar - Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lição suplementar - Hierarquias desbalanceadas](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
