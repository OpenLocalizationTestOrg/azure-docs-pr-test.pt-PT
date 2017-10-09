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
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="652b6-103">Criar um Gateway de Aplicação com um Balanceador de Carga Interno (ILB)</span><span class="sxs-lookup"><span data-stu-id="652b6-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="652b6-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="652b6-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="652b6-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="652b6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="652b6-106">Gateway de aplicação pode ser configurado com um internet com o virtual IP ou com um toohello de ponto final interno não exposto à internet, também conhecido como ponto final do Balanceador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="652b6-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="652b6-107">Configurar Olá gateway com um ILB é útil para aplicações de linha de negócio internas não expostas toointernet.</span><span class="sxs-lookup"><span data-stu-id="652b6-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="652b6-108">Também é útil para serviços/camadas dentro de uma aplicação multicamada, que se encontre num toointernet de limites não exposto de segurança, mas ainda necessitam de distribuição de carga round robin, a persistência da sessão ou a terminação de SSL.</span><span class="sxs-lookup"><span data-stu-id="652b6-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="652b6-109">Este artigo explica os passos de Olá tooconfigure um gateway de aplicação com um ILB.</span><span class="sxs-lookup"><span data-stu-id="652b6-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="652b6-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="652b6-110">Before you begin</span></span>

1. <span data-ttu-id="652b6-111">Instale a versão mais recente dos cmdlets do Azure PowerShell Olá utilizando Olá instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="652b6-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="652b6-112">Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferência](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="652b6-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="652b6-113">Certifique-se de que tem uma rede virtual de trabalhar com sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="652b6-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="652b6-114">Certifique-se de que possui servidores de back-end na rede virtual hello, ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="652b6-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="652b6-115">toocreate um gateway de aplicação, execute Olá os seguintes passos por ordem de Olá listados.</span><span class="sxs-lookup"><span data-stu-id="652b6-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="652b6-116">Criar um gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="652b6-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="652b6-117">Configurar o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="652b6-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="652b6-118">Configuração do gateway de Olá de conjunto</span><span class="sxs-lookup"><span data-stu-id="652b6-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="652b6-119">Iniciar Olá gateway</span><span class="sxs-lookup"><span data-stu-id="652b6-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="652b6-120">Certifique-se de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="652b6-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="652b6-121">Crie um gateway de aplicação:</span><span class="sxs-lookup"><span data-stu-id="652b6-121">Create an application gateway:</span></span>

<span data-ttu-id="652b6-122">**gateway de Olá toocreate**, utilize Olá `New-AzureApplicationGateway` cmdlet, substituindo os valores de Olá com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="652b6-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="652b6-123">Tenha em atenção que a faturação para o gateway de Olá não iniciada neste momento.</span><span class="sxs-lookup"><span data-stu-id="652b6-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="652b6-124">Faturação começa num passo posterior, quando o gateway de Olá for iniciada com êxito.</span><span class="sxs-lookup"><span data-stu-id="652b6-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

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

