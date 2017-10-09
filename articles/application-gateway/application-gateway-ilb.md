---
title: "Gateway de aplicação do Azure com o Balanceador de carga interno de aaaUsing | Microsoft Docs"
description: "Esta página fornece instruções tooconfigure um Gateway de aplicação do Azure com um ponto final de balanceamento de carga interno"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Criar um Gateway de Aplicação com um Balanceador de Carga Interno (ILB)

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

Gateway de aplicação pode ser configurado com um internet com o virtual IP ou com um toohello de ponto final interno não exposto à internet, também conhecido como ponto final do Balanceador de carga interno (ILB). Configurar Olá gateway com um ILB é útil para aplicações de linha de negócio internas não expostas toointernet. Também é útil para serviços/camadas dentro de uma aplicação multicamada, que se encontre num toointernet de limites não exposto de segurança, mas ainda necessitam de distribuição de carga round robin, a persistência da sessão ou a terminação de SSL. Este artigo explica os passos de Olá tooconfigure um gateway de aplicação com um ILB.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente dos cmdlets do Azure PowerShell Olá utilizando Olá instalador de plataforma Web. Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferência](https://azure.microsoft.com/downloads/).
2. Certifique-se de que tem uma rede virtual de trabalhar com sub-rede válida.
3. Certifique-se de que possui servidores de back-end na rede virtual hello, ou com um IP/VIP público atribuído.

toocreate um gateway de aplicação, execute Olá os seguintes passos por ordem de Olá listados. 

1. [Criar um gateway de aplicação](#create-a-new-application-gateway)
2. [Configurar o gateway de Olá](#configure-the-gateway)
3. [Configuração do gateway de Olá de conjunto](#set-the-gateway-configuration)
4. [Iniciar Olá gateway](#start-the-gateway)
5. [Certifique-se de gateway Olá](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Crie um gateway de aplicação:

**gateway de Olá toocreate**, utilize Olá `New-AzureApplicationGateway` cmdlet, substituindo os valores de Olá com os seus próprios. Tenha em atenção que a faturação para o gateway de Olá não iniciada neste momento. Faturação começa num passo posterior, quando o gateway de Olá for iniciada com êxito.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** que foi criado o gateway de Olá, pode utilizar Olá `Get-AzureApplicationGateway` cmdlet. 

Exemplo de Olá, *Descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais. Olá valor predefinido para *InstanceCount* é 2, com um valor máximo de 10. Olá valor predefinido para *GatewaySize* é médio. Pequenas e grandes outros valores disponíveis. *VIP* e *DnsName* são apresentados em branco, porque o gateway de Olá ainda não foi iniciado. Estes são criados quando o gateway de Olá está num Estado de execução de Olá. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Configurar o gateway de Olá
Uma configuração de gateway de aplicação consiste de vários valores. podem ser vinculados a valores de Olá configuração de Olá tooconstruct em conjunto.

os valores de Olá são:

* **Agrupamento de servidores de back-end:** lista Olá de endereços IP dos servidores de back-end Olá. endereços IP Olá listados devem pertencer toohello VNet sub-rede ou devem ser um IP/VIP público. 
* **Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies. Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá.
* **Porta de front-end:** esta porta é Olá de porta pública aberta no gateway de aplicação Olá. O tráfego chega a esta porta e, em seguida, obtém tooone redirecionada dos servidores de back-end Olá.
* **Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estes são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload). 
* **Regra:** regra Olá vincula o serviço de escuta de Olá e agrupamento de servidores de back-end Olá e define o tráfego de Olá do agrupamento de servidor back-end deve ser direcionado toowhen chegar a um determinado serviço de escuta. Atualmente, apenas Olá *básico* regra é suportada. Olá *básico* regra é a distribuição de carga round robin.

Pode criar a configuração através da criação de um objeto de configuração ou através de um ficheiro XML de configuração. tooconstruct a configuração, utilizando um ficheiro XML de configuração, utilize Olá exemplo abaixo.

Tenha em atenção o seguinte Olá:

* Olá *FrontendIPConfigurations* elemento descreve Olá ILB os detalhes relevantes para configurar o Gateway de aplicação com um ILB. 
* IP de front-end Hello *tipo* deve ser definido too'Private'
* Olá *StaticIPAddress* deve ser definido IP interno toohello pretendido no qual Olá gateway recebe o tráfego. Tenha em atenção que Olá *StaticIPAddress* elemento é opcional. Se não for definido, um IP interno disponível da sub-rede Olá implementado é escolhido. 
* Olá, valor de Olá *nome* elemento especificado na *FrontendIPConfiguration* deve ser utilizada no Olá HTTPListener *FrontendIP* elemento toorefer toohello FrontendIPConfiguration.
  
  **Exemplo XML de configuração**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-hello-gateway-configuration"></a>Configuração do gateway de Olá de conjunto
Em seguida, iremos definir o gateway de aplicação Olá. Pode utilizar Olá `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um ficheiro XML de configuração. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Iniciar Olá gateway

Assim que tiver sido configurada gateway Olá, utilize Olá `Start-AzureApplicationGateway` gateway do cmdlet toostart Olá. Faturação de um gateway de aplicação começa depois do gateway de Olá foi iniciado com êxito. 

> [!NOTE]
> Olá `Start-AzureApplicationGateway` cmdlet poderá demorar até toocomplete too15-20 minutos. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Verifique o estado do gateway Olá

Olá utilize `Get-AzureApplicationGateway` cmdlet toocheck Olá Estado gateway. Se `Start-AzureApplicationGateway` foi concluída com êxito no passo anterior Olá, estado de Olá deve ser *executar*, Olá Vip e DnsName deverão ter entradas válidas. Este exemplo mostra o cmdlet Olá na primeira linha Olá, seguido pela saída Olá. Neste exemplo Olá gateway está em execução e pronto tootake tráfego. 

> [!NOTE]
> gateway de aplicação Olá está configurado tooaccept tráfego em Olá configurado ILB ponto final de 10.0.0.10 neste exemplo.

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Passos seguintes
Se pretender obter mais informações sobre as opções de balanceamento de carga em geral, veja:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestor de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

