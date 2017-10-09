---
title: "aaaConfigure SSL offload - Gateway de aplicação do Azure - PowerShell | Microsoft Docs"
description: "Esta página fornece toocreate instruções um gateway de aplicação com SSL offload utilizando o Gestor de recursos do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Configurar um gateway de aplicação para a descarga de SSL com o Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI 2.0 do Azure](application-gateway-ssl-cli.md)

Gateway de aplicação do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão em Olá gateway tooavoid dispendiosa SSL desencriptação tarefas toohappen no farm do Olá web. Descarga de SSL também simplifica a configuração do servidor front-end Olá e a gestão de aplicações web de Olá.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente do Olá Olá Azure de cmdlets do PowerShell, utilizando Olá instalador de plataforma Web. Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferências](https://azure.microsoft.com/downloads/).
2. Criar uma rede virtual e uma sub-rede de gateway de aplicação Olá. Certifique-se de que nenhuma máquina virtual ou implementações de nuvem estão a utilizar a sub-rede de Olá. O Application Gateway tem de constar, por si só, numa sub-rede de rede virtual.
3. servidores de Olá configurar o gateway de aplicação Olá toouse tem de existir ou tem os respetivos pontos finais criados na rede virtual Olá ou com um IP/VIP público atribuído.

## <a name="what-is-required-toocreate-an-application-gateway"></a>O que é necessário toocreate um gateway de aplicação?

* **Agrupamento de servidores de back-end:** lista Olá de endereços IP dos servidores de back-end Olá. endereços IP Olá listados devem pertencer toohello sub-rede da rede virtual ou devem ser um IP/VIP público.
* **Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies. Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá.
* **Porta de front-end:** esta porta é Olá Porta pública aberta no gateway de aplicação Olá. O tráfego chega a esta porta e, em seguida, obtém redirecionado tooone dos servidores de back-end Olá.
* **Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estas definições são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).
* **Regra:** regra Olá vincula o serviço de escuta de Olá e agrupamento de servidores de back-end de Olá e define o tráfego de Olá de agrupamento de servidores de back-end deve ser direcionado toowhen chegar a um determinado serviço de escuta. Atualmente, apenas Olá *básico* regra é suportada. Olá *básico* regra é a distribuição de carga round robin.

**Notas de configuração adicionais**

Para a configuração de certificados SSL, Olá protocolo no **HttpListener** deve alterar demasiado*Https* (sensível às maiúsculas e). Olá **SslCertificate** elemento é adicionado demasiado**HttpListener** com o valor da variável Olá configurado para o certificado SSL Olá. porta de front-end Olá deve ser too443 atualizado.

**a afinidade de com base em cookies tooenable**: um gateway de aplicação pode ser configurado tooensure que um pedido de uma sessão de cliente é sempre toohello direcionado mesma VM no farm do Olá web. Este cenário é feito ao injetar um cookie de sessão que permita o tráfego de toodirect do gateway de Olá adequadamente. definir a afinidade com base no cookie tooenable, **CookieBasedAffinity** demasiado*ativado* no Olá **BackendHttpSettings** elemento.

## <a name="create-an-application-gateway"></a>Criar um gateway de aplicação

diferença Olá entre a utilização do modelo de implementação clássico do Azure Olá e o Azure Resource Manager é a ordem de Olá que criar uma aplicação gateway e Olá itens que precisam de toobe configurado.

Com o Resource Manager, todos os componentes de um gateway de aplicação são configurados individualmente e, em seguida, colocar em conjunto toocreate um recurso de gateway de aplicação.

Seguem-se Olá passos necessários toocreate um gateway de aplicação:

1. Criar um grupo de recursos para o Resource Manager
2. Criar rede virtual, uma sub-rede e um IP público para o gateway de aplicação Olá
3. Criar um objeto de configuração do gateway de aplicação
4. Criar um recurso do gateway de aplicação

## <a name="create-a-resource-group-for-resource-manager"></a>Criar um grupo de recursos para o Resource Manager

