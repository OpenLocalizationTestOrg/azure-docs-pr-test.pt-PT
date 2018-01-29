---
title: "Como ver dados relacionados ativos no catálogo de dados do Azure | Microsoft Docs"
description: "Este artigo explica como visualizar recursos de dados relacionados de um recurso de dados selecionadas no catálogo de dados do Azure."
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
ms.date: 01/18/2018
ms.author: maroche
ms.openlocfilehash: 37d12209d28b73f0d7fc6d940ded344fbeae968d
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a>Como ver dados relacionados ativos no catálogo de dados do Azure?
Catálogo de dados do Azure permite-lhe ver os recursos de dados relacionados com um relações de recurso e a vista de dados selecionados entre eles. 

## <a name="supported-data-sources"></a>Origens de dados suportadas 
Quando registar recursos de dados das seguintes origens de dados, o catálogo de dados do Azure regista automaticamente metadados sobre relações de associação entre os recursos de dados selecionada. 

- SQL Server
- Base de Dados SQL do Azure
- MySQL
- Oracle

> [!NOTE]
> Catálogo de dados importar a relação entre os recursos de dados de dois, tem de registar os dois recursos ao mesmo tempo. Se tinha adicionado um deles separadamente, adicione-a novamente e os outros recursos de dados para importar a relação entre eles.

## <a name="view-related-data-assets"></a>Ver dados relacionados ativos
Para ver os recursos de dados que estão relacionados com um conjunto de dados selecionado, utilize o **relações** separador conforme mostrado na imagem seguinte: 

![Catálogo de dados do Azure - ver relacionados com os recursos de dados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

Neste exemplo, existem duas relações para selecionado **ProductSubcategory** recurso de dados: 

- ProductSubcategoryID a coluna da tabela Produto tem uma relação de chave externa com ProductSubcategoryID coluna da tabela ProductSubcategory selecionada. 
- ProductCategoryID a coluna da tabela ProductSubCategory tem uma relação de chave externa com ProductCategoryID coluna da tabela ProductCategory selecionada.

> [!NOTE]
> Tenha em atenção a direção da seta na vista de árvore de relações.  

Para ver mais detalhes, tais como o nome completamente qualificado da coluna, mova o rato sobre e vir um pop-up semelhante para a imagem seguinte: 

![Catálogo de dados do Azure - pop-up de relação](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

Para incluir as relações entre os recursos que já foram registados, volte a registar esses recursos.

## <a name="next-steps"></a>Passos Seguintes
- [How to manage data assets (Como gerir recursos de dados)](data-catalog-how-to-manage.md)