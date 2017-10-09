---
title: "escala de aaaAutomatically unidades de débito de Event Hubs do Azure | Microsoft Docs"
description: "Ativar automaticamente-inflate numa escala tooautomatically espaço de nomes unidades de débito"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Dimensionar automaticamente unidades de débito de Event Hubs do Azure

## <a name="overview"></a>Descrição geral

Os Hubs de eventos do Azure é uma plataforma de transmissão em fluxo de dados altamente dimensionáveis. Como tal, os clientes de Event Hubs, muitas vezes, aumentam a respetiva utilização após integração toohello serviço. Essa aumenta requerem crescente Olá predetermined débito unidades (TUs) tooscale Event Hubs e processar taxas de transferência maior. Olá *Auto-inflate* funcionalidade dos Event Hubs automaticamente ajusta-se o número de Olá de necessidades de utilização de toomeet TUs. Aumentar TUs impede cenários, na qual a limitação:

* Entrada de dados excedem as taxas de definir TUs.
* Pedido de saída de dados excedem as taxas de definir TUs.

## <a name="how-auto-inflate-works"></a>Como funciona o inflate de automática

Tráfego de Hubs de eventos é controlado pelas unidades de débito. Um único TU permite 1 MB por segundo de entrada e de duas vezes que quantidade de saída. Hubs de eventos Standard pode ser configurados com 1-20 unidades de débito. Auto-inflate permite-lhe toostart pequeno com unidades de débito necessário mínimo Olá. funcionalidade de Olá dimensiona, em seguida, automaticamente toohello limite máximo de unidades de débito que precisa, consoante Olá aumento no tráfego. Auto-inflate fornece Olá seguintes vantagens:

- Um toostart de mecanismo dimensionamento eficiente pequeno e o trabalho de dimensionamento como aumentar.
- Dimensione o limite superior especificado toohello sem problemas de limitação.
- Mais controlam sobre o dimensionamento, como pode controlar quando e quantidade tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Ativar o inflate de automaticamente um espaço de nomes

Pode ativar ou desativar a inflate de automática de mensagens em fila um espaço de nomes utilizando um dos seguintes métodos de Olá:

1. Olá [portal do Azure](https://portal.azure.com).
2. Um modelo Azure Resource Manager.

### <a name="enable-auto-inflate-through-hello-portal"></a>Ativar automaticamente-inflate através do portal Olá

Pode ativar Olá Auto-inflate funcionalidade num espaço de nomes ao criar um espaço de nomes de Hubs de eventos:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Com esta opção ativada, pode começar por algo pequeno nas suas unidades de débito e dimensione à medida que a utilização da necessidades aumento. Olá limite superior para inflation não afeta os preços, que depende do número de Olá de TUs utilizada por hora.

Também pode ativar Auto-inflate utilizando Olá **escala** opção no painel de definições de Olá no portal de Olá:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Ativar Inflate automático utilizando um modelo Azure Resource Manager

Pode ativar inflate de automática durante uma implementação de modelo Azure Resource Manager. Por exemplo, o conjunto Olá `isAutoInflateEnabled` propriedade demasiado**verdadeiro** e defina `maximumThroughputUnits` too10.

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

Para o modelo completo Olá, consulte Olá [criar Hubs de eventos espaço de nomes e ativar inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modelo no GitHub.

## <a name="next-steps"></a>Passos seguintes

Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:

* [Descrição geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um Hub de Eventos](event-hubs-create.md)
