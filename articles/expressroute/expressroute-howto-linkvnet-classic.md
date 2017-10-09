---
title: "Ligar uma rede virtual de tooan circuito do ExpressRoute: PowerShell: clássico: Azure | Microsoft Docs"
description: "Este documento fornece uma descrição geral de como toolink virtual redes (VNets) tooExpressRoute circuitos utilizando o modelo de implementação clássica Olá e o PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="dfa61-103">Ligar um circuito de ExpressRoute de tooan de rede virtual com o PowerShell (clássica)</span><span class="sxs-lookup"><span data-stu-id="dfa61-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfa61-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dfa61-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="dfa61-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfa61-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="dfa61-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dfa61-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="dfa61-107">Vídeo - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dfa61-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="dfa61-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="dfa61-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="dfa61-109">Este artigo ajuda-o ligação circuitos do ExpressRoute redes virtuais (VNets) tooAzure utilizando o modelo de implementação clássica Olá e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfa61-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="dfa61-110">Redes virtuais podem ser na Olá mesma subscrição ou pode fazer parte de outra subscrição.</span><span class="sxs-lookup"><span data-stu-id="dfa61-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="dfa61-111">**Acerca dos modelos de implementação do Azure**</span><span class="sxs-lookup"><span data-stu-id="dfa61-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="dfa61-112">Pré-requisitos da configuração</span><span class="sxs-lookup"><span data-stu-id="dfa61-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="dfa61-113">Tem a versão mais recente do Olá de módulos do Azure PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="dfa61-114">Pode transferir módulos do PowerShell mais recentes Olá da Olá secção PowerShell Olá [página de transferências do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dfa61-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="dfa61-115">Siga as instruções de Olá em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter orientações passo a passo sobre como tooconfigure os módulos do PowerShell do Azure do computador toouse Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="dfa61-116">Terá de tooreview Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de encaminhamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="dfa61-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="dfa61-117">Deve ter um circuito ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="dfa61-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="dfa61-118">Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) e solicite ao seu fornecedor de conectividade ativar circuito Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="dfa61-119">Certifique-se de que tem o peering privado do Azure configurada para o seu circuito.</span><span class="sxs-lookup"><span data-stu-id="dfa61-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="dfa61-120">Consulte Olá [configurar encaminhamento](expressroute-howto-routing-classic.md) artigo para obter instruções de encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="dfa61-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="dfa61-121">Certifique-se de que o peering privado do Azure está configurado e peering de BGP Olá entre a rede e a Microsoft está a funcionar, de modo a que pode ativar a conetividade de ponto a ponto.</span><span class="sxs-lookup"><span data-stu-id="dfa61-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="dfa61-122">Tem de ter uma rede virtual e um gateway de rede virtual criada e totalmente aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="dfa61-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="dfa61-123">Siga as instruções de Olá demasiado[configurar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="dfa61-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="dfa61-124">Pode ligar a cópia de segurança too10 redes virtuais tooan circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dfa61-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="dfa61-125">Todas as redes virtuais tem de constar Olá mesma região geopolítica.</span><span class="sxs-lookup"><span data-stu-id="dfa61-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="dfa61-126">Pode associar um grande número de redes virtuais tooyour circuito ExpressRoute ou ligar redes virtuais que se encontrem noutras regiões geopolíticas, se tiver ativado o suplemento premium do ExpressRoute de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="dfa61-127">Verifique Olá [FAQ](expressroute-faqs.md) para obter mais detalhes sobre o suplemento do Olá premium.</span><span class="sxs-lookup"><span data-stu-id="dfa61-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="dfa61-128">Ligar uma rede virtual no Olá mesmo circuito tooa de subscrição</span><span class="sxs-lookup"><span data-stu-id="dfa61-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="dfa61-129">Pode ligar uma rede virtual de tooan circuito ExpressRoute utilizando o seguinte cmdlet de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="dfa61-130">Certifique-se de que gateway de rede virtual Olá é criado e está pronta para a ligação antes de executar o cmdlet Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="dfa61-131">Ligar uma rede virtual no circuito de tooa subscrição diferente</span><span class="sxs-lookup"><span data-stu-id="dfa61-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="dfa61-132">Pode partilhar um circuito ExpressRoute entre várias subscrições.</span><span class="sxs-lookup"><span data-stu-id="dfa61-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="dfa61-133">Olá figura a seguir mostra um simples schematic de funciona como partilha para circuitos do ExpressRoute entre várias subscrições.</span><span class="sxs-lookup"><span data-stu-id="dfa61-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="dfa61-134">Cada uma das nuvens mais pequenas de Olá na nuvem grande Olá é utilizado toorepresent subscrições que pertencem os departamentos de toodifferent dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="dfa61-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="dfa61-135">Cada um dos departamentos de Olá dentro da organização Olá pode utilizar as seus próprios subscrição para implementar os seus serviços - mas departamentos Olá pode partilhar uma única ExpressRoute circuito tooconnect back tooyour rede no local.</span><span class="sxs-lookup"><span data-stu-id="dfa61-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="dfa61-136">Um único departamento (neste exemplo: IT) pode ter o circuito de ExpressRoute Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="dfa61-137">Outras subscrições dentro da organização Olá podem utilizar o circuito de ExpressRoute Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="dfa61-138">Custos de largura de banda e conectividade de circuito dedicado de Olá será o proprietário de circuito de ExpressRoute toohello aplicados.</span><span class="sxs-lookup"><span data-stu-id="dfa61-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="dfa61-139">Todas as redes virtuais partilham Olá mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="dfa61-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividade entre subscrições](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="dfa61-141">Administração</span><span class="sxs-lookup"><span data-stu-id="dfa61-141">Administration</span></span>
<span data-ttu-id="dfa61-142">Olá *proprietário do circuito* é Olá administrador/coadministrador da subscrição Olá que Olá ExpressRoute é criar circuito.</span><span class="sxs-lookup"><span data-stu-id="dfa61-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="dfa61-143">Olá proprietário do circuito pode autorizar administradores/coadministrators de outras subscrições, referidos tooas *circuito utilizadores*, toouse Olá dedicado circuito que possuem.</span><span class="sxs-lookup"><span data-stu-id="dfa61-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="dfa61-144">Circuito os utilizadores podem de circuito de ExpressRoute toouse autorizados Olá organização ligação de rede virtual do Olá no respetivo toohello subscrição circuito ExpressRoute depois estiverem autorizadas.</span><span class="sxs-lookup"><span data-stu-id="dfa61-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="dfa61-145">proprietário do circuito Olá tem as autorizações Olá energia toomodify e revogar em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="dfa61-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="dfa61-146">Revogar uma autorização resultará em todas as ligações seja eliminadas da subscrição Olá cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="dfa61-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="dfa61-147">Operações de proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="dfa61-147">Circuit owner operations</span></span>

<span data-ttu-id="dfa61-148">**Criar uma autorização**</span><span class="sxs-lookup"><span data-stu-id="dfa61-148">**Creating an authorization**</span></span>

<span data-ttu-id="dfa61-149">Olá proprietário do circuito autoriza Olá os administradores de outras subscrições toouse Olá especificado circuito.</span><span class="sxs-lookup"><span data-stu-id="dfa61-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="dfa61-150">No seguinte exemplo de Olá, o administrador de Olá do circuito Olá (Contoso TI) permite ao administrador Olá de outra subscrição (Dev-teste) toolink segurança circuito de toohello tootwo redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="dfa61-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="dfa61-151">administrador de TI da Contoso Olá permite isto, especificando o ID de teste de desenvolvimento Microsoft Olá.</span><span class="sxs-lookup"><span data-stu-id="dfa61-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="dfa61-152">cmdlet de Olá não enviar correio eletrónico toohello especificado ID da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dfa61-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="dfa61-153">tem de proprietário do circuito Olá tooexplicitly notificar Olá outro proprietário da subscrição que Olá autorização está concluído.</span><span class="sxs-lookup"><span data-stu-id="dfa61-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="dfa61-154">**Rever autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfa61-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="dfa61-155">proprietário do circuito Olá pode rever todas as autorizações que são emitidas sobre um determinado circuito executando Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dfa61-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="dfa61-156">**Atualizar autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfa61-156">**Updating authorizations**</span></span>

<span data-ttu-id="dfa61-157">proprietário do circuito Olá pode modificar autorizações utilizando Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dfa61-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="dfa61-158">**Eliminar autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfa61-158">**Deleting authorizations**</span></span>

<span data-ttu-id="dfa61-159">proprietário do circuito Olá pode revogar/eliminar utilizador de toohello autorizações executando Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dfa61-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="dfa61-160">Operações de utilizador do circuito</span><span class="sxs-lookup"><span data-stu-id="dfa61-160">Circuit user operations</span></span>

<span data-ttu-id="dfa61-161">**Rever autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfa61-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="dfa61-162">utilizador do circuito Olá pode rever autorizações utilizando Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dfa61-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="dfa61-163">**Resgatar autorizações de ligações**</span><span class="sxs-lookup"><span data-stu-id="dfa61-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="dfa61-164">utilizador do circuito Olá pode executar Olá seguintes cmdlet tooredeem uma autorização de ligação:</span><span class="sxs-lookup"><span data-stu-id="dfa61-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="dfa61-165">Execute este comando na subscrição Olá recentemente ligado para a rede virtual Olá:</span><span class="sxs-lookup"><span data-stu-id="dfa61-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="dfa61-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dfa61-166">Next steps</span></span>
<span data-ttu-id="dfa61-167">Para obter mais informações sobre o ExpressRoute, consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="dfa61-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

