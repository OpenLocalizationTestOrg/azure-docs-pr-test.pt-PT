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
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="27906-103">Descodificar mensagens EDIFACT para Azure Logic Apps com Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="27906-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="27906-104">Com o conector de mensagem de descodificar EDIFACT Olá, pode validar EDI e propriedades específicos de parceiro, dividir interchanges para conjuntos de transações ou manter todos interchanges e gerar em que as confirmações para transações processadas.</span><span class="sxs-lookup"><span data-stu-id="27906-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="27906-105">toouse este conector, tem de adicionar Olá conector tooan existente acionador na sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="27906-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="27906-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="27906-106">Before you start</span></span>

<span data-ttu-id="27906-107">Segue-se itens Olá que precisa de:</span><span class="sxs-lookup"><span data-stu-id="27906-107">Here's hello items you need:</span></span>

* <span data-ttu-id="27906-108">Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="27906-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="27906-109">Um [conta integração](logic-apps-enterprise-integration-create-integration-account.md) que já foi definida e associados à subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="27906-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="27906-110">Tem de ter um conector de mensagem do integração conta toouse Olá EDIFACT descodificar.</span><span class="sxs-lookup"><span data-stu-id="27906-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="27906-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidas na sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="27906-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="27906-112">Um [contratos EDIFACT](logic-apps-enterprise-integration-edifact.md) que já está definido na sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="27906-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="27906-113">Descodificar mensagens EDIFACT</span><span class="sxs-lookup"><span data-stu-id="27906-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="27906-114">[Criar uma aplicação lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="27906-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="27906-115">conector de mensagem de descodificar EDIFACT Olá não tem acionadores, pelo que tem de adicionar um acionador para iniciar a sua aplicação lógica, como um acionador pedido.</span><span class="sxs-lookup"><span data-stu-id="27906-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="27906-116">Olá Designer de aplicação lógica, adicionar um acionador e, em seguida, adicionar uma aplicação de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="27906-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="27906-117">Na caixa de pesquisa de Olá, introduza "EDIFACT" como o filtro.</span><span class="sxs-lookup"><span data-stu-id="27906-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="27906-118">Selecione **descodificar a mensagem EDIFACT**.</span><span class="sxs-lookup"><span data-stu-id="27906-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![EDIFACT de pesquisa](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="27906-120">Se anteriormente não tenha criado todas as ligações a conta de integração tooyour, lhe for pedida toocreate agora essa ligação.</span><span class="sxs-lookup"><span data-stu-id="27906-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="27906-121">Nome da ligação e selecione a conta de integração de Olá que pretende que o tooconnect.</span><span class="sxs-lookup"><span data-stu-id="27906-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![criar conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="27906-123">Propriedades com um asterisco são necessárias.</span><span class="sxs-lookup"><span data-stu-id="27906-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="27906-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="27906-124">Property</span></span> | <span data-ttu-id="27906-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="27906-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="27906-126">Nome da ligação *</span><span class="sxs-lookup"><span data-stu-id="27906-126">Connection Name *</span></span> |<span data-ttu-id="27906-127">Introduza um nome para a sua ligação.</span><span class="sxs-lookup"><span data-stu-id="27906-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="27906-128">Conta de integração *</span><span class="sxs-lookup"><span data-stu-id="27906-128">Integration Account *</span></span> |<span data-ttu-id="27906-129">Introduza um nome para a sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="27906-129">Enter a name for your integration account.</span></span> <span data-ttu-id="27906-130">Certifique-se de que a aplicação de conta e a lógica de integração estão Olá mesma localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="27906-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="27906-131">Quando tiver terminado toofinish criar a ligação, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="27906-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="27906-132">Os detalhes de ligação devem ter um aspeto semelhante toothis exemplo:</span><span class="sxs-lookup"><span data-stu-id="27906-132">Your connection details should look similar toothis example:</span></span>

    ![Detalhes da conta de integração](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="27906-134">Depois de criar a ligação, conforme mostrado neste exemplo, selecione Olá EDIFACT ficheiro simples mensagem toodecode.</span><span class="sxs-lookup"><span data-stu-id="27906-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![ligação de conta de integração criada](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="27906-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="27906-136">For example:</span></span>

    ![Selecione a mensagem de ficheiro simples EDIFACT para descodificação](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="27906-138">Detalhes de descodificador EDIFACT</span><span class="sxs-lookup"><span data-stu-id="27906-138">EDIFACT decoder details</span></span>

<span data-ttu-id="27906-139">conector de descodificar EDIFACT Olá executa estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="27906-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="27906-140">Valida o envelope Olá contra comerciais contrato para parceiros.</span><span class="sxs-lookup"><span data-stu-id="27906-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="27906-141">Resolve contrato Olá por correspondente qualificador de remetente Olá & identificador e o qualificador de recetor & Identificador.</span><span class="sxs-lookup"><span data-stu-id="27906-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="27906-142">Divide um intercâmbio em várias transações quando intercâmbio Olá tem mais de uma transação com base num contrato de Olá receber a configuração de definições.</span><span class="sxs-lookup"><span data-stu-id="27906-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="27906-143">Disassembles intercâmbio Olá.</span><span class="sxs-lookup"><span data-stu-id="27906-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="27906-144">Valida EDI e propriedades específicos de parceiros, incluindo:</span><span class="sxs-lookup"><span data-stu-id="27906-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="27906-145">Validação da estrutura de envelope de intercâmbio de Olá</span><span class="sxs-lookup"><span data-stu-id="27906-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="27906-146">Validação de esquema do envelope Olá em relação ao esquema do controlo de Olá</span><span class="sxs-lookup"><span data-stu-id="27906-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="27906-147">Validação de esquema de elementos de dados do conjunto de transação de Olá em relação ao esquema de mensagem de Olá</span><span class="sxs-lookup"><span data-stu-id="27906-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="27906-148">A validação de EDI efetuada em elementos de dados do conjunto de transação</span><span class="sxs-lookup"><span data-stu-id="27906-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="27906-149">Verifica se Olá intercâmbio, grupo e transação conjunto controlo números não são duplicados (se configurada)</span><span class="sxs-lookup"><span data-stu-id="27906-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="27906-150">Verifica o número de controlo de intercâmbio de Olá contra interchanges anteriormente recebidos.</span><span class="sxs-lookup"><span data-stu-id="27906-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="27906-151">Verifica o número de controlo do Olá grupo em relação a outros números de controlo de grupo no intercâmbio Olá.</span><span class="sxs-lookup"><span data-stu-id="27906-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="27906-152">Verifica a transação Olá definir o número de controlo em relação a outros números de controlo do conjunto de transação nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="27906-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="27906-153">Divide Olá intercâmbio para conjuntos de transação ou preserva intercâmbio todo Olá:</span><span class="sxs-lookup"><span data-stu-id="27906-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="27906-154">Intercâmbio de divisão como conjuntos de transação - suspender conjuntos de transação com o erro: divisões intercâmbio numa transação define e analisa cada conjunto de transação.</span><span class="sxs-lookup"><span data-stu-id="27906-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="27906-155">ação de Decode Olá X12 produz apenas os conjuntos de transação que falharem a validação demasiado`badMessages`e produz Olá restantes transações define demasiado`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="27906-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="27906-156">Intercâmbio de divisão como conjuntos de transação - suspender intercâmbio com o erro: divisões intercâmbio numa transação define e analisa cada conjunto de transação.</span><span class="sxs-lookup"><span data-stu-id="27906-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="27906-157">Se um ou mais transações define na validação de falha de intercâmbio de Olá, a ação de Decode Olá X12 produz todas as transações de Olá define em que intercâmbio demasiado`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="27906-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="27906-158">Preservar intercâmbio - suspender conjuntos de transação com o erro: intercâmbio de Olá Preserve e processo Olá todo intercâmbio de batch.</span><span class="sxs-lookup"><span data-stu-id="27906-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="27906-159">ação de Decode Olá X12 produz apenas os conjuntos de transação que falharem a validação demasiado`badMessages`e produz Olá restantes transações define demasiado`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="27906-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="27906-160">Preservar intercâmbio - suspender intercâmbio com o erro: intercâmbio de Olá Preserve e processo Olá todo intercâmbio de batch.</span><span class="sxs-lookup"><span data-stu-id="27906-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="27906-161">Se um ou mais transações define na validação de falha de intercâmbio de Olá, a ação de Decode Olá X12 produz todas as transações de Olá define em que intercâmbio demasiado`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="27906-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="27906-162">Gera uma técnica (controlo) e/ou a confirmação funcional (se configurada).</span><span class="sxs-lookup"><span data-stu-id="27906-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="27906-163">Uma confirmação técnicos ou Olá CONTRL ACK reporta resultados Olá uma verificação syntactical de intercâmbio de Olá concluída recebido.</span><span class="sxs-lookup"><span data-stu-id="27906-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="27906-164">Uma confirmação funcional reconhece aceitar ou rejeitar um intercâmbio recebido ou um grupo</span><span class="sxs-lookup"><span data-stu-id="27906-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="27906-165">Ver o ficheiro Swagger</span><span class="sxs-lookup"><span data-stu-id="27906-165">View Swagger file</span></span>
<span data-ttu-id="27906-166">tooview Olá Swagger detalhes para o conector EDIFACT Olá, consulte [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="27906-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27906-167">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="27906-167">Next steps</span></span>
[<span data-ttu-id="27906-168">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="27906-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

