---
title: "esquemas de controlo de aaaAS2 para monitorização B2B - Azure Logic Apps | Microsoft Docs"
description: "Utilizar AS2 mensagens toomonitor B2B de esquemas de controlo de transações na sua conta de integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Iniciar ou ativar o controlo de propriedades da mensagem, erros e MDNs toomonitor êxito e as mensagens de AS2
Pode utilizar estes esquemas de controlo AS2 no seu toohelp de conta de integração do Azure, monitorizar transações de empresa-empresa (B2B):

* Esquema de controlo de mensagem AS2
* Esquema de controlo AS2 MDN

## <a name="as2-message-tracking-schema"></a>Esquema de controlo de mensagem AS2
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia | Nome do parceiro do remetente da mensagem AS2. (Opcional) |
| receiverPartnerName | Cadeia | Nome do parceiro do recetor de mensagem AS2. (Opcional) |
| as2To | Cadeia | Nome de recetor de mensagem a AS2, de cabeçalhos de Olá de mensagem de saudação AS2. (Obrigatório) |
| as2From | Cadeia | Nome do remetente da mensagem AS2, de cabeçalhos de Olá de mensagem de saudação AS2. (Obrigatório) |
| agreementName | Cadeia | Nome de mensagens hello do AS2 contrato toowhich Olá são resolvidos. (Opcional) |
| direção | Cadeia | Direção do fluxo de mensagens de Olá, receber ou enviar. (Obrigatório) |
| messageId | Cadeia | ID de mensagem AS2, de cabeçalhos de Olá de mensagem de saudação AS2 (opcional) |
| dispositionType |Cadeia | Valor de tipo de mensagem disposição notificação (MDN) disposição. (Opcional) |
| fileName | Cadeia | Nome do ficheiro de cabeçalho de Olá da mensagem de saudação AS2. (Opcional) |
| isMessageFailed |Valor booleano | Indica se a mensagem de saudação AS2 falhou. (Obrigatório) |
| isMessageSigned | Valor booleano | Indica se a mensagem de saudação AS2 foi assinada. (Obrigatório) |
| isMessageEncrypted | Valor booleano | Indica se a mensagem de saudação AS2 foi encriptada. (Obrigatório) |
| isMessageCompressed |Valor booleano | Indica se a mensagem de saudação AS2 foi comprimida. (Obrigatório) |
| CorrelationMessageId | Cadeia | ID de mensagem AS2, mensagens de toocorrelate com MDNs. (Opcional) |
| incomingHeaders |Dicionário de JToken | Detalhes de cabeçalho de mensagem de entrada AS2. (Opcional) |
| outgoingHeaders |Dicionário de JToken | Detalhes de cabeçalho de mensagem de saída AS2. (Opcional) |
| isNrrEnabled | Valor booleano | Utilize o valor predefinido se o valor de Olá não é conhecido. (Obrigatório) |
| isMdnExpected | Valor booleano | Utilize o valor predefinido se o valor de Olá não é conhecido. (Obrigatório) |
| mdnType | Enum | Valores permitidos são **NotConfigured**, **sincronização**, e **Async**. (Obrigatório) |

## <a name="as2-mdn-tracking-schema"></a>Esquema de controlo AS2 MDN
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia | Nome do parceiro do remetente da mensagem AS2. (Opcional) |
| receiverPartnerName | Cadeia | Nome do parceiro do recetor de mensagem AS2. (Opcional) |
| as2To | Cadeia | Nome do parceiro que recebe a mensagem de saudação AS2. (Obrigatório) |
| as2From | Cadeia | Nome do parceiro que envia a mensagem de saudação AS2. (Obrigatório) |
| agreementName | Cadeia | Nome de mensagens hello do AS2 contrato toowhich Olá são resolvidos. (Opcional) |
| direção |Cadeia | Direção do fluxo de mensagens de Olá, receber ou enviar. (Obrigatório) |
| messageId | Cadeia | ID de mensagem AS2. (Opcional) |
| originalMessageId |Cadeia | AS2 original ID de mensagem. (Opcional) |
| dispositionType | Cadeia | Valor do tipo MDN disposição. (Opcional) |
| isMessageFailed |Valor booleano | Indica se a mensagem de saudação AS2 falhou. (Obrigatório) |
| isMessageSigned |Valor booleano | Indica se a mensagem de saudação AS2 foi assinada. (Obrigatório) |
| isNrrEnabled | Valor booleano | Utilize o valor predefinido se o valor de Olá não é conhecido. (Obrigatório) |
| statusCode | Enum | Valores permitidos são **aceites**, **rejeitado**, e **AcceptedWithErrors**. (Obrigatório) |
| micVerificationStatus | Enum | Valores permitidos são **NotApplicable**, **com êxito**, e **falha**. (Obrigatório) |
| CorrelationMessageId | Cadeia | ID de correlação. Olá original messaged ID (ID de mensagem de mensagem de saudação para o qual está configurada MDN Olá). (Opcional) |
| incomingHeaders | Dicionário de JToken | Indica os detalhes de cabeçalho da mensagem recebida. (Opcional) |
| outgoingHeaders |Dicionário de JToken | Indica a enviar detalhes de cabeçalho da mensagem. (Opcional) |

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* Saiba mais sobre [monitorização mensagens B2B](logic-apps-monitor-b2b-message.md).   
* Saiba mais sobre [B2B esquemas de controlo personalizado](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Saiba mais sobre [X12 controlo esquemas](logic-apps-track-integration-account-x12-tracking-schema.md).   
* Saiba mais sobre [controlo mensagens B2B no portal de Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