Certifique-se de que muda de cmdlets do PowerShell modo toouse Olá do Azure Resource Manager. Para obter mais informações, veja [Using Windows PowerShell with Resource Manager (Usar o Windows PowerShell com o Resource Manager)](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Passo 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Passo 2

Verifique Olá subscrições para a conta de Olá.

```powershell
Get-AzureRmSubscription
```

São tooauthenticate pedido com as suas credenciais.

### <a name="step-3"></a>Passo 3

Escolha qual das suas toouse de subscrições do Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Passo 4

Crie um novo grupo de recursos (ignore este passo se estiver a utilizar um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização, Esta definição é utilizada como localização predefinida de Olá para recursos nesse grupo de recursos. Certifique-se de que todos os comandos toocreate, utiliza um gateway de aplicação Olá mesmo grupo de recursos.

No exemplo de Olá acima, criámos um grupo de recursos denominado **appgw-RG** e a localização **EUA oeste**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede virtual e uma sub-rede de gateway de aplicação Olá

Olá seguinte exemplo mostra como toocreate uma rede virtual utilizando o Gestor de recursos:

### <a name="step-1"></a>Passo 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Este exemplo atribui Olá endereço intervalo 10.0.0.0/24 tooa sub-rede toobe variável utilizado toocreate uma rede virtual.

### <a name="step-2"></a>Passo 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Este exemplo cria uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw-rg** região EUA oeste de Olá com Olá prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.

### <a name="step-3"></a>Passo 3

```powershell
$subnet = $vnet.Subnets[0]
```

Este exemplo atribui o objeto de sub-rede Olá toovariable $subnet para passos Olá.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Este exemplo cria um recurso IP público **publicIP01** no grupo de recursos **appgw-rg** para a região EUA oeste de Olá.

## <a name="create-an-application-gateway-configuration-object"></a>Criar um objeto de configuração do gateway de aplicação

### <a name="step-1"></a>Passo 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Este exemplo cria uma configuração de IP do gateway de aplicação com o nome **gatewayIP01**. Quando é iniciado o Gateway de aplicação, escolherá um endereço IP da sub-rede Olá configurado e encaminhar os endereços IP de toohello de tráfego de rede no conjunto IP back-end Olá. Note que cada instância terá um endereço IP.

### <a name="step-2"></a>Passo 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Este exemplo configura com o nome dos conjunto de endereços IP para back-end Olá **pool01** com endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Esses valores são os endereços IP de Olá que recebem tráfego de rede de Olá provém do ponto final de IP Front-end Olá. Substitua os endereços IP de Olá de Olá anterior exemplo com endereços IP Olá de pontos finais da sua aplicação web.

### <a name="step-3"></a>Passo 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Este exemplo configura a definição de gateway de aplicação **poolsetting01** tráfego de rede com balanceamento de tooload no conjunto de back-end Olá.

### <a name="step-4"></a>Passo 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Este exemplo configura a porta IP Front-end Olá com o nome **frontendport01** para o ponto final IP público Olá.

### <a name="step-5"></a>Passo 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Este exemplo configura o certificado de Olá utilizado para a ligação SSL. necessita de certificado Olá toobe no formato. pfx e palavras-passe de Olá tem de ter entre 4 too12 carateres.

### <a name="step-6"></a>Passo 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Este exemplo cria a configuração IP Front-end Olá com o nome **fipconfig01** e associa Olá endereço IP público com a configuração de IP Front-end Olá.

### <a name="step-7"></a>Passo 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Este exemplo cria o nome do serviço de escuta de Olá **listener01** e associa Olá certificado e à configuração de IP de front-end de toohello de porta de front-end.

### <a name="step-8"></a>Passo 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Este exemplo cria Olá regra Balanceador de carga encaminhamento com o nome **rule01** que configura o comportamento do Balanceador de carga de Olá.

### <a name="step-9"></a>Passo 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Este exemplo configura o tamanho da instância Olá Olá do gateway de aplicação.

> [!NOTE]
> Olá valor predefinido para *InstanceCount* é 2, com um valor máximo de 10. Olá valor predefinido para *GatewaySize* é médio. Pode escolher entre Standard_Small, Standard_Medium e Standard_Large.

### <a name="step-10"></a>Passo 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Este passo define Olá SSL política toouse no gateway de aplicação Olá. Visite [versões de política de configurar o SSL e conjuntos de cifras no Gateway de aplicação](application-gateway-configure-ssl-policy-powershell.md) toolearn mais.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Criar um gateway de aplicação com o New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Este exemplo cria um gateway de aplicação com todos os itens de configuração do Olá precedente passos. Exemplo de Olá, o gateway de aplicação Olá denomina **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Obter nome de DNS de gateway de aplicação

Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação. Ao utilizar um IP público, o gateway de aplicação requer um nome DNS dinamicamente atribuído, que não é amigável. os utilizadores finais de tooensure pode atingiu o gateway de aplicação Olá, um registo CNAME pode ser utilizado toopoint toohello ponto final público Olá do gateway de aplicação. [Configurar um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo, detalhes de obtenção de gateway de aplicação Olá e o respetivo nome IP/DNS associado com o gateway de aplicação do Olá PublicIPAddress elemento toohello anexado. nome DNS do gateway de aplicação Olá deve ser utilizado toocreate um registo CNAME, nome DNS de toothis de aplicações que pontos Olá dois web. utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway de aplicação.


```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Passos seguintes

Se quiser tooconfigure um toouse de gateway de aplicação com um balanceador de carga interno (ILB), consulte [criar um gateway de aplicação com um balanceador de carga interno (ILB)](application-gateway-ilb.md).

Se pretender obter mais informações sobre as opções de balanceamento de carga em geral, veja:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestor de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

