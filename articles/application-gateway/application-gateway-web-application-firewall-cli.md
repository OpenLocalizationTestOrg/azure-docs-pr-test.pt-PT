---
title: "firewall de aplicação web de aaaConfigure - Gateway de aplicação do Azure | Microsoft Docs"
description: "Este artigo fornece orientação sobre como utilizar toostart web firewall de aplicação num gateway de aplicação nova ou existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="0ab51-103">Configurar a firewall de aplicação web num Gateway de aplicação nova ou existente com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0ab51-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ab51-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0ab51-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="0ab51-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ab51-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="0ab51-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0ab51-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="0ab51-107">Saiba como toocreate uma firewall de aplicação web ativado o gateway de aplicação ou adicione web firewall tooan existente application gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="0ab51-108">Olá firewall de aplicações web (WAF) no Gateway de aplicação do Azure protege as aplicações web de ataques baseados na web comuns, como a injeção de SQL, ataques de scripts entre sites e hijacks de sessão.</span><span class="sxs-lookup"><span data-stu-id="0ab51-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="0ab51-109">O Application Gateway do Azure é um balanceador de carga de 7 camadas.</span><span class="sxs-lookup"><span data-stu-id="0ab51-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="0ab51-110">Fornece ativação pós-falha, pedidos HTTP de encaminhamento de desempenho entre diferentes servidores, quer estejam na nuvem de Olá ou no local.</span><span class="sxs-lookup"><span data-stu-id="0ab51-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="0ab51-111">Gateway de aplicação fornece as funcionalidades do controlador (ADC) entrega muitas aplicações, incluindo HTTP carga balanceamento, com base no cookie de afinidade de sessão, a descarga de segura SSL (sockets layer), sondas de estado de funcionamento personalizado, o suporte para vários sites e muitas outras.</span><span class="sxs-lookup"><span data-stu-id="0ab51-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="0ab51-112">toofind uma lista completa das funcionalidades suportadas, visite: [descrição geral do Gateway de aplicação](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ab51-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="0ab51-113">Olá seguinte artigo mostra como demasiado[adicionar web firewall tooan existente application gateway de aplicação](#add-web-application-firewall-to-an-existing-application-gateway) e [criar um gateway de aplicação que utiliza a firewall de aplicações web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="0ab51-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![imagem do cenário][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="0ab51-115">Pré-requisito: Instalar Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ab51-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="0ab51-116">Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0ab51-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="0ab51-117">Diferenças de configuração WAF</span><span class="sxs-lookup"><span data-stu-id="0ab51-117">WAF configuration differences</span></span>

<span data-ttu-id="0ab51-118">Se tiver ler [criar um Gateway de aplicação com a CLI do Azure](application-gateway-create-gateway-cli.md), compreender Olá SKU definições tooconfigure ao criar um gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="0ab51-119">WAF fornece definições adicionais toodefine quando configurar Olá SKU num gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="0ab51-120">Não foram efetuadas alterações adicionais que efetuar no gateway de aplicação Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="0ab51-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="0ab51-121">**Definição**</span><span class="sxs-lookup"><span data-stu-id="0ab51-121">**Setting**</span></span> | <span data-ttu-id="0ab51-122">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="0ab51-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="0ab51-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="0ab51-123">**SKU**</span></span> |<span data-ttu-id="0ab51-124">Um gateway de aplicação normal sem WAF suporta **padrão\_pequeno**, **padrão\_média**, e **padrão\_grande**tamanhos.</span><span class="sxs-lookup"><span data-stu-id="0ab51-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="0ab51-125">Com a introdução de Olá de WAF, existem dois SKUs adicionais, **WAF\_média** e **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="0ab51-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="0ab51-126">WAF não é suportado nos gateways de aplicação pequeno.</span><span class="sxs-lookup"><span data-stu-id="0ab51-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="0ab51-127">**Modo**</span><span class="sxs-lookup"><span data-stu-id="0ab51-127">**Mode**</span></span> | <span data-ttu-id="0ab51-128">Esta definição é o modo de Olá da WAF.</span><span class="sxs-lookup"><span data-stu-id="0ab51-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="0ab51-129">valores permitidos são **deteção** e **prevenção**.</span><span class="sxs-lookup"><span data-stu-id="0ab51-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="0ab51-130">Quando WAF está configurado no modo de deteção, todas as ameaças são armazenadas num ficheiro de registo.</span><span class="sxs-lookup"><span data-stu-id="0ab51-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="0ab51-131">No modo de prevenção, os eventos são registados ainda mas atacante Olá recebe uma resposta não autorizado 403 do gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="0ab51-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="0ab51-132">Adicionar web firewall tooan existente application gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="0ab51-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="0ab51-133">Olá siga as alterações do comando de um gateway de aplicação ativada de tooa WAF de gateway da aplicação padrão existente.</span><span class="sxs-lookup"><span data-stu-id="0ab51-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="0ab51-134">Este comando atualiza o gateway de aplicação Olá com firewall de aplicações web.</span><span class="sxs-lookup"><span data-stu-id="0ab51-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="0ab51-135">Visite [diagnóstico do Gateway de aplicação](application-gateway-diagnostics.md) toounderstand como tooview registos para o gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="0ab51-136">Devido a toohello segurança natureza WAF, registos necessidade toobe revisto regularmente postura de segurança de Olá toounderstand das suas aplicações web.</span><span class="sxs-lookup"><span data-stu-id="0ab51-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="0ab51-137">Criar um Gateway de aplicação com firewall de aplicações web</span><span class="sxs-lookup"><span data-stu-id="0ab51-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="0ab51-138">Olá comando a seguir cria um Gateway de aplicação com firewall de aplicações web.</span><span class="sxs-lookup"><span data-stu-id="0ab51-138">hello following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="0ab51-139">Gateways de aplicação criados com a configuração de firewall de aplicação de web básico Olá estão configurados com CR 3.0 para proteção.</span><span class="sxs-lookup"><span data-stu-id="0ab51-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0ab51-140">Obter nome de DNS de gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="0ab51-140">Get application gateway DNS name</span></span>

<span data-ttu-id="0ab51-141">Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="0ab51-142">Ao utilizar um IP público, o gateway de aplicação requer um nome DNS dinamicamente atribuído, que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="0ab51-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0ab51-143">os utilizadores finais de tooensure pode atingiu o gateway de aplicação Olá, um registo CNAME pode ser utilizado toopoint toohello ponto final público Olá do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="0ab51-144">[Configurar um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ab51-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="0ab51-145">tooconfigure um registo CNAME, obter detalhes do gateway de aplicação Olá e o respetivo nome IP/DNS associado com o gateway de aplicação do Olá PublicIPAddress elemento toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="0ab51-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="0ab51-146">nome DNS do gateway de aplicação Olá deve ser utilizado toocreate um registo CNAME, nome DNS de toothis de aplicações que pontos Olá dois web.</span><span class="sxs-lookup"><span data-stu-id="0ab51-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="0ab51-147">utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ab51-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="0ab51-148">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0ab51-148">Next steps</span></span>

<span data-ttu-id="0ab51-149">Saiba como toocustomize WAF regras, visitando: [personalizar regras de firewall de aplicação web através de Olá Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0ab51-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
