---
title: "aaaAccess e segurança nos modelos do Azure para VMs com Linux | Microsoft Docs"
description: "Tutorial do DotNet núcleos de Máquina Virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="400d0-103">Acesso e segurança de modelos Azure Resource Manager para VMs com Linux</span><span class="sxs-lookup"><span data-stu-id="400d0-103">Access and security in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="400d0-104">Aplicações alojadas no Azure necessidade provável toobe acesso através de Olá internet ou uma VPN / ligação Expressroute com o Azure.</span><span class="sxs-lookup"><span data-stu-id="400d0-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="400d0-105">Exemplo de aplicação do Olá loja de música, Olá web site é disponibilizada no Olá internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="400d0-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="400d0-106">Com acesso estabelecido, devem ser protegidos ligações toohello aplicação e acesso toohello recursos da máquina virtual próprios.</span><span class="sxs-lookup"><span data-stu-id="400d0-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="400d0-107">Esta segurança de acesso é fornecida com um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="400d0-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="400d0-108">Este documento fornece detalhes sobre como Olá aplicação da loja de música está protegida no modelo de Gestor de recursos do Azure de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="400d0-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="400d0-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="400d0-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="400d0-110">Para uma experiência otimizada Olá, pré-implemente uma instância de trabalho, juntamente com o modelo do Azure Resource Manager Olá e Olá solução tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="400d0-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="400d0-111">modelo completo Olá pode ser encontrado aqui – [a implementação da loja de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="400d0-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="public-ip-address"></a><span data-ttu-id="400d0-112">Endereço IP público</span><span class="sxs-lookup"><span data-stu-id="400d0-112">Public IP Address</span></span>
<span data-ttu-id="400d0-113">tooprovide acesso público tooan recursos do Azure, um recurso de endereço IP público pode ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="400d0-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="400d0-114">Endereço IP público pode ser configurado com um endereço IP estático ou dinâmico.</span><span class="sxs-lookup"><span data-stu-id="400d0-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="400d0-115">Se é utilizado um endereço dinâmico e a máquina virtual de Olá está parada e desalocada, endereços de Olá é removido.</span><span class="sxs-lookup"><span data-stu-id="400d0-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="400d0-116">Quando a máquina de Olá é iniciada novamente, poderá atribuído um endereço IP público diferentes.</span><span class="sxs-lookup"><span data-stu-id="400d0-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="400d0-117">tooprevent um IP endereços de alteração, pode ser utilizado um endereço IP reservado.</span><span class="sxs-lookup"><span data-stu-id="400d0-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="400d0-118">Um endereço IP público pode ser adicionado o modelo do Azure Resource Manager tooan utilizando Olá Visual Studio Adicionar Assistente de novos recursos, ou por inserir um JSON válido de um modelo.</span><span class="sxs-lookup"><span data-stu-id="400d0-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="400d0-119">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span><span class="sxs-lookup"><span data-stu-id="400d0-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="400d0-120">Um endereço IP público pode ser associado com um adaptador de rede Virtual ou um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="400d0-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="400d0-121">Neste exemplo, uma vez Olá Web site da loja de música é balanceamento de carga em várias máquinas de virtuais, Olá endereço IP público é anexado toohello Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="400d0-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="400d0-122">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [associação de endereço IP público com Balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="400d0-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="400d0-123">Olá endereço IP público, como visto a partir de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="400d0-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="400d0-124">Repare que o endereço IP público Olá é Balanceador de carga tooa associados e não uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="400d0-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="400d0-125">Balanceadores de carga de rede estão descritos no documento seguinte do Olá desta série.</span><span class="sxs-lookup"><span data-stu-id="400d0-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Endereço IP público](./media/dotnet-core-3-access-security/pubip.png)

<span data-ttu-id="400d0-127">Para obter mais informações sobre os endereços IP públicos do Azure, consulte [endereços IP no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="400d0-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="400d0-128">Grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="400d0-128">Network Security Group</span></span>
<span data-ttu-id="400d0-129">Depois do acesso foi estabelecida tooAzure recursos, este acesso deve ser limitado.</span><span class="sxs-lookup"><span data-stu-id="400d0-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="400d0-130">Máquinas virtuais do Azure, proteger o acesso é realizado através de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="400d0-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="400d0-131">Exemplo de aplicação do arquivo de música Olá, todas as máquinas de toohello acesso é restrito, exceto para através da porta 80 para acesso http e a porta 22 para SSH acesso.</span><span class="sxs-lookup"><span data-stu-id="400d0-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 22 for SSH access.</span></span> <span data-ttu-id="400d0-132">Um grupo de segurança de rede podem ser adicionado modelo do Azure Resource Manager tooan utilizando Olá Visual Studio Adicionar Assistente de novos recursos, ou por inserir um JSON válido de um modelo.</span><span class="sxs-lookup"><span data-stu-id="400d0-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="400d0-133">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [grupo de segurança de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span><span class="sxs-lookup"><span data-stu-id="400d0-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
}
```

<span data-ttu-id="400d0-134">Neste exemplo, o grupo de segurança de rede de Olá está associado ao objeto de sub-rede Olá declarado no recurso de rede Virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="400d0-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="400d0-135">Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [associação de grupo de segurança de rede com a rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span><span class="sxs-lookup"><span data-stu-id="400d0-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
```

<span data-ttu-id="400d0-136">Eis o grupo de segurança de rede que Olá aspeto do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="400d0-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="400d0-137">Tenha em atenção que pode ser associar um NSG com uma interface de sub-rede e / ou rede.</span><span class="sxs-lookup"><span data-stu-id="400d0-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="400d0-138">Neste caso, Olá NSG é associado tooa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="400d0-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="400d0-139">Nesta configuração, hello regras de entrada aplicam tooall máquinas virtuais ligadas toohello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="400d0-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Grupo de segurança de rede](./media/dotnet-core-3-access-security/nsg.png)

<span data-ttu-id="400d0-141">Para obter informações aprofundadas sobre grupos de segurança de rede, consulte [que é um grupo de segurança de rede](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="400d0-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="400d0-142">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="400d0-142">Next step</span></span>
<hr>

[<span data-ttu-id="400d0-143">Passo 3 - disponibilidade e dimensionamento em modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="400d0-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

