---
title: "aaaConfigure SSL offload - Gateway de aplicação do Azure - PowerShell clássico | Microsoft Docs"
description: "Este artigo fornece instruções toocreate um gateway de aplicação com SSL offload utilizando Olá modelo de implementação clássica do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Configurar um gateway de aplicação para a descarga SSL de utilizando o modelo de implementação clássica Olá

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI 2.0 do Azure](application-gateway-ssl-cli.md)

Gateway de aplicação do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão em Olá gateway tooavoid dispendiosa SSL desencriptação tarefas toohappen no farm do Olá web. Descarga de SSL também simplifica a configuração do servidor front-end Olá e a gestão de aplicações web de Olá.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente do Olá Olá Azure de cmdlets do PowerShell, utilizando Olá instalador de plataforma Web. Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferências](https://azure.microsoft.com/downloads/).
2. Verifique se a rede virtual funciona com uma sub-rede válida. Certifique-se de que nenhuma máquina virtual ou implementações de nuvem estão a utilizar a sub-rede de Olá. gateway de aplicação Olá tem de ser por si só, numa sub-rede de rede virtual.
3. servidores de Olá que configurar o gateway de aplicação Olá toouse tem de existir ou tem os respetivos pontos finais criados na rede virtual Olá ou com um IP/VIP público atribuído.

tooconfigure SSL descarregamento de um gateway de aplicação, Olá os seguintes passos por ordem de Olá listado:

1. [Criar um gateway de aplicação](#create-an-application-gateway)
2. [Carregar certificados SSL](#upload-ssl-certificates)
3. [Configurar o gateway de Olá](#configure-the-gateway)
4. [Configuração do gateway de Olá de conjunto](#set-the-gateway-configuration)
5. [Iniciar Olá gateway](#start-the-gateway)
6. [Verifique o estado do gateway Olá](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Criar um gateway de aplicação

gateway de Olá toocreate, utilize Olá `New-AzureApplicationGateway` cmdlet, substituindo os valores de Olá com os seus próprios. Faturação para o gateway de Olá não inicia neste momento. Faturação começa num passo posterior, quando o gateway de Olá for iniciada com êxito.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate Olá gateway foi criado, pode utilizar Olá `Get-AzureApplicationGateway` cmdlet.

Exemplo de Olá, *Descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais. Olá valor predefinido para *InstanceCount* é 2, com um valor máximo de 10. Olá valor predefinido para *GatewaySize* é médio. Pequenas e grandes outros valores disponíveis. *VirtualIPs* e *DnsName* são apresentados em branco, porque o gateway de Olá ainda não foi iniciado. Estes valores são criados quando o gateway de Olá está num Estado de execução de Olá.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Carregar certificados SSL

Utilize `Add-AzureApplicationGatewaySslCertificate` certificado de servidor Olá tooupload no *pfx* gateway de aplicação do formato toohello. nome do certificado Olá é um nome de utilizador escolhida e tem de ser exclusivo no gateway de aplicação Olá. Este certificado é referenciado tooby este nome em todas as operações de gestão de certificados no gateway de aplicação Olá.

Este exemplo seguinte mostra o cmdlet Olá, substitua os valores de Olá exemplo Olá com os seus próprios.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Em seguida, valide o carregamento do certificado Olá. Olá utilize `Get-AzureApplicationGatewayCertificate` cmdlet.

Este exemplo mostra o cmdlet Olá na primeira linha Olá, seguido pela saída Olá.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> palavra-passe de certificados de Olá tem toobe entre 4 too12 carateres, letras ou números. Não são aceites carateres especiais.

## <a name="configure-hello-gateway"></a>Configurar o gateway de Olá

Uma configuração de gateway de aplicação consiste de vários valores. podem ser vinculados a valores de Olá configuração de Olá tooconstruct em conjunto.

os valores de Olá são:

* **Agrupamento de servidores de back-end:** lista Olá de endereços IP dos servidores de back-end Olá. endereços IP Olá listados devem pertencer toohello sub-rede da rede virtual ou devem ser um IP/VIP público.
* **Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies. Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá.
* **Porta de front-end:** esta porta é Olá Porta pública aberta no gateway de aplicação Olá. O tráfego chega a esta porta e, em seguida, obtém redirecionado tooone dos servidores de back-end Olá.
* **Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estes valores são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).
* **Regra:** regra Olá vincula o serviço de escuta de Olá e agrupamento de servidores de back-end de Olá e define o tráfego de Olá de agrupamento de servidores de back-end deve ser direcionado toowhen chegar a um determinado serviço de escuta. Atualmente, apenas Olá *básico* regra é suportada. Olá *básico* regra é a distribuição de carga round robin.

**Notas de configuração adicionais**

Para a configuração de certificados SSL, Olá protocolo no **HttpListener** deve alterar demasiado*Https* (sensível às maiúsculas e). Olá **SslCert** elemento é adicionado demasiado**HttpListener** com Olá valor definido toohello mesmo nome como utilizada no carregamento de Olá do anterior a secção de certificados SSL. porta de front-end Olá deve ser too443 atualizado.

**a afinidade de com base em cookies tooenable**: um gateway de aplicação pode ser configurado tooensure que um pedido de uma sessão de cliente é sempre toohello direcionado mesma VM no farm do Olá web. Este cenário é feito ao injetar um cookie de sessão que permita o tráfego de toodirect do gateway de Olá adequadamente. definir a afinidade com base no cookie tooenable, **CookieBasedAffinity** demasiado*ativado* no Olá **BackendHttpSettings** elemento.

Pode criar a configuração através da criação de um objeto de configuração ou utilizando um ficheiro XML de configuração.
Utilize a configuração utilizando uma ficheiro XML, de configuração de tooconstruct Olá seguinte exemplo:

**Exemplo XML de configuração**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

Em seguida, configure o gateway de aplicação Olá. Pode utilizar Olá `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um ficheiro XML de configuração.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Iniciar Olá gateway

Assim que tiver sido configurada gateway Olá, utilize Olá `Start-AzureApplicationGateway` gateway do cmdlet toostart Olá. Faturação de um gateway de aplicação começa depois do gateway de Olá foi iniciado com êxito.

> [!NOTE]
> Olá `Start-AzureApplicationGateway` cmdlet poderá demorar até toofinish too15-20 minutos.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Verifique o estado do gateway Olá

Olá utilize `Get-AzureApplicationGateway` cmdlet toocheck Olá Estado gateway Olá. Se `Start-AzureApplicationGateway` foi concluída com êxito no passo anterior Olá, *estado* deve estar em execução e *VirtualIPs* e *DnsName* deverão ter entradas válidas.

Este exemplo mostra um gateway de aplicação que, em execução e está pronto tootake tráfego.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Passos seguintes

Se pretender obter mais informações sobre as opções de balanceamento de carga em geral, veja:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestor de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

