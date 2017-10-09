---
title: "verificar o tráfego de aaaverify com o fluxo de IP de observador de rede do Azure - PowerShell | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual for permitido ou negado utilizando o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="2ffdd-103">Verifique se o tráfego é permitido ou negado tooor de uma VM com o fluxo IP Certifique-se de um componente do observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="2ffdd-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2ffdd-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2ffdd-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="2ffdd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ffdd-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="2ffdd-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2ffdd-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="2ffdd-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2ffdd-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="2ffdd-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="2ffdd-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="2ffdd-109">Verificar o fluxo IP é uma funcionalidade do observador de rede que permite-lhe tooverify se o tráfego é permitido tooor de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="2ffdd-110">Este cenário é útil tooget um estado atual da se uma máquina virtual pode comunicar com um recurso externo tooan ou back-end.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="2ffdd-111">Fluxo IP verificar tooverify utilizada se as regras do grupo de segurança de rede (NSG) estão configuradas corretamente e resolver problemas relacionados com fluxos que estão a ser bloqueados por regras NSG.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="2ffdd-112">Outra razão para utilizar o IP fluxo verifique tráfego tooensure que pretende bloqueadas que está a ser bloqueado corretamente por Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2ffdd-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2ffdd-113">Before you begin</span></span>

<span data-ttu-id="2ffdd-114">Este cenário pressupõe que já tiver seguido os passos de Olá no [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="2ffdd-115">cenário de Olá também parte do princípio de que um grupo de recursos com uma máquina virtual válida existe toobe utilizado.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2ffdd-116">Cenário</span><span class="sxs-lookup"><span data-stu-id="2ffdd-116">Scenario</span></span>

<span data-ttu-id="2ffdd-117">Este fluxo IP do cenário utiliza verificar tooverify se uma máquina virtual pode falar tooa conhecidos endereço IP do Bing.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="2ffdd-118">Se for negado o tráfego de Olá, devolve regra de segurança de Olá que está a negar esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="2ffdd-119">mais informações sobre o fluxo IP verificar, visite toolearn [fluxo IP verificar descrição geral](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2ffdd-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2ffdd-120">Obter o observador de rede</span><span class="sxs-lookup"><span data-stu-id="2ffdd-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="2ffdd-121">Step-by-Olá primeiro passo é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2ffdd-122">Olá `$networkWatcher` variável ser passada toohello IP fluxo verificar cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="2ffdd-123">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="2ffdd-123">Get a VM</span></span>

<span data-ttu-id="2ffdd-124">Fluxo IP verifique tooor de tráfego de testes de um endereço IP no tooor máquina virtual de um destino remoto.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="2ffdd-125">Um Id de uma máquina virtual é necessário para Olá cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="2ffdd-126">Se já souber o ID Olá Olá toouse de máquina virtual, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="2ffdd-127">Obter Olá NICS</span><span class="sxs-lookup"><span data-stu-id="2ffdd-127">Get hello NICS</span></span>

<span data-ttu-id="2ffdd-128">endereço IP Olá de uma NIC na máquina virtual de Olá for necessária, neste exemplo, obtemos Olá NICs numa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="2ffdd-129">Se já conhece o IP de Olá endereço que pretende tootest numa máquina virtual de Olá, pode ignorar este passo.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="2ffdd-130">Certifique-se de execução de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="2ffdd-130">Run IP flow verify</span></span>

<span data-ttu-id="2ffdd-131">Agora que temos informações Olá necessário toorun Olá cmdlet, iremos executar Olá `Test-AzureRmNetworkWatcherIPFlow` tráfego do cmdlet tootest Olá.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="2ffdd-132">Neste exemplo, estamos a utilizar endereço IP primeiro Olá numa NIC primeiro Olá em</span><span class="sxs-lookup"><span data-stu-id="2ffdd-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="2ffdd-133">Fluxo IP verificar requer que o recurso VM Olá está alocado toorun.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="2ffdd-134">Reveja os resultados</span><span class="sxs-lookup"><span data-stu-id="2ffdd-134">Review Results</span></span>

<span data-ttu-id="2ffdd-135">Após a execução `Test-AzureRmNetworkWatcherIPFlow` Olá resultados são devolvidos, hello exemplo seguinte é resultados Olá devolvidos de Olá precedente passo.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="2ffdd-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2ffdd-136">Next steps</span></span>

<span data-ttu-id="2ffdd-137">Se o tráfego está a ser bloqueado e não deve ser, consulte [gerir grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack baixo Olá rede segurança e de grupo de regras de segurança que estão definidos.</span><span class="sxs-lookup"><span data-stu-id="2ffdd-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













