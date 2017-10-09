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
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Como tooview relacionados com os recursos de dados no catálogo de dados do Azure?
Catálogo de dados do Azure permite-lhe tooview dados ativos relacionados tooa selecionado dados ativos e vista relações entre eles. 

## <a name="supported-data-sources"></a>Origens de dados suportadas 
Quando registar recursos de dados da Olá as seguintes origens de dados, o catálogo de dados do Azure regista automaticamente metadados sobre relações de associação entre os recursos de dados de Olá selecionado. 

- SQL Server
- Base de Dados SQL do Azure
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Ver dados relacionados ativos
recursos de dados de tooview que estão relacionados tooa selecionado conjunto de dados, utilize Olá **relações** separador conforme mostrado no Olá seguinte imagem: 

![Catálogo de dados do Azure - ver relacionados com os recursos de dados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

Neste exemplo, existem duas relações para Olá selecionado **ProductSubcategory** recurso de dados: 

- ProductSubcategoryID a coluna da tabela de produto Olá tem uma relação de chave externa com ProductSubcategoryID coluna da tabela de ProductSubcategory Olá selecionado. 
- ProductCategoryID a coluna da tabela de ProductSubCategory Olá tem uma relação de chave externa com ProductCategoryID coluna da tabela de ProductCategory Olá selecionado.

> [!NOTE]
> Tenha em atenção a direção de Olá da seta de Olá na vista de árvore de relações de Olá.  

toosee mais detalhes, tais como o nome completamente qualificado do Olá da coluna de Olá, mova o rato de Olá sobre e vir um toohello semelhante de pop-up seguinte imagem: 

![Catálogo de dados do Azure - pop-up de relação](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude relações entre os recursos que já foram registados, volte a registar esses recursos.

## <a name="next-steps"></a>Passos seguintes
- [Como toomanage recursos de dados](data-catalog-how-to-manage.md)
