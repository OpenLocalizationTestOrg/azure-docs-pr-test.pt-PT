---
title: "Como tooconfigure encaminhamento (peering) para um circuito ExpressRoute: Azure: clássica | Microsoft Docs"
description: "Este artigo explica Olá passos para criar e aprovisionar Olá privado, público e peering da Microsoft de um circuito ExpressRoute. Este artigo mostra também como estado de Olá toocheck, atualizar ou eliminar peerings no seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="691b7-104">Criar e modificar o peering de um circuito de ExpressRoute (clássica)</span><span class="sxs-lookup"><span data-stu-id="691b7-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="691b7-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="691b7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="691b7-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="691b7-107">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="691b7-108">Vídeo - privada peering</span><span class="sxs-lookup"><span data-stu-id="691b7-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="691b7-109">Vídeo - peering público</span><span class="sxs-lookup"><span data-stu-id="691b7-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="691b7-110">Vídeo - peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="691b7-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="691b7-111">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="691b7-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="691b7-112">Este artigo explica-lhe Olá passos toocreate e gerir a configuração de encaminhamento para um circuito ExpressRoute com o PowerShell e Olá modelo de implementação clássica.</span><span class="sxs-lookup"><span data-stu-id="691b7-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="691b7-113">passos de Olá abaixo também irão mostrar como toocheck Olá Estado, atualizar, ou eliminar e retirar o aprovisionamento do peerings para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="691b7-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="691b7-114">**Acerca dos modelos de implementação do Azure**</span><span class="sxs-lookup"><span data-stu-id="691b7-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="691b7-115">Pré-requisitos da configuração</span><span class="sxs-lookup"><span data-stu-id="691b7-115">Configuration prerequisites</span></span>
* <span data-ttu-id="691b7-116">Terá a versão mais recente do Olá do Olá cmdlets do PowerShell de gestão de serviço do Azure (SM).</span><span class="sxs-lookup"><span data-stu-id="691b7-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="691b7-117">Para obter mais informações, consulte [introdução aos cmdlets do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="691b7-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="691b7-118">Certifique-se de que reviu Olá [pré-requisitos](expressroute-prerequisites.md) página Olá [requisitos de encaminhamento](expressroute-routing.md) página e Olá [fluxos de trabalho](expressroute-workflows.md) página antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="691b7-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="691b7-119">Deve ter um circuito ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="691b7-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="691b7-120">Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="691b7-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="691b7-121">Olá circuito ExpressRoute tem de ser num Estado aprovisionado e ativado para si toobe toorun capaz de Olá cmdlets descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="691b7-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="691b7-122">Estas instruções aplicam-se apenas toocircuits criados com fornecedores de serviços de oferta de serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="691b7-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="691b7-123">Se estiver a utilizar um fornecedor de serviço que oferece serviços geridos de Camada 3 (normalmente, um VPN de IP, como MPLS), o seu fornecedor de conectividade irá configurar e gerir encaminhamento por si.</span><span class="sxs-lookup"><span data-stu-id="691b7-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="691b7-124">Pode configurar um, dois ou todos os três peerings (Azure privado, Azure público e Microsoft) para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="691b7-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="691b7-125">Pode configurar peerings em qualquer ordem que escolha.</span><span class="sxs-lookup"><span data-stu-id="691b7-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="691b7-126">No entanto, tem de se certificar de que concluir configuração Olá cada peering, um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="691b7-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="691b7-127">Inicie sessão no tooyour conta do Azure e selecionar uma subscrição</span><span class="sxs-lookup"><span data-stu-id="691b7-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="691b7-128">Abra a consola do PowerShell com direitos elevados e ligue tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="691b7-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="691b7-129">Utilize Olá toohelp de exemplo, ligar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="691b7-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="691b7-130">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="691b7-131">Se tiver mais do que uma subscrição, selecione a subscrição de Olá que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="691b7-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="691b7-132">Em seguida, utilize Olá seguintes cmdlet tooadd tooPowerShell sua subscrição do Azure para o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="691b7-133">Peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-133">Azure private peering</span></span>
<span data-ttu-id="691b7-134">Esta secção fornece instruções sobre como toocreate, obter, atualizar e eliminar Olá configuração do peering privado do Azure para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="691b7-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="691b7-135">toocreate peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="691b7-136">**Importe o módulo do PowerShell de Olá para o ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="691b7-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="691b7-137">Tem de importar módulos do Azure e ExpressRoute Olá para a sessão do PowerShell Olá no toostart ordem utilizando cmdlets do ExpressRoute Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="691b7-138">Seguinte Olá executar comandos tooimport Olá do Azure e ExpressRoute os módulos para a sessão de PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="691b7-139">**Crie um circuito ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="691b7-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="691b7-140">Siga Olá instruções toocreate um [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao fornecedor de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="691b7-141">Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="691b7-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="691b7-142">Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="691b7-143">No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="691b7-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="691b7-144">**Verifique tooensure de circuito de ExpressRoute Olá que está aprovisionado.**</span><span class="sxs-lookup"><span data-stu-id="691b7-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="691b7-145">Verifique primeiro toosee se Olá circuito ExpressRoute está aprovisionado e também ativado.</span><span class="sxs-lookup"><span data-stu-id="691b7-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="691b7-146">Veja o exemplo de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="691b7-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="691b7-147">Certifique-se de que o circuito Olá mostra como aprovisionado e ativado.</span><span class="sxs-lookup"><span data-stu-id="691b7-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="691b7-148">Se não, funciona com a sua tooget do fornecedor de conectividade do Estado do circuito toohello necessário e o estado.</span><span class="sxs-lookup"><span data-stu-id="691b7-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="691b7-149">**Configure o peering privado do Azure para o circuito Olá.**</span><span class="sxs-lookup"><span data-stu-id="691b7-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="691b7-150">Certifique-se de que tem Olá seguintes itens antes de continuar com os passos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="691b7-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="691b7-151">Um /30 sub-rede para a ligação primária Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="691b7-152">Esta não pode fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="691b7-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="691b7-153">Um /30 sub-rede para a ligação secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="691b7-154">Esta não pode fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="691b7-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="691b7-155">Um tooestablish de ID de VLAN válido este peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="691b7-156">Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="691b7-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="691b7-157">Número AS para peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-157">AS number for peering.</span></span> <span data-ttu-id="691b7-158">Pode utilizar números AS de 2 e 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="691b7-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="691b7-159">Pode utilizar um número AS privado para este peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="691b7-160">Assegure que não está a utilizar 65515.</span><span class="sxs-lookup"><span data-stu-id="691b7-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="691b7-161">Um hash MD5 se optar por toouse um.</span><span class="sxs-lookup"><span data-stu-id="691b7-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="691b7-162">**Isto é opcional**.</span><span class="sxs-lookup"><span data-stu-id="691b7-162">**This is optional**.</span></span>
     
    <span data-ttu-id="691b7-163">Pode executar Olá seguir tooconfigure cmdlet peering privado do Azure para o seu circuito.</span><span class="sxs-lookup"><span data-stu-id="691b7-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="691b7-164">Novo AzureBGPPeering - AccessType privada - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100</span><span class="sxs-lookup"><span data-stu-id="691b7-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="691b7-165">Pode utilizar o cmdlet Olá abaixo se optar por toouse um hash MD5.</span><span class="sxs-lookup"><span data-stu-id="691b7-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="691b7-166">Novo AzureBGPPeering - AccessType privada - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="691b7-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="691b7-167">Assegure que especifica o seu número AS como ASN de peering, não cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="691b7-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="691b7-168">tooview detalhes de peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-168">tooview Azure private peering details</span></span>
