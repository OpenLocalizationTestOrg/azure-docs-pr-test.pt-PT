---
title: "mensagens de aaaEncode AS2 – Azure Logic Apps | Microsoft Docs"
description: "Como toouse Olá AS2 codificador no Olá Enterprise Integration Pack para o Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar AS2 mensagens para o Azure Logic Apps com Olá Enterprise Integration Pack

tooestablish segurança e fiabilidade ao transmitir mensagens, utilize o conector de mensagem de codificar AS2 Olá. Este conector fornece a assinatura digital, encriptação e confirmações através de mensagem disposição notificações (MDN), que também toosupport para não rejeição.

## <a name="before-you-start"></a>Antes de começar

Segue-se itens Olá que precisa de:

* Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)
* Um [conta integração](logic-apps-enterprise-integration-create-integration-account.md) que já foi definida e associados à subscrição do Azure. Tem de ter um conector de mensagem do integração conta toouse Olá codificar AS2.
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidas na sua conta de integração
* Um [contratos AS2](logic-apps-enterprise-integration-as2.md) que já está definido na sua conta de integração

## <a name="encode-as2-messages"></a>Codificar mensagens AS2

1. [Criar uma aplicação lógica](logic-apps-create-a-logic-app.md).

2. conector de mensagem de codificar AS2 Olá não tem acionadores, pelo que tem de adicionar um acionador para iniciar a sua aplicação lógica, como um acionador pedido. Olá Designer de aplicação lógica, adicionar um acionador e, em seguida, adicionar uma aplicação de lógica de tooyour de ação.

3.  Na caixa de pesquisa de Olá, introduza "AS2" para o filtro. Selecione **AS2 - mensagem codificar AS2**.
   
    ![Procure "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Se anteriormente não tenha criado todas as ligações a conta de integração tooyour, lhe for pedida toocreate agora essa ligação. Nome da ligação e selecione a conta de integração de Olá que pretende que o tooconnect. 
   
    ![criar conta de ligação de toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Propriedades com um asterisco são necessárias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da ligação * |Introduza um nome para a sua ligação. |
    | Conta de integração * |Introduza um nome para a sua conta de integração. Certifique-se de que a aplicação de conta e a lógica de integração estão Olá mesma localização do Azure. |

5.  Quando tiver terminado, os detalhes de ligação devem ter um aspeto semelhante toothis exemplo. toofinish criar a ligação, escolha **criar**.
   
    ![detalhes de ligação de integração](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Depois de criar a ligação, conforme mostrado neste exemplo, forneça os detalhes para **AS2-do**, **AS2 tooidentifiers** conforme configurado no seu contrato e **corpo**, que é payload da mensagem Olá.
   
    ![Forneça os campos de preenchimento obrigatórios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Detalhes de codificador AS2

conector AS2 codificar de Olá executa estas tarefas: 

* Aplica-se os cabeçalhos de AS2/HTTP
* Sinais de envio de mensagens (se configurada)
* Encripta as mensagens de saída (se configurada)
* Comprimir a mensagem de saudação (se configurada)

## <a name="try-this-sample"></a>Repita este exemplo

tootry implementar uma lógica totalmente operacional aplicação e exemplo AS2 cenário, consulte Olá [AS2 cenário e do modelo de aplicação lógica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger Olá de vista
Consulte Olá [swagger detalhes](/connectors/as2/). 

## <a name="next-steps"></a>Passos seguintes
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

