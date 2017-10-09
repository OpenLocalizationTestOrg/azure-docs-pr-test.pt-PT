---
title: "mensagens de aaaEncode X12 – Azure Logic Apps | Microsoft Docs"
description: "Validar EDI e converter com codificação XML mensagens com o X12 mensagem codificador no Olá Enterprise Integration Pack para o Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificar X12 mensagens para o Azure Logic Apps com Olá Enterprise Integration Pack

Com o conector de mensagem de codificar X12 Olá, pode validar EDI e propriedades específicos de parceiro, converter mensagens com codificação XML em conjuntos de transação EDI intercâmbio Olá e pedir uma confirmação técnicas, funcionais de confirmação ou ambos.
toouse este conector, tem de adicionar Olá conector tooan existente acionador na sua aplicação lógica.

## <a name="before-you-start"></a>Antes de começar

Segue-se itens Olá que precisa de:

* Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)
* Um [conta integração](logic-apps-enterprise-integration-create-integration-account.md) que já foi definida e associados à subscrição do Azure. Tem de ter um conector do integração conta toouse Olá codificar X12 mensagem.
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidas na sua conta de integração
* Um [X12 contrato](logic-apps-enterprise-integration-x12.md) que já está definido na sua conta de integração

## <a name="encode-x12-messages"></a>Codificar X12 mensagens

1. [Criar uma aplicação lógica](logic-apps-create-a-logic-app.md).

2. conector de mensagem de codificar X12 Olá não tem acionadores, pelo que tem de adicionar um acionador para iniciar a sua aplicação lógica, como um acionador pedido. Olá Designer de aplicação lógica, adicionar um acionador e, em seguida, adicionar uma aplicação de lógica de tooyour de ação.

3.  Na caixa de pesquisa de Olá, introduza "x12" para o filtro. Selecione **X12-codificar a mensagem de tooX12 pelo nome do contrato** ou **X12-codificar a mensagem de tooX12 por identidades**.
   
    ![Procure "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Se anteriormente não tenha criado todas as ligações a conta de integração tooyour, lhe for pedida toocreate agora essa ligação. Nome da ligação e selecione a conta de integração de Olá que pretende que o tooconnect. 
   
    ![ligação de conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Propriedades com um asterisco são necessárias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da ligação * |Introduza um nome para a sua ligação. |
    | Conta de integração * |Introduza um nome para a sua conta de integração. Certifique-se de que a aplicação de conta e a lógica de integração estão Olá mesma localização do Azure. |

5.  Quando tiver terminado, os detalhes de ligação devem ter um aspeto semelhante toothis exemplo. toofinish criar a ligação, escolha **criar**.

    ![ligação de conta de integração criada](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    A ligação está agora criada.

    ![detalhes de ligação da conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Codificar X12 mensagens pelo nome do contrato

Se optou por mensagens tooencode X12 pelo nome do contrato, abra Olá **nome de X12 contrato** lista, introduza ou selecione o X12 existente contrato. Introduza Olá XML mensagem tooencode.

![Introduza X12 contrato de mensagem de nome e XML tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Codificar X12 mensagens por identidades

Se escolher tooencode X12 mensagens por identidades, introduza o identificador do remetente Olá, qualificador do remetente, identificador de recetor e qualificador do recetor como configurado na sua X12 contrato. Selecione Olá XML mensagem tooencode.
   
![Fornecer identidades para o remetente e o recetor, selecione tooencode de mensagem XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>X12 codificar detalhes

conector de codificar Olá X12 executa estas tarefas:

* Resolução de contrato por correspondência de propriedades de contexto do remetente e o recetor.
* Serializa intercâmbio EDI Olá, conversão de mensagens com codificação XML em conjuntos de transação EDI intercâmbio Olá.
* Aplica-se de segmentos de cabeçalho e trailer do conjunto de transação
* Gera um número de controlo do intercâmbio, um número de controlo de grupo e um número de controlo do conjunto de transação para cada intercâmbio de saída
* Substitui os separadores de dados do payload de Olá
* Valida EDI e propriedades específicos de parceiro
  * Validação de esquema de elementos de dados do conjunto de transação de Olá contra a mensagem de saudação esquema
  * Validação de EDI efetuada em elementos de conjunto de transação de dados.
  * A validação expandida efetuada em elementos de dados do conjunto de transação
* Solicita uma confirmação técnica e/ou funcional (se configurada).
  * Gera uma confirmação técnicos como resultado da validação de cabeçalho. Olá confirmação técnica relatórios Olá estado de processamento de Olá de um cabeçalho de intercâmbio e trailer por recetor de endereço Olá
  * Gera uma confirmação funcional como resultado da validação de corpo. Olá confirmação funcional relatórios de cada Ocorreu um erro ao processar Olá recebeu o documento

## <a name="view-hello-swagger"></a>Swagger Olá de vista
Consulte Olá [swagger detalhes](/connectors/x12/). 

## <a name="next-steps"></a>Passos seguintes
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

