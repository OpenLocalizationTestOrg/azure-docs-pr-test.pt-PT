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
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="f6e67-103">Configurar um gateway de aplicação para a descarga de SSL com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6e67-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6e67-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f6e67-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="f6e67-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6e67-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="f6e67-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6e67-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="f6e67-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="f6e67-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="f6e67-108">Gateway de aplicação do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão em Olá gateway tooavoid dispendiosa SSL desencriptação tarefas toohappen no farm do Olá web.</span><span class="sxs-lookup"><span data-stu-id="f6e67-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="f6e67-109">Descarga de SSL também simplifica a configuração do servidor front-end Olá e a gestão de aplicações web de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f6e67-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f6e67-110">Before you begin</span></span>

1. <span data-ttu-id="f6e67-111">Instale a versão mais recente do Olá Olá Azure de cmdlets do PowerShell, utilizando Olá instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="f6e67-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="f6e67-112">Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferências](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f6e67-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f6e67-113">Criar uma rede virtual e uma sub-rede de gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="f6e67-114">Certifique-se de que nenhuma máquina virtual ou implementações de nuvem estão a utilizar a sub-rede de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="f6e67-115">O Application Gateway tem de constar, por si só, numa sub-rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f6e67-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="f6e67-116">servidores de Olá configurar o gateway de aplicação Olá toouse tem de existir ou tem os respetivos pontos finais criados na rede virtual Olá ou com um IP/VIP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="f6e67-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="f6e67-117">O que é necessário toocreate um gateway de aplicação?</span><span class="sxs-lookup"><span data-stu-id="f6e67-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="f6e67-118">**Agrupamento de servidores de back-end:** lista Olá de endereços IP dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="f6e67-119">endereços IP Olá listados devem pertencer toohello sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="f6e67-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="f6e67-120">**Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies.</span><span class="sxs-lookup"><span data-stu-id="f6e67-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f6e67-121">Estas definições estão associada tooa conjunto e são aplicados tooall servidores dentro do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="f6e67-122">**Porta de front-end:** esta porta é Olá Porta pública aberta no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="f6e67-123">O tráfego chega a esta porta e, em seguida, obtém redirecionado tooone dos servidores de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="f6e67-124">**Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estas definições são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).</span><span class="sxs-lookup"><span data-stu-id="f6e67-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f6e67-125">**Regra:** regra Olá vincula o serviço de escuta de Olá e agrupamento de servidores de back-end de Olá e define o tráfego de Olá de agrupamento de servidores de back-end deve ser direcionado toowhen chegar a um determinado serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="f6e67-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="f6e67-126">Atualmente, apenas Olá *básico* regra é suportada.</span><span class="sxs-lookup"><span data-stu-id="f6e67-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="f6e67-127">Olá *básico* regra é a distribuição de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="f6e67-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="f6e67-128">**Notas de configuração adicionais**</span><span class="sxs-lookup"><span data-stu-id="f6e67-128">**Additional configuration notes**</span></span>

<span data-ttu-id="f6e67-129">Para a configuração de certificados SSL, Olá protocolo no **HttpListener** deve alterar demasiado*Https* (sensível às maiúsculas e).</span><span class="sxs-lookup"><span data-stu-id="f6e67-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="f6e67-130">Olá **SslCertificate** elemento é adicionado demasiado**HttpListener** com o valor da variável Olá configurado para o certificado SSL Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="f6e67-131">porta de front-end Olá deve ser too443 atualizado.</span><span class="sxs-lookup"><span data-stu-id="f6e67-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="f6e67-132">**a afinidade de com base em cookies tooenable**: um gateway de aplicação pode ser configurado tooensure que um pedido de uma sessão de cliente é sempre toohello direcionado mesma VM no farm do Olá web.</span><span class="sxs-lookup"><span data-stu-id="f6e67-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="f6e67-133">Este cenário é feito ao injetar um cookie de sessão que permita o tráfego de toodirect do gateway de Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f6e67-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="f6e67-134">definir a afinidade com base no cookie tooenable, **CookieBasedAffinity** demasiado*ativado* no Olá **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6e67-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="f6e67-135">Criar um gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="f6e67-135">Create an application gateway</span></span>

