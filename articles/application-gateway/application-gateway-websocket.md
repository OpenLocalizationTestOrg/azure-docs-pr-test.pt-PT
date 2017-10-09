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
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="667ad-103">Descrição geral do suporte de WebSocket no Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="667ad-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="667ad-104">Gateway de aplicação fornece suporte nativo para WebSocket em todos os tamanhos de gateway.</span><span class="sxs-lookup"><span data-stu-id="667ad-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="667ad-105">Não há nenhuma definição configurável pelo utilizador tooselectively ativar ou desativar o suporte de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="667ad-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="667ad-106">Protocolo de WebSocket padronizado nas [RFC6455](https://tools.ietf.org/html/rfc6455) permite uma comunicação completa duplex entre um servidor e um cliente através de uma ligação de TCP de longa execução.</span><span class="sxs-lookup"><span data-stu-id="667ad-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="667ad-107">Esta funcionalidade permite para uma comunicação mais interativa entre Olá servidor web e o cliente Olá, que pode ser bidirecional sem necessidade de Olá para consulta como implementações necessárias no baseado em HTTP.</span><span class="sxs-lookup"><span data-stu-id="667ad-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="667ad-108">WebSocket baixa tem sobrecarga ao contrário de HTTP e pode reutilizar Olá mesma ligação TCP de vários/respostas de pedidos que resulta numa utilização mais eficiente dos recursos.</span><span class="sxs-lookup"><span data-stu-id="667ad-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="667ad-109">Protocolos de WebSocket são toowork concebida tradicionais HTTP as portas 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="667ad-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="667ad-110">Pode continuar a utilizar um serviço de escuta HTTP padrão na porta 80 ou 443 tooreceive tráfego de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="667ad-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="667ad-111">O tráfego de WebSocket é então direcionado toohello WebSocket ativado utilizando o conjunto de back-end adequado Olá conforme especificado nas regras de gateway de aplicação de servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="667ad-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="667ad-112">servidor de back-end Olá tem de responder toohello application gateway sondas que são descritas nas Olá [descrição geral de sonda de estado de funcionamento](application-gateway-probe-overview.md) secção.</span><span class="sxs-lookup"><span data-stu-id="667ad-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="667ad-113">Sondas de estado de funcionamento do gateway de aplicação só são HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="667ad-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="667ad-114">Cada servidor de back-end tem de responder tooHTTP sondas aplicação servidor de gateway tooroute WebSocket tráfego toohello.</span><span class="sxs-lookup"><span data-stu-id="667ad-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="667ad-115">Elemento de configuração do serviço de escuta</span><span class="sxs-lookup"><span data-stu-id="667ad-115">Listener configuration element</span></span>

<span data-ttu-id="667ad-116">Um serviço de escuta HTTP existente pode ser utilizado toosupport tráfego de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="667ad-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="667ad-117">Olá que se segue um fragmento de um elemento de httpListeners de um ficheiro de modelo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="667ad-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="667ad-118">Seria necessário toosupport de serviços de escuta HTTP e HTTPS WebSocket e proteger o tráfego de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="667ad-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="667ad-119">Da mesma forma pode utilizar Olá [portal](application-gateway-create-gateway-portal.md) ou [PowerShell](application-gateway-create-gateway-arm.md) toocreate um gateway de aplicação com os serviços de escuta o tráfego do porta 80/443 toosupport WebSocket.</span><span class="sxs-lookup"><span data-stu-id="667ad-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="667ad-120">Configuração da regra BackendAddressPool, BackendHttpSetting e encaminhamento</span><span class="sxs-lookup"><span data-stu-id="667ad-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="667ad-121">Um BackendAddressPool é toodefine utilizado um conjunto de back-end com servidores de WebSocket ativada.</span><span class="sxs-lookup"><span data-stu-id="667ad-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="667ad-122">Olá backendHttpSetting está definida com uma back-end a porta 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="667ad-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="667ad-123">Propriedades de Olá de afinidade com base em cookies e requestTimeouts não são relevantes tooWebSocket tráfego.</span><span class="sxs-lookup"><span data-stu-id="667ad-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="667ad-124">Não há nenhuma alteração necessária na regra de encaminhamento Olá, 'Basic' tootie utilizados Olá adequado do serviço de escuta toohello correspondente do conjunto de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="667ad-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="667ad-125">Back-end de WebSocket ativada</span><span class="sxs-lookup"><span data-stu-id="667ad-125">WebSocket enabled backend</span></span>

<span data-ttu-id="667ad-126">Back-end tem de ter um servidor de web HTTP/HTTPS em execução no Olá configurado porta (normalmente, 80/443) para toowork de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="667ad-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="667ad-127">Este requisito é porque protocolo WebSocket requer Olá handshake inicial toobe HTTP com o protocolo de atualização tooWebSocket como um campo de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="667ad-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="667ad-128">Olá segue-se um exemplo de um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="667ad-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="667ad-129">Outra razão para isto é que sonda de estado de funcionamento de back-end de gateway de aplicação suporta apenas protocolos HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="667ad-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="667ad-130">Se o servidor de back-end Olá não responder tooHTTP ou sondas HTTPS, é colocado fora do conjunto back-end.</span><span class="sxs-lookup"><span data-stu-id="667ad-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="667ad-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="667ad-131">Next steps</span></span>

<span data-ttu-id="667ad-132">Depois de aprender mais sobre o suporte de WebSocket, aceda demasiado[criar um gateway de aplicação](application-gateway-create-gateway.md) tooget começar a utilizar um WebSocket ativada a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="667ad-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

