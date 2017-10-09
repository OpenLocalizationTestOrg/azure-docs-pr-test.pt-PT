---
title: "os conectores de Proxy de aplicações do Azure AD portais aaaClassic | Microsoft Docs"
description: "Abrange como toocreate e gerir grupos de conectores no Proxy de aplicações do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="37d5b-103">Publicar aplicações em redes separadas e localizações utilizar grupos de conector</span><span class="sxs-lookup"><span data-stu-id="37d5b-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37d5b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37d5b-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="37d5b-105">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="37d5b-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="37d5b-106">Grupos de conector são úteis para vários cenários, incluindo:</span><span class="sxs-lookup"><span data-stu-id="37d5b-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="37d5b-107">Sites com vários centros de dados interligados.</span><span class="sxs-lookup"><span data-stu-id="37d5b-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="37d5b-108">Neste caso, pretende tookeep o mesmo tráfego num centro de dados de Olá possível porque as ligações do Centro de dados entre são dispendiosas e lenta.</span><span class="sxs-lookup"><span data-stu-id="37d5b-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="37d5b-109">Pode implementar conectores em cada datacenter tooserve apenas Olá aplicações que residem no Olá Centro de dados.</span><span class="sxs-lookup"><span data-stu-id="37d5b-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="37d5b-110">Esta abordagem minimiza o Centro de dados entre ligações e fornece uma experiência totalmente transparente tooyour utilizadores.</span><span class="sxs-lookup"><span data-stu-id="37d5b-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="37d5b-111">Gerir aplicações instaladas em redes isoladas que não fazem parte da rede empresarial principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="37d5b-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="37d5b-112">Pode utilizar os conectores do conector grupos tooinstall dedicada na rede de toohello redes isoladas tooalso isolar aplicações.</span><span class="sxs-lookup"><span data-stu-id="37d5b-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="37d5b-113">Para as aplicações instaladas no IaaS para acesso à nuvem, os grupos de conector fornecem um serviço toosecure Olá acesso tooall Olá aplicações comuns.</span><span class="sxs-lookup"><span data-stu-id="37d5b-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="37d5b-114">Grupos de conector não criar dependência adicional na sua rede empresarial ou experiência de aplicação Olá de fragmento.</span><span class="sxs-lookup"><span data-stu-id="37d5b-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="37d5b-115">Os conectores podem ser instalados em todos os centros de dados de nuvem e servem apenas as aplicações que residem nesta rede.</span><span class="sxs-lookup"><span data-stu-id="37d5b-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="37d5b-116">Pode instalar vários conectores tooachieve elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="37d5b-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="37d5b-117">Suporte para ambientes de várias florestas que conectores específicos podem ser implementados por floresta e tooserve de aplicações específicas.</span><span class="sxs-lookup"><span data-stu-id="37d5b-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="37d5b-118">Grupos de conector podem ser utilizados em locais de recuperação após desastre tooeither detetar ativação pós-falha ou como cópia de segurança para Olá principal site.</span><span class="sxs-lookup"><span data-stu-id="37d5b-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="37d5b-119">Grupos de conector também podem ser utilizado tooserve várias empresas a partir de um único inquilino.</span><span class="sxs-lookup"><span data-stu-id="37d5b-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="37d5b-120">Pré-requisito: Criar a sua conectores</span><span class="sxs-lookup"><span data-stu-id="37d5b-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="37d5b-121">toogroup os conectores, [instalar vários conectores](active-directory-application-proxy-enable.md), em seguida, atribua um nome e agrupá-los.</span><span class="sxs-lookup"><span data-stu-id="37d5b-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="37d5b-122">Por fim tiver tooassign toospecific aplicações-los.</span><span class="sxs-lookup"><span data-stu-id="37d5b-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="37d5b-123">Passo 1: Criar grupos de conector</span><span class="sxs-lookup"><span data-stu-id="37d5b-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="37d5b-124">Pode criar grupos de conector tantos conforme pretender.</span><span class="sxs-lookup"><span data-stu-id="37d5b-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="37d5b-125">Criação do conector de grupo é efetuada no Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="37d5b-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="37d5b-126">Selecione o diretório e clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="37d5b-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="37d5b-127">![Proxy de aplicações, configure a captura de ecrã - clique em Gerir grupos de conetor](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="37d5b-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="37d5b-128">No Proxy de aplicações, clique em **gerir grupos de conector** e criar um grupo de conector, concedendo um nome de grupo Olá.</span><span class="sxs-lookup"><span data-stu-id="37d5b-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="37d5b-129">![Captura de ecrã - novo grupo de nome de grupos do conector do proxy da aplicação](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="37d5b-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="37d5b-130">Passo 2: Atribuir conectores tooyour grupos</span><span class="sxs-lookup"><span data-stu-id="37d5b-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="37d5b-131">Depois de Olá conector grupos são criados, mova grupo adequado do Olá conectores toohello.</span><span class="sxs-lookup"><span data-stu-id="37d5b-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="37d5b-132">Em **Proxy de aplicações**, clique em **gerir conectores**.</span><span class="sxs-lookup"><span data-stu-id="37d5b-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="37d5b-133">Em **grupo**, selecione o grupo de Olá que pretende para cada conector.</span><span class="sxs-lookup"><span data-stu-id="37d5b-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="37d5b-134">Poderá demorar conectores Olá segurança too10 minutos toobecome ativos no novo grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="37d5b-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="37d5b-135">![Captura de conectores ecrã aplicação proxy - selecione grupo a partir do menu pendente](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="37d5b-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="37d5b-136">Passo 3: Atribuir aplicações tooyour grupos de conetor</span><span class="sxs-lookup"><span data-stu-id="37d5b-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="37d5b-137">último passo de Olá é tooset cada grupo de conector de toohello de aplicação que serve-lo.</span><span class="sxs-lookup"><span data-stu-id="37d5b-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="37d5b-138">No Olá portal clássico do Azure, no seu diretório, selecione Olá a aplicação que pretende tooassign toohello grupo e clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="37d5b-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="37d5b-139">Em **grupo conector**, selecione o grupo de Olá pretende Olá toouse de aplicação.</span><span class="sxs-lookup"><span data-stu-id="37d5b-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="37d5b-140">Esta alteração será imediatamente aplicada.</span><span class="sxs-lookup"><span data-stu-id="37d5b-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="37d5b-141">![Aplicação proxy conector grupo captura de ecrã - selecione grupo a partir do menu pendente](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="37d5b-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="37d5b-142">Consultar também</span><span class="sxs-lookup"><span data-stu-id="37d5b-142">See also</span></span>
* [<span data-ttu-id="37d5b-143">Ativar o Proxy da aplicação</span><span class="sxs-lookup"><span data-stu-id="37d5b-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="37d5b-144">Ativar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="37d5b-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="37d5b-145">Ativar o acesso condicional</span><span class="sxs-lookup"><span data-stu-id="37d5b-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="37d5b-146">Resolver problemas com o Proxy da aplicação</span><span class="sxs-lookup"><span data-stu-id="37d5b-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="37d5b-147">Para obter notícias mais recentes Olá e atualizações, consulte Olá [blogue do Proxy da aplicação](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="37d5b-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
