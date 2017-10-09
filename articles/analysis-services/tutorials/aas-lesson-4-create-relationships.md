---
Título: aaa "lesson tutorial do Azure Analysis Services 4: criar relações | Descrição da Microsoft Docs": descreve a forma como toocreate relações na Olá projeto tutorial Azure Analysis Services. serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '

MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 05/26/2017 Author: owend
---
# <a name="lesson-4-create-relationships"></a>Lição 4: Criar relações

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Este lesson, pode verificar as relações de Olá que foram criadas automaticamente quando importou dados e adicionar novas relações entre tabelas diferentes. Uma relação é uma ligação entre duas tabelas estabelece a forma como os dados de Olá nessas tabelas devem ser correlacionados. Por exemplo, tabela de DimProduct Olá e tabela de DimProductSubcategory Olá tem uma relação com base no facto de Olá que cada produto pertence tooa subcategoria. toolearn mais, consulte [relações](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Estimado tempo toocomplete este lesson: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem. Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 3: Marcar como tabela de datas](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Rever relações existentes e adicionar novas  
Quando importar dados utilizando a obter dados, obteve sete tabelas da base de dados do Olá AdventureWorksDW2014. Geralmente, ao importar dados a partir de uma origem relacional, as relações existentes são automaticamente importadas juntamente com dados Olá. No entanto, antes de continuar a criar seu modelo, deve confirmar se as relações entre as tabelas foram criadas adequadamente. Neste tutorial, vai adicionar três relações novas.  
  
#### <a name="tooreview-existing-relationships"></a>relações existentes de tooreview  
  
1.  Clique em Olá **modelo** menu > **vista do modelo** > **vista de diagrama**.  

    Olá designer modelo aparece na vista de diagrama, um formato de gráfico que apresenta todas as tabelas de Olá importados com linhas entre eles. linhas de Olá entre as tabelas indicam as relações de Olá que foram criadas automaticamente quando importou dados Olá.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Inclua como muitas das tabelas de Olá quanto possível através da utilização de controlos de minimapa no canto inferior direito de Olá do designer de modelo Olá. Também pode clique e arraste a localizações de toodifferent tabelas, colocar o próximo tabelas em conjunto ou colocando-los por uma ordem específica. Mover tabelas não afeta as relações de Olá já entre Olá as tabelas. tooview todas as colunas de Olá numa tabela específica, clique e arraste um tooexpand de limite de tabela ou torná-lo mais pequeno.  
  
2.  Clique em linha contínua de Olá entre Olá **DimCustomer** tabela e Olá **DimGeography** tabela. linha contínua de Olá entre estas duas tabelas mostra que esta relação está ativa, ou seja, que é utilizado por predefinição quando se calcular fórmulas DAX.  
  
    Olá aviso **GeographyKey** coluna na Olá **DimCustomer** tabela e Olá **GeographyKey** coluna na Olá **DimGeography** tabela Agora ambos cada aparecem dentro de uma caixa. Estas colunas são utilizadas numa relação de Olá. Olá propriedades da relação são agora também apresentadas Olá **propriedades** janela.  
  
    > [!TIP]  
    > Além disso toousing Olá designer de modelo na vista de diagrama, também pode utilizar Olá gerir relações diálogo caixa tooshow Olá relações entre todas as tabelas num formato de tabela. No Explorador de Modelos em Tabela, clique com o botão direito do rato em **Relações** > **Gerir Relações**.
  
3.  Certifique-se de que Olá seguintes relações criada quando cada uma das tabelas de Olá foram importadas da base de dados do Olá AdventureWorksDW:  
  
    |Ativa|Tabela|Tabela de Pesquisa Relacionada|  
    |----------|---------|------------------------|  
    |Sim|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sim|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sim|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sim|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sim|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se alguma das relações de Olá estão em falta, certifique-se de que o seu modelo inclui Olá seguintes tabelas: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se as tabelas de Olá mesma ligação de origem de dados são importados no separam vezes, quaisquer relações entre as tabelas não são criadas e têm de ser criadas manualmente.  

### <a name="take-a-closer-look"></a>Uma visão mais detalhada
Na vista de diagrama, tenha em atenção uma seta, um asterisco e um número de linhas de Olá que mostram a relação de Olá entre as tabelas.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

seta Olá mostra a direção do filtro de Olá. asterisco Olá mostra que esta tabela for Olá lado muitos no cardinalidade da relação Olá e hello um mostra que esta tabela for Olá lado de Olá relação. Se precisar de tooedit uma relação; Por exemplo, alterar a direção do filtro ou cardinalidade da relação Olá, faça duplo clique Olá relação linha tooopen Olá Editar relação caixa de diálogo.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Estas funcionalidades são destinam-se dados avançados de modelação e são âmbito de Olá fora deste tutorial. toolearn mais, consulte [bidirecional entre os filtros para modelos em tabela do Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

Em alguns casos, poderá ter relações de adicionais toocreate entre tabelas na sua toosupport modelo determinada lógica de negócio. Para este tutorial, terá de toocreate três adicionais as relações entre a tabela FactInternetSales de Olá e tabela de DimDate Olá.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd novas relações entre tabelas  
  
1.  No estruturador de modelo de Olá, no Olá **FactInternetSales** tabela, clique e espere Olá **OrderDate** coluna, em seguida, arraste Olá cursor toohello **data** coluna na Olá  **DimDate** tabela e, em seguida, da versão.  

    Uma linha contínua aparece que mostra que criou uma relação ativa entre Olá **OrderDate** coluna na Olá **Internet vendas** tabela e Olá **data** coluna na Olá **Data** tabela. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Ao criar relações, a direção cardinalidade e filtrar Olá entre a tabela primária Olá e tabela de referência relacionada de Olá é selecionada automaticamente.  
  
2.  No Olá **FactInternetSales** tabela, clique e espere Olá **DueDate** coluna, em seguida, arraste Olá cursor toohello **data** coluna na Olá **DimDate** tabela e, em seguida, da versão.  
  
    Uma linha ponteada aparece que mostra que criou uma relação entre Olá inativa **DueDate** coluna na Olá **FactInternetSales** tabela e Olá **data** coluna Olá **DimDate** tabela. Pode ter várias relações entre tabelas, mas só pode estar ativa uma relação de cada vez. As relações Inativas podem ser efetuadas agregações especial tooperform Active Directory em expressões DAX personalizadas.  
  
3.  Por fim, crie mais uma relação. No Olá **FactInternetSales** tabela, clique e espere Olá **ShipDate** coluna, em seguida, arraste Olá cursor toohello **data** coluna na Olá **DimDate** tabela e, em seguida, da versão.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Passos seguintes?
[Lição 5: Criar colunas calculadas (Lesson 5: Create calculated columns)](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
