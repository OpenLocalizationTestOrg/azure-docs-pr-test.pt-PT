---
title: "aaaHow tooview relacionados com os recursos de dados no catálogo de dados do Azure | Microsoft Docs"
description: "Este artigo explica como tooview relacionados com os recursos de dados de um recurso de dados selecionadas no catálogo de dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="f6b17-103">Como tooview relacionados com os recursos de dados no catálogo de dados do Azure?</span><span class="sxs-lookup"><span data-stu-id="f6b17-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="f6b17-104">Catálogo de dados do Azure permite-lhe tooview dados ativos relacionados tooa selecionado dados ativos e vista relações entre eles.</span><span class="sxs-lookup"><span data-stu-id="f6b17-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="f6b17-105">Origens de dados suportadas</span><span class="sxs-lookup"><span data-stu-id="f6b17-105">Supported data sources</span></span> 
<span data-ttu-id="f6b17-106">Quando registar recursos de dados da Olá as seguintes origens de dados, o catálogo de dados do Azure regista automaticamente metadados sobre relações de associação entre os recursos de dados de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="f6b17-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="f6b17-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f6b17-107">SQL Server</span></span>
- <span data-ttu-id="f6b17-108">Base de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f6b17-108">Azure SQL Database</span></span>
- <span data-ttu-id="f6b17-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="f6b17-109">MySQL</span></span>
- <span data-ttu-id="f6b17-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="f6b17-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="f6b17-111">Ver dados relacionados ativos</span><span class="sxs-lookup"><span data-stu-id="f6b17-111">View related data assets</span></span>
<span data-ttu-id="f6b17-112">recursos de dados de tooview que estão relacionados tooa selecionado conjunto de dados, utilize Olá **relações** separador conforme mostrado no Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="f6b17-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Catálogo de dados do Azure - ver relacionados com os recursos de dados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="f6b17-114">Neste exemplo, existem duas relações para Olá selecionado **ProductSubcategory** recurso de dados:</span><span class="sxs-lookup"><span data-stu-id="f6b17-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="f6b17-115">ProductSubcategoryID a coluna da tabela de produto Olá tem uma relação de chave externa com ProductSubcategoryID coluna da tabela de ProductSubcategory Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="f6b17-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="f6b17-116">ProductCategoryID a coluna da tabela de ProductSubCategory Olá tem uma relação de chave externa com ProductCategoryID coluna da tabela de ProductCategory Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="f6b17-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b17-117">Tenha em atenção a direção de Olá da seta de Olá na vista de árvore de relações de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6b17-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="f6b17-118">toosee mais detalhes, tais como o nome completamente qualificado do Olá da coluna de Olá, mova o rato de Olá sobre e vir um toohello semelhante de pop-up seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="f6b17-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Catálogo de dados do Azure - pop-up de relação](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="f6b17-120">tooinclude relações entre os recursos que já foram registados, volte a registar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="f6b17-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6b17-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f6b17-121">Next steps</span></span>
- [<span data-ttu-id="f6b17-122">Como toomanage recursos de dados</span><span class="sxs-lookup"><span data-stu-id="f6b17-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
