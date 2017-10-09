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
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="09647-103">Configurar um gateway de aplicação para a descarga SSL de utilizando o modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="09647-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09647-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="09647-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="09647-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="09647-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="09647-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="09647-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="09647-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="09647-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="09647-108">Gateway de aplicação do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão em Olá gateway tooavoid dispendiosa SSL desencriptação tarefas toohappen no farm do Olá web.</span><span class="sxs-lookup"><span data-stu-id="09647-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="09647-109">Descarga de SSL também simplifica a configuração do servidor front-end Olá e a gestão de aplicações web de Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="09647-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="09647-110">Before you begin</span></span>

1. <span data-ttu-id="09647-111">Instale a versão mais recente do Olá Olá Azure de cmdlets do PowerShell, utilizando Olá instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="09647-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="09647-112">Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferências](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="09647-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="09647-113">Verifique se a rede virtual funciona com uma sub-rede válida.</span><span class="sxs-lookup"><span data-stu-id="09647-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="09647-114">Certifique-se de que nenhuma máquina virtual ou implementações de nuvem estão a utilizar a sub-rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="09647-115">gateway de aplicação Olá tem de ser por si só, numa sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="09647-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="09647-116">servidores de Olá que configurar o gateway de aplicação Olá toouse tem de existir ou tem os respetivos pontos finais criados na rede virtual Olá ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="09647-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="09647-117">tooconfigure SSL descarregamento de um gateway de aplicação, Olá os seguintes passos por ordem de Olá listado:</span><span class="sxs-lookup"><span data-stu-id="09647-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="09647-118">Criar um gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="09647-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="09647-119">Carregar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="09647-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="09647-120">Configurar o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="09647-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="09647-121">Configuração do gateway de Olá de conjunto</span><span class="sxs-lookup"><span data-stu-id="09647-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="09647-122">Iniciar Olá gateway</span><span class="sxs-lookup"><span data-stu-id="09647-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="09647-123">Verifique o estado do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="09647-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="09647-124">Criar um gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="09647-124">Create an application gateway</span></span>

<span data-ttu-id="09647-125">gateway de Olá toocreate, utilize Olá `New-AzureApplicationGateway` cmdlet, substituindo os valores de Olá com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="09647-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="09647-126">Faturação para o gateway de Olá não inicia neste momento.</span><span class="sxs-lookup"><span data-stu-id="09647-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="09647-127">Faturação começa num passo posterior, quando o gateway de Olá for iniciada com êxito.</span><span class="sxs-lookup"><span data-stu-id="09647-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="09647-128">toovalidate Olá gateway foi criado, pode utilizar Olá `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09647-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="09647-129">Exemplo de Olá, *Descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="09647-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="09647-130">Olá valor predefinido para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="09647-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="09647-131">Olá valor predefinido para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="09647-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="09647-132">Pequenas e grandes outros valores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="09647-132">Small and Large are other available values.</span></span> <span data-ttu-id="09647-133">*VirtualIPs* e *DnsName* são apresentados em branco, porque o gateway de Olá ainda não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="09647-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="09647-134">Estes valores são criados quando o gateway de Olá está num Estado de execução de Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="09647-135">Carregar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="09647-135">Upload SSL certificates</span></span>

