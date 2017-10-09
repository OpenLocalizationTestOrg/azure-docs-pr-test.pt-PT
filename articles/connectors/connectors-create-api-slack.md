---
title: "aaaUse Olá Slack conector nas suas Azure logic apps | Microsoft Docs"
description: Ligar tooSlack nas suas logic apps
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Introdução ao conector Slack Olá
Slack é uma ferramenta de comunicação de equipa, que reúne todas as suas comunicações equipa num colocar, de forma instantânea pesquisáveis e disponível onde quer que esteja. 

Começar através da criação de uma aplicação lógica agora; consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Criar uma ligação tooSlack
conector de Slack Olá toouse, crie primeiro um **ligação** , em seguida, fornecer detalhes de Olá estas propriedades: 

| Propriedade | Necessário | Descrição |
| --- | --- | --- |
| Token |Sim |Forneça credenciais Slack |

Siga estes passos toosign ao Slack e configuração de Olá completa de Olá Slack **ligação** na sua aplicação lógica:

1. Selecione **periodicidade**
2. Selecione um **frequência** e introduza um **intervalo**
3. Selecione **adicionar uma ação**  
   ![Configurar Slack][1]  
4. Introduza Slack na caixa de pesquisa de Olá e aguarde Olá pesquisa tooreturn todas as entradas com Slack no nome de Olá
5. Selecione **Slack - mensagem Post**
6. Selecione **sessão tooSlack**:  
   ![Configurar Slack][2]
7. Forneça o toosign credenciais Slack na aplicação de Olá tooauthorize    
   ![Configurar Slack][3]  
8. Será página de início de sessão redirecionado tooyour organização. **Autorizar** toointeract Slack com a sua aplicação lógica:      
   ![Configurar Slack][5] 
9. Após a conclusão da autorização de Olá será redirecionado tooyour logic app toocomplete-configurando Olá **Slack - obter todas as mensagens** secção. Adicione outros acionadores e ações que precisa.  
   ![Configurar Slack][6]
10. Guarde o trabalho selecionando **guardar** na barra de menus Olá acima.

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/slack/).

## <a name="more-connectors"></a>Mais conectores
Voltar atrás toohello [lista APIs](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