<span data-ttu-id="652b6-125">**toovalidate** que foi criado o gateway de Olá, pode utilizar Olá `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="652b6-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="652b6-126">Exemplo de Olá, *Descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="652b6-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="652b6-127">Olá valor predefinido para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="652b6-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="652b6-128">Olá valor predefinido para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="652b6-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="652b6-129">Pequenas e grandes outros valores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="652b6-129">Small and Large are other available values.</span></span> <span data-ttu-id="652b6-130">*VIP* e *DnsName* são apresentados em branco, porque o gateway de Olá ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="652b6-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="652b6-131">Estes são criados quando o gateway de Olá está num Estado de execução de Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-131">These are created once hello gateway is in hello running state.</span></span> 

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

## <a name="configure-hello-gateway"></a><span data-ttu-id="652b6-132">Configurar o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="652b6-132">Configure hello gateway</span></span>
<span data-ttu-id="652b6-133">Uma configuração de gateway de aplicação consiste de vários valores.</span><span class="sxs-lookup"><span data-stu-id="652b6-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="652b6-134">podem ser vinculados a valores de Olá configuração de Olá tooconstruct em conjunto.</span><span class="sxs-lookup"><span data-stu-id="652b6-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="652b6-135">os valores de Olá são:</span><span class="sxs-lookup"><span data-stu-id="652b6-135">hello values are:</span></span>

* <span data-ttu-id="652b6-136">**Agrupamento de servidores de back-end:** lista Olá de endereços IP dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="652b6-137">endereços IP Olá listados devem pertencer toohello VNet sub-rede ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="652b6-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="652b6-138">**Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies.</span><span class="sxs-lookup"><span data-stu-id="652b6-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="652b6-139">Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="652b6-140">**Porta de front-end:** esta porta é Olá de porta pública aberta no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="652b6-141">O tráfego chega a esta porta e, em seguida, obtém tooone redirecionada dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="652b6-142">**Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estes são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).</span><span class="sxs-lookup"><span data-stu-id="652b6-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="652b6-143">**Regra:** regra Olá vincula o serviço de escuta de Olá e agrupamento de servidores de back-end Olá e define o tráfego de Olá do agrupamento de servidor back-end deve ser direcionado toowhen chegar a um determinado serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="652b6-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="652b6-144">Atualmente, apenas Olá *básico* regra é suportada.</span><span class="sxs-lookup"><span data-stu-id="652b6-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="652b6-145">Olá *básico* regra é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="652b6-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="652b6-146">Pode criar a configuração através da criação de um objeto de configuração ou através de um ficheiro XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="652b6-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="652b6-147">tooconstruct a configuração, utilizando um ficheiro XML de configuração, utilize Olá exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="652b6-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="652b6-148">Tenha em atenção o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="652b6-148">Note hello following:</span></span>

* <span data-ttu-id="652b6-149">Olá *FrontendIPConfigurations* elemento descreve Olá ILB os detalhes relevantes para configurar o Gateway de aplicação com um ILB.</span><span class="sxs-lookup"><span data-stu-id="652b6-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="652b6-150">IP de front-end Hello *tipo* deve ser definido too'Private'</span><span class="sxs-lookup"><span data-stu-id="652b6-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="652b6-151">Olá *StaticIPAddress* deve ser definido IP interno toohello pretendido no qual Olá gateway recebe o tráfego.</span><span class="sxs-lookup"><span data-stu-id="652b6-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="652b6-152">Tenha em atenção que Olá *StaticIPAddress* elemento é opcional.</span><span class="sxs-lookup"><span data-stu-id="652b6-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="652b6-153">Se não for definido, um IP interno disponível da sub-rede Olá implementado é escolhido.</span><span class="sxs-lookup"><span data-stu-id="652b6-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="652b6-154">Olá, valor de Olá *nome* elemento especificado na *FrontendIPConfiguration* deve ser utilizada no Olá HTTPListener *FrontendIP* elemento toorefer toohello FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="652b6-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="652b6-155">**Exemplo XML de configuração**</span><span class="sxs-lookup"><span data-stu-id="652b6-155">**Configuration XML sample**</span></span>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="652b6-156">Configuração do gateway de Olá de conjunto</span><span class="sxs-lookup"><span data-stu-id="652b6-156">Set hello gateway configuration</span></span>
<span data-ttu-id="652b6-157">Em seguida, iremos definir o gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="652b6-158">Pode utilizar Olá `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um ficheiro XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="652b6-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-hello-gateway"></a><span data-ttu-id="652b6-159">Iniciar Olá gateway</span><span class="sxs-lookup"><span data-stu-id="652b6-159">Start hello gateway</span></span>

<span data-ttu-id="652b6-160">Assim que tiver sido configurada gateway Olá, utilize Olá `Start-AzureApplicationGateway` gateway do cmdlet toostart Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="652b6-161">Faturação de um gateway de aplicação começa depois do gateway de Olá foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="652b6-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="652b6-162">Olá `Start-AzureApplicationGateway` cmdlet poderá demorar até toocomplete too15-20 minutos.</span><span class="sxs-lookup"><span data-stu-id="652b6-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
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

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="652b6-163">Verifique o estado do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="652b6-163">Verify hello gateway status</span></span>

<span data-ttu-id="652b6-164">Olá utilize `Get-AzureApplicationGateway` cmdlet toocheck Olá Estado gateway.</span><span class="sxs-lookup"><span data-stu-id="652b6-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="652b6-165">Se `Start-AzureApplicationGateway` foi concluída com êxito no passo anterior Olá, estado de Olá deve ser *executar*, Olá Vip e DnsName deverão ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="652b6-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="652b6-166">Este exemplo mostra o cmdlet Olá na primeira linha Olá, seguido pela saída Olá.</span><span class="sxs-lookup"><span data-stu-id="652b6-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="652b6-167">Neste exemplo Olá gateway está em execução e pronto tootake tráfego.</span><span class="sxs-lookup"><span data-stu-id="652b6-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="652b6-168">gateway de aplicação Olá está configurado tooaccept tráfego em Olá configurado ILB ponto final de 10.0.0.10 neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="652b6-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="652b6-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="652b6-169">Next steps</span></span>
<span data-ttu-id="652b6-170">Se pretender obter mais informações sobre as opções de balanceamento de carga em geral, veja:</span><span class="sxs-lookup"><span data-stu-id="652b6-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="652b6-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="652b6-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="652b6-172">Gestor de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="652b6-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

