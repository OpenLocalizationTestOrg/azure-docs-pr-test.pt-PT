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
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="20059-103">Lição 8: Criar perspetivas</span><span class="sxs-lookup"><span data-stu-id="20059-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="20059-104">Nesta lição, irá criar uma perspetiva de vendas na Internet.</span><span class="sxs-lookup"><span data-stu-id="20059-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="20059-105">Uma perspetiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos da empresa ou específicos de aplicações.</span><span class="sxs-lookup"><span data-stu-id="20059-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="20059-106">Quando um utilizador liga tooa modelo através da utilização de uma perspetiva, este vê apenas os objetos modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspetiva.</span><span class="sxs-lookup"><span data-stu-id="20059-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="20059-107">toolearn mais, consulte [Perspetivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="20059-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="20059-108">Olá perspetiva de vendas de Internet que criar neste lesson exclui objeto de tabela Olá DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="20059-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="20059-109">Quando cria uma perspetiva que exclui a determinados objetos de vista, esse objeto continuará a existir no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="20059-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="20059-110">No entanto, não é visível na lista de campos de relatórios do cliente.</span><span class="sxs-lookup"><span data-stu-id="20059-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="20059-111">Colunas calculadas e medidas incluídas numa perspetiva ou não ainda podem ser calculadas a partir de dados de objeto que foram excluídos.</span><span class="sxs-lookup"><span data-stu-id="20059-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="20059-112">objetivo Olá este lesson é toodescribe como toocreate perspetivas e se familiarize com o modelo de tabela Olá ferramentas de criação.</span><span class="sxs-lookup"><span data-stu-id="20059-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="20059-113">Se expandir esta tabelas adicionais do modelo tooinclude mais tarde, pode criar mais perspetivas toodefine diferentes viewpoints do modelo de Olá, por exemplo, inventário e de vendas.</span><span class="sxs-lookup"><span data-stu-id="20059-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="20059-114">Estimado tempo toocomplete este lesson: **cinco minutos**</span><span class="sxs-lookup"><span data-stu-id="20059-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="20059-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="20059-115">Prerequisites</span></span>  
<span data-ttu-id="20059-116">Este tópico faz parte de um tutorial de modelação em tabela que deve ser concluído por ordem.</span><span class="sxs-lookup"><span data-stu-id="20059-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="20059-117">Antes de executar tarefas de Olá neste lesson, deve concluir lesson anterior Olá: [Lesson 7: criar indicadores de desempenho de chave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="20059-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="20059-118">Criar perspetivas</span><span class="sxs-lookup"><span data-stu-id="20059-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="20059-119">toocreate uma perspetiva de vendas da Internet</span><span class="sxs-lookup"><span data-stu-id="20059-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="20059-120">Clique em Olá **modelo** menu > **Perspetivas** > **criar e gerir**.</span><span class="sxs-lookup"><span data-stu-id="20059-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="20059-121">No Olá **Perspetivas** caixa de diálogo, clique em **nova perspetiva**.</span><span class="sxs-lookup"><span data-stu-id="20059-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="20059-122">Faça duplo clique em Olá **nova perspetiva** no cabeçalho de coluna e, em seguida, mude o nome **Internet vendas**.</span><span class="sxs-lookup"><span data-stu-id="20059-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="20059-123">Olá, selecione todas as tabelas de Olá *exceto* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="20059-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="20059-125">Um lesson posterior, utiliza Olá analisar no Excel funcionalidade tootest esta perspetiva.</span><span class="sxs-lookup"><span data-stu-id="20059-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="20059-126">Lista de campos da tabela dinâmica de Excel de Olá inclui cada tabela, exceto a tabela de DimCustomer Olá.</span><span class="sxs-lookup"><span data-stu-id="20059-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="20059-127">Passos seguintes?</span><span class="sxs-lookup"><span data-stu-id="20059-127">What's next?</span></span>
<span data-ttu-id="20059-128">[Lição 9: Criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="20059-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
