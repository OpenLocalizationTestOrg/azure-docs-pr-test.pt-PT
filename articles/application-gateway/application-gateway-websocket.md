---
title: "suporte de aaaWebSocket no Gateway de aplicação do Azure | Microsoft Docs"
description: "Esta página fornece uma descrição geral de Olá suporte de WebSocket do Gateway de aplicação."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>Descrição geral do suporte de WebSocket no Gateway de aplicação

Gateway de aplicação fornece suporte nativo para WebSocket em todos os tamanhos de gateway. Não há nenhuma definição configurável pelo utilizador tooselectively ativar ou desativar o suporte de WebSocket. 

Protocolo de WebSocket padronizado nas [RFC6455](https://tools.ietf.org/html/rfc6455) permite uma comunicação completa duplex entre um servidor e um cliente através de uma ligação de TCP de longa execução. Esta funcionalidade permite para uma comunicação mais interativa entre Olá servidor web e o cliente Olá, que pode ser bidirecional sem necessidade de Olá para consulta como implementações necessárias no baseado em HTTP. WebSocket baixa tem sobrecarga ao contrário de HTTP e pode reutilizar Olá mesma ligação TCP de vários/respostas de pedidos que resulta numa utilização mais eficiente dos recursos. Protocolos de WebSocket são toowork concebida tradicionais HTTP as portas 80 e 443.

Pode continuar a utilizar um serviço de escuta HTTP padrão na porta 80 ou 443 tooreceive tráfego de WebSocket. O tráfego de WebSocket é então direcionado toohello WebSocket ativado utilizando o conjunto de back-end adequado Olá conforme especificado nas regras de gateway de aplicação de servidor de back-end. servidor de back-end Olá tem de responder toohello application gateway sondas que são descritas nas Olá [descrição geral de sonda de estado de funcionamento](application-gateway-probe-overview.md) secção. Sondas de estado de funcionamento do gateway de aplicação só são HTTP/HTTPS. Cada servidor de back-end tem de responder tooHTTP sondas aplicação servidor de gateway tooroute WebSocket tráfego toohello.

## <a name="listener-configuration-element"></a>Elemento de configuração do serviço de escuta

Um serviço de escuta HTTP existente pode ser utilizado toosupport tráfego de WebSocket. Olá que se segue um fragmento de um elemento de httpListeners de um ficheiro de modelo de exemplo. Seria necessário toosupport de serviços de escuta HTTP e HTTPS WebSocket e proteger o tráfego de WebSocket. Da mesma forma pode utilizar Olá [portal](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) toocreate um gateway de aplicação com os serviços de escuta o tráfego do porta 80/443 toosupport WebSocket.

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>Configuração da regra BackendAddressPool, BackendHttpSetting e encaminhamento

Um BackendAddressPool é toodefine utilizado um conjunto de back-end com servidores de WebSocket ativada. Olá backendHttpSetting está definida com uma back-end a porta 80 e 443. Propriedades de Olá de afinidade com base em cookies e requestTimeouts não são relevantes tooWebSocket tráfego. Não há nenhuma alteração necessária na regra de encaminhamento Olá, 'Basic' tootie utilizados Olá adequado do serviço de escuta toohello correspondente do conjunto de endereços de back-end. 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>Back-end de WebSocket ativada

Back-end tem de ter um servidor de web HTTP/HTTPS em execução no Olá configurado porta (normalmente, 80/443) para toowork de WebSocket. Este requisito é porque protocolo WebSocket requer Olá handshake inicial toobe HTTP com o protocolo de atualização tooWebSocket como um campo de cabeçalho. Olá segue-se um exemplo de um cabeçalho:

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

Outra razão para isto é que sonda de estado de funcionamento de back-end de gateway de aplicação suporta apenas protocolos HTTP e HTTPS. Se o servidor de back-end Olá não responder tooHTTP ou sondas HTTPS, é colocado fora do conjunto back-end.

## <a name="next-steps"></a>Passos seguintes

Depois de aprender mais sobre o suporte de WebSocket, aceda demasiado[criar um gateway de aplicação](application-gateway-create-gateway.md) tooget começar a utilizar um WebSocket ativada a aplicação web.

