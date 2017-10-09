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
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="77ac4-103">Integrar a gestão de API numa VNET interna com Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="77ac4-104"><a name="overview"></a> Descrição geral</span><span class="sxs-lookup"><span data-stu-id="77ac4-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="77ac4-105">Olá serviço de API Management pode ser configurada numa rede Virtual no modo interno que torna acessível apenas a partir de dentro de Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="77ac4-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="77ac4-106">Gateway de aplicação do Azure é um serviço de PAAS que fornece um balanceador de carga de 7 camadas.</span><span class="sxs-lookup"><span data-stu-id="77ac4-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="77ac4-107">É também age como um serviço de proxy inverso e fornece entre a oferta de uma Firewall de aplicação Web (WAF).</span><span class="sxs-lookup"><span data-stu-id="77ac4-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="77ac4-108">Combinar aprovisionados numa VNET interna com Gateway de aplicação de Olá front-end de API de gestão permite Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="77ac4-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="77ac4-109">Utilize Olá mesmo recurso da gestão de API para consumo por consumidores internos e externos consumidores.</span><span class="sxs-lookup"><span data-stu-id="77ac4-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="77ac4-110">Utilizar um único recurso de gestão de API e um subconjunto de APIs definidas na API Management disponível para consumidores externos.</span><span class="sxs-lookup"><span data-stu-id="77ac4-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="77ac4-111">Fornecer uma forma de chave de ative tooswitch acesso tooAPI gestão de Olá Internet pública e desativar.</span><span class="sxs-lookup"><span data-stu-id="77ac4-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="77ac4-112"><a name="scenario"></a> Cenário</span><span class="sxs-lookup"><span data-stu-id="77ac4-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="77ac4-113">Este artigo irá cobrir como toouse uma única API Management service para consumidores internos e externos e torná-lo atuar como um único front-end para ambos no local e APIs da nuvem.</span><span class="sxs-lookup"><span data-stu-id="77ac4-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="77ac4-114">Também verá como tooexpose apenas um subconjunto das suas APIs (por exemplo de Olá que são realçados verde) para consumo externo utilizando Olá PathBasedRouting funcionalidade disponível no Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="77ac4-115">Exemplo de configuração primeiro Olá as suas APIs são geridos apenas a partir de dentro da sua rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="77ac4-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="77ac4-116">Consumidores internos (cor de laranja realçado em) podem aceder a todas as suas APIs internos e externos.</span><span class="sxs-lookup"><span data-stu-id="77ac4-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="77ac4-117">Tráfego nunca vai tooInternet que é entregue um elevado desempenho através de circuitos do Expressroute.</span><span class="sxs-lookup"><span data-stu-id="77ac4-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![rota de URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="77ac4-119"><a name="before-you-begin"></a> Antes de começar</span><span class="sxs-lookup"><span data-stu-id="77ac4-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="77ac4-120">Instale a versão mais recente do Olá Olá Azure de cmdlets do PowerShell, utilizando Olá instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="77ac4-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="77ac4-121">Pode transferir e instalar a versão mais recente Olá de Olá **do Windows PowerShell** secção Olá [página de transferências](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="77ac4-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="77ac4-122">Criar uma rede Virtual e crie sub-redes separadas para a API Management e o Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="77ac4-123">Se tenciona toocreate um servidor DNS personalizado para Olá rede Virtual, tal antes de iniciar a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="77ac4-124">Verifique novamente funciona, assegurando que uma máquina virtual criada numa sub-rede nova no Olá rede Virtual pode resolver e aceder a todos os pontos finais de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ac4-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="77ac4-125">O que é necessário toocreate uma integração entre a API Management e o Gateway de aplicação?</span><span class="sxs-lookup"><span data-stu-id="77ac4-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="77ac4-126">**Agrupamento de servidores de back-end:** este é o endereço IP virtual interno por Olá de Olá serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="77ac4-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="77ac4-127">**Definições do conjunto de servidores de back-end:** cada conjunto tem definições como a porta, o protocolo e a afinidade com base em cookies.</span><span class="sxs-lookup"><span data-stu-id="77ac4-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="77ac4-128">Estas definições são aplicadas tooall servidores dentro do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="77ac4-129">**Porta de front-end:** é Olá Porta pública aberta no gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="77ac4-130">Tráfego de alcance obtém tooone redirecionada de Olá servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="77ac4-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="77ac4-131">**Serviço de escuta:** escuta Olá possui uma porta de front-end, um protocolo (Http ou Https, estes valores são maiúsculas e minúsculas) e Olá nome do certificado SSL (se configurar o SSL offload).</span><span class="sxs-lookup"><span data-stu-id="77ac4-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="77ac4-132">**Regra:** regra Olá está vinculado um agrupamento de servidores de back-end do serviço de escuta tooa.</span><span class="sxs-lookup"><span data-stu-id="77ac4-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="77ac4-133">**Sonda de estado de funcionamento personalizada:** Gateway de aplicação, por predefinição, utiliza IP endereço com base em pesquisas toofigure enviados os servidores no Olá BackendAddressPool estão ativas.</span><span class="sxs-lookup"><span data-stu-id="77ac4-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="77ac4-134">Olá serviço de API Management responde apenas toorequests que tem o cabeçalho de anfitrião correto de Olá, por conseguinte, as pesquisas de predefinição Olá falharem.</span><span class="sxs-lookup"><span data-stu-id="77ac4-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="77ac4-135">Necessita de uma sonda do Estado de funcionamento personalizado toobe definido pelo gateway de aplicação toohelp determinar que o serviço de Olá está ativo e deve reencaminhar pedidos.</span><span class="sxs-lookup"><span data-stu-id="77ac4-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="77ac4-136">**Certificado de domínio personalizado:** tooaccess API Management do Olá terá toocreate um mapeamento CNAME de nome de anfitrião toohello Gateway de aplicação front-end nome DNS de internet.</span><span class="sxs-lookup"><span data-stu-id="77ac4-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="77ac4-137">Isto garante que cabeçalho de nome de anfitrião de Olá e certificados enviados tooApplication Gateway seja reencaminhado tooAPI gestão é um que APIM pode reconhecer como válido.</span><span class="sxs-lookup"><span data-stu-id="77ac4-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="77ac4-138"><a name="overview-steps"></a> Passos necessários para integrar o API Management e o Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="77ac4-139">Crie um grupo de recursos para o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77ac4-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="77ac4-140">Crie uma rede Virtual, uma sub-rede e um IP público para Olá Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="77ac4-141">Crie outra sub-rede para a API Management.</span><span class="sxs-lookup"><span data-stu-id="77ac4-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="77ac4-142">Criar um serviço de API Management dentro de sub-rede da VNET de Olá criado acima e certifique-se de que utilizar o modo interno Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="77ac4-143">Configure o nome de domínio personalizado de Olá no Olá serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="77ac4-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="77ac4-144">Crie um objeto de configuração do Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="77ac4-145">Crie um recurso de Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="77ac4-146">Crie um CNAME do nome DNS público Olá de nome de anfitrião do Olá Gateway de aplicação toohello API Management proxy.</span><span class="sxs-lookup"><span data-stu-id="77ac4-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="77ac4-147">Criar um grupo de recursos para o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="77ac4-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="77ac4-148">Certifique-se de que está a utilizar Olá versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ac4-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="77ac4-149">Para obter mais informações, veja [Using Windows PowerShell with Resource Manager (Usar o Windows PowerShell com o Resource Manager)](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="77ac4-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="77ac4-150">Passo 1</span><span class="sxs-lookup"><span data-stu-id="77ac4-150">Step 1</span></span>

