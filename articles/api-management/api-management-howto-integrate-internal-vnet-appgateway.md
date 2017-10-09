---
title: "aaaHow toouse Azure API Management numa rede Virtual com Gateway de aplicação | Microsoft Docs"
description: "Saiba como toosetup e configurar a gestão de API do Azure na rede Virtual interna com o aplicação Gateway (WAF) como front-end"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Integrar a gestão de API numa VNET interna com Gateway de aplicação 

##<a name="overview"></a> Descrição geral
 
Olá serviço de API Management pode ser configurada numa rede Virtual no modo interno que torna acessível apenas a partir de dentro de Olá rede Virtual. Gateway de aplicação do Azure é um serviço de PAAS que fornece um balanceador de carga de 7 camadas. É também age como um serviço de proxy inverso e fornece entre a oferta de uma Firewall de aplicação Web (WAF).

Combinar aprovisionados numa VNET interna com Gateway de aplicação de Olá front-end de API de gestão permite Olá os seguintes cenários:

* Utilize Olá mesmo recurso da gestão de API para consumo por consumidores internos e externos consumidores.
* Utilizar um único recurso de gestão de API e um subconjunto de APIs definidas na API Management disponível para consumidores externos.
* Fornecer uma forma de chave de ative tooswitch acesso tooAPI gestão de Olá Internet pública e desativar. 

##<a name="scenario"></a> Cenário
Este artigo irá cobrir como toouse uma única API Management service para consumidores internos e externos e torná-lo atuar como um único front-end para ambos no local e APIs da nuvem. Também verá como tooexpose apenas um subconjunto das suas APIs (por exemplo de Olá que são realçados verde) para consumo externo utilizando Olá PathBasedRouting funcionalidade disponível no Gateway de aplicação.

Exemplo de configuração primeiro Olá as suas APIs são geridos apenas a partir de dentro da sua rede Virtual. Consumidores internos (cor de laranja realçado em) podem aceder a todas as suas APIs internos e externos. Tráfego nunca vai tooInternet que é entregue um elevado desempenho através de circuitos do Expressroute.

![rota de URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Antes de começar

1. Instale a versão mais recente do Olá Olá Azure de cmdlets do PowerShell, utilizando Olá instalador de plataforma Web. Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferências](https://azure.microsoft.com/downloads/).
2. Criar uma rede Virtual e crie sub-redes separadas para a API Management e o Gateway de aplicação. 
3. Se tenciona toocreate um servidor DNS personalizado para Olá rede Virtual, tal antes de iniciar a implementação de Olá. Verifique novamente funciona, assegurando que uma máquina virtual criada numa sub-rede nova no Olá rede Virtual pode resolver e aceder a todos os pontos finais de serviço do Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>O que é necessário toocreate uma integração entre a API Management e o Gateway de aplicação?

* **Agrupamento de servidores de back-end:** este é o endereço IP virtual interno por Olá de Olá serviço de API Management.
* **Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies. Estas definições são aplicadas tooall servidores dentro do conjunto de Olá.
* **Porta de front-end:** é Olá Porta pública aberta no gateway de aplicação Olá. Tráfego de alcance obtém tooone redirecionada de Olá servidores back-end.
* **Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estes valores são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).
* **Regra:** regra Olá está vinculado um agrupamento de servidores de back-end do serviço de escuta tooa.
* **Sonda de estado de funcionamento personalizada:** Gateway de aplicação, por predefinição, utiliza IP endereço com base em pesquisas toofigure enviados os servidores no Olá BackendAddressPool estão ativas. Olá serviço de API Management responde apenas toorequests que tem o cabeçalho de anfitrião correto de Olá, por conseguinte, as pesquisas de predefinição Olá falharem. Necessita de uma sonda do Estado de funcionamento personalizado toobe definido pelo gateway de aplicação toohelp determinar que o serviço de Olá está ativo e deve reencaminhar pedidos.
* **Certificado de domínio personalizado:** tooaccess API Management do Olá terá toocreate um mapeamento CNAME de nome de anfitrião toohello Gateway de aplicação front-end nome DNS de internet. Isto garante que cabeçalho de nome de anfitrião de Olá e certificados enviados tooApplication Gateway seja reencaminhado tooAPI gestão é um que APIM pode reconhecer como válido.

## <a name="overview-steps"></a> Passos necessários para integrar o API Management e o Gateway de aplicação 

1. Crie um grupo de recursos para o Resource Manager.
2. Crie uma rede Virtual, uma sub-rede e um IP público para Olá Gateway de aplicação. Crie outra sub-rede para a API Management.
3. Criar um serviço de API Management dentro de sub-rede da VNET de Olá criado acima e certifique-se de que utilizar o modo interno Olá.
4. Configure o nome de domínio personalizado de Olá no Olá serviço de API Management.
5. Crie um objeto de configuração do Gateway de aplicação.
6. Crie um recurso de Gateway de aplicação.
7. Crie um CNAME do nome DNS público Olá de nome de anfitrião do Olá Gateway de aplicação toohello API Management proxy.