<span data-ttu-id="691b7-169">Pode obter os detalhes de configuração utilizando o seguinte cmdlet de Olá</span><span class="sxs-lookup"><span data-stu-id="691b7-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="691b7-170">tooupdate configuração do peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="691b7-171">Pode atualizar qualquer parte da configuração de Olá utilizando Olá seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691b7-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="691b7-172">Exemplo de Olá abaixo, Olá ID de VLAN do circuito Olá está a ser atualizado de 100 too500.</span><span class="sxs-lookup"><span data-stu-id="691b7-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="691b7-173">toodelete peering privado do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-173">toodelete Azure private peering</span></span>
<span data-ttu-id="691b7-174">Pode remover a configuração de peering executando o seguinte cmdlet de Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="691b7-175">Tem de se certificar de que todas as redes virtuais são desassociadas do Olá circuito ExpressRoute antes de executar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691b7-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="691b7-176">Peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-176">Azure public peering</span></span>
<span data-ttu-id="691b7-177">Esta secção fornece instruções sobre como toocreate, obter, atualizar e eliminar Olá configuração do peering público do Azure para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="691b7-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="691b7-178">toocreate peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="691b7-179">**Importe o módulo do PowerShell de Olá para o ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="691b7-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="691b7-180">Tem de importar módulos do Azure e ExpressRoute Olá para a sessão do PowerShell Olá no toostart ordem utilizando cmdlets do ExpressRoute Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="691b7-181">Seguinte Olá executar comandos tooimport Olá do Azure e ExpressRoute os módulos para a sessão de PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="691b7-182">**Crie um circuito do ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="691b7-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="691b7-183">Siga Olá instruções toocreate um [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao fornecedor de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="691b7-184">Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering público do Azure.</span><span class="sxs-lookup"><span data-stu-id="691b7-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="691b7-185">Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="691b7-186">No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="691b7-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="691b7-187">**Verifique tooensure do circuito ExpressRoute que está aprovisionado**</span><span class="sxs-lookup"><span data-stu-id="691b7-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="691b7-188">Verifique primeiro toosee se Olá circuito ExpressRoute está aprovisionado e também ativado.</span><span class="sxs-lookup"><span data-stu-id="691b7-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="691b7-189">Veja o exemplo de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="691b7-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="691b7-190">Certifique-se de que o circuito Olá mostra como aprovisionado e ativado.</span><span class="sxs-lookup"><span data-stu-id="691b7-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="691b7-191">Se não, funciona com a sua tooget do fornecedor de conectividade do Estado do circuito toohello necessário e o estado.</span><span class="sxs-lookup"><span data-stu-id="691b7-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="691b7-192">**Configure o peering público do Azure para o circuito Olá**</span><span class="sxs-lookup"><span data-stu-id="691b7-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="691b7-193">Certifique-se de que tem Olá seguintes informações antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="691b7-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="691b7-194">Um /30 sub-rede para a ligação primária Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="691b7-195">Esta tem de ser um prefixo IPv4 válido.</span><span class="sxs-lookup"><span data-stu-id="691b7-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="691b7-196">Um /30 sub-rede para a ligação secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="691b7-197">Esta tem de ser um prefixo IPv4 válido.</span><span class="sxs-lookup"><span data-stu-id="691b7-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="691b7-198">Um tooestablish de ID de VLAN válido este peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="691b7-199">Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="691b7-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="691b7-200">Número AS para peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-200">AS number for peering.</span></span> <span data-ttu-id="691b7-201">Pode utilizar números AS de 2 e 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="691b7-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="691b7-202">Um hash MD5 se optar por toouse um.</span><span class="sxs-lookup"><span data-stu-id="691b7-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="691b7-203">**Isto é opcional**.</span><span class="sxs-lookup"><span data-stu-id="691b7-203">**This is optional**.</span></span>
     
    <span data-ttu-id="691b7-204">Pode executar Olá seguir tooconfigure cmdlet peering público do Azure para o seu circuito</span><span class="sxs-lookup"><span data-stu-id="691b7-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="691b7-205">Novo AzureBGPPeering - AccessType público - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200</span><span class="sxs-lookup"><span data-stu-id="691b7-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="691b7-206">Pode utilizar o cmdlet Olá abaixo se optar por toouse um hash MD5</span><span class="sxs-lookup"><span data-stu-id="691b7-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="691b7-207">Novo AzureBGPPeering - AccessType público - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="691b7-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="691b7-208">Assegure que especifica o seu número AS como ASN de peering e não cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="691b7-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="691b7-209">tooview detalhes de peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-209">tooview Azure public peering details</span></span>
