---
title: "Alojar vários sites no Gateway de Aplicações do Azure | Microsoft Docs"
description: "Esta página fornece uma descrição geral do suporte para vários sites do Gateway de Aplicação."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Alojamento de vários sites do Gateway de Aplicação

O alojamento de vários sites permite-lhe configurar mais do que uma aplicação Web na mesma instância do gateway de aplicação. Esta funcionalidade permite-lhe configurar uma topologia mais eficiente para as suas implementações ao adicionar até 20 sites a um gateway de aplicação. Cada site pode ser direcionado para o seu próprio agrupamento de back-end. No exemplo seguinte, o gateway de aplicação está a enviar tráfego para contoso.com e fabrikam.com a partir de dois agrupamentos de servidores de back-end com o nome ContosoServerPool e FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> As regras são processadas pela ordem em que são apresentadas no portal. Antes de configurar um serviço de escuta básico, recomenda-se vivamente que configure serviços de escuta de múltiplos sites.  Desta forma, assegura-se que o tráfego é encaminhado para o back-end certo. Se for apresentado primeiro um serviço de escuta básico e este corresponde a um pedido de entrada, o pedido é processado por esse serviço de escuta.

Os pedidos enviados para http://contoso.com são encaminhados para ContosoServerPool, enquanto os pedidos para http://fabrikam.com são encaminhados para FabrikamServerPool.

Da mesma forma, dois subdomínios do mesmo domínio principal podem ser alojados na mesma implementação do gateway de aplicação. Os exemplos de como utilizar subdomínios podem incluir o http://blog.contoso.com e o http://app.contoso.com alojados numa única implementação do gateway de aplicação.

## <a name="host-headers-and-server-name-indication-sni"></a>Cabeçalhos de anfitrião e Indicação do Nome de Servidor (SNI)

Existem três mecanismos comuns que permitem alojar vários sites na mesma infraestrutura.

1. Aloje várias aplicações Web, cada uma num endereço IP exclusivo.
2. Utilize o nome do anfitrião para alojar várias aplicações Web no mesmo endereço IP.
3. Utilize portas diferentes para alojar várias aplicações Web no mesmo endereço IP.

De momento, um gateway de aplicação obtém um endereço IP público exclusivo no qual escuta tráfego. Por conseguinte, atualmente, não é possível suportar várias aplicações, cada uma com o seu próprio endereço IP. O Gateway de Aplicação suporta o alojamento de várias aplicações, cada uma a escutar em portas diferentes. No entanto, este cenário requer que as aplicações aceitem tráfego em portas não padrão, o que, normalmente, não é uma configuração desejada. O Gateway de Aplicação conta com os cabeçalhos de anfitrião HTTP 1.1 para alojar mais do que um site no mesmo endereço IP público e porta. Os sites alojados no gateway de aplicação também podem suportar descarga de SSL com a extensão TLS da Indicação do Nome de Servidor (SNI). Neste cenário, o browser cliente e o web farm de back-end têm de suportar HTTP/1.1 e a extensão TLS conforme definido em RFC 6066.

## <a name="listener-configuration-element"></a>Elemento de configuração do serviço de escuta

O elemento de configuração HTTPListener existente foi melhorado para suportar elementos de nome de anfitrião e de indicação do nome de servidor, os quais são utilizados pelo gateway de aplicação para encaminhar tráfego para o agrupamento de back-end adequado. O seguinte exemplo de código é o fragmento do elemento HttpListeners do ficheiro de modelo.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Pode visitar o [modelo do Resource Manager através do alojamento de vários sites](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) para obter uma implementação baseada num modelo ponto a ponto.

## <a name="routing-rule"></a>Regra de encaminhamento

Não há qualquer alteração obrigatória na regra de encaminhamento. Deve continuar a escolher a regra de encaminhamento “Básica” para associar o serviço de escuta de sites ao conjunto de endereços de back-end correspondente.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Passos seguintes

Depois de saber mais sobre o alojamento de vários sites, veja o artigo [Criar um gateway de aplicação através do alojamento de vários sites](application-gateway-create-multisite-azureresourcemanager-powershell.md) para criar um gateway de aplicação com capacidade para suportar mais do que uma aplicação Web.