<span data-ttu-id="f6e67-136">diferença Olá entre a utilização do modelo de implementação clássico do Azure Olá e o Azure Resource Manager é a ordem de Olá que criar uma aplicação gateway e Olá itens que precisam de toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="f6e67-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="f6e67-137">Com o Resource Manager, todos os componentes de um gateway de aplicação são configurados individualmente e, em seguida, colocar em conjunto toocreate um recurso de gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="f6e67-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="f6e67-138">Seguem-se Olá passos necessários toocreate um gateway de aplicação:</span><span class="sxs-lookup"><span data-stu-id="f6e67-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="f6e67-139">Criar um grupo de recursos para o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6e67-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="f6e67-140">Criar rede virtual, uma sub-rede e um IP público para o gateway de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="f6e67-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="f6e67-141">Criar um objeto de configuração do gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="f6e67-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="f6e67-142">Criar um recurso do gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="f6e67-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="f6e67-143">Criar um grupo de recursos para o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6e67-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="f6e67-144">Certifique-se de que muda de cmdlets do PowerShell modo toouse Olá do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f6e67-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="f6e67-145">Para obter mais informações, veja [Using Windows PowerShell with Resource Manager (Usar o Windows PowerShell com o Resource Manager)](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f6e67-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="f6e67-146">Passo 1</span><span class="sxs-lookup"><span data-stu-id="f6e67-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="f6e67-147">Passo 2</span><span class="sxs-lookup"><span data-stu-id="f6e67-147">Step 2</span></span>

<span data-ttu-id="f6e67-148">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f6e67-149">São tooauthenticate pedido com as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="f6e67-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="f6e67-150">Passo 3</span><span class="sxs-lookup"><span data-stu-id="f6e67-150">Step 3</span></span>

<span data-ttu-id="f6e67-151">Escolha qual das suas toouse de subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e67-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="f6e67-152">Passo 4</span><span class="sxs-lookup"><span data-stu-id="f6e67-152">Step 4</span></span>

<span data-ttu-id="f6e67-153">Crie um novo grupo de recursos (ignore este passo se estiver a utilizar um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="f6e67-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="f6e67-154">O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização,</span><span class="sxs-lookup"><span data-stu-id="f6e67-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f6e67-155">Esta definição é utilizada como localização predefinida de Olá para recursos nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f6e67-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="f6e67-156">Certifique-se de que todos os comandos toocreate, utiliza um gateway de aplicação Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f6e67-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="f6e67-157">No exemplo de Olá acima, criámos um grupo de recursos denominado **appgw-RG** e a localização **EUA oeste**.</span><span class="sxs-lookup"><span data-stu-id="f6e67-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="f6e67-158">Criar uma rede virtual e uma sub-rede de gateway de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="f6e67-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="f6e67-159">Olá seguinte exemplo mostra como toocreate uma rede virtual utilizando o Gestor de recursos:</span><span class="sxs-lookup"><span data-stu-id="f6e67-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="f6e67-160">Passo 1</span><span class="sxs-lookup"><span data-stu-id="f6e67-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="f6e67-161">Este exemplo atribui Olá endereço intervalo 10.0.0.0/24 tooa sub-rede toobe variável utilizado toocreate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f6e67-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="f6e67-162">Passo 2</span><span class="sxs-lookup"><span data-stu-id="f6e67-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="f6e67-163">Este exemplo cria uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw-rg** região EUA oeste de Olá com Olá prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f6e67-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="f6e67-164">Passo 3</span><span class="sxs-lookup"><span data-stu-id="f6e67-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="f6e67-165">Este exemplo atribui o objeto de sub-rede Olá toovariable $subnet para passos Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="f6e67-166">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="f6e67-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="f6e67-167">Este exemplo cria um recurso IP público **publicIP01** no grupo de recursos **appgw-rg** para a região EUA oeste de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="f6e67-168">Criar um objeto de configuração do gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="f6e67-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="f6e67-169">Passo 1</span><span class="sxs-lookup"><span data-stu-id="f6e67-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="f6e67-170">Este exemplo cria uma configuração de IP do gateway de aplicação com o nome **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="f6e67-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="f6e67-171">Quando é iniciado o Gateway de aplicação, escolherá um endereço IP da sub-rede Olá configurado e encaminhar os endereços IP de toohello de tráfego de rede no conjunto IP back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="f6e67-172">Note que cada instância terá um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="f6e67-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="f6e67-173">Passo 2</span><span class="sxs-lookup"><span data-stu-id="f6e67-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="f6e67-174">Este exemplo configura com o nome dos conjunto de endereços IP para back-end Olá **pool01** com endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="f6e67-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="f6e67-175">Esses valores são os endereços IP de Olá que recebem tráfego de rede de Olá provém do ponto final de IP Front-end Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="f6e67-176">Substitua os endereços IP de Olá de Olá anterior exemplo com endereços IP Olá de pontos finais da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="f6e67-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="f6e67-177">Passo 3</span><span class="sxs-lookup"><span data-stu-id="f6e67-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="f6e67-178">Este exemplo configura a definição de gateway de aplicação **poolsetting01** tráfego de rede com balanceamento de tooload no conjunto de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="f6e67-179">Passo 4</span><span class="sxs-lookup"><span data-stu-id="f6e67-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="f6e67-180">Este exemplo configura a porta IP Front-end Olá com o nome **frontendport01** para o ponto final IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="f6e67-181">Passo 5</span><span class="sxs-lookup"><span data-stu-id="f6e67-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="f6e67-182">Este exemplo configura o certificado de Olá utilizado para a ligação SSL.</span><span class="sxs-lookup"><span data-stu-id="f6e67-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="f6e67-183">necessita de certificado Olá toobe no formato. pfx e palavras-passe de Olá tem de ter entre 4 too12 carateres.</span><span class="sxs-lookup"><span data-stu-id="f6e67-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="f6e67-184">Passo 6</span><span class="sxs-lookup"><span data-stu-id="f6e67-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="f6e67-185">Este exemplo cria a configuração IP Front-end Olá com o nome **fipconfig01** e associa Olá endereço IP público com a configuração de IP Front-end Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="f6e67-186">Passo 7</span><span class="sxs-lookup"><span data-stu-id="f6e67-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="f6e67-187">Este exemplo cria o nome do serviço de escuta de Olá **listener01** e associa Olá certificado e à configuração de IP de front-end de toohello de porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="f6e67-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="f6e67-188">Passo 8</span><span class="sxs-lookup"><span data-stu-id="f6e67-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="f6e67-189">Este exemplo cria Olá regra Balanceador de carga encaminhamento com o nome **rule01** que configura o comportamento do Balanceador de carga de Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="f6e67-190">Passo 9</span><span class="sxs-lookup"><span data-stu-id="f6e67-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="f6e67-191">Este exemplo configura o tamanho da instância Olá Olá do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="f6e67-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e67-192">Olá valor predefinido para *InstanceCount* é 2, com um valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="f6e67-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="f6e67-193">Olá valor predefinido para *GatewaySize* é médio.</span><span class="sxs-lookup"><span data-stu-id="f6e67-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="f6e67-194">Pode escolher entre Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="f6e67-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="f6e67-195">Passo 10</span><span class="sxs-lookup"><span data-stu-id="f6e67-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="f6e67-196">Este passo define Olá SSL política toouse no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f6e67-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="f6e67-197">Visite [versões de política de configurar o SSL e conjuntos de cifras no Gateway de aplicação](application-gateway-configure-ssl-policy-powershell.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="f6e67-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="f6e67-198">Criar um gateway de aplicação com o New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="f6e67-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="f6e67-199">Este exemplo cria um gateway de aplicação com todos os itens de configuração do Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="f6e67-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="f6e67-200">Exemplo de Olá, o gateway de aplicação Olá denomina **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="f6e67-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f6e67-201">Obter nome de DNS de gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="f6e67-201">Get application gateway DNS name</span></span>

<span data-ttu-id="f6e67-202">Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="f6e67-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f6e67-203">Ao utilizar um IP público, o gateway de aplicação requer um nome DNS dinamicamente atribuído, que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="f6e67-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f6e67-204">os utilizadores finais de tooensure pode atingiu o gateway de aplicação Olá, um registo CNAME pode ser utilizado toopoint toohello ponto final público Olá do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="f6e67-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="f6e67-205">[Configurar um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6e67-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f6e67-206">toodo, detalhes de obtenção de gateway de aplicação Olá e o respetivo nome IP/DNS associado com o gateway de aplicação do Olá PublicIPAddress elemento toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="f6e67-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="f6e67-207">nome DNS do gateway de aplicação Olá deve ser utilizado toocreate um registo CNAME, nome DNS de toothis de aplicações que pontos Olá dois web.</span><span class="sxs-lookup"><span data-stu-id="f6e67-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="f6e67-208">utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="f6e67-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="f6e67-209">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f6e67-209">Next steps</span></span>

<span data-ttu-id="f6e67-210">Se quiser tooconfigure um toouse de gateway de aplicação com um balanceador de carga interno (ILB), consulte [criar um gateway de aplicação com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="f6e67-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="f6e67-211">Se pretender obter mais informações sobre as opções de balanceamento de carga em geral, veja:</span><span class="sxs-lookup"><span data-stu-id="f6e67-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="f6e67-212">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="f6e67-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="f6e67-213">Gestor de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="f6e67-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

