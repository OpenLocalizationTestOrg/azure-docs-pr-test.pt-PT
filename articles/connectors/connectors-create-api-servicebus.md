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
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Introdução ao conector do Service Bus do Azure Olá
Ligue tooAzure toosend de Service Bus e receber mensagens. Pode realizar ações tais como tooqueue de envio, enviar tootopic, receber da fila e receber da subscrição.

toouse [qualquer conector](apis-list.md), terá primeiro de toocreate uma aplicação lógica. Pode começar a utilizar pelo [criar uma aplicação lógica agora](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Ligar tooService Bus
Antes da aplicação lógica pode aceder a qualquer serviço, terá primeiro de toocreate um serviço de toohello de ligação. A [ligação](connectors-overview.md) fornece conectividade entre uma aplicação lógica e outro serviço.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Utilizar um acionador de Service Bus
Um acionador é um evento que pode ser o fluxo de trabalho do Olá toostart utilizados definido numa aplicação lógica. [Saiba mais sobre acionadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Utilizar uma ação de barramento de serviço
Uma ação é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica. [Saiba mais sobre as ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/servicebus/). 

## <a name="next-steps"></a>Passos seguintes
[Criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md).

