---
title: "aaaCustom esquemas de controlo para B2B monitorização - Azure Logic Apps | Microsoft Docs"
description: "Crie controlo personalizado esquemas toomonitor B2B mensagens de transações na sua conta de integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Ativar toomonitor de controlo de fluxo de trabalho completado, ponto a ponto
Não há incorporadas que pode ativar para diferentes partes da sua empresa-empresa de fluxo de trabalho, tais como controlo AS2 ou X12 mensagens de controlo. Quando criar fluxos de trabalho que inclui uma aplicação lógica, BizTalk Server, SQL Server ou qualquer outra camada, em seguida, pode ativar o controlo personalizado que regista eventos a partir da extremidade de toohello Olá início do fluxo de trabalho. 

Este tópico fornece código personalizado que pode utilizar camadas de Olá fora da sua aplicação lógica. 

## <a name="custom-tracking-schema"></a>Esquema de controlo personalizado
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| SourceType |   | Tipo de origem Olá executar. Valores permitidos são **Microsoft.Logic/workflows** e **personalizado**. (Obrigatório) |
| Origem |   | Se for de tipo de origem Olá **Microsoft.Logic/workflows**, precisam de informações da origem Olá toofollow neste esquema. Se for de tipo de origem Olá **personalizado**, esquema de Olá é um JToken. (Obrigatório) |
| systemId | Cadeia | ID de sistema da aplicação lógica. (Obrigatório) |
| runId | Cadeia | Aplicação de lógica executar ID. (Obrigatório) |
| operationName | Cadeia | Nome da operação de Olá (por exemplo, ação ou acionador). (Obrigatório) |
| repeatItemScopeName | Cadeia | Repita o nome do item se ação Olá está dentro de um `foreach` / `until` ciclo. (Obrigatório) |
| repeatItemIndex | Número inteiro | Se a ação de Olá está dentro de um `foreach` / `until` ciclo. Indica o índice de itens repetido de Olá. (Obrigatório) |
| trackingId | Cadeia | ID de controlo, mensagens hello do toocorrelate. (Opcional) |
| correlationId | Cadeia | ID de correlação, mensagens hello do toocorrelate. (Opcional) |
| clientRequestId | Cadeia | Cliente pode preenchê-lo toocorrelate mensagens. (Opcional) |
| eventLevel |   | Nível de evento Olá. (Obrigatório) |
| eventTime |   | Hora do evento de Olá, em formato UTC aaaa-MM-DDTHH:MM:SS.00000Z. (Obrigatório) |
| recordType |   | Tipo de registo de controlar Olá. Permitido é de valor **personalizado**. (Obrigatório) |
| registo |   | Tipo de registo personalizado. O formato permitido é JToken. (Obrigatório) |

## <a name="b2b-protocol-tracking-schemas"></a>Esquemas de controlo de protocolo de B2B
Para obter informações sobre o protocolo de B2B esquemas de controlo, consulte:
* [Esquemas de controlo de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Esquemas de controlo de X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [monitorização mensagens B2B](logic-apps-monitor-b2b-message.md).   
* Saiba mais sobre [controlo mensagens B2B no portal de Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).
