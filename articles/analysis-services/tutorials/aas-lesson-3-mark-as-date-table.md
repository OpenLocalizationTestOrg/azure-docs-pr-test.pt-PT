---
Título: aaa "lesson tutorial do Azure Analysis Services 3: Marcar como tabela de datas | Descrição da Microsoft Docs": descreve a forma como toomark uma data de tabela no projeto tutorial do Olá Azure Analysis Services. serviços: documentationcenter do Analysis Services: ' autor: Gestor minewiskan: erikre editor: ' etiquetas: '

MS. AssetID: MS. Service: devlang do Analysis Services: MS. topic de NA: get-started-article tgt_pltfrm: NA workload: na MS. Date: 06/01/2017 Author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Lição 3: marcar como tabela de datas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Na Lição 2: obter dados, importou uma tabela de dimensões com o nome DimDate. Enquanto no seu modelo esta tabela é denominada DimDate, também pode ser conhecida como uma *tabela de datas* que contém dados de data e hora.  
  
Sempre que utilizar funções de inteligência de tempo DAX, como quando cria medidas mais tarde, deve especificar as propriedades que incluem uma *tabela de datas* e um identificador exclusivo *Coluna de datas* nessa tabela.
  
Neste lesson, marcar a tabela de DimDate de Olá como Olá *tabela de datas* e na coluna de data Olá (na tabela de datas Olá) como Olá *coluna data* (Identificador exclusivo).  

Antes de marcar a coluna de tabela e a data da data Olá, é toodo uma boa altura um pouco os toomake sua toounderstand mais fácil de modelo. Repare na tabela de DimDate Olá uma coluna chamada **FullDateAlternateKey**. Esta coluna contém uma linha para cada dia do ano de calendário cada incluído na tabela de Olá. Utiliza muito esta coluna em fórmulas de medições e relatórios. Porém, FullDateAlternateKey não é um identificador válido para esta coluna. Mudar o nome demasiado**data**, tornando mais fácil tooidentify e incluir em fórmulas. Sempre que possível, é uma boa ideia toorename objetos, como tabelas e colunas toomake-los mais fácil tooidentify no SSDT e o cliente de relatórios de aplicações, como o Power BI e o Excel. 
  
Estimado tempo toocomplete este lesson: **três minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem. Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 2: obter dados](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>coluna de FullDateAlternateKey toorename Olá

1.  No estruturador de modelo de Olá, clique em Olá **DimDate** tabela.

2.  Faça duplo clique em cabeçalho Olá Olá **FullDateAlternateKey** coluna e, em seguida, mude o nome demasiado**data**.

  
### <a name="tooset-mark-as-date-table"></a>tooset marcar como tabela de datas  
  
1.  Selecione Olá **data** coluna e, em seguida, no Olá **propriedades** janela, em **tipo de dados**, certifique-se **data** está selecionada.  
  
2.  Clique em Olá **tabela** menu, em seguida, clique em **data**e, em seguida, clique em **marcar como tabela de datas**.  
  
3.  No Olá **marcar como tabela de datas** Olá caixa de diálogo **data** listbox, selecione de Olá **data** coluna como Olá Identificador exclusivo. Está geralmente selecionado predefinição. Clique em **OK**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Passos seguintes?
[Lição 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md)
  
