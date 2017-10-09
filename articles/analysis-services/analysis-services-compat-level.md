---
title: "nível de compatibilidade do modelo de aaaData no Azure Analysis Services | Microsoft Docs"
description: "Compreender o nível de compatibilidade do modelo de dados de tabela."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nível de compatibilidade para modelos em tabela do Analysis Services

*Nível de compatibilidade* refere-se comportamentos toorelease específico no motor do Analysis Services Olá. Nível de compatibilidade de toohello de alterações, normalmente, a operação com as versões principais do SQL Server. Estas alterações também são implementadas no paridade de toomaintain Azure Analysis Services entre ambas as plataformas. Alterações de nível de compatibilidade também afetam as funcionalidades disponíveis nos seus modelos em tabela. Por exemplo, DirectQuery e de metadados do objeto de tabela tem implementações diferentes, dependendo do nível de compatibilidade de Olá. 

Serviços de análise do Azure suporta modelos em tabela níveis de compatibilidade de Olá 1200 e 1400.

nível de compatibilidade mais recente Olá é 1400. Este nível coincide com o SQL Server 2017 Analysis Services. Nível de compatibilidade de 1400 Olá principais funcionalidades incluem:

*  Nova infraestrutura para conectividade de dados e importação para modelos em tabela com suporte para personalizada APIs e TMSL scripting. Esta nova funcionalidade permite suporte para origens de dados adicionais, como o armazenamento de Blobs do Azure.
*  Transformação de dados e as capacidades de aplicação híbrida de dados através de expressões de obter dados e o M.
*  Medidas suportam uma propriedade de linhas de detalhe com uma expressão DAX. Esta propriedade permite que as ferramentas de cliente, como o Microsoft Excel toodrill baixo toodetailed dados a partir de um relatório agregado. Por exemplo, quando os utilizadores visualizar vendas totais para uma região e o mês, podem visualizar os detalhes da encomenda Olá associado. 
*  Segurança ao nível do objeto de tabela e coluna de nomes, além disso toohello dados nelas.
*  Suporte melhorado para hierarquias desalinhadas.
*  Monitorização de desempenho e melhoramentos.
  
## <a name="set-compatibility-level"></a>Nível de compatibilidade de conjunto 
 Quando criar um novo projeto de modelo em tabela no SSDT, pode especificar o nível de compatibilidade de Olá no Olá **estruturador de modelos em tabela** caixa de diálogo. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Se selecionar Olá **não mostrar esta mensagem novamente** opção, todos os projetos subsequentes utilizam o nível de compatibilidade de Olá especificado como predefinição de Olá. Pode alterar o nível de compatibilidade predefinido Olá no SSDT no **ferramentas** > **opções**.  
  
 tooupgrade um projeto de modelo em tabela existente no SSDT, conjunto Olá **nível de compatibilidade** propriedade no modelo de Olá **propriedades** janela. Tenha em atenção, atualizar o nível de compatibilidade de Olá é irreversível.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Verifique o nível de compatibilidade para uma base de dados do modelo em tabela no SQL Server Management Studio 
 No SSMS, clique no nome da base de dados de Olá > **propriedades** > **nível de compatibilidade**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Verifique o nível de compatibilidade suportado para um servidor no SSMS  
 No SSMS, clique no nome do servidor Olá > **propriedades** > **nível de compatibilidade suportado**.  
  
 Esta propriedade especifica Olá mais elevado nível de compatibilidade de uma base de dados que será executado no servidor de Olá (excluindo pré-visualização). Não é possível alterar o nível de compatibilidade de Olá suportado.  

## <a name="next-steps"></a>Passos seguintes
  [Criar um modelo no portal do Azure](analysis-services-create-model-portal.md)   
  [Gerir do Analysis Services](analysis-services-manage.md)  
