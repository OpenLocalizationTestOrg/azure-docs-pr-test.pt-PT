---
title: "Configurar o redirecionamento para o Gateway de Aplicação do Azure - PowerShell | Microsoft Docs"
description: "Esta página mostra cenários para configurar o redirecionamento para o Gateway de Aplicação através do PowerShell"
documentationcenter: na
services: application-gateway
author: davidmu1
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: e0c7bfbffac0fffebe0c054226a5ad30403e4888
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/09/2018
---
# <a name="configure-redirection-on-application-gateway-with-powershell"></a>Configurar o redirecionamento no Gateway de Aplicação com o PowerShell

O Gateway de Aplicação suporta a capacidade de redirecionar o tráfego com base numa configuração definida. Para saber mais sobre o redirecionamento de um modo geral, veja [Application Gateway redirect overview](application-gateway-redirect-overview.md) (Descrição geral do redirecionamento do Gateway de Aplicação). Este artigo mostra exemplos de redirecionamentos HTTP e HTTPS, redirecionamentos baseados no caminho, redirecionamentos de múltiplos sites e redirecionamentos para sites externos.

## <a name="http-to-https-redirect-on-an-existing-application-gateway"></a>Redirecionamento de HTTP para HTTPS num gateway de aplicação já existente

O exemplo seguinte cria um serviço de escuta HTTP novo na porta 80 para redirecionar pedidos para o serviço de escuta já existente na porta 443.

```powershell
# Get the application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get the existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get the existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port to support HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get the recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using the port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get the new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting the existing listener
Add-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -RedirectType Permanent -TargetListener $httpslistener -IncludePath $true -IncludeQueryString $true -ApplicationGateway $gw

# Get the redirect configuration
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -ApplicationGateway $gw


# Add a new rule to handle the redirect and use the new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

Depois de o gateway de aplicação ser atualizado, teste o novo serviço de escuta na porta 80.  O exemplo seguinte mostra a utilização de `curl` para testar o redirecionamento.

```
curl http://40.69.161.221 -i
HTTP/1.1 301 Moved Permanently
Content-Type: text/html; charset=UTF-8
Location: https://40.69.161.221/
Server: Microsoft-IIS/10.0
Date: Tue, 11 Jul 2017 20:54:00 GMT
Content-Length: 145

<head><title>Document Moved</title></head>
<body><h1>Object Moved</h1>This document may be found <a HREF="https://40.69.161.221/">here</a></body>
```

## <a name="path-based-redirect"></a>Redirecionamento baseado no caminho

O exemplo seguinte cria um serviço de escuta novo e uma regra baseada em caminho num gateway de aplicação já existente que redireciona apenas o tráfego que corresponde ao caminho do url especificado.

```powershell
# Get the application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get the existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get the existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port to support HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get the recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using the port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get the new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect targeting the existing listener and get the redirect configuration
Add-AzureRmApplicationGatewayRedirectConfiguration -Name redirectpath6 -RedirectType Permanent -TargetListener $httpslistener -IncludePath $true -IncludeQueryString $true -ApplicationGateway $gw
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectpath6 -ApplicationGateway $gw

# Retrieve the existing backend http settings to be used
$poolSetting = Get-AzureRmApplicationGatewayBackendHttpSettings -Name "appGatewayBackendHttpSettings" -ApplicationGateway $gw

# Retrieve an existing backend pool
$pool = Get-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -ApplicationGateway $gw

# Create a new path rule for the path map configuration
$pathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule6" -Paths "/image/*" -RedirectConfiguration $redirectconfig

# Create a path map to add to the rule
Add-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $pathRule -DefaultBackendAddressPool $pool -DefaultBackendHttpSettings $poolSetting -ApplicationGateway $gw

# Retrieve the url path map created
$urlPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -ApplicationGateway $gw

# Add a new rule to handle the redirect and use the new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name "rule6" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap -ApplicationGateway $gw

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

## <a name="multi-site-redirect"></a>Redirecionamento de múltiplos sites

O exemplo seguinte cria um gateway de aplicação novo com dois serviços de escuta de múltiplos sites na porta 80. Os serviços de escuta são para adatum.com e adatum.org. É criada uma regra de redirecionamento para redirecionar o tráfego de adatum.org para adatum.com. É necessária uma configuração adicional para configurar os aliases de CNAME para o endereço IP público do gateway de aplicação. Para obter mais informações sobre como delegar o seu domínio para o DNS do Azure e criar registos CNAME para o domínio, veja [Delegar um domínio ao DNS do Azure](../dns/dns-delegate-domain-azure-dns.md).

```powershell
# Create a new resource group for the application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "East US"

# Create a subnet configuration object for the application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with the application gateway. Defining the domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "East US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool to hold the addresses or NICs for the application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration to associate the public IP address with the application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create the HTTP listener for the application gateway for adatum.com. Assign the front-end ip configuration, and port.
$listener1 = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.com

# Create the HTTP listener for the application gateway for adatum.org this listener will redirect to the abc.com listener. Assign the front-end ip configuration, and port.
$listener2 = New-AzureRmApplicationGatewayHttpListener -Name listener02 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.org

# Create the redirect configuration that will point traffic to the 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name redirectOrgtoCom -RedirectType Found -TargetListener $listener1 -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule1 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener1 -BackendHttpSettings $poolSetting -BackendAddressPool $pool

#Create a load balancer routing rule that redirects traffic to the adatum.com listener
$rule2 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener2 -RedirectConfiguration $redirectconfig

# Configure the SKU of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Medium -Tier Standard -Capacity 2

# Create the application gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener,$listener2 -RequestRoutingRules $rule1,$rule2 -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="redirect-to-an-external-site"></a>Redirecionar para um site externo

O exemplo seguinte redireciona o tráfego enviado para o gateway de aplicação para um Web site externo (bing.com). Ao utilizar o comutador `TargetUrl`, os comutadores `IncludePath` e `IncludeQuery` não são permitidos.

```powershell
# Create a new resource group for the application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"

# Create a subnet configuration object for the application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with the application gateway. Defining the domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool to hold the addresses or NICs for the application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration to associate the public IP address with the application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create the HTTP listener for the application gateway. Assign the front-end ip configuration, and port.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp 

# Create the redirect configuration that will point traffic to the 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name myredirect -RedirectType Temporary -TargetUrl "http://bing.com"

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig 

# Configure the SKU of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Create the application gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="next-steps"></a>Passos seguintes

Veja [configure end to end SSL with application gateway using PowerShell](application-gateway-end-to-end-ssl-powershell.md) (Configurar SSL ponto a ponto com o gateway de aplicação através do PowerShell)
