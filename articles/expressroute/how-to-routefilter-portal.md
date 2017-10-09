---
title: 'Configurar filtros de rota para peering de ExpressRoute ao Microsoft Azure: Portal | Microsoft Docs'
description: "Este artigo descreve como tooconfigure filtros de rota para Peering da Microsoft utilizando Olá portal do Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="1032c-103">Configurar filtros de rota para o peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="1032c-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="1032c-104">Filtros de rota são uma forma tooconsume um subconjunto de serviços suportados através do peering da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1032c-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="1032c-105">passos seguintes Olá nesta ajuda de artigo, configurar e gerir filtros de rota para circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1032c-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="1032c-106">Serviços de Dynamics 365 e serviços do Office 365, como o Exchange Online, SharePoint Online e Skype para empresas, estão acessíveis através do peering da Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="1032c-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="1032c-107">Ao peering da Microsoft está configurado num circuito do ExpressRoute, todos os serviços de toothese relacionados prefixos estão anunciados através de sessões de BGP de Olá que são estabelecidas.</span><span class="sxs-lookup"><span data-stu-id="1032c-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="1032c-108">Um valor das Comunidades de BGP é anexado tooevery prefixo tooidentify Olá serviço é fornecido através de prefixo de Olá.</span><span class="sxs-lookup"><span data-stu-id="1032c-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="1032c-109">Para obter uma lista de valores das Comunidades BGP Olá e mapeiam para os serviços de Olá, consulte [Comunidades BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="1032c-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="1032c-110">Se necessitar de serviços de tooall de conectividade, um grande número de prefixos está anunciado através da BGP.</span><span class="sxs-lookup"><span data-stu-id="1032c-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="1032c-111">Isto aumenta significativamente tamanho Olá Olá de tabelas de rotas mantida por routers na sua rede.</span><span class="sxs-lookup"><span data-stu-id="1032c-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="1032c-112">Se planear tooconsume apenas um subconjunto de serviços fornecido via peering da Microsoft, pode reduzir o tamanho de Olá das suas tabelas de rota de duas formas.</span><span class="sxs-lookup"><span data-stu-id="1032c-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="1032c-113">Pode:</span><span class="sxs-lookup"><span data-stu-id="1032c-113">You can:</span></span>

