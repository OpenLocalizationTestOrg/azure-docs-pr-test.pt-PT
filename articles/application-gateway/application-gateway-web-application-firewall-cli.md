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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Configurar a firewall de aplicação web num Gateway de aplicação nova ou existente com a CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI do Azure](application-gateway-web-application-firewall-cli.md)

Saiba como toocreate uma firewall de aplicação web ativado o gateway de aplicação ou adicione web firewall tooan existente application gateway de aplicação.

Olá firewall de aplicações web (WAF) no Gateway de aplicação do Azure protege as aplicações web de ataques baseados na web comuns, como a injeção de SQL, ataques de scripts entre sites e hijacks de sessão.

O Application Gateway do Azure é um balanceador de carga de 7 camadas. Fornece ativação pós-falha, pedidos HTTP de encaminhamento de desempenho entre diferentes servidores, quer estejam na nuvem de Olá ou no local. Gateway de aplicação fornece as funcionalidades do controlador (ADC) entrega muitas aplicações, incluindo HTTP carga balanceamento, com base no cookie de afinidade de sessão, a descarga de segura SSL (sockets layer), sondas de estado de funcionamento personalizado, o suporte para vários sites e muitas outras. toofind uma lista completa das funcionalidades suportadas, visite: [descrição geral do Gateway de aplicação](application-gateway-introduction.md).

Olá seguinte artigo mostra como demasiado[adicionar web firewall tooan existente application gateway de aplicação](#add-web-application-firewall-to-an-existing-application-gateway) e [criar um gateway de aplicação que utiliza a firewall de aplicações web](#create-an-application-gateway-with-web-application-firewall).

![imagem do cenário][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Pré-requisito: Instalar Olá Azure CLI 2.0

Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Diferenças de configuração WAF

Se tiver ler [criar um Gateway de aplicação com a CLI do Azure](application-gateway-create-gateway-cli.md), compreender Olá SKU definições tooconfigure ao criar um gateway de aplicação. WAF fornece definições adicionais toodefine quando configurar Olá SKU num gateway de aplicação. Não foram efetuadas alterações adicionais que efetuar no gateway de aplicação Olá próprio.

| **Definição** | **Detalhes**
|---|---|
|**SKU** |Um gateway de aplicação normal sem WAF suporta **padrão\_pequeno**, **padrão\_média**, e **padrão\_grande**tamanhos. Com a introdução de Olá de WAF, existem dois SKUs adicionais, **WAF\_média** e **WAF\_grande**. WAF não é suportado nos gateways de aplicação pequeno.|
|**Modo** | Esta definição é o modo de Olá da WAF. valores permitidos são **deteção** e **prevenção**. Quando WAF está configurado no modo de deteção, todas as ameaças são armazenadas num ficheiro de registo. No modo de prevenção, os eventos são registados ainda mas atacante Olá recebe uma resposta não autorizado 403 do gateway de aplicação Olá.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Adicionar web firewall tooan existente application gateway de aplicação

Olá siga as alterações do comando de um gateway de aplicação ativada de tooa WAF de gateway da aplicação padrão existente.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Este comando atualiza o gateway de aplicação Olá com firewall de aplicações web. Visite [diagnóstico do Gateway de aplicação](application-gateway-diagnostics.md) toounderstand como tooview registos para o gateway de aplicação. Devido a toohello segurança natureza WAF, registos necessidade toobe revisto regularmente postura de segurança de Olá toounderstand das suas aplicações web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Criar um Gateway de aplicação com firewall de aplicações web

Olá comando a seguir cria um Gateway de aplicação com firewall de aplicações web.

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
> Gateways de aplicação criados com a configuração de firewall de aplicação de web básico Olá estão configurados com CR 3.0 para proteção.

## <a name="get-application-gateway-dns-name"></a>Obter nome de DNS de gateway de aplicação

Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação. Ao utilizar um IP público, o gateway de aplicação requer um nome DNS dinamicamente atribuído, que não é amigável. os utilizadores finais de tooensure pode atingiu o gateway de aplicação Olá, um registo CNAME pode ser utilizado toopoint toohello ponto final público Olá do gateway de aplicação. [Configurar um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure um registo CNAME, obter detalhes do gateway de aplicação Olá e o respetivo nome IP/DNS associado com o gateway de aplicação do Olá PublicIPAddress elemento toohello anexado. nome DNS do gateway de aplicação Olá deve ser utilizado toocreate um registo CNAME, nome DNS de toothis de aplicações que pontos Olá dois web. utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway de aplicação.

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

## <a name="next-steps"></a>Passos seguintes

Saiba como toocustomize WAF regras, visitando: [personalizar regras de firewall de aplicação web através de Olá Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