<span data-ttu-id="691b7-210">Pode obter os detalhes de configuração utilizando o seguinte cmdlet de Olá</span><span class="sxs-lookup"><span data-stu-id="691b7-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="691b7-211">tooupdate configuração do peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="691b7-212">Pode atualizar qualquer parte da configuração de Olá utilizando o seguinte cmdlet de Olá</span><span class="sxs-lookup"><span data-stu-id="691b7-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="691b7-213">Olá ID de VLAN do circuito Olá está a ser atualizado de 200 too600 no Olá acima exemplo.</span><span class="sxs-lookup"><span data-stu-id="691b7-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="691b7-214">toodelete peering público do Azure</span><span class="sxs-lookup"><span data-stu-id="691b7-214">toodelete Azure public peering</span></span>
<span data-ttu-id="691b7-215">Pode remover a configuração de peering executando o seguinte cmdlet de Olá</span><span class="sxs-lookup"><span data-stu-id="691b7-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="691b7-216">Peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="691b7-216">Microsoft peering</span></span>
<span data-ttu-id="691b7-217">Esta secção fornece instruções sobre como toocreate, obter, atualizar e eliminar Olá configuração peering da Microsoft para um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="691b7-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="691b7-218">toocreate peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="691b7-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="691b7-219">**Importe o módulo do PowerShell de Olá para o ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="691b7-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="691b7-220">Tem de importar módulos do Azure e ExpressRoute Olá para a sessão do PowerShell Olá no toostart ordem utilizando cmdlets do ExpressRoute Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="691b7-221">Seguinte Olá executar comandos tooimport Olá do Azure e ExpressRoute os módulos para a sessão de PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="691b7-222">**Crie um circuito do ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="691b7-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="691b7-223">Siga Olá instruções toocreate um [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao fornecedor de conectividade Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="691b7-224">Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="691b7-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="691b7-225">Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="691b7-226">No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="691b7-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="691b7-227">**Verifique tooensure do circuito ExpressRoute que está aprovisionado**</span><span class="sxs-lookup"><span data-stu-id="691b7-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="691b7-228">Verifique primeiro toosee se Olá circuito do ExpressRoute estiver num Estado aprovisionado e ativado.</span><span class="sxs-lookup"><span data-stu-id="691b7-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="691b7-229">Certifique-se de que o circuito Olá mostra como aprovisionado e ativado.</span><span class="sxs-lookup"><span data-stu-id="691b7-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="691b7-230">Se não, funciona com a sua tooget do fornecedor de conectividade do Estado do circuito toohello necessário e o estado.</span><span class="sxs-lookup"><span data-stu-id="691b7-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="691b7-231">**Configurar o peering da Microsoft para o circuito Olá**</span><span class="sxs-lookup"><span data-stu-id="691b7-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="691b7-232">Certifique-se de que tem Olá seguintes informações antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="691b7-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="691b7-233">Um /30 sub-rede para a ligação primária Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="691b7-234">Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.</span><span class="sxs-lookup"><span data-stu-id="691b7-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="691b7-235">Um /30 sub-rede para a ligação secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="691b7-236">Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.</span><span class="sxs-lookup"><span data-stu-id="691b7-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="691b7-237">Um tooestablish de ID de VLAN válido este peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="691b7-238">Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="691b7-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="691b7-239">Número AS para peering.</span><span class="sxs-lookup"><span data-stu-id="691b7-239">AS number for peering.</span></span> <span data-ttu-id="691b7-240">Pode utilizar números AS de 2 e 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="691b7-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="691b7-241">Prefixos anunciados: tem de fornecer uma lista de todos os prefixos planear tooadvertise através de sessão de BGP Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="691b7-242">São aceites apenas prefixos de endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="691b7-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="691b7-243">Pode enviar uma lista separada por vírgulas se planear toosend um conjunto de prefixos.</span><span class="sxs-lookup"><span data-stu-id="691b7-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="691b7-244">Estes prefixos têm de ser registado tooyou num RIR / TIR.</span><span class="sxs-lookup"><span data-stu-id="691b7-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="691b7-245">Cliente ASN: Se estiver a anunciar prefixos que não são registado toohello número AS de peering, pode especificar Olá como número toowhich que estão registados.</span><span class="sxs-lookup"><span data-stu-id="691b7-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="691b7-246">**Isto é opcional**.</span><span class="sxs-lookup"><span data-stu-id="691b7-246">**This is optional**.</span></span>
   * <span data-ttu-id="691b7-247">Nome do registo de encaminhamento: Pode especificar Olá RIR / IRR em relação a que Olá como número e prefixos são registados.</span><span class="sxs-lookup"><span data-stu-id="691b7-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="691b7-248">Um hash MD5, se escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="691b7-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="691b7-249">**Isto é opcional.**</span><span class="sxs-lookup"><span data-stu-id="691b7-249">**This is optional.**</span></span>
     
    <span data-ttu-id="691b7-250">Pode executar Olá seguir pering de Microsoft tooconfigure cmdlet para o seu circuito</span><span class="sxs-lookup"><span data-stu-id="691b7-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="691b7-251">Novo AzureBGPPeering - AccessType Microsoft - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - VlanId 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes "123.0.0.0/30" - RoutingRegistryName "ARIN" - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="691b7-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="691b7-252">Detalhes do tooview Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="691b7-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="691b7-253">Pode obter os detalhes de configuração com Olá seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691b7-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="691b7-254">configuração do peering da Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="691b7-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="691b7-255">Pode atualizar qualquer parte da configuração de Olá utilizando Olá seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691b7-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="691b7-256">toodelete peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="691b7-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="691b7-257">Pode remover a configuração de peering executando o seguinte cmdlet de Olá.</span><span class="sxs-lookup"><span data-stu-id="691b7-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="691b7-258">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="691b7-258">Next steps</span></span>
<span data-ttu-id="691b7-259">Em seguida, [ligação tooan uma VNet circuito ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="691b7-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="691b7-260">Para obter mais informações sobre fluxos de trabalho, consulte [fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="691b7-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="691b7-261">Para obter mais informações sobre peering do circuito, veja [Circuitos ExpressRoute e domínios de encaminhamento](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="691b7-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