- <span data-ttu-id="1032c-114">Filtre prefixos indesejáveis aplicando filtros de rota no Comunidades BGP.</span><span class="sxs-lookup"><span data-stu-id="1032c-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="1032c-115">Esta é uma prática padrão de rede e é utilizada frequentemente no diversas redes.</span><span class="sxs-lookup"><span data-stu-id="1032c-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="1032c-116">Definir os filtros de rota e aplicá-las tooyour circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1032c-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="1032c-117">Um filtro de rota é um novo recurso, que permite selecionar lista Olá de serviços planeie tooconsume através do peering da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1032c-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="1032c-118">Routers de ExpressRoute enviam apenas lista de Olá de prefixos que pertencem os serviços de toohello identificados no filtro de rota Olá.</span><span class="sxs-lookup"><span data-stu-id="1032c-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="1032c-119"><a name="about"></a>Sobre os filtros de rotas</span><span class="sxs-lookup"><span data-stu-id="1032c-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="1032c-120">Quando o peering da Microsoft está configurado no seu circuito do ExpressRoute, routers de limite de Microsoft Olá estabelecer um par de sessões de BGP com routers de limite de Olá (seu ou o fornecedor de conectividade).</span><span class="sxs-lookup"><span data-stu-id="1032c-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="1032c-121">Não existem rotas são rede tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="1032c-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="1032c-122">rede de tooyour de anúncios de rota tooenable, tem de associar um filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="1032c-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="1032c-123">Um filtro de rota permite-lhe identificar os serviços que pretende tooconsume através do peering da Microsoft do circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1032c-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="1032c-124">É, essencialmente, uma lista de técnico de todos os valores das Comunidades BGP de Olá.</span><span class="sxs-lookup"><span data-stu-id="1032c-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="1032c-125">Depois de um recurso de filtro de rota é definido e anexado tooan circuito do ExpressRoute, todos os prefixos que mapeiam os valores das Comunidades BGP toohello são rede tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="1032c-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="1032c-126">toobe tooattach capaz de filtros de rotas com os serviços do Office 365 nos mesmos, tem de ter serviços do Office 365 de tooconsume de autorização através do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1032c-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="1032c-127">Se não tiver serviços autorizados tooconsume do Office 365 através do ExpressRoute, filtros de rota Olá operação tooattach falhar.</span><span class="sxs-lookup"><span data-stu-id="1032c-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="1032c-128">Para obter mais informações sobre o processo de autorização de Olá, consulte [Azure ExpressRoute para o Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="1032c-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="1032c-129">Serviços de 365 conectividade tooDynamics não requer qualquer autorização anterior.</span><span class="sxs-lookup"><span data-stu-id="1032c-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1032c-130">Peering da Microsoft dos circuitos ExpressRoute que foram configuradas tooAugust anterior 1, 2017 terá todos os serviço prefixos anunciados através do peering da Microsoft, mesmo se os filtros de rota não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="1032c-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="1032c-131">Peering da Microsoft dos circuitos ExpressRoute que estão configurados em ou após 1 de Agosto de 2017 não terão qualquer prefixos anunciados até que está ligado um filtro de rota toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="1032c-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="1032c-132"><a name="workflow"></a>Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="1032c-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="1032c-133">toobe toosuccessfully de capaz de ligar tooservices através do peering da Microsoft, tem de concluir os seguintes passos de configuração de Olá:</span><span class="sxs-lookup"><span data-stu-id="1032c-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="1032c-134">Tem de ter um circuito ExpressRoute ativo que tenha aprovisionado de peering da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1032c-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="1032c-135">Pode utilizar Olá seguir instruções tooaccomplish estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="1032c-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="1032c-136">[Criar um circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="1032c-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="1032c-137">Olá circuito ExpressRoute tem de estar num Estado aprovisionado e ativado.</span><span class="sxs-lookup"><span data-stu-id="1032c-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="1032c-138">[Criar peering da Microsoft](expressroute-howto-routing-portal-resource-manager.md) se gerir sessões BGP de Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="1032c-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="1032c-139">Ou, solicite ao seu fornecedor de conectividade aprovisionar o peering da Microsoft para o seu circuito.</span><span class="sxs-lookup"><span data-stu-id="1032c-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="1032c-140">Tem de criar e configurar um filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="1032c-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="1032c-141">Identificar Olá serviços com tooconsume através do peering da Microsoft</span><span class="sxs-lookup"><span data-stu-id="1032c-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="1032c-142">Identifique Olá lista dos valores das Comunidades BGP associados Olá serviços</span><span class="sxs-lookup"><span data-stu-id="1032c-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="1032c-143">Criar uma regra tooallow Olá prefixo lista correspondente Olá valores das Comunidades BGP</span><span class="sxs-lookup"><span data-stu-id="1032c-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="1032c-144">Tem de anexar o circuito do ExpressRoute toohello Olá rota filtro.</span><span class="sxs-lookup"><span data-stu-id="1032c-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1032c-145">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1032c-145">Before you begin</span></span>

<span data-ttu-id="1032c-146">Antes de iniciar a configuração, certifique-se de que cumpre os seguintes critérios de Olá:</span><span class="sxs-lookup"><span data-stu-id="1032c-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="1032c-147">Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="1032c-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="1032c-148">Deve ter um circuito ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="1032c-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="1032c-149">Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="1032c-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="1032c-150">Olá circuito ExpressRoute tem de estar num Estado aprovisionado e ativado.</span><span class="sxs-lookup"><span data-stu-id="1032c-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="1032c-151">Tem de ter um peering da Microsoft Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1032c-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="1032c-152">Siga as instruções apresentadas em [criar e modificar a configuração do peering](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="1032c-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="1032c-153"><a name="prefixes"></a>Passo 1.</span><span class="sxs-lookup"><span data-stu-id="1032c-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="1032c-154">Obter uma lista de prefixos e os valores das Comunidades BGP</span><span class="sxs-lookup"><span data-stu-id="1032c-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="1032c-155">1. Obter uma lista de valores das Comunidades BGP</span><span class="sxs-lookup"><span data-stu-id="1032c-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="1032c-156">Valores das Comunidades BGP associados a serviços acessíveis através do peering da Microsoft está disponível no Olá [requisitos de encaminhamento do ExpressRoute](expressroute-routing.md) página.</span><span class="sxs-lookup"><span data-stu-id="1032c-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="1032c-157">2. Se uma lista de valores de Olá que pretende que o toouse</span><span class="sxs-lookup"><span data-stu-id="1032c-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="1032c-158">Se uma lista dos valores das Comunidades BGP que pretende toouse num filtro de rota Olá.</span><span class="sxs-lookup"><span data-stu-id="1032c-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="1032c-159">Por exemplo, Olá valor das Comunidades de BGP para os serviços de Dynamics 365 é 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="1032c-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="1032c-160"><a name="filter"></a>Passo 2.</span><span class="sxs-lookup"><span data-stu-id="1032c-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="1032c-161">Criar um filtro de rota e uma regra de filtro</span><span class="sxs-lookup"><span data-stu-id="1032c-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="1032c-162">Um filtro de rota pode ter apenas uma regra e Olá regra tem de ser do tipo 'Permitir'.</span><span class="sxs-lookup"><span data-stu-id="1032c-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="1032c-163">Esta regra pode ter uma lista dos valores das Comunidades BGP associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="1032c-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="1032c-164">1. Criar um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="1032c-164">1. Create a route filter</span></span>
<span data-ttu-id="1032c-165">Pode criar um filtro de rota selecionando Olá opção toocreate um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="1032c-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="1032c-166">Clique em **novo** > **redes** > **RouteFilter**, conforme apresentado na Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="1032c-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="1032c-168">Tem de colocar o filtro de rota Olá num grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1032c-168">You must place hello route filter in a resource group.</span></span> 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="1032c-170">2. Criar uma regra de filtro</span><span class="sxs-lookup"><span data-stu-id="1032c-170">2. Create a filter rule</span></span>

<span data-ttu-id="1032c-171">Pode adicionar e regras de atualização selecionando Olá gerir separador de regra para o filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="1032c-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="1032c-173">Pode selecionar Olá serviços pretende tooconnect toofrom Olá na lista pendente e guardar a regra de Olá quando terminar.</span><span class="sxs-lookup"><span data-stu-id="1032c-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="1032c-175"><a name="attach"></a>Passo 3.</span><span class="sxs-lookup"><span data-stu-id="1032c-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="1032c-176">Anexar o circuito do ExpressRoute tooan Olá rota filtro</span><span class="sxs-lookup"><span data-stu-id="1032c-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="1032c-177">Pode anexar o circuito de tooa de filtro de rota Olá selecionando o botão "adicionar o circuito" de Olá e selecionando circuito de ExpressRoute Olá Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="1032c-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="1032c-179"><a name="getproperties"></a>Propriedades de Olá tooget de um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="1032c-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="1032c-180">Pode ver as propriedades de um filtro de rota quando abrir o recurso de Olá no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="1032c-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="1032c-182"><a name="updateproperties"></a>Propriedades de Olá tooupdate de um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="1032c-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="1032c-183">Pode atualizar a lista de Olá do BGP Comunidade valores tooa anexado circuito selecionando o botão de Olá "Gerir regra".</span><span class="sxs-lookup"><span data-stu-id="1032c-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="1032c-186"><a name="detach"></a>toodetach um filtro de rota de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1032c-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="1032c-187">toodetach um circuito do filtro de rota Olá, clique em circuito Olá e clique em "desassocie".</span><span class="sxs-lookup"><span data-stu-id="1032c-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="1032c-189"><a name="delete"></a>toodelete um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="1032c-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="1032c-190">Pode eliminar um filtro de rota, selecionando o botão para eliminar Olá.</span><span class="sxs-lookup"><span data-stu-id="1032c-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="1032c-192">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1032c-192">Next steps</span></span>

<span data-ttu-id="1032c-193">Para obter mais informações sobre o ExpressRoute, consulte Olá [FAQ do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1032c-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
