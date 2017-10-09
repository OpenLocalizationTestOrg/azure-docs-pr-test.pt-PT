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
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="a71e5-103">Codificar X12 mensagens para o Azure Logic Apps com Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a71e5-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="a71e5-104">Com o conector de mensagem de codificar X12 Olá, pode validar EDI e propriedades específicos de parceiro, converter mensagens com codificação XML em conjuntos de transação EDI intercâmbio Olá e pedir uma confirmação técnicas, funcionais de confirmação ou ambos.</span><span class="sxs-lookup"><span data-stu-id="a71e5-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="a71e5-105">toouse este conector, tem de adicionar Olá conector tooan existente acionador na sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="a71e5-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a71e5-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a71e5-106">Before you start</span></span>

<span data-ttu-id="a71e5-107">Segue-se itens Olá que precisa de:</span><span class="sxs-lookup"><span data-stu-id="a71e5-107">Here's hello items you need:</span></span>

* <span data-ttu-id="a71e5-108">Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="a71e5-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="a71e5-109">Um [conta integração](logic-apps-enterprise-integration-create-integration-account.md) que já foi definida e associados à subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="a71e5-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="a71e5-110">Tem de ter um conector do integração conta toouse Olá codificar X12 mensagem.</span><span class="sxs-lookup"><span data-stu-id="a71e5-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="a71e5-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidas na sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="a71e5-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="a71e5-112">Um [X12 contrato](logic-apps-enterprise-integration-x12.md) que já está definido na sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="a71e5-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="a71e5-113">Codificar X12 mensagens</span><span class="sxs-lookup"><span data-stu-id="a71e5-113">Encode X12 messages</span></span>

