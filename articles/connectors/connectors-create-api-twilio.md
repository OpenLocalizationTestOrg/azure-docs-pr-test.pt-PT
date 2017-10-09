---
title: "aaaAdd Olá Twilio conector nas suas Azure Logic apps | Microsoft Docs"
description: "Descrição geral do Olá Twilio conector com parâmetros de REST API"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="dc166-103">Introdução ao conector do Twilio Olá</span><span class="sxs-lookup"><span data-stu-id="dc166-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="dc166-104">Ligue tooTwilio toosend e receber mensagens IP, SMS e MMS global.</span><span class="sxs-lookup"><span data-stu-id="dc166-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="dc166-105">Com Twilio, pode:</span><span class="sxs-lookup"><span data-stu-id="dc166-105">With Twilio, you can:</span></span>

* <span data-ttu-id="dc166-106">Crie o fluxo de negócio com base nos dados de Olá que aproveitar Twilio.</span><span class="sxs-lookup"><span data-stu-id="dc166-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="dc166-107">Utilize ações obter uma mensagem, mensagens de lista e muito mais.</span><span class="sxs-lookup"><span data-stu-id="dc166-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="dc166-108">Estas ações obter uma resposta e a saída de Olá disponível para outras ações.</span><span class="sxs-lookup"><span data-stu-id="dc166-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="dc166-109">Por exemplo, quando receber uma nova mensagem do Twilio, pode efetuar esta mensagem e utilizá-lo um fluxo de trabalho do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dc166-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="dc166-110">Começar através da criação de uma aplicação lógica; consulte [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dc166-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="dc166-111">Criar uma ligação tooTwilio</span><span class="sxs-lookup"><span data-stu-id="dc166-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="dc166-112">Ao adicionar este tooyour logic apps do conector, introduza Olá Twilio valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc166-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="dc166-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="dc166-113">Property</span></span> | <span data-ttu-id="dc166-114">Necessário</span><span class="sxs-lookup"><span data-stu-id="dc166-114">Required</span></span> | <span data-ttu-id="dc166-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="dc166-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc166-116">ID da conta</span><span class="sxs-lookup"><span data-stu-id="dc166-116">Account ID</span></span> |<span data-ttu-id="dc166-117">Sim</span><span class="sxs-lookup"><span data-stu-id="dc166-117">Yes</span></span> |<span data-ttu-id="dc166-118">Introduza o seu ID de conta do Twilio</span><span class="sxs-lookup"><span data-stu-id="dc166-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="dc166-119">Token de acesso</span><span class="sxs-lookup"><span data-stu-id="dc166-119">Access Token</span></span> |<span data-ttu-id="dc166-120">Sim</span><span class="sxs-lookup"><span data-stu-id="dc166-120">Yes</span></span> |<span data-ttu-id="dc166-121">Introduza o seu token de acesso do Twilio</span><span class="sxs-lookup"><span data-stu-id="dc166-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="dc166-122">Se não tiver um token de acesso do Twilio, consulte [identidade de utilizador e Tokens de acesso](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="dc166-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="dc166-123">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="dc166-123">Connector-specific details</span></span>

<span data-ttu-id="dc166-124">Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="dc166-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="dc166-125">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="dc166-125">More connectors</span></span>
<span data-ttu-id="dc166-126">Voltar atrás toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="dc166-126">Go back toohello [APIs list](apis-list.md).</span></span>