## <a name="create-a-resource-group-for-resource-manager"></a>Criar um grupo de recursos para o Resource Manager

Certifique-se de que está a utilizar Olá versão mais recente do Azure PowerShell. Para obter mais informações, veja [Using Windows PowerShell with Resource Manager (Usar o Windows PowerShell com o Resource Manager)](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Passo 1

Inicie sessão no tooAzure

```powershell
Login-AzureRmAccount
```

Autenticar com as suas credenciais.<BR>

### <a name="step-2"></a>Passo 2

Verifique Olá subscrições para a conta de Olá e selecione-o.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Passo 3

Crie um novo grupo de recursos (ignore este passo se estiver a utilizar um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização, Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos. Certifique-se de que todos os comandos toocreate um Olá de utilização do gateway de aplicação mesmo grupo de recursos.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede Virtual e uma sub-rede de gateway de aplicação Olá

Olá seguinte exemplo mostra como toocreate utilizando uma rede Virtual hello do resource manager.

### <a name="step-1"></a>Passo 1

Atribua Olá endereço intervalo 10.0.0.0/24 toohello sub-rede variável toobe utilizado para o Gateway de aplicação ao criar uma rede Virtual.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Passo 2

Atribua Olá endereço intervalo 10.0.1.0/24 toohello sub-rede variável toobe utilizado para gestão de API ao criar uma rede Virtual.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Passo 3

Criar uma rede Virtual denominada **appgwvnet** no grupo de recursos **apim-appGw-RG** para a região EUA oeste de Olá utilizando Olá prefixo 10.0.0.0/16 com 10.0.0.0/24 sub-redes e 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Passo 4

Atribua uma variável de sub-rede para passos Olá

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Criar um serviço de API Management dentro de uma VNET configurado no modo interno

Olá exemplo seguinte mostra como toocreate um serviço de API Management numa VNET configuradas para acesso interno apenas.

### <a name="step-1"></a>Passo 1
Crie um objeto de rede Virtual de gestão de API utilizando sub-rede Olá $apimsubnetdata criado acima.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Passo 2
Crie um serviço de API Management dentro Olá rede Virtual.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Após ter êxito Olá acima comando consulte demasiado[configuração de DNS necessário serviço de gestão de API de VNET interno tooaccess](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess-lo.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Configurar um nome de domínio personalizado na API Management

### <a name="step-1"></a>Passo 1
Carregue o certificado de Olá com chave privada para o domínio de Olá. Neste exemplo será `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Passo 2
Depois do certificado de Olá é carregado, criar um objeto de configuração do nome de anfitrião para o proxy de Olá com um nome de anfitrião do `api.contoso.net`, como o certificado de exemplo de Olá fornece autoridade para Olá `*.contoso.net` domínio. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

Criar um recurso IP público **publicIP01** no grupo de recursos **apim-appGw-RG** para a região EUA oeste de Olá.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Um endereço IP é atribuído o gateway de aplicação toohello quando Olá serviço for iniciado.

## <a name="create-application-gateway-configuration"></a>Criar a configuração do gateway de aplicação

Todos os itens de configuração tem de ser configurados antes de criar o gateway de aplicação Olá. Olá passos seguintes criar Olá itens de configuração que são necessários para um recurso de gateway de aplicação.

### <a name="step-1"></a>Passo 1

Crie uma configuração de IP do gateway de aplicação com o nome **gatewayIP01**. Quando é iniciado o Gateway de aplicação, escolherá um endereço IP da sub-rede Olá configurado e encaminhar os endereços IP de toohello de tráfego de rede no conjunto IP back-end Olá. Note que cada instância terá um endereço IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Passo 2

Configure a porta IP de front-end do Olá para o ponto final IP público Olá. Esta porta é a porta de Olá que os utilizadores finais que se ligam a.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Passo 3

Configure o IP de front-end Olá com ponto final IP público.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Passo 4

Configurar o certificado de Olá para hello Gateway de aplicação, utilizado toodecrypt e reencriptar o tráfego de Olá passar pela.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Passo 5

Crie o serviço de escuta HTTP de Olá para Olá Gateway de aplicação. Atribua a configuração de IP Front-end Olá, porta e tooit de certificado de ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Passo 6

Criar um serviço de gestão de API de toohello sonda personalizada `ContosoApi` ponto final de domínio do proxy. caminho de Olá `/status-0123456789abcdef` é um ponto final de estado de funcionamento predefinido alojado em todos os serviços de gestão de API de Olá. Definir `api.contoso.net` como toosecure de nome de anfitrião uma sonda personalizada com o certificado SSL.

> [!NOTE]
> Olá hostname `contosoapi.azure-api.net` é o nome de anfitrião do Olá predefinido proxy configurado quando um serviço com o nome `contosoapi` é criada no Azure público. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Passo 7

Carregar o certificado de Olá toobe utilizada nos recursos de conjunto de back-end SSL ativado Olá. Este é Olá mesmo certificado que é fornecido no passo 4 acima.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Passo 8

Configure definições de back-end HTTP para Olá Gateway de aplicação. Isto inclui a definição de um limite de tempo limite para o pedido de back-end após o qual são canceladas. Este valor é diferente do tempo limite de sonda de Olá.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Passo 9

Configurar um conjunto de endereços IP back-end com o nome **apimbackend** com Olá IP virtual interno endereço do Olá serviço de API Management criado acima.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Passo 10

Crie as definições para um back-end de (inexistente) fictício. Os caminhos de tooAPI de pedidos que não queremos tooexpose da API de gestão através do Gateway de aplicação serão acessos este back-end e devolver 404.

Configure definições de HTTP para Olá fictício back-end.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Configurar um back-end fictício **dummyBackendPool**, que aponta de endereço FQDN tooa **dummybackend.com**. Este endereço FQDN não existe na rede virtual Olá.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Criar uma regra de definição que Olá Gateway de aplicação irão utilizar por predefinição que aponta de back-end do toohello inexistente **dummybackend.com** no Olá rede Virtual.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Passo 11

Configure caminhos de regra de URL para os conjuntos de back-end Olá. Isto permite selecionar apenas a alguns dos Olá das APIs de gestão de API para a ser expostos toohello público. Por exemplo, se existirem `Echo API` (eco /), `Calculator API` (/calc/), etc. disponibilizar apenas `Echo API` acessível a partir da Internet). 

Olá exemplo seguinte cria uma regra simples para Olá "eco /" caminho encaminhamento tráfego toohello back-end "apimProxyBackendPool".

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Se o caminho de Olá não corresponde ao caminho de Olá regras queremos tooenable da gestão de API, configuração de mapa de caminho configura também um conjunto predefinido de endereços de back-end com o nome de regra de Olá **dummyBackendPool**. Por exemplo, http://api.contoso.net/calc/ * ficar demasiado**dummyBackendPool** como está definida como conjunto predefinido de Olá para o tráfego não correspondente.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Olá acima passo garante que apenas os pedidos para o caminho de Olá "/ eco" são permitidos através de Olá Gateway de aplicação. Tooother pedidos que APIs configuradas na API Management irá gerar 404 erros do Gateway de aplicação quando acedido a partir de Olá Internet. 

### <a name="step-12"></a>Passo 12

Crie uma definição de regra para Olá Gateway de aplicação toouse URL com base no caminho encaminhamento.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Passo 13

Configure Olá número de instâncias e o tamanho para Olá Gateway de aplicação. Aqui vamos utilizar Olá [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para maior segurança de Olá recurso da gestão de API.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Passo 14

Configure WAF toobe no modo de "Prevenção".
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Criar Gateway de aplicação

Crie um Gateway de aplicação com todos os objetos de configuração de Olá de Olá precedente passos.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME Olá API Management proxy hostname toohello nome DNS público do Olá recurso do Gateway de aplicação

Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação. Quando utilizar um IP público, o Gateway de aplicação requer um nome DNS dinamicamente atribuído, que pode não ser toouse fácil. 

Olá nome DNS do Gateway de aplicação deve ser utilizado toocreate um registo CNAME que aponta de nome de anfitrião proxy Olá APIM (por exemplo, `api.contoso.net` nos exemplos de Olá acima) toothis nome DNS. tooconfigure Olá front-end um registo CNAME de IP, obter detalhes sobre Olá Olá Gateway de aplicação e o seu nome IP/DNS associado utilizando o elemento de PublicIPAddress Olá. utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a> Resumo
Gestão de API do Azure configurada numa VNET fornece uma interface de gateway único para todos os APIs configuradas, se estiverem alojado no local ou na nuvem de Olá. Integrar o Gateway de aplicação com a API Management proporciona flexibilidade de Olá de seletivamente ativar específico toobe APIs acessível no Olá Internet, bem como fornecer uma Firewall de aplicação Web como uma instância de API Management tooyour front-end.

##<a name="next-steps"></a> Próximos passos
* Saiba mais sobre o Gateway de aplicação do Azure
  * [Descrição geral do Gateway de aplicação](../application-gateway/application-gateway-introduction.md)
  * [Firewall de aplicação de Web de Gateway de aplicação](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Gateway de aplicação com o encaminhamento com base no caminho](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* Saiba mais sobre a gestão de API e as VNETs
  * [Utilizar a API Management disponível apenas dentro do Olá VNET](api-management-using-with-internal-vnet.md)
  * [Utilizar a API Management na VNET](api-management-using-with-vnet.md)