1. <span data-ttu-id="a71e5-114">[Criar uma aplicação lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a71e5-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="a71e5-115">conector de mensagem de codificar X12 Olá não tem acionadores, pelo que tem de adicionar um acionador para iniciar a sua aplicação lógica, como um acionador pedido.</span><span class="sxs-lookup"><span data-stu-id="a71e5-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="a71e5-116">Olá Designer de aplicação lógica, adicionar um acionador e, em seguida, adicionar uma aplicação de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="a71e5-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="a71e5-117">Na caixa de pesquisa de Olá, introduza "x12" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="a71e5-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="a71e5-118">Selecione **X12-codificar a mensagem de tooX12 pelo nome do contrato** ou **X12-codificar a mensagem de tooX12 por identidades**.</span><span class="sxs-lookup"><span data-stu-id="a71e5-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Procure "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="a71e5-120">Se anteriormente não tenha criado todas as ligações a conta de integração tooyour, lhe for pedida toocreate agora essa ligação.</span><span class="sxs-lookup"><span data-stu-id="a71e5-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="a71e5-121">Nome da ligação e selecione a conta de integração de Olá que pretende que o tooconnect.</span><span class="sxs-lookup"><span data-stu-id="a71e5-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![ligação de conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="a71e5-123">Propriedades com um asterisco são necessárias.</span><span class="sxs-lookup"><span data-stu-id="a71e5-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="a71e5-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a71e5-124">Property</span></span> | <span data-ttu-id="a71e5-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="a71e5-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="a71e5-126">Nome da ligação *</span><span class="sxs-lookup"><span data-stu-id="a71e5-126">Connection Name *</span></span> |<span data-ttu-id="a71e5-127">Introduza um nome para a sua ligação.</span><span class="sxs-lookup"><span data-stu-id="a71e5-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="a71e5-128">Conta de integração *</span><span class="sxs-lookup"><span data-stu-id="a71e5-128">Integration Account *</span></span> |<span data-ttu-id="a71e5-129">Introduza um nome para a sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="a71e5-129">Enter a name for your integration account.</span></span> <span data-ttu-id="a71e5-130">Certifique-se de que a aplicação de conta e a lógica de integração estão Olá mesma localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="a71e5-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="a71e5-131">Quando tiver terminado, os detalhes de ligação devem ter um aspeto semelhante toothis exemplo.</span><span class="sxs-lookup"><span data-stu-id="a71e5-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="a71e5-132">toofinish criar a ligação, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="a71e5-132">toofinish creating your connection, choose **Create**.</span></span>

    ![ligação de conta de integração criada](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="a71e5-134">A ligação está agora criada.</span><span class="sxs-lookup"><span data-stu-id="a71e5-134">Your connection is now created.</span></span>

    ![detalhes de ligação da conta de integração](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="a71e5-136">Codificar X12 mensagens pelo nome do contrato</span><span class="sxs-lookup"><span data-stu-id="a71e5-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="a71e5-137">Se optou por mensagens tooencode X12 pelo nome do contrato, abra Olá **nome de X12 contrato** lista, introduza ou selecione o X12 existente contrato.</span><span class="sxs-lookup"><span data-stu-id="a71e5-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="a71e5-138">Introduza Olá XML mensagem tooencode.</span><span class="sxs-lookup"><span data-stu-id="a71e5-138">Enter hello XML message tooencode.</span></span>

![Introduza X12 contrato de mensagem de nome e XML tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="a71e5-140">Codificar X12 mensagens por identidades</span><span class="sxs-lookup"><span data-stu-id="a71e5-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="a71e5-141">Se escolher tooencode X12 mensagens por identidades, introduza o identificador do remetente Olá, qualificador do remetente, identificador de recetor e qualificador do recetor como configurado na sua X12 contrato.</span><span class="sxs-lookup"><span data-stu-id="a71e5-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="a71e5-142">Selecione Olá XML mensagem tooencode.</span><span class="sxs-lookup"><span data-stu-id="a71e5-142">Select hello XML message tooencode.</span></span>
   
![Fornecer identidades para o remetente e o recetor, selecione tooencode de mensagem XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="a71e5-144">X12 codificar detalhes</span><span class="sxs-lookup"><span data-stu-id="a71e5-144">X12 Encode details</span></span>

<span data-ttu-id="a71e5-145">conector de codificar Olá X12 executa estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="a71e5-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="a71e5-146">Resolução de contrato por correspondência de propriedades de contexto do remetente e o recetor.</span><span class="sxs-lookup"><span data-stu-id="a71e5-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="a71e5-147">Serializa intercâmbio EDI Olá, conversão de mensagens com codificação XML em conjuntos de transação EDI intercâmbio Olá.</span><span class="sxs-lookup"><span data-stu-id="a71e5-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="a71e5-148">Aplica-se de segmentos de cabeçalho e trailer do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="a71e5-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="a71e5-149">Gera um número de controlo do intercâmbio, um número de controlo de grupo e um número de controlo do conjunto de transação para cada intercâmbio de saída</span><span class="sxs-lookup"><span data-stu-id="a71e5-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="a71e5-150">Substitui os separadores de dados do payload de Olá</span><span class="sxs-lookup"><span data-stu-id="a71e5-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="a71e5-151">Valida EDI e propriedades específicos de parceiro</span><span class="sxs-lookup"><span data-stu-id="a71e5-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="a71e5-152">Validação de esquema de elementos de dados do conjunto de transação de Olá contra a mensagem de saudação esquema</span><span class="sxs-lookup"><span data-stu-id="a71e5-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="a71e5-153">Validação de EDI efetuada em elementos de conjunto de transação de dados.</span><span class="sxs-lookup"><span data-stu-id="a71e5-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="a71e5-154">A validação expandida efetuada em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="a71e5-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="a71e5-155">Solicita uma confirmação técnica e/ou funcional (se configurada).</span><span class="sxs-lookup"><span data-stu-id="a71e5-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="a71e5-156">Gera uma confirmação técnicos como resultado da validação de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a71e5-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="a71e5-157">Olá confirmação técnica relatórios Olá estado de processamento de Olá de um cabeçalho de intercâmbio e trailer por recetor de endereço Olá</span><span class="sxs-lookup"><span data-stu-id="a71e5-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="a71e5-158">Gera uma confirmação funcional como resultado da validação de corpo.</span><span class="sxs-lookup"><span data-stu-id="a71e5-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="a71e5-159">Olá confirmação funcional relatórios de cada Ocorreu um erro ao processar Olá recebeu o documento</span><span class="sxs-lookup"><span data-stu-id="a71e5-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="a71e5-160">Swagger Olá de vista</span><span class="sxs-lookup"><span data-stu-id="a71e5-160">View hello swagger</span></span>
<span data-ttu-id="a71e5-161">Consulte Olá [swagger detalhes](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="a71e5-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a71e5-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a71e5-162">Next steps</span></span>
[<span data-ttu-id="a71e5-163">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a71e5-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

