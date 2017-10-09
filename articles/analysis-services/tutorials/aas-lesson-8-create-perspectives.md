---
title: AAA "perspetivas do Azure Analysis Services tutorial lesson 8 criar | Microsoft Docs"
description: "Descreve como toocreate perspetivas no Olá projeto tutorial Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Lição 8: Criar perspetivas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, irá criar uma perspetiva de vendas na Internet. Uma perspetiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos da empresa ou específicos de aplicações. Quando um utilizador liga tooa modelo através da utilização de uma perspetiva, este vê apenas os objetos modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspetiva. toolearn mais, consulte [Perspetivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Olá perspetiva de vendas de Internet que criar neste lesson exclui objeto de tabela Olá DimCustomer. Quando cria uma perspetiva que exclui a determinados objetos de vista, esse objeto continuará a existir no modelo de Olá. No entanto, não é visível na lista de campos de relatórios do cliente. Colunas calculadas e medidas incluídas numa perspetiva ou não ainda podem ser calculadas a partir de dados de objeto que foram excluídos.  
  
objetivo Olá este lesson é toodescribe como toocreate perspetivas e se familiarize com o modelo de tabela Olá ferramentas de criação. Se expandir esta tabelas adicionais do modelo tooinclude mais tarde, pode criar mais perspetivas toodefine diferentes viewpoints do modelo de Olá, por exemplo, inventário e de vendas.  
  
Estimado tempo toocomplete este lesson: **cinco minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem. Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 7: criar indicadores de desempenho de chave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Criar perspetivas  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate uma perspetiva de vendas da Internet  
  
1.  Clique em Olá **modelo** menu > **Perspetivas** > **criar e gerir**.  
  
2.  No Olá **Perspetivas** caixa de diálogo, clique em **nova perspetiva**.  
  
3.  Faça duplo clique em Olá **nova perspetiva** no cabeçalho de coluna e, em seguida, mude o nome **Internet vendas**.  
  
4.  Olá, selecione todas as tabelas de Olá *exceto* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    Um lesson posterior, utiliza Olá analisar no Excel funcionalidade tootest esta perspetiva. Lista de campos da tabela dinâmica de Excel de Olá inclui cada tabela, exceto a tabela de DimCustomer Olá.  

## <a name="whats-next"></a>Passos seguintes?
[Lição 9: Criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
