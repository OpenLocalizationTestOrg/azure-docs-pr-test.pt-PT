---
title: "aaaCreate um Gateway de aplicação do Azure - Azure CLI 2.0 | Microsoft Docs"
description: "Saiba como toocreate um Gateway de aplicação utilizando Olá 2.0 CLI do Azure no Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Criar um gateway de aplicação utilizando Olá Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modelo do Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI do Azure 1.0](application-gateway-create-gateway-cli.md)
> * [CLI 2.0 do Azure](application-gateway-create-gateway-cli.md)

Gateway de aplicação é uma aplicação virtual dedicada que fornece o controlador de entrega de aplicações (ADC) como um serviço, oferece várias camada 7 carregar balanceamento capacidades para a sua aplicação.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá

Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -nosso CLI para Olá clássica e resource Gestão modelos de implementação.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá

## <a name="prerequisite-install-hello-azure-cli-20"></a>Pré-requisito: Instalar Olá Azure CLI 2.0

Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Se não tiver uma conta do Azure, é necessário um. Subscreva [uma avaliação gratuita aqui](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Cenário

Neste cenário, saiba como toocreate um gateway de aplicação utilizando Olá portal do Azure.

Neste cenário irão:

* Crie um gateway de aplicação médias com duas instâncias.
* Crie uma rede virtual denominada AdatumAppGatewayVNET com um bloco CIDR reservado de 10.0.0.0/16.
* Criar uma sub-rede denominada Appgatewaysubnet que utiliza 10.0.0.0/28 como bloco CIDR.

> [!NOTE]
> Pesquisas de configuração adicional do gateway de aplicação Olá, incluindo o estado de funcionamento personalizado, os endereços do conjunto de back-end e regras adicionais são configurados após a configuração do gateway de aplicação Olá e não durante a implementação inicial.

## <a name="before-you-begin"></a>Antes de começar

Gateway de aplicação do Azure requer a sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que deixe suficiente toohave de espaço de endereço várias sub-redes. Depois de implementar uma sub-rede de tooa do gateway de aplicação, gateways de aplicação apenas adicionais podem ser adicionados toohello sub-rede.

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure

Abra Olá **linha de comandos do Microsoft Azure**e inicie sessão. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> Também pode utilizar `az login` sem comutador Olá para início de sessão de dispositivo que necessita de introduzir um código no aka.ms/devicelogin.

Depois de escrever Olá anterior exemplo, é fornecido um código. Navegue toohttps://aka.ms/devicelogin um processo de início de sessão do browser toocontinue Olá.

![o início de sessão do cmd que mostra dispositivos][1]

No browser Olá, introduza o código de Olá que recebeu. São tooa redirecionada-página sessão.

![código de tooenter do browser][2]

Assim que foi introduzido um código de Olá tem sessão iniciada, fechar Olá browser toocontinue com cenário Olá.

![sessão iniciada com êxito][3]

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de Olá

Antes de criar o gateway de aplicação Olá, o gateway de aplicação Olá toocontain é criado um grupo de recursos. seguinte Olá mostra comandos Olá.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Criar gateway de aplicação Olá

endereços IP de Olá utilizados para o back-end de Olá são endereços IP de Olá para o servidor de back-end. Estes valores podem ser ambos IPs privados numa rede virtual Olá, os ips públicos ou nomes de domínio totalmente qualificados para os servidores de back-end. Olá exemplo seguinte cria um gateway de aplicação com as definições de configuração adicionais para definições de http, portas e regras.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Olá anterior exemplo mostra várias propriedades que não são necessárias durante a criação de Olá de um gateway de aplicação. Olá seguinte exemplo de código cria um gateway de aplicação com as informações de Olá necessário.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Para obter uma lista de parâmetros que podem ser fornecidos durante Olá de criação, execute os seguintes comandos: `az network application-gateway create --help`.

Este exemplo cria um gateway de aplicação básico com as predefinições para o serviço de escuta de Olá, conjunto back-end, as definições http de back-end e regras. Pode modificar estas definições toosuit a implementação depois de aprovisionamento de Olá é efetuada com êxito.
Se já tiver a sua aplicação web definida com o conjunto de back-end Olá no Olá precedente passos, uma vez criados, o balanceamento de carga é iniciada.

## <a name="get-application-gateway-dns-name"></a>Obter nome de DNS de gateway de aplicação

Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação. Ao utilizar um IP público, o gateway de aplicação requer um nome DNS dinamicamente atribuído, que não é amigável. os utilizadores finais de tooensure pode atingiu o gateway de aplicação Olá, um registo CNAME pode ser utilizado toopoint toohello ponto final público Olá do gateway de aplicação. [Configurar um nome de domínio personalizado no Azure](../dns/dns-custom-domain.md). tooconfigure alias, obter detalhes do gateway de aplicação Olá e o respetivo nome IP/DNS associado com o gateway de aplicação do Olá PublicIPAddress elemento toohello anexado. nome DNS do gateway de aplicação Olá deve ser utilizado toocreate um registo CNAME, nome DNS de toothis de aplicações que pontos Olá dois web. utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway de aplicação.


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
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

## <a name="delete-all-resources"></a>Eliminar todos os recursos

toodelete todos os recursos criados neste artigo, Olá concluir os seguintes passos:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Passos seguintes

Saiba como o estado de funcionamento personalizado toocreate sondas, visitando [criar uma sonda do Estado de funcionamento personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarga de SSL e de desencriptação de SSL dispendiosa do tirar Olá desativado seus servidores web, visitando [configurar a descarga de SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
