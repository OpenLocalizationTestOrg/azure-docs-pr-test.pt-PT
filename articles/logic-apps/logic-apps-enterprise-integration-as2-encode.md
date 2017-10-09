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
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="aa65b-103">Codificar AS2 mensagens para o Azure Logic Apps com Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="aa65b-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="aa65b-104">tooestablish segurança e fiabilidade ao transmitir mensagens, utilize o conector de mensagem de codificar AS2 Olá.</span><span class="sxs-lookup"><span data-stu-id="aa65b-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="aa65b-105">Este conector fornece a assinatura digital, encriptação e confirmações através de mensagem disposição notificações (MDN), que também toosupport para não rejeição.</span><span class="sxs-lookup"><span data-stu-id="aa65b-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="aa65b-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="aa65b-106">Before you start</span></span>

<span data-ttu-id="aa65b-107">Segue-se itens Olá que precisa de:</span><span class="sxs-lookup"><span data-stu-id="aa65b-107">Here's hello items you need:</span></span>

* <span data-ttu-id="aa65b-108">Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="aa65b-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="aa65b-109">Um [conta integração](logic-apps-enterprise-integration-create-integration-account.md) que já foi definida e associados à subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa65b-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="aa65b-110">Tem de ter um conector de mensagem do integração conta toouse Olá codificar AS2.</span><span class="sxs-lookup"><span data-stu-id="aa65b-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="aa65b-111">Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidas na sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="aa65b-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="aa65b-112">Um [contratos AS2](logic-apps-enterprise-integration-as2.md) que já está definido na sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="aa65b-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="aa65b-113">Codificar mensagens AS2</span><span class="sxs-lookup"><span data-stu-id="aa65b-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="aa65b-114">[Criar uma aplicação lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa65b-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="aa65b-115">conector de mensagem de codificar AS2 Olá não tem acionadores, pelo que tem de adicionar um acionador para iniciar a sua aplicação lógica, como um acionador pedido.</span><span class="sxs-lookup"><span data-stu-id="aa65b-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="aa65b-116">Olá Designer de aplicação lógica, adicionar um acionador e, em seguida, adicionar uma aplicação de lógica de tooyour de ação.</span><span class="sxs-lookup"><span data-stu-id="aa65b-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="aa65b-117">Na caixa de pesquisa de Olá, introduza "AS2" para o filtro.</span><span class="sxs-lookup"><span data-stu-id="aa65b-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="aa65b-118">Selecione **AS2 - mensagem codificar AS2**.</span><span class="sxs-lookup"><span data-stu-id="aa65b-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![Procure "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="aa65b-120">Se anteriormente não tenha criado todas as ligações a conta de integração tooyour, lhe for pedida toocreate agora essa ligação.</span><span class="sxs-lookup"><span data-stu-id="aa65b-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="aa65b-121">Nome da ligação e selecione a conta de integração de Olá que pretende que o tooconnect.</span><span class="sxs-lookup"><span data-stu-id="aa65b-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![criar conta de ligação de toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="aa65b-123">Propriedades com um asterisco são necessárias.</span><span class="sxs-lookup"><span data-stu-id="aa65b-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="aa65b-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="aa65b-124">Property</span></span> | <span data-ttu-id="aa65b-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="aa65b-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="aa65b-126">Nome da ligação *</span><span class="sxs-lookup"><span data-stu-id="aa65b-126">Connection Name *</span></span> |<span data-ttu-id="aa65b-127">Introduza um nome para a sua ligação.</span><span class="sxs-lookup"><span data-stu-id="aa65b-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="aa65b-128">Conta de integração *</span><span class="sxs-lookup"><span data-stu-id="aa65b-128">Integration Account *</span></span> |<span data-ttu-id="aa65b-129">Introduza um nome para a sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="aa65b-129">Enter a name for your integration account.</span></span> <span data-ttu-id="aa65b-130">Certifique-se de que a aplicação de conta e a lógica de integração estão Olá mesma localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa65b-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="aa65b-131">Quando tiver terminado, os detalhes de ligação devem ter um aspeto semelhante toothis exemplo.</span><span class="sxs-lookup"><span data-stu-id="aa65b-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="aa65b-132">toofinish criar a ligação, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="aa65b-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![detalhes de ligação de integração](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="aa65b-134">Depois de criar a ligação, conforme mostrado neste exemplo, forneça os detalhes para **AS2-do**, **AS2 tooidentifiers** conforme configurado no seu contrato e **corpo**, que é payload da mensagem Olá.</span><span class="sxs-lookup"><span data-stu-id="aa65b-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![Forneça os campos de preenchimento obrigatórios](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="aa65b-136">Detalhes de codificador AS2</span><span class="sxs-lookup"><span data-stu-id="aa65b-136">AS2 encoder details</span></span>

<span data-ttu-id="aa65b-137">conector AS2 codificar de Olá executa estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="aa65b-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="aa65b-138">Aplica-se os cabeçalhos de AS2/HTTP</span><span class="sxs-lookup"><span data-stu-id="aa65b-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="aa65b-139">Sinais de envio de mensagens (se configurada)</span><span class="sxs-lookup"><span data-stu-id="aa65b-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="aa65b-140">Encripta as mensagens de saída (se configurada)</span><span class="sxs-lookup"><span data-stu-id="aa65b-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="aa65b-141">Comprimir a mensagem de saudação (se configurada)</span><span class="sxs-lookup"><span data-stu-id="aa65b-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="aa65b-142">Repita este exemplo</span><span class="sxs-lookup"><span data-stu-id="aa65b-142">Try this sample</span></span>

<span data-ttu-id="aa65b-143">tootry implementar uma lógica totalmente operacional aplicação e exemplo AS2 cenário, consulte Olá [AS2 cenário e do modelo de aplicação lógica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span><span class="sxs-lookup"><span data-stu-id="aa65b-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="aa65b-144">Swagger Olá de vista</span><span class="sxs-lookup"><span data-stu-id="aa65b-144">View hello swagger</span></span>
<span data-ttu-id="aa65b-145">Consulte Olá [swagger detalhes](/connectors/as2/).</span><span class="sxs-lookup"><span data-stu-id="aa65b-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aa65b-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="aa65b-146">Next steps</span></span>
[<span data-ttu-id="aa65b-147">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="aa65b-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise") 

