---
title: 'Criar e modificar um circuito ExpressRoute: portal do Azure | Microsoft Docs'
description: Este artigo descreve como toocreate, aprovisionar, certifique-se, atualizar, eliminar e retirar o aprovisionamento um circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="135f0-103">Criar e modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="135f0-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="135f0-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="135f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="135f0-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="135f0-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="135f0-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="135f0-107">Vídeo - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="135f0-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="135f0-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="135f0-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="135f0-109">Este artigo descreve como toocreate um circuito ExpressRoute do Azure utilizando Olá Azure modelo de implementação de Gestor de recursos do Azure de portal e Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="135f0-110">Olá também os seguintes passos mostra como toocheck Olá estado do circuito Olá, a atualização, ou eliminar e retirar o aprovisionamento do mesmo.</span><span class="sxs-lookup"><span data-stu-id="135f0-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="135f0-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="135f0-111">Before you begin</span></span>
* <span data-ttu-id="135f0-112">Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="135f0-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="135f0-113">Certifique-se de que tem acesso toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="135f0-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="135f0-114">Certifique-se de que dispõe de permissões toocreate novos recursos de rede.</span><span class="sxs-lookup"><span data-stu-id="135f0-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="135f0-115">Se não tiver permissões corretas Olá, contacte o administrador de conta.</span><span class="sxs-lookup"><span data-stu-id="135f0-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="135f0-116">Pode [ver um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de começar por ordem toobetter compreender os passos de Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="135f0-117">Criar e aprovisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="135f0-118">1. A iniciar sessão toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="135f0-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="135f0-119">Num browser, navegue toohello [portal do Azure](http://portal.azure.com) e inicie sessão com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="135f0-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="135f0-120">2. Criar um novo circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="135f0-121">O circuito de ExpressRoute será cobrado a partir do momento em que Olá uma chave de serviço é emitida.</span><span class="sxs-lookup"><span data-stu-id="135f0-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="135f0-122">Certifique-se de que efetuar esta operação quando o fornecedor de conectividade de Olá circuito de Olá tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="135f0-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="135f0-123">Pode criar um circuito ExpressRoute selecionando Olá opção toocreate um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="135f0-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="135f0-124">Clique em **novo** > **redes** > **ExpressRoute**, conforme apresentado na Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="135f0-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Criar um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="135f0-126">Depois de clicar em **ExpressRoute**, verá Olá **circuito ExpressRoute criar** painel.</span><span class="sxs-lookup"><span data-stu-id="135f0-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="135f0-127">Quando estiver a preencher valores de Olá neste painel, certifique-se de que especifica a camada SKU correta Olá e medição de dados.</span><span class="sxs-lookup"><span data-stu-id="135f0-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="135f0-128">**Camada** determina se a um padrão de ExpressRoute ou de um suplemento ExpressRoute premium está ativado.</span><span class="sxs-lookup"><span data-stu-id="135f0-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="135f0-129">Pode especificar **padrão** tooget Olá standard SKU ou **Premium** para o suplemento do Olá premium.</span><span class="sxs-lookup"><span data-stu-id="135f0-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="135f0-130">**Medição de dados** determina o tipo de faturação Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="135f0-131">Pode especificar **Metered** para um plano de dados limitados e **ilimitada** para um plano de dados ilimitados.</span><span class="sxs-lookup"><span data-stu-id="135f0-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="135f0-132">Tenha em atenção que pode alterar o tipo de faturação Olá de **Metered** demasiado**ilimitada**, mas não é possível alterar o tipo de Olá da **ilimitada** demasiado**Metered**.</span><span class="sxs-lookup"><span data-stu-id="135f0-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Configurar a camada SKU Olá e medição de dados](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="135f0-134">. Lembre-se de que a localização de Peering de Olá indica Olá [localização física](expressroute-locations.md) onde são peering com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="135f0-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="135f0-135">Este é **não** ligado demasiado propriedade de "Localização", que se refere geografia toohello onde está localizada a Olá fornecedor de recursos de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="135f0-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="135f0-136">Apesar de não estão relacionadas, é uma boa prática toochoose um toohello geograficamente fechar o fornecedor de recursos de rede de localização de Peering do circuito Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="135f0-137">3. Vista Olá circuitos e propriedades</span><span class="sxs-lookup"><span data-stu-id="135f0-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="135f0-138">**Ver todos os circuitos de Olá**</span><span class="sxs-lookup"><span data-stu-id="135f0-138">**View all hello circuits**</span></span>

<span data-ttu-id="135f0-139">Pode ver todos os circuitos Olá que criou, selecionando **todos os recursos** no menu do lado esquerdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Circuitos de vista](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="135f0-141">**Ver propriedades de Olá**</span><span class="sxs-lookup"><span data-stu-id="135f0-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Ver propriedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="135f0-143">4. Enviar o fornecedor de conectividade do Olá serviço tooyour chave para o aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="135f0-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="135f0-144">Neste painel, **Estado fornecedor** fornece informações sobre o estado atual do Olá de aprovisionamento no lado do fornecedor de serviços de Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="135f0-145">**Estado de circuitos** fornece o estado de Olá Olá do lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="135f0-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="135f0-146">Para obter mais informações sobre os Estados de aprovisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.</span><span class="sxs-lookup"><span data-stu-id="135f0-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="135f0-147">Quando cria um novo circuito do ExpressRoute, circuito Olá estarão disponíveis na Olá seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="135f0-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="135f0-148">Estado do fornecedor: não aprovisionado</span><span class="sxs-lookup"><span data-stu-id="135f0-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="135f0-149">Estado de circuitos: ativado</span><span class="sxs-lookup"><span data-stu-id="135f0-149">Circuit status: Enabled</span></span>

![Iniciar o processo de aprovisionamento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="135f0-151">o circuito de Olá mudará toohello seguinte estado quando o fornecedor de conectividade Olá está no processo de Olá de ativação-lo por si:</span><span class="sxs-lookup"><span data-stu-id="135f0-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="135f0-152">Estado do fornecedor: aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="135f0-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="135f0-153">Estado de circuitos: ativado</span><span class="sxs-lookup"><span data-stu-id="135f0-153">Circuit status: Enabled</span></span>

<span data-ttu-id="135f0-154">Para toobe capaz de toouse um circuito do ExpressRoute, tem de ter Olá seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="135f0-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="135f0-155">Estado do fornecedor: aprovisionado</span><span class="sxs-lookup"><span data-stu-id="135f0-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="135f0-156">Estado de circuitos: ativado</span><span class="sxs-lookup"><span data-stu-id="135f0-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="135f0-157">5. Verificar periodicamente o estado de Olá e estado de Olá da chave de circuito Olá</span><span class="sxs-lookup"><span data-stu-id="135f0-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="135f0-158">Pode ver as propriedades de Olá do circuito Olá que está a interessados ao selecioná-la.</span><span class="sxs-lookup"><span data-stu-id="135f0-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="135f0-159">Verifique Olá **Estado fornecedor** e certifique-se de que foi movida demasiado**aprovisionado** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="135f0-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Estado do circuito e fornecedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="135f0-161">6. Criar a configuração de encaminhamento</span><span class="sxs-lookup"><span data-stu-id="135f0-161">6. Create your routing configuration</span></span>
<span data-ttu-id="135f0-162">Para obter instruções passo a passo, consulte toohello [configuração de encaminhamento de circuito de ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) artigo toocreate e modificar peerings do circuito.</span><span class="sxs-lookup"><span data-stu-id="135f0-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="135f0-163">Estas instruções aplicam-se apenas toocircuits que são criados com fornecedores de serviços que oferecem serviços de 2 conectividade de camada.</span><span class="sxs-lookup"><span data-stu-id="135f0-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="135f0-164">Se estiver a utilizar um fornecedor de serviço que oferece gerido layer 3 serviços (normalmente, uma VPN de IP, como MPLS), o seu fornecedor de conectividade irá configurar e gerir encaminhamento por si.</span><span class="sxs-lookup"><span data-stu-id="135f0-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="135f0-165">7. Ligar uma rede virtual de tooan circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="135f0-166">Em seguida, associe um tooyour de rede virtual circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="135f0-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="135f0-167">Olá utilize [ligação virtual redes tooExpressRoute circuitos](expressroute-howto-linkvnet-arm.md) artigo quando trabalha com o modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="135f0-168">Ao obter o estado de Olá de um circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="135f0-169">Pode ver o estado de Olá de um circuito ao selecioná-la.</span><span class="sxs-lookup"><span data-stu-id="135f0-169">You can view hello status of a circuit by selecting it.</span></span> 

![Estado de um circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="135f0-171">Modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="135f0-172">Pode modificar algumas propriedades de um circuito ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="135f0-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="135f0-173">Pode fazê-lo Olá sem período de indisponibilidade os seguintes:</span><span class="sxs-lookup"><span data-stu-id="135f0-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="135f0-174">Ativar ou desativar um suplemento ExpressRoute premium para o seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="135f0-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="135f0-175">Aumento Olá largura de banda do circuito de ExpressRoute fornecido está capacidade disponível na porta Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="135f0-176">Tenha em atenção que a largura de banda de Olá de um circuito de desatualização não é suportado.</span><span class="sxs-lookup"><span data-stu-id="135f0-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="135f0-177">Alterar Olá plano do tooUnlimited dados limitados de dados de medição.</span><span class="sxs-lookup"><span data-stu-id="135f0-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="135f0-178">Tenha em atenção que a alteração plano medição Olá de tooMetered dados ilimitados de dados não é suportada.</span><span class="sxs-lookup"><span data-stu-id="135f0-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="135f0-179">Pode ativar e desativar *permitir operações clássicas*.</span><span class="sxs-lookup"><span data-stu-id="135f0-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="135f0-180">Para obter mais informações sobre limites e limitações, consulte toohello [FAQ do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="135f0-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="135f0-181">toomodify um circuito do ExpressRoute, clique em Olá **configuração** conforme mostrado na figura Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="135f0-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Modificar o circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="135f0-183">Pode modificar Olá da largura de banda, SKU e modelo de faturação e permitir operações clássicas dentro do painel de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="135f0-184">Pode ter o circuito de ExpressRoute toorecreate Olá se existir capacidade inadequada na porta existente Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="135f0-185">Não é possível atualizar o circuito Olá se não houver nenhuma capacidade adicional nessa localização.</span><span class="sxs-lookup"><span data-stu-id="135f0-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="135f0-186">Não é possível reduzir a largura de banda de Olá de um circuito de ExpressRoute sem interrupção.</span><span class="sxs-lookup"><span data-stu-id="135f0-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="135f0-187">Desatualização de largura de banda requer que o circuito de ExpressRoute toodeprovision Olá e, em seguida, reaprovisionar um circuito de ExpressRoute novo.</span><span class="sxs-lookup"><span data-stu-id="135f0-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="135f0-188">Desativar o suplemento premium operação pode falhar se estiver a utilizar recursos que são maiores que o que é permitido para o circuito standard Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="135f0-189">Desaprovisionamento e eliminar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="135f0-190">Pode eliminar o circuito de ExpressRoute selecionando Olá **eliminar** ícone.</span><span class="sxs-lookup"><span data-stu-id="135f0-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="135f0-191">Tenha em atenção o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="135f0-191">Note hello following:</span></span>

* <span data-ttu-id="135f0-192">Tem de desassociar todas as redes virtuais do Olá circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="135f0-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="135f0-193">Se esta operação falhar, verifique se as redes virtuais ligadas toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="135f0-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="135f0-194">Se for Olá ExpressRoute circuito fornecedor do serviço de estado de aprovisionamento **aprovisionamento** ou **aprovisionado** tem de trabalhar com o seu circuito de Olá de toodeprovision de fornecedor de serviço no seu lado.</span><span class="sxs-lookup"><span data-stu-id="135f0-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="135f0-195">Iremos continuar tooreserve recursos e faturar-lhe até que o fornecedor de serviços de Olá conclui o circuito de Olá desaprovisionamento e notifica-nos.</span><span class="sxs-lookup"><span data-stu-id="135f0-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="135f0-196">Se o fornecedor de serviços de Olá tem desaprovisionada circuito Olá (fornecedor de serviços de Olá estado de aprovisionamento está definido demasiado**não aprovisionado**), em seguida, pode eliminar o circuito Olá.</span><span class="sxs-lookup"><span data-stu-id="135f0-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="135f0-197">Isto irá parar faturação para o circuito Olá</span><span class="sxs-lookup"><span data-stu-id="135f0-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="135f0-198">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="135f0-198">Next steps</span></span>
<span data-ttu-id="135f0-199">Depois de criar o seu circuito, certifique-se de que Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="135f0-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="135f0-200">Criar e modificar o encaminhamento para o seu circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="135f0-201">Ligar o seu tooyour de rede virtual circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="135f0-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

