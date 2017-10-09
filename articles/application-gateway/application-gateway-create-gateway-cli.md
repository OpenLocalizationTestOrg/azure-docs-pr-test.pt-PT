---
title: "aaaCreate um Gateway de aplicação do Azure - Azure CLI 2.0 | Microsoft Docs"
description: "Saiba como toocreate um Gateway de aplicação utilizando Olá 2.0 CLI do Azure no Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="074fe-103">Criar um gateway de aplicação utilizando Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="074fe-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="074fe-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="074fe-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="074fe-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="074fe-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="074fe-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="074fe-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="074fe-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="074fe-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="074fe-108">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="074fe-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="074fe-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="074fe-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="074fe-110">Gateway de aplicação é uma aplicação virtual dedicada que fornece o controlador de entrega de aplicações (ADC) como um serviço, oferece várias camada 7 carregar balanceamento capacidades para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="074fe-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="074fe-111">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="074fe-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="074fe-112">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="074fe-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="074fe-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -nosso CLI para Olá clássica e resource Gestão modelos de implementação.</span><span class="sxs-lookup"><span data-stu-id="074fe-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="074fe-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="074fe-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="074fe-115">Pré-requisito: Instalar Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="074fe-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="074fe-116">Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="074fe-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="074fe-117">Se não tiver uma conta do Azure, é necessário um.</span><span class="sxs-lookup"><span data-stu-id="074fe-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="074fe-118">Subscreva [uma avaliação gratuita aqui](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="074fe-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="074fe-119">Cenário</span><span class="sxs-lookup"><span data-stu-id="074fe-119">Scenario</span></span>

<span data-ttu-id="074fe-120">Neste cenário, saiba como toocreate um gateway de aplicação utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="074fe-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="074fe-121">Neste cenário irão:</span><span class="sxs-lookup"><span data-stu-id="074fe-121">This scenario will:</span></span>

* <span data-ttu-id="074fe-122">Crie um gateway de aplicação médias com duas instâncias.</span><span class="sxs-lookup"><span data-stu-id="074fe-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="074fe-123">Crie uma rede virtual denominada AdatumAppGatewayVNET com um bloco CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="074fe-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="074fe-124">Criar uma sub-rede denominada Appgatewaysubnet que utiliza 10.0.0.0/28 como bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="074fe-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="074fe-125">Pesquisas de configuração adicional do gateway de aplicação Olá, incluindo o estado de funcionamento personalizado, os endereços do conjunto de back-end e regras adicionais são configurados após a configuração do gateway de aplicação Olá e não durante a implementação inicial.</span><span class="sxs-lookup"><span data-stu-id="074fe-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="074fe-126">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="074fe-126">Before you begin</span></span>

<span data-ttu-id="074fe-127">Gateway de aplicação do Azure requer a sua própria sub-rede.</span><span class="sxs-lookup"><span data-stu-id="074fe-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="074fe-128">Ao criar uma rede virtual, certifique-se de que deixe suficiente toohave de espaço de endereço várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="074fe-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="074fe-129">Depois de implementar uma sub-rede de tooa do gateway de aplicação, gateways de aplicação apenas adicionais podem ser adicionados toohello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="074fe-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="074fe-130">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="074fe-130">Log in tooAzure</span></span>

<span data-ttu-id="074fe-131">Abra Olá **linha de comandos do Microsoft Azure**e inicie sessão.</span><span class="sxs-lookup"><span data-stu-id="074fe-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="074fe-132">Também pode utilizar `az login` sem comutador Olá para início de sessão de dispositivo que necessita de introduzir um código no aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="074fe-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="074fe-133">Depois de escrever Olá anterior exemplo, é fornecido um código.</span><span class="sxs-lookup"><span data-stu-id="074fe-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="074fe-134">Navegue toohttps://aka.ms/devicelogin um processo de início de sessão do browser toocontinue Olá.</span><span class="sxs-lookup"><span data-stu-id="074fe-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![o início de sessão do cmd que mostra dispositivos][1]

<span data-ttu-id="074fe-136">No browser Olá, introduza o código de Olá que recebeu.</span><span class="sxs-lookup"><span data-stu-id="074fe-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="074fe-137">São tooa redirecionada-página sessão.</span><span class="sxs-lookup"><span data-stu-id="074fe-137">You are redirected tooa sign-in page.</span></span>

![código de tooenter do browser][2]