<span data-ttu-id="77ac4-151">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="77ac4-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="77ac4-152">Autenticar com as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="77ac4-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="77ac4-153">Passo 2</span><span class="sxs-lookup"><span data-stu-id="77ac4-153">Step 2</span></span>

<span data-ttu-id="77ac4-154">Verifique Olá subscrições para a conta de Olá e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="77ac4-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="77ac4-155">Passo 3</span><span class="sxs-lookup"><span data-stu-id="77ac4-155">Step 3</span></span>

<span data-ttu-id="77ac4-156">Crie um novo grupo de recursos (ignore este passo se estiver a utilizar um grupo de recursos existente).</span><span class="sxs-lookup"><span data-stu-id="77ac4-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="77ac4-157">O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização,</span><span class="sxs-lookup"><span data-stu-id="77ac4-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="77ac4-158">Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77ac4-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="77ac4-159">Certifique-se de que todos os comandos toocreate um Olá de utilização do gateway de aplicação mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77ac4-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="77ac4-160">Criar uma rede Virtual e uma sub-rede de gateway de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="77ac4-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="77ac4-161">Olá seguinte exemplo mostra como toocreate utilizando uma rede Virtual hello do resource manager.</span><span class="sxs-lookup"><span data-stu-id="77ac4-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="77ac4-162">Passo 1</span><span class="sxs-lookup"><span data-stu-id="77ac4-162">Step 1</span></span>

