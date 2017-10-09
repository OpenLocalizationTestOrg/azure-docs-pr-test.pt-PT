---
title: "tráfego de aaaVerify com Azure rede observador IP fluxo verifique - CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual for permitido ou negado utilizando a CLI do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="54397-103">Verifique se o tráfego é permitido ou negado tooor de uma VM com o IP fluxo Certifique-se um componente do observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="54397-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="54397-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="54397-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="54397-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54397-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="54397-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="54397-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="54397-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="54397-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="54397-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="54397-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="54397-109">Fluxo de IP verificar é uma funcionalidade do observador de rede que permite-lhe tooverify se o tráfego é permitido tooor de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="54397-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="54397-110">Este cenário é útil tooget um estado atual da se uma máquina virtual pode comunicar com um recurso externo tooan ou back-end.</span><span class="sxs-lookup"><span data-stu-id="54397-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="54397-111">Fluxo IP verificar tooverify utilizada se as regras do grupo de segurança de rede (NSG) estão configuradas corretamente e resolver problemas relacionados com fluxos que estão a ser bloqueados por regras NSG.</span><span class="sxs-lookup"><span data-stu-id="54397-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="54397-112">Outra razão para utilizar o IP fluxo verifique tráfego tooensure que pretende bloqueadas que está a ser bloqueado corretamente por Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="54397-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="54397-113">Este artigo utiliza a nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá, Azure CLI 2.0, que está disponível para o Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="54397-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="54397-114">Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="54397-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="54397-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="54397-115">Before you begin</span></span>

<span data-ttu-id="54397-116">Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="54397-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="54397-117">cenário de Olá também parte do princípio de que um grupo de recursos com uma máquina virtual válida existe toobe utilizado.</span><span class="sxs-lookup"><span data-stu-id="54397-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="54397-118">Cenário</span><span class="sxs-lookup"><span data-stu-id="54397-118">Scenario</span></span>

<span data-ttu-id="54397-119">Este cenário utiliza tooverify IP fluxo verificar se uma máquina virtual pode falar tooa conhecidos endereço IP do Bing.</span><span class="sxs-lookup"><span data-stu-id="54397-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="54397-120">Se for negado o tráfego de Olá, devolve regra de segurança de Olá que está a negar esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="54397-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="54397-121">toolearn mais informações sobre o fluxo verificar IP, visite [IP fluxo Certifique-se de descrição geral](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="54397-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="54397-122">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="54397-122">Get a VM</span></span>

<span data-ttu-id="54397-123">Fluxo IP verifique tooor de tráfego de testes de um endereço IP no tooor máquina virtual de um destino remoto.</span><span class="sxs-lookup"><span data-stu-id="54397-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="54397-124">Um Id de uma máquina virtual é necessário para Olá cmdlet.</span><span class="sxs-lookup"><span data-stu-id="54397-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="54397-125">Se já souber o ID Olá Olá toouse de máquina virtual, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="54397-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="54397-126">Obter Olá NICS</span><span class="sxs-lookup"><span data-stu-id="54397-126">Get hello NICS</span></span>

<span data-ttu-id="54397-127">endereço IP Olá de uma NIC na máquina virtual de Olá for necessária, neste exemplo, obtemos Olá NICs numa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="54397-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="54397-128">Se já conhece o IP de Olá endereço que pretende tootest numa máquina virtual de Olá, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="54397-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="54397-129">Certifique-se de execução de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="54397-129">Run IP flow verify</span></span>

<span data-ttu-id="54397-130">Agora que temos informações Olá necessário toorun Olá cmdlet, iremos executar Olá `az network watcher test-ip-flow` tráfego do cmdlet tootest Olá.</span><span class="sxs-lookup"><span data-stu-id="54397-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="54397-131">Neste exemplo, estamos a utilizar endereço IP primeiro Olá numa NIC primeiro Olá em</span><span class="sxs-lookup"><span data-stu-id="54397-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="54397-132">Fluxo de IP verificar requer que o recurso VM Olá está alocado toorun.</span><span class="sxs-lookup"><span data-stu-id="54397-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="54397-133">Reveja os resultados</span><span class="sxs-lookup"><span data-stu-id="54397-133">Review Results</span></span>

<span data-ttu-id="54397-134">Após a execução `az network watcher test-ip-flow` Olá resultados são devolvidos, hello exemplo seguinte é resultados Olá devolvidos de Olá precedente passo.</span><span class="sxs-lookup"><span data-stu-id="54397-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="54397-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="54397-135">Next steps</span></span>

<span data-ttu-id="54397-136">Se o tráfego está a ser bloqueado e não deve ser, consulte [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que estão definidos.</span><span class="sxs-lookup"><span data-stu-id="54397-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="54397-137">Saiba tooaudit as definições de NSG, visitando [auditoria de segurança de rede grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="54397-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
