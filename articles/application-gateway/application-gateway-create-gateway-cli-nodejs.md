---
title: "aaaCreate um Gateway de aplicação do Azure - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate um Gateway de aplicação utilizando Olá 1.0 CLI do Azure no Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="0166a-103">Criar um gateway de aplicação utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0166a-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0166a-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0166a-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="0166a-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="0166a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="0166a-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="0166a-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="0166a-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0166a-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="0166a-108">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0166a-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="0166a-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0166a-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="0166a-110">O Application Gateway do Azure é um balanceador de carga de 7 camadas.</span><span class="sxs-lookup"><span data-stu-id="0166a-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="0166a-111">Fornece ativação pós-falha, pedidos HTTP de encaminhamento de desempenho entre diferentes servidores, quer estejam na nuvem de Olá ou no local.</span><span class="sxs-lookup"><span data-stu-id="0166a-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="0166a-112">Gateway de aplicação tem Olá seguintes funcionalidades de entrega de aplicações: carregar sondas de estado de funcionamento personalizado de balanceamento, afinidade de sessão com base em cookies e descarga de Secure Sockets Layer (SSL), HTTP e suporte para vários sites.</span><span class="sxs-lookup"><span data-stu-id="0166a-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="0166a-113">Pré-requisito: Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0166a-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="0166a-114">Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](../xplat-cli-install.md) e terá de demasiado[iniciar sessão tooAzure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0166a-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="0166a-115">Se não tiver uma conta do Azure, é necessário um.</span><span class="sxs-lookup"><span data-stu-id="0166a-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="0166a-116">Subscreva [uma avaliação gratuita aqui](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="0166a-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="0166a-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="0166a-117">Scenario</span></span>

<span data-ttu-id="0166a-118">Neste cenário, saiba como toocreate um gateway de aplicação utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0166a-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="0166a-119">Neste cenário irão:</span><span class="sxs-lookup"><span data-stu-id="0166a-119">This scenario will:</span></span>

* <span data-ttu-id="0166a-120">Crie um gateway de aplicação médias com duas instâncias.</span><span class="sxs-lookup"><span data-stu-id="0166a-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="0166a-121">Crie uma rede virtual denominada ContosoVNET com um bloco CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="0166a-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="0166a-122">Crie uma sub-rede denominada subnet01 que utiliza 10.0.0.0/28 como bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="0166a-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="0166a-123">Pesquisas de configuração adicional do gateway de aplicação Olá, incluindo o estado de funcionamento personalizado, os endereços do conjunto de back-end e regras adicionais são configurados após a configuração do gateway de aplicação Olá e não durante a implementação inicial.</span><span class="sxs-lookup"><span data-stu-id="0166a-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0166a-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0166a-124">Before you begin</span></span>

<span data-ttu-id="0166a-125">Gateway de aplicação do Azure requer a sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0166a-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="0166a-126">Ao criar uma rede virtual, certifique-se de que deixe suficiente toohave de espaço de endereço várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="0166a-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="0166a-127">Depois de implementar uma sub-rede de tooa do gateway de aplicação, os gateways de aplicação apenas adicionais são toobe capaz de adicionado toohello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0166a-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="0166a-128">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="0166a-128">Log in tooAzure</span></span>

<span data-ttu-id="0166a-129">Abra Olá **linha de comandos do Microsoft Azure**e inicie sessão.</span><span class="sxs-lookup"><span data-stu-id="0166a-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="0166a-130">Depois de escrever Olá anterior exemplo, é fornecido um código.</span><span class="sxs-lookup"><span data-stu-id="0166a-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="0166a-131">Navegue toohttps://aka.ms/devicelogin um processo de início de sessão do browser toocontinue Olá.</span><span class="sxs-lookup"><span data-stu-id="0166a-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![o início de sessão do cmd que mostra dispositivos][1]

<span data-ttu-id="0166a-133">No browser Olá, introduza o código de Olá que recebeu.</span><span class="sxs-lookup"><span data-stu-id="0166a-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="0166a-134">São tooa redirecionada-página sessão.</span><span class="sxs-lookup"><span data-stu-id="0166a-134">You are redirected tooa sign-in page.</span></span>

![código de tooenter do browser][2]

<span data-ttu-id="0166a-136">Assim que foi introduzido um código de Olá tem sessão iniciada, fechar Olá browser toocontinue com cenário Olá.</span><span class="sxs-lookup"><span data-stu-id="0166a-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![sessão iniciada com êxito][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="0166a-138">Comutador tooResource modo Manager</span><span class="sxs-lookup"><span data-stu-id="0166a-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="0166a-139">Criar grupo de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="0166a-139">Create hello resource group</span></span>

<span data-ttu-id="0166a-140">Antes de criar o gateway de aplicação Olá, o gateway de aplicação Olá toocontain é criado um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0166a-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="0166a-141">seguinte Olá mostra comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="0166a-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="0166a-142">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="0166a-142">Create a virtual network</span></span>

<span data-ttu-id="0166a-143">Após criar o grupo de recursos de Olá, uma rede virtual é criada para o gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="0166a-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="0166a-144">No seguinte exemplo de Olá, espaço de endereços de Olá foi como 10.0.0.0/16 como definido no Olá precedente notas de cenário.</span><span class="sxs-lookup"><span data-stu-id="0166a-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="0166a-145">Criar uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="0166a-145">Create a subnet</span></span>

<span data-ttu-id="0166a-146">Depois de criar rede virtual Olá, é adicionada uma sub-rede de gateway de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="0166a-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="0166a-147">Se planear toouse o gateway de aplicação com uma aplicação web alojadas no Olá mesmo virtual de rede como gateway de aplicação Olá, ser tooleave se tenha espaço suficiente para outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0166a-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="0166a-148">Criar gateway de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="0166a-148">Create hello application gateway</span></span>

<span data-ttu-id="0166a-149">Assim que a rede virtual Olá e sub-rede são criados, pré-requisitos Olá Olá gateway de aplicação estão concluídos.</span><span class="sxs-lookup"><span data-stu-id="0166a-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="0166a-150">Além de um. pfx exportado anteriormente certificado e Olá palavra-passe Olá certificado são necessários para Olá seguinte passo: endereços IP de Olá utilizados para o back-end de Olá são endereços IP de Olá para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="0166a-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="0166a-151">Estes valores podem ser ambos IPs privados numa rede virtual Olá, os ips públicos ou nomes de domínio totalmente qualificados para os servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="0166a-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="0166a-152">Para obter uma lista de parâmetros que podem ser fornecidos durante a criação do executar Olá os seguintes comandos: **criar gateway de aplicação de rede do azure – ajudar**.</span><span class="sxs-lookup"><span data-stu-id="0166a-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="0166a-153">Este exemplo cria um gateway de aplicação básico com as predefinições para o serviço de escuta de Olá, conjunto back-end, as definições http de back-end e regras.</span><span class="sxs-lookup"><span data-stu-id="0166a-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="0166a-154">Pode modificar estas definições toosuit a implementação depois de aprovisionamento de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0166a-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="0166a-155">Se já tiver a sua aplicação web definida com o conjunto de back-end Olá no Olá precedente passos, uma vez criados, o balanceamento de carga é iniciada.</span><span class="sxs-lookup"><span data-stu-id="0166a-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0166a-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0166a-156">Next steps</span></span>

<span data-ttu-id="0166a-157">Saiba como o estado de funcionamento personalizado toocreate sondas, visitando [criar uma sonda do Estado de funcionamento personalizado](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0166a-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="0166a-158">Saiba como tooconfigure descarga de SSL e de desencriptação de SSL dispendiosa do tirar Olá desativado seus servidores web, visitando [configurar a descarga de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="0166a-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