<span data-ttu-id="77ac4-163">Atribua Olá endereço intervalo 10.0.0.0/24 toohello sub-rede variável toobe utilizado para o Gateway de aplicação ao criar uma rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="77ac4-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="77ac4-164">Passo 2</span><span class="sxs-lookup"><span data-stu-id="77ac4-164">Step 2</span></span>

<span data-ttu-id="77ac4-165">Atribua Olá endereço intervalo 10.0.1.0/24 toohello sub-rede variável toobe utilizado para gestão de API ao criar uma rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="77ac4-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="77ac4-166">Passo 3</span><span class="sxs-lookup"><span data-stu-id="77ac4-166">Step 3</span></span>

<span data-ttu-id="77ac4-167">Criar uma rede Virtual denominada **appgwvnet** no grupo de recursos **apim-appGw-RG** para a região EUA oeste de Olá utilizando Olá prefixo 10.0.0.0/16 com 10.0.0.0/24 sub-redes e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="77ac4-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="77ac4-168">Passo 4</span><span class="sxs-lookup"><span data-stu-id="77ac4-168">Step 4</span></span>

<span data-ttu-id="77ac4-169">Atribua uma variável de sub-rede para passos Olá</span><span class="sxs-lookup"><span data-stu-id="77ac4-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="77ac4-170">Criar um serviço de API Management dentro de uma VNET configurado no modo interno</span><span class="sxs-lookup"><span data-stu-id="77ac4-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="77ac4-171">Olá exemplo seguinte mostra como toocreate um serviço de API Management numa VNET configuradas para acesso interno apenas.</span><span class="sxs-lookup"><span data-stu-id="77ac4-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="77ac4-172">Passo 1</span><span class="sxs-lookup"><span data-stu-id="77ac4-172">Step 1</span></span>
<span data-ttu-id="77ac4-173">Crie um objeto de rede Virtual de gestão de API utilizando sub-rede Olá $apimsubnetdata criado acima.</span><span class="sxs-lookup"><span data-stu-id="77ac4-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="77ac4-174">Passo 2</span><span class="sxs-lookup"><span data-stu-id="77ac4-174">Step 2</span></span>
<span data-ttu-id="77ac4-175">Crie um serviço de API Management dentro Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="77ac4-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="77ac4-176">Após ter êxito Olá acima comando consulte demasiado[configuração de DNS necessário serviço de gestão de API de VNET interno tooaccess](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="77ac4-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="77ac4-177">Configurar um nome de domínio personalizado na API Management</span><span class="sxs-lookup"><span data-stu-id="77ac4-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="77ac4-178">Passo 1</span><span class="sxs-lookup"><span data-stu-id="77ac4-178">Step 1</span></span>
<span data-ttu-id="77ac4-179">Carregue o certificado de Olá com chave privada para o domínio de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="77ac4-180">Neste exemplo será `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="77ac4-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="77ac4-181">Passo 2</span><span class="sxs-lookup"><span data-stu-id="77ac4-181">Step 2</span></span>
<span data-ttu-id="77ac4-182">Depois do certificado de Olá é carregado, criar um objeto de configuração do nome de anfitrião para o proxy de Olá com um nome de anfitrião do `api.contoso.net`, como o certificado de exemplo de Olá fornece autoridade para Olá `*.contoso.net` domínio.</span><span class="sxs-lookup"><span data-stu-id="77ac4-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="77ac4-183">Criar um endereço IP público para a configuração de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="77ac4-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="77ac4-184">Criar um recurso IP público **publicIP01** no grupo de recursos **apim-appGw-RG** para a região EUA oeste de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="77ac4-185">Um endereço IP é atribuído o gateway de aplicação toohello quando Olá serviço for iniciado.</span><span class="sxs-lookup"><span data-stu-id="77ac4-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="77ac4-186">Criar a configuração do gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-186">Create application gateway configuration</span></span>

<span data-ttu-id="77ac4-187">Todos os itens de configuração tem de ser configurados antes de criar o gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="77ac4-188">Olá passos seguintes criar Olá itens de configuração que são necessários para um recurso de gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="77ac4-189">Passo 1</span><span class="sxs-lookup"><span data-stu-id="77ac4-189">Step 1</span></span>

<span data-ttu-id="77ac4-190">Crie uma configuração de IP do gateway de aplicação com o nome **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="77ac4-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="77ac4-191">Quando é iniciado o Gateway de aplicação, escolherá um endereço IP da sub-rede Olá configurado e encaminhar os endereços IP de toohello de tráfego de rede no conjunto IP back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="77ac4-192">Note que cada instância terá um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="77ac4-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="77ac4-193">Passo 2</span><span class="sxs-lookup"><span data-stu-id="77ac4-193">Step 2</span></span>

<span data-ttu-id="77ac4-194">Configure a porta IP de front-end do Olá para o ponto final IP público Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="77ac4-195">Esta porta é a porta de Olá que os utilizadores finais que se ligam a.</span><span class="sxs-lookup"><span data-stu-id="77ac4-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="77ac4-196">Passo 3</span><span class="sxs-lookup"><span data-stu-id="77ac4-196">Step 3</span></span>

<span data-ttu-id="77ac4-197">Configure o IP de front-end Olá com ponto final IP público.</span><span class="sxs-lookup"><span data-stu-id="77ac4-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="77ac4-198">Passo 4</span><span class="sxs-lookup"><span data-stu-id="77ac4-198">Step 4</span></span>

<span data-ttu-id="77ac4-199">Configurar o certificado de Olá para hello Gateway de aplicação, utilizado toodecrypt e reencriptar o tráfego de Olá passar pela.</span><span class="sxs-lookup"><span data-stu-id="77ac4-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="77ac4-200">Passo 5</span><span class="sxs-lookup"><span data-stu-id="77ac4-200">Step 5</span></span>

<span data-ttu-id="77ac4-201">Crie o serviço de escuta HTTP de Olá para Olá Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="77ac4-202">Atribua a configuração de IP Front-end Olá, porta e tooit de certificado de ssl.</span><span class="sxs-lookup"><span data-stu-id="77ac4-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="77ac4-203">Passo 6</span><span class="sxs-lookup"><span data-stu-id="77ac4-203">Step 6</span></span>

<span data-ttu-id="77ac4-204">Criar um serviço de gestão de API de toohello sonda personalizada `ContosoApi` ponto final de domínio do proxy.</span><span class="sxs-lookup"><span data-stu-id="77ac4-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="77ac4-205">caminho de Olá `/status-0123456789abcdef` é um ponto final de estado de funcionamento predefinido alojado em todos os serviços de gestão de API de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="77ac4-206">Definir `api.contoso.net` como toosecure de nome de anfitrião uma sonda personalizada com o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="77ac4-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="77ac4-207">Olá hostname `contosoapi.azure-api.net` é o nome de anfitrião do Olá predefinido proxy configurado quando um serviço com o nome `contosoapi` é criada no Azure público.</span><span class="sxs-lookup"><span data-stu-id="77ac4-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="77ac4-208">Passo 7</span><span class="sxs-lookup"><span data-stu-id="77ac4-208">Step 7</span></span>

<span data-ttu-id="77ac4-209">Carregar o certificado de Olá toobe utilizada nos recursos de conjunto de back-end SSL ativado Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="77ac4-210">Este é Olá mesmo certificado que é fornecido no passo 4 acima.</span><span class="sxs-lookup"><span data-stu-id="77ac4-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="77ac4-211">Passo 8</span><span class="sxs-lookup"><span data-stu-id="77ac4-211">Step 8</span></span>

<span data-ttu-id="77ac4-212">Configure definições de back-end HTTP para Olá Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="77ac4-213">Isto inclui a definição de um limite de tempo limite para o pedido de back-end após o qual são canceladas.</span><span class="sxs-lookup"><span data-stu-id="77ac4-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="77ac4-214">Este valor é diferente do tempo limite de sonda de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="77ac4-215">Passo 9</span><span class="sxs-lookup"><span data-stu-id="77ac4-215">Step 9</span></span>

<span data-ttu-id="77ac4-216">Configurar um conjunto de endereços IP back-end com o nome **apimbackend** com Olá IP virtual interno endereço do Olá serviço de API Management criado acima.</span><span class="sxs-lookup"><span data-stu-id="77ac4-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="77ac4-217">Passo 10</span><span class="sxs-lookup"><span data-stu-id="77ac4-217">Step 10</span></span>

<span data-ttu-id="77ac4-218">Crie as definições para um back-end de (inexistente) fictício.</span><span class="sxs-lookup"><span data-stu-id="77ac4-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="77ac4-219">Os caminhos de tooAPI de pedidos que não queremos tooexpose da API de gestão através do Gateway de aplicação serão acessos este back-end e devolver 404.</span><span class="sxs-lookup"><span data-stu-id="77ac4-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="77ac4-220">Configure definições de HTTP para Olá fictício back-end.</span><span class="sxs-lookup"><span data-stu-id="77ac4-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="77ac4-221">Configurar um back-end fictício **dummyBackendPool**, que aponta de endereço FQDN tooa **dummybackend.com**. Este endereço FQDN não existe na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="77ac4-222">Criar uma regra de definição que Olá Gateway de aplicação irão utilizar por predefinição que aponta de back-end do toohello inexistente **dummybackend.com** no Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="77ac4-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="77ac4-223">Passo 11</span><span class="sxs-lookup"><span data-stu-id="77ac4-223">Step 11</span></span>

<span data-ttu-id="77ac4-224">Configure caminhos de regra de URL para os conjuntos de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="77ac4-225">Isto permite selecionar apenas a alguns dos Olá das APIs de gestão de API para a ser expostos toohello público.</span><span class="sxs-lookup"><span data-stu-id="77ac4-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="77ac4-226">Por exemplo, se existirem `Echo API` (eco /), `Calculator API` (/calc/), etc. disponibilizar apenas `Echo API` acessível a partir da Internet).</span><span class="sxs-lookup"><span data-stu-id="77ac4-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="77ac4-227">Olá exemplo seguinte cria uma regra simples para Olá "eco /" caminho encaminhamento tráfego toohello back-end "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="77ac4-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="77ac4-228">Se o caminho de Olá não corresponde ao caminho de Olá regras queremos tooenable da gestão de API, configuração de mapa de caminho configura também um conjunto predefinido de endereços de back-end com o nome de regra de Olá **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="77ac4-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="77ac4-229">Por exemplo, http://api.contoso.net/calc/ * ficar demasiado**dummyBackendPool** como está definida como conjunto predefinido de Olá para o tráfego não correspondente.</span><span class="sxs-lookup"><span data-stu-id="77ac4-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="77ac4-230">Olá acima passo garante que apenas os pedidos para o caminho de Olá "/ eco" são permitidos através de Olá Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="77ac4-231">Tooother pedidos que APIs configuradas na API Management irá gerar 404 erros do Gateway de aplicação quando acedido a partir de Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="77ac4-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="77ac4-232">Passo 12</span><span class="sxs-lookup"><span data-stu-id="77ac4-232">Step 12</span></span>

<span data-ttu-id="77ac4-233">Crie uma definição de regra para Olá Gateway de aplicação toouse URL com base no caminho encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="77ac4-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="77ac4-234">Passo 13</span><span class="sxs-lookup"><span data-stu-id="77ac4-234">Step 13</span></span>

<span data-ttu-id="77ac4-235">Configure Olá número de instâncias e o tamanho para Olá Gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="77ac4-236">Aqui vamos utilizar Olá [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para maior segurança de Olá recurso da gestão de API.</span><span class="sxs-lookup"><span data-stu-id="77ac4-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="77ac4-237">Passo 14</span><span class="sxs-lookup"><span data-stu-id="77ac4-237">Step 14</span></span>

<span data-ttu-id="77ac4-238">Configure WAF toobe no modo de "Prevenção".</span><span class="sxs-lookup"><span data-stu-id="77ac4-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="77ac4-239">Criar Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-239">Create Application Gateway</span></span>

<span data-ttu-id="77ac4-240">Crie um Gateway de aplicação com todos os objetos de configuração de Olá de Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="77ac4-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="77ac4-241">CNAME Olá API Management proxy hostname toohello nome DNS público do Olá recurso do Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="77ac4-242">Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="77ac4-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="77ac4-243">Quando utilizar um IP público, o Gateway de aplicação requer um nome DNS dinamicamente atribuído, que pode não ser toouse fácil.</span><span class="sxs-lookup"><span data-stu-id="77ac4-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="77ac4-244">Olá nome DNS do Gateway de aplicação deve ser utilizado toocreate um registo CNAME que aponta de nome de anfitrião proxy Olá APIM (por exemplo, `api.contoso.net` nos exemplos de Olá acima) toothis nome DNS.</span><span class="sxs-lookup"><span data-stu-id="77ac4-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="77ac4-245">tooconfigure Olá front-end um registo CNAME de IP, obter detalhes sobre Olá Olá Gateway de aplicação e o seu nome IP/DNS associado utilizando o elemento de PublicIPAddress Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="77ac4-246">utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway.</span><span class="sxs-lookup"><span data-stu-id="77ac4-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="77ac4-247"><a name="summary"></a> Resumo</span><span class="sxs-lookup"><span data-stu-id="77ac4-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="77ac4-248">Gestão de API do Azure configurada numa VNET fornece uma interface de gateway único para todos os APIs configuradas, se estiverem alojado no local ou na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="77ac4-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="77ac4-249">Integrar o Gateway de aplicação com a API Management proporciona flexibilidade de Olá de seletivamente ativar específico toobe APIs acessível no Olá Internet, bem como fornecer uma Firewall de aplicação Web como uma instância de API Management tooyour front-end.</span><span class="sxs-lookup"><span data-stu-id="77ac4-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="77ac4-250"><a name="next-steps"></a> Próximos passos</span><span class="sxs-lookup"><span data-stu-id="77ac4-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="77ac4-251">Saiba mais sobre o Gateway de aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="77ac4-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="77ac4-252">Descrição geral do Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="77ac4-253">Firewall de aplicação de Web de Gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="77ac4-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="77ac4-254">Gateway de aplicação com o encaminhamento com base no caminho</span><span class="sxs-lookup"><span data-stu-id="77ac4-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="77ac4-255">Saiba mais sobre a gestão de API e as VNETs</span><span class="sxs-lookup"><span data-stu-id="77ac4-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="77ac4-256">Utilizar a API Management disponível apenas dentro do Olá VNET</span><span class="sxs-lookup"><span data-stu-id="77ac4-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="77ac4-257">Utilizar a API Management na VNET</span><span class="sxs-lookup"><span data-stu-id="77ac4-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
