---
title: "conector do aaaLearn toouse Olá Service Bus do Azure nas suas logic apps | Microsoft Docs"
description: "Crie aplicações lógicas com o App service do Azure. Ligue tooAzure toosend de Service Bus e receber mensagens. Pode realizar ações tais como tooqueue de envio, enviar tootopic, receber da fila e receber da subscrição."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="66881-105">Introdução ao conector do Service Bus do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="66881-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="66881-106">Ligue tooAzure toosend de Service Bus e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="66881-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="66881-107">Pode realizar ações tais como tooqueue de envio, enviar tootopic, receber da fila e receber da subscrição.</span><span class="sxs-lookup"><span data-stu-id="66881-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="66881-108">toouse [qualquer conector](apis-list.md), terá primeiro de toocreate uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="66881-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="66881-109">Pode começar a utilizar pelo [criar uma aplicação lógica agora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="66881-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="66881-110">Ligar tooService Bus</span><span class="sxs-lookup"><span data-stu-id="66881-110">Connect tooService Bus</span></span>
<span data-ttu-id="66881-111">Antes da aplicação lógica pode aceder a qualquer serviço, terá primeiro de toocreate um serviço de toohello de ligação.</span><span class="sxs-lookup"><span data-stu-id="66881-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="66881-112">A [ligação](connectors-overview.md) fornece conectividade entre uma aplicação lógica e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="66881-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="66881-113">Utilizar um acionador de Service Bus</span><span class="sxs-lookup"><span data-stu-id="66881-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="66881-114">Um acionador é um evento que pode ser o fluxo de trabalho do Olá toostart utilizados definido numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="66881-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="66881-115">[Saiba mais sobre acionadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="66881-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="66881-116">Utilizar uma ação de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="66881-116">Use a Service Bus action</span></span>
<span data-ttu-id="66881-117">Uma ação é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="66881-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="66881-118">[Saiba mais sobre as ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="66881-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="66881-119">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="66881-119">Connector-specific details</span></span>

<span data-ttu-id="66881-120">Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="66881-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="66881-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="66881-121">Next steps</span></span>
<span data-ttu-id="66881-122">[Criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="66881-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

