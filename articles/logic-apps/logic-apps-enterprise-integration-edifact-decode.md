---
title: "mensagens de EDIFACT aaaDecode – Azure Logic Apps | Microsoft Docs"
description: "Validar EDI e gerar confirmações de receção com descodificador de mensagem Olá EDIFACT na Olá Enterprise Integration Pack para o Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Descodificar mensagens EDIFACT para Azure Logic Apps com Olá Enterprise Integration Pack

Com o conector de mensagem de descodificar EDIFACT Olá, pode validar EDI e propriedades específicos de parceiro, dividir interchanges para conjuntos de transações ou manter todos interchanges e gerar em que as confirmações para transações processadas. toouse este conector, tem de adicionar Olá conector tooan existente acionador na sua aplicação lógica.

## <a name="before-you-start"></a>Antes de começar

Segue-se itens Olá que precisa de:

* Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)
* Um [conta integração](logic-apps-enterprise-integration-create-integration-account.md) que já foi definida e associados à subscrição do Azure. Tem de ter um conector de mensagem do integração conta toouse Olá EDIFACT descodificar. 
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidas na sua conta de integração
* Um [contratos EDIFACT](logic-apps-enterprise-integration-edifact.md) que já está definido na sua conta de integração

## <a name="decode-edifact-messages"></a>Descodificar mensagens EDIFACT

1. [Criar uma aplicação lógica](logic-apps-create-a-logic-app.md).

2. conector de mensagem de descodificar EDIFACT Olá não tem acionadores, pelo que tem de adicionar um acionador para iniciar a sua aplicação lógica, como um acionador pedido. Olá Designer de aplicação lógica, adicionar um acionador e, em seguida, adicionar uma aplicação de lógica de tooyour de ação.

3. Na caixa de pesquisa de Olá, introduza "EDIFACT" como o filtro. Selecione **descodificar a mensagem EDIFACT**.
   
    ![EDIFACT de pesquisa](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Se anteriormente não tenha criado todas as ligações a conta de integração tooyour, lhe for pedida toocreate agora essa ligação. Nome da ligação e selecione a conta de integração de Olá que pretende que o tooconnect.
   
    ![criar conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Propriedades com um asterisco são necessárias.

    | Propriedade | Detalhes |
    | --- | --- |
    | Nome da ligação * |Introduza um nome para a sua ligação. |
    | Conta de integração * |Introduza um nome para a sua conta de integração. Certifique-se de que a aplicação de conta e a lógica de integração estão Olá mesma localização do Azure. |

4. Quando tiver terminado toofinish criar a ligação, escolha **criar**. Os detalhes de ligação devem ter um aspeto semelhante toothis exemplo:

    ![Detalhes da conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Depois de criar a ligação, conforme mostrado neste exemplo, selecione Olá EDIFACT ficheiro simples mensagem toodecode.

    ![ligação de conta de integração criada](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Por exemplo:

    ![Selecione a mensagem de ficheiro simples EDIFACT para descodificação](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Detalhes de descodificador EDIFACT

conector de descodificar EDIFACT Olá executa estas tarefas: 

* Valida o envelope Olá contra comerciais contrato para parceiros.
* Resolve contrato Olá por correspondente qualificador de remetente Olá & identificador e o qualificador de recetor & Identificador.
* Divide um intercâmbio em várias transações quando intercâmbio Olá tem mais de uma transação com base num contrato de Olá receber a configuração de definições.
* Disassembles intercâmbio Olá.
* Valida EDI e propriedades específicos de parceiros, incluindo:
  * Validação da estrutura de envelope de intercâmbio de Olá
  * Validação de esquema do envelope Olá em relação ao esquema do controlo de Olá
  * Validação de esquema de elementos de dados do conjunto de transação de Olá em relação ao esquema de mensagem de Olá
  * A validação de EDI efetuada em elementos de dados do conjunto de transação
* Verifica se Olá intercâmbio, grupo e transação conjunto controlo números não são duplicados (se configurada) 
  * Verifica o número de controlo de intercâmbio de Olá contra interchanges anteriormente recebidos. 
  * Verifica o número de controlo do Olá grupo em relação a outros números de controlo de grupo no intercâmbio Olá. 
  * Verifica a transação Olá definir o número de controlo em relação a outros números de controlo do conjunto de transação nesse grupo.
* Divide Olá intercâmbio para conjuntos de transação ou preserva intercâmbio todo Olá:
  * Intercâmbio de divisão como conjuntos de transação - suspender conjuntos de transação com o erro: divisões intercâmbio numa transação define e analisa cada conjunto de transação. 
  ação de Decode Olá X12 produz apenas os conjuntos de transação que falharem a validação demasiado`badMessages`e produz Olá restantes transações define demasiado`goodMessages`.
  * Intercâmbio de divisão como conjuntos de transação - suspender intercâmbio com o erro: divisões intercâmbio numa transação define e analisa cada conjunto de transação. 
  Se um ou mais transações define na validação de falha de intercâmbio de Olá, a ação de Decode Olá X12 produz todas as transações de Olá define em que intercâmbio demasiado`badMessages`.
  * Preservar intercâmbio - suspender conjuntos de transação com o erro: intercâmbio de Olá Preserve e processo Olá todo intercâmbio de batch. 
  ação de Decode Olá X12 produz apenas os conjuntos de transação que falharem a validação demasiado`badMessages`e produz Olá restantes transações define demasiado`goodMessages`.
  * Preservar intercâmbio - suspender intercâmbio com o erro: intercâmbio de Olá Preserve e processo Olá todo intercâmbio de batch. 
  Se um ou mais transações define na validação de falha de intercâmbio de Olá, a ação de Decode Olá X12 produz todas as transações de Olá define em que intercâmbio demasiado`badMessages`.
* Gera uma técnica (controlo) e/ou a confirmação funcional (se configurada).
  * Uma confirmação técnicos ou Olá CONTRL ACK reporta resultados Olá uma verificação syntactical de intercâmbio de Olá concluída recebido.
  * Uma confirmação funcional reconhece aceitar ou rejeitar um intercâmbio recebido ou um grupo

## <a name="view-swagger-file"></a>Ver o ficheiro Swagger
tooview Olá Swagger detalhes para o conector EDIFACT Olá, consulte [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Passos seguintes
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