<span data-ttu-id="09647-136">Utilize `Add-AzureApplicationGatewaySslCertificate` certificado de servidor Olá tooupload no *pfx* gateway de aplicação do formato toohello.</span><span class="sxs-lookup"><span data-stu-id="09647-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="09647-137">nome do certificado Olá é um nome de utilizador escolhida e tem de ser exclusivo no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="09647-138">Este certificado é referenciado tooby este nome em todas as operações de gestão de certificados no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="09647-139">Este exemplo seguinte mostra o cmdlet Olá, substitua os valores de Olá exemplo Olá com os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="09647-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="09647-140">Em seguida, valide o carregamento do certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="09647-141">Olá utilize `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09647-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="09647-142">Este exemplo mostra o cmdlet Olá na primeira linha Olá, seguido pela saída Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

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
> <span data-ttu-id="09647-143">palavra-passe de certificados de Olá tem toobe entre 4 too12 carateres, letras ou números.</span><span class="sxs-lookup"><span data-stu-id="09647-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="09647-144">Não são aceites carateres especiais.</span><span class="sxs-lookup"><span data-stu-id="09647-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="09647-145">Configurar o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="09647-145">Configure hello gateway</span></span>

<span data-ttu-id="09647-146">Uma configuração de gateway de aplicação consiste de vários valores.</span><span class="sxs-lookup"><span data-stu-id="09647-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="09647-147">podem ser vinculados a valores de Olá configuração de Olá tooconstruct em conjunto.</span><span class="sxs-lookup"><span data-stu-id="09647-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="09647-148">os valores de Olá são:</span><span class="sxs-lookup"><span data-stu-id="09647-148">hello values are:</span></span>

* <span data-ttu-id="09647-149">**Agrupamento de servidores de back-end:** lista Olá de endereços IP dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="09647-150">endereços IP Olá listados devem pertencer toohello sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="09647-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="09647-151">**Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies.</span><span class="sxs-lookup"><span data-stu-id="09647-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="09647-152">Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="09647-153">**Porta de front-end:** esta porta é Olá Porta pública aberta no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="09647-154">O tráfego chega a esta porta e, em seguida, obtém redirecionado tooone dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="09647-155">**Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estes valores são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).</span><span class="sxs-lookup"><span data-stu-id="09647-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="09647-156">**Regra:** regra Olá vincula o serviço de escuta de Olá e agrupamento de servidores de back-end de Olá e define o tráfego de Olá de agrupamento de servidores de back-end deve ser direcionado toowhen chegar a um determinado serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="09647-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="09647-157">Atualmente, apenas Olá *básico* regra é suportada.</span><span class="sxs-lookup"><span data-stu-id="09647-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="09647-158">Olá *básico* regra é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="09647-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="09647-159">**Notas de configuração adicionais**</span><span class="sxs-lookup"><span data-stu-id="09647-159">**Additional configuration notes**</span></span>

<span data-ttu-id="09647-160">Para a configuração de certificados SSL, Olá protocolo no **HttpListener** deve alterar demasiado*Https* (sensível às maiúsculas e).</span><span class="sxs-lookup"><span data-stu-id="09647-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="09647-161">Olá **SslCert** elemento é adicionado demasiado**HttpListener** com Olá valor definido toohello mesmo nome como utilizada no carregamento de Olá do anterior a secção de certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="09647-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="09647-162">porta de front-end Olá deve ser too443 atualizado.</span><span class="sxs-lookup"><span data-stu-id="09647-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="09647-163">**a afinidade de com base em cookies tooenable**: um gateway de aplicação pode ser configurado tooensure que um pedido de uma sessão de cliente é sempre toohello direcionado mesma VM no farm do Olá web.</span><span class="sxs-lookup"><span data-stu-id="09647-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="09647-164">Este cenário é feito ao injetar um cookie de sessão que permita o tráfego de toodirect do gateway de Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="09647-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="09647-165">definir a afinidade com base no cookie tooenable, **CookieBasedAffinity** demasiado*ativado* no Olá **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="09647-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="09647-166">Pode criar a configuração através da criação de um objeto de configuração ou utilizando um ficheiro XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="09647-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="09647-167">Utilize a configuração utilizando uma ficheiro XML, de configuração de tooconstruct Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="09647-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="09647-168">**Exemplo XML de configuração**</span><span class="sxs-lookup"><span data-stu-id="09647-168">**Configuration XML sample**</span></span>

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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="09647-169">Configuração do gateway de Olá de conjunto</span><span class="sxs-lookup"><span data-stu-id="09647-169">Set hello gateway configuration</span></span>

<span data-ttu-id="09647-170">Em seguida, configure o gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="09647-171">Pode utilizar Olá `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um ficheiro XML de configuração.</span><span class="sxs-lookup"><span data-stu-id="09647-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="09647-172">Iniciar Olá gateway</span><span class="sxs-lookup"><span data-stu-id="09647-172">Start hello gateway</span></span>

<span data-ttu-id="09647-173">Assim que tiver sido configurada gateway Olá, utilize Olá `Start-AzureApplicationGateway` gateway do cmdlet toostart Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="09647-174">Faturação de um gateway de aplicação começa depois do gateway de Olá foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="09647-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="09647-175">Olá `Start-AzureApplicationGateway` cmdlet poderá demorar até toofinish too15-20 minutos.</span><span class="sxs-lookup"><span data-stu-id="09647-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="09647-176">Verifique o estado do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="09647-176">Verify hello gateway status</span></span>

<span data-ttu-id="09647-177">Olá utilize `Get-AzureApplicationGateway` cmdlet toocheck Olá Estado gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="09647-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="09647-178">Se `Start-AzureApplicationGateway` foi concluída com êxito no passo anterior Olá, *estado* deve estar em execução e *VirtualIPs* e *DnsName* deverão ter entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="09647-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="09647-179">Este exemplo mostra um gateway de aplicação que, em execução e está pronto tootake tráfego.</span><span class="sxs-lookup"><span data-stu-id="09647-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="09647-180">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="09647-180">Next steps</span></span>

<span data-ttu-id="09647-181">Se pretender obter mais informações sobre as opções de balanceamento de carga em geral, veja:</span><span class="sxs-lookup"><span data-stu-id="09647-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="09647-182">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="09647-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="09647-183">Gestor de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="09647-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

