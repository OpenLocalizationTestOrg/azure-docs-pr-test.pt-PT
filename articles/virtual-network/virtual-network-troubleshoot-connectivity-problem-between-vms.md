---
title: problemas de conectividade aaaTroubleshooting entre as VMs do Azure | Microsoft Docs
description: "Saiba como tooTroubleshoot Olá problemas de conectividade entre as VMs do Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="adfe8-103">Resolução de problemas de conectividade entre as VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="adfe8-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="adfe8-104">Podem ocorrer problemas de conectividade entre as VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="adfe8-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="adfe8-105">Este artigo fornece a resolução de problemas de passos toohelp resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="adfe8-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="adfe8-106">Sintoma</span><span class="sxs-lookup"><span data-stu-id="adfe8-106">Symptom</span></span>

<span data-ttu-id="adfe8-107">VM do Azure não consegue ligar tooanother VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="adfe8-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="adfe8-108">Orientação na resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="adfe8-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="adfe8-109">Verifique se a NIC está configurada incorretamente</span><span class="sxs-lookup"><span data-stu-id="adfe8-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="adfe8-110">Verifique se o tráfego de rede é bloqueado por NSG ou UDR</span><span class="sxs-lookup"><span data-stu-id="adfe8-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="adfe8-111">Verifique se o tráfego de rede é bloqueado pela firewall da VM</span><span class="sxs-lookup"><span data-stu-id="adfe8-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="adfe8-112">Verifique se VM aplicação ou serviço está a escutar na porta Olá</span><span class="sxs-lookup"><span data-stu-id="adfe8-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="adfe8-113">Verifique se o problema de Olá é causado por realizar o SNAT</span><span class="sxs-lookup"><span data-stu-id="adfe8-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="adfe8-114">Verifique se o tráfego está bloqueado por ACLs para Olá VMS clássicas</span><span class="sxs-lookup"><span data-stu-id="adfe8-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="adfe8-115">Verifique se o ponto final de Olá é criado para Olá VMS clássicas</span><span class="sxs-lookup"><span data-stu-id="adfe8-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="adfe8-116">Não é possível tooconnect tooa partilha de rede VM</span><span class="sxs-lookup"><span data-stu-id="adfe8-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="adfe8-117">Conectividade inter-Vnet</span><span class="sxs-lookup"><span data-stu-id="adfe8-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="adfe8-118">Passos de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="adfe8-118">Troubleshooting steps</span></span>

<span data-ttu-id="adfe8-119">Siga estes problema de Olá tootroubleshoot passos.</span><span class="sxs-lookup"><span data-stu-id="adfe8-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="adfe8-120">Verifique se o problema de Olá resolvido depois de cada passo.</span><span class="sxs-lookup"><span data-stu-id="adfe8-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="adfe8-121">Passo 1: Verificar se a NIC está configurada incorretamente</span><span class="sxs-lookup"><span data-stu-id="adfe8-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="adfe8-122">Siga [como tooreset interface de rede para a VM do Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="adfe8-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="adfe8-123">Se o problema de Olá ocorrer depois de modificar a interface de rede Olá (NIC), siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="adfe8-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="adfe8-124">**VMs de Mulit NIC**</span><span class="sxs-lookup"><span data-stu-id="adfe8-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="adfe8-125">Adicionar uma NIC.</span><span class="sxs-lookup"><span data-stu-id="adfe8-125">Add a NIC.</span></span>
2. <span data-ttu-id="adfe8-126">Corrigir problemas de Olá no Olá incorreto NIC ou remover incorreto NIC.</span><span class="sxs-lookup"><span data-stu-id="adfe8-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="adfe8-127">Em seguida, readd Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="adfe8-127">Then readd hello NIC.</span></span>