<span data-ttu-id="074fe-139">Assim que foi introduzido um código de Olá tem sessão iniciada, fechar Olá browser toocontinue com cenário Olá.</span><span class="sxs-lookup"><span data-stu-id="074fe-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![sessão iniciada com êxito][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="074fe-141">Criar grupo de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="074fe-141">Create hello resource group</span></span>

<span data-ttu-id="074fe-142">Antes de criar o gateway de aplicação Olá, o gateway de aplicação Olá toocontain é criado um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="074fe-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="074fe-143">seguinte Olá mostra comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="074fe-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="074fe-144">Criar gateway de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="074fe-144">Create hello application gateway</span></span>

<span data-ttu-id="074fe-145">endereços IP de Olá utilizados para o back-end de Olá são endereços IP de Olá para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="074fe-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="074fe-146">Estes valores podem ser ambos IPs privados numa rede virtual Olá, os ips públicos ou nomes de domínio totalmente qualificados para os servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="074fe-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="074fe-147">Olá exemplo seguinte cria um gateway de aplicação com as definições de configuração adicionais para definições de http, portas e regras.</span><span class="sxs-lookup"><span data-stu-id="074fe-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="074fe-148">Olá anterior exemplo mostra várias propriedades que não são necessárias durante a criação de Olá de um gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="074fe-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="074fe-149">Olá seguinte exemplo de código cria um gateway de aplicação com as informações de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="074fe-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="074fe-150">Para obter uma lista de parâmetros que podem ser fornecidos durante Olá de criação, execute os seguintes comandos: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="074fe-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="074fe-151">Este exemplo cria um gateway de aplicação básico com as predefinições para o serviço de escuta de Olá, conjunto back-end, as definições http de back-end e regras.</span><span class="sxs-lookup"><span data-stu-id="074fe-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="074fe-152">Pode modificar estas definições toosuit a implementação depois de aprovisionamento de Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="074fe-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="074fe-153">Se já tiver a sua aplicação web definida com o conjunto de back-end Olá no Olá precedente passos, uma vez criados, o balanceamento de carga é iniciada.</span><span class="sxs-lookup"><span data-stu-id="074fe-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="074fe-154">Obter nome de DNS de gateway de aplicação</span><span class="sxs-lookup"><span data-stu-id="074fe-154">Get application gateway DNS name</span></span>

<span data-ttu-id="074fe-155">Assim que for criado o gateway de Olá, o passo seguinte Olá é tooconfigure Olá front-end para comunicação.</span><span class="sxs-lookup"><span data-stu-id="074fe-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="074fe-156">Ao utilizar um IP público, o gateway de aplicação requer um nome DNS dinamicamente atribuído, que não é amigável.</span><span class="sxs-lookup"><span data-stu-id="074fe-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="074fe-157">os utilizadores finais de tooensure pode atingiu o gateway de aplicação Olá, um registo CNAME pode ser utilizado toopoint toohello ponto final público Olá do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="074fe-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="074fe-158">[Configurar um nome de domínio personalizado no Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="074fe-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="074fe-159">tooconfigure alias, obter detalhes do gateway de aplicação Olá e o respetivo nome IP/DNS associado com o gateway de aplicação do Olá PublicIPAddress elemento toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="074fe-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="074fe-160">nome DNS do gateway de aplicação Olá deve ser utilizado toocreate um registo CNAME, nome DNS de toothis de aplicações que pontos Olá dois web.</span><span class="sxs-lookup"><span data-stu-id="074fe-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="074fe-161">utilização de Olá de registos não é recomendada, uma vez que podem ser alterados Olá VIP no momento do reinício do gateway de aplicação.</span><span class="sxs-lookup"><span data-stu-id="074fe-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="074fe-162">Eliminar todos os recursos</span><span class="sxs-lookup"><span data-stu-id="074fe-162">Delete all resources</span></span>

<span data-ttu-id="074fe-163">toodelete todos os recursos criados neste artigo, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="074fe-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="074fe-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="074fe-164">Next steps</span></span>

<span data-ttu-id="074fe-165">Saiba como o estado de funcionamento personalizado toocreate sondas, visitando [criar uma sonda do Estado de funcionamento personalizado](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="074fe-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="074fe-166">Saiba como tooconfigure descarga de SSL e de desencriptação de SSL dispendiosa do tirar Olá desativado seus servidores web, visitando [configurar a descarga de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="074fe-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
