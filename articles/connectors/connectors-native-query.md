---
title: "ação de consulta de Olá aaaAdd nas logic apps | Microsoft Docs"
description: "Descrição geral da ação de consulta Olá para efetuar ações como filtro matriz."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Introdução à ação de consulta Olá
Utilizando a ação de consulta Olá, pode trabalhar com lotes e matrizes tooaccomplish fluxos de trabalho para:

* Crie uma tarefa para todos os registos de alta prioridade a partir de uma base de dados.
* Guarde anexos de PDF todas as mensagens de correio eletrónico para um blob do Azure.

tooget iniciado utilizando a ação de consulta Olá numa aplicação lógica, consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Utilize a ação de consulta Olá
Uma ação é uma operação que é efetuada pelo fluxo de trabalho de Olá que está definido uma aplicação lógica. [Saiba mais sobre as ações](connectors-overview.md).  

ação de consulta Olá tem atualmente uma operação, denominada matriz de filtro de Olá, que é exposto no estruturador de Olá. Isto permite-lhe tooquery uma matriz e devolver um conjunto de resultados filtrados.

Eis como pode adicioná-lo numa aplicação lógica:

1. Selecione Olá **novo passo** botão.
2. Escolha **adicionar uma ação**.
3. Na caixa de pesquisa de ação de Olá, escreva **filtro** Olá toolist **matriz de filtro** ação.
   
    ![Selecione a ação de consulta Olá](./media/connectors-native-query/using-action-1.png)
4. Selecione um toofilter de matriz. (hello seguinte captura de ecrã mostra matriz Olá de resultados a partir de uma pesquisa do Twitter.)
5. Crie uma condição tooevaluate em cada item. (Olá seguinte captura de ecrã filtra tweets dos utilizadores que tenham mais do que 100 followers.)
   
    ![Ação de consulta Olá concluída](./media/connectors-native-query/using-action-2.png)
   
    ação de Olá será saída uma matriz nova que contém apenas os resultados que são cumpridos os requisitos de filtro de Olá.
6. Clique em canto superior esquerdo de Olá de Olá toosave de barra de ferramentas e a lógica aplicação será ambos os guardar e publicar (ativar).

## <a name="query-action"></a>Ação de consulta
Seguem-se detalhes Olá para a ação de Olá que suporte este conector. conector de Olá tem uma ação possíveis.

| Ação | Descrição |
| --- | --- |
| Matriz de filtro |Avalia uma condição para cada item numa matriz e devolve resultados Olá |

## <a name="action-details"></a>Detalhes de ação
ação de consulta Olá vem com uma ação possíveis. Olá tabelas seguintes descrevem Olá necessários e opcionais campos de entrada para a ação de Olá e detalhes saída correspondente Olá associadas através da ação de Olá.

### <a name="filter-array"></a>Matriz de filtro
Olá seguem-se os campos de entrada para a ação de Olá, o que faz um pedido de saída de HTTP.
A * significa que é um campo obrigatório.

| Nome a apresentar | Nome da propriedade | Descrição |
| --- | --- | --- |
| De * |Do |Olá matriz toofilter |
| Condição * |onde |Olá condição tooevaluate para cada item |

<br>

### <a name="output-details"></a>Detalhes de saída
Olá seguem-se detalhes de saída para Olá resposta de HTTP.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Matriz filtrado |Matriz |Uma matriz que contenha um objeto para cada resultado filtrado |

## <a name="next-steps"></a>Passos seguintes
Agora, experimente a plataforma de Olá e [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md). Pode explorar Olá outros conectores disponíveis em aplicações lógicas observando nosso [lista APIs](apis-list.md).