<span data-ttu-id="adfe8-128">Para obter mais informações, consulte [tooor de interfaces de rede de adicionar, remover máquinas virtuais](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="adfe8-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="adfe8-129">**VM NIC único**</span><span class="sxs-lookup"><span data-stu-id="adfe8-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="adfe8-130">Reimplementar a VM do Windows</span><span class="sxs-lookup"><span data-stu-id="adfe8-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="adfe8-131">Reimplementar a VM com Linux</span><span class="sxs-lookup"><span data-stu-id="adfe8-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="adfe8-132">Passo 2: Verificar se o tráfego de rede é bloqueado por NSG ou UDR</span><span class="sxs-lookup"><span data-stu-id="adfe8-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="adfe8-133">Utilizar [verificar do fluxo de rede do observador do IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo registo](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se existir um grupo de segurança de rede ou as rotas definidas pelo utilizador que está a interferir com o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="adfe8-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="adfe8-134">Passo 3: Verificar se o tráfego de rede é bloqueado pela firewall da VM</span><span class="sxs-lookup"><span data-stu-id="adfe8-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="adfe8-135">Desative a firewall Olá e, em seguida, testar o resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="adfe8-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="adfe8-136">Se o problema de Olá for resolvido, validar as definições de Olá na firewall de Olá e volte a ativar.</span><span class="sxs-lookup"><span data-stu-id="adfe8-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="adfe8-137">Passo 4: Verificar se VM aplicação ou serviço está a escutar na porta Olá</span><span class="sxs-lookup"><span data-stu-id="adfe8-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="adfe8-138">Pode utilizar um Olá os seguintes métodos toocheck se VM aplicação ou serviço está a escutar na porta Olá</span><span class="sxs-lookup"><span data-stu-id="adfe8-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="adfe8-139">Olá execute os seguintes comandos toocheck se Olá servidor está a escutar nessa porta.</span><span class="sxs-lookup"><span data-stu-id="adfe8-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="adfe8-140">**VM do Windows**</span><span class="sxs-lookup"><span data-stu-id="adfe8-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="adfe8-141">**VM do Linux**</span><span class="sxs-lookup"><span data-stu-id="adfe8-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="adfe8-142">Executar Olá **Telnet** comando no Olá porta do VM tooitself tootest Olá.</span><span class="sxs-lookup"><span data-stu-id="adfe8-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="adfe8-143">Se Olá teste falhar, aplicação ou serviço não é toolisten configurado na porta Olá.</span><span class="sxs-lookup"><span data-stu-id="adfe8-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="adfe8-144">Passo 5: Verificar se o problema de Olá é causado por realizar o SNAT</span><span class="sxs-lookup"><span data-stu-id="adfe8-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="adfe8-145">Em alguns cenários, hello VM é colocada atrás de uma solução de balanceamento de carga que tem uma dependência de recursos fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="adfe8-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="adfe8-146">Nestes cenários, se surgirem problemas de ligação intermitente, Olá problema poderá ser causado pelo [esgotamento de porta de realizar o SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="adfe8-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="adfe8-147">problema de Olá tooresolve, criar um VIP (ou ILPIP para clássico) para cada VM que está por trás do Balanceador de carga Olá e proteger com o NSG ou ACL.</span><span class="sxs-lookup"><span data-stu-id="adfe8-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="adfe8-148">Passo 6: Verifique se o tráfego está bloqueado por ACLs para Olá VMS clássicas</span><span class="sxs-lookup"><span data-stu-id="adfe8-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="adfe8-149">Uma ACL fornece Olá capacidade tooselectively permitir ou negar o tráfego para um ponto final da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="adfe8-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="adfe8-150">Para obter mais informações, consulte [gerir Olá ACL num ponto final](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="adfe8-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="adfe8-151">Passo 7: Verifique se o ponto final de Olá é criado para Olá VMS clássicas</span><span class="sxs-lookup"><span data-stu-id="adfe8-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="adfe8-152">Todas as VMs que criar no Azure utilizando o modelo de implementação clássica Olá automaticamente comunicar através de um canal de rede privada com outras máquinas virtuais na Olá que mesma rede virtual ou serviço da nuvem.</span><span class="sxs-lookup"><span data-stu-id="adfe8-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="adfe8-153">No entanto, os computadores em outras redes virtuais requerem pontos finais toodirect Olá rede entrada tráfego tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="adfe8-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="adfe8-154">Para obter mais informações, consulte [como tooset dos pontos finais](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="adfe8-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="adfe8-155">Passo 8: Partilha de rede VM não é possível tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="adfe8-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="adfe8-156">Se não é possível tooconnect tooa partilha de rede VM, problema Olá pode dever-se indisponível NICs em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="adfe8-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="adfe8-157">toodelete Olá NICs indisponíveis, consulte [como toodelete Olá NICs indisponíveis](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="adfe8-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="adfe8-158">Passo 9: Inter-vnet conectividade</span><span class="sxs-lookup"><span data-stu-id="adfe8-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="adfe8-159">Utilizar [verificar do fluxo de rede do observador do IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo registo](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se existir um grupo de segurança de rede ou as rotas definidas pelo utilizador que está a interferir com o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="adfe8-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="adfe8-160">Também pode validar a configuração do Inter-Vnet [aqui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="adfe8-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="adfe8-161">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="adfe8-161">Need help?</span></span> <span data-ttu-id="adfe8-162">Contacte o suporte.</span><span class="sxs-lookup"><span data-stu-id="adfe8-162">Contact support.</span></span>
<span data-ttu-id="adfe8-163">Se ainda precisar de ajuda, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="adfe8-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
