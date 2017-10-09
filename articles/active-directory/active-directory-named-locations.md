---
title: "localizações de aaaNamed no Azure Active Directory | Microsoft Docs"
description: "Ao configurar a chamada localizações, pode evitar a necessidade de IP endereços que são proprietário pela sua organização geram falsos positivos para localizações de tooatypical Olá impossível o risco de tipo de evento."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="030e8-103">Localizações nomeadas no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="030e8-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="030e8-104">Com Olá com o nome da funcionalidade de localizações do Azure Active Directory, pode Etiquetar intervalos de endereços IP fidedignos nas suas organizações.</span><span class="sxs-lookup"><span data-stu-id="030e8-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="030e8-105">No seu ambiente, pode utilizar localizações chamadas no contexto de Olá deteção Olá de [eventos de risco](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="030e8-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="030e8-106">funcionalidade de Olá ajuda a reduzir o número de Olá de comunicado falsos positivos para Olá *impossível tooatypical localizações* o risco de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="030e8-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="030e8-107">Configuração</span><span class="sxs-lookup"><span data-stu-id="030e8-107">Configuration</span></span>

<span data-ttu-id="030e8-108">tooconfigure uma localização com nome:</span><span class="sxs-lookup"><span data-stu-id="030e8-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="030e8-109">Inicie sessão no toohello [portal do Azure](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="030e8-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="030e8-110">No painel esquerdo Olá, clique em **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="030e8-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![ligação do Azure Active Directory Olá no painel esquerdo Olá](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="030e8-112">No Olá **do Azure Active Directory** painel, no Olá **segurança** secção, clique em **acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="030e8-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Olá comandos de acesso condicional](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="030e8-114">No Olá **acesso condicional** painel, no Olá **gerir** secção, clique em **denominado localizações**.</span><span class="sxs-lookup"><span data-stu-id="030e8-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Olá denominado localizações comando](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="030e8-116">No Olá **denominado localizações** painel, clique em **nova localização**.</span><span class="sxs-lookup"><span data-stu-id="030e8-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Olá novo comando localização](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="030e8-118">No Olá **novo** painel, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="030e8-118">On hello **New** blade, do hello following:</span></span>

    ![Painel nova Olá](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="030e8-120">a.</span><span class="sxs-lookup"><span data-stu-id="030e8-120">a.</span></span> <span data-ttu-id="030e8-121">No Olá **nome** caixa, escreva um nome para a sua localização com nome.</span><span class="sxs-lookup"><span data-stu-id="030e8-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="030e8-122">b.</span><span class="sxs-lookup"><span data-stu-id="030e8-122">b.</span></span> <span data-ttu-id="030e8-123">No Olá **intervalos IP** caixa, escreva um intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="030e8-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="030e8-124">intervalo IP Olá tem toobe no Olá *encaminhamento-Classless Inter-Domain* formato (CIDR).</span><span class="sxs-lookup"><span data-stu-id="030e8-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="030e8-125">c.</span><span class="sxs-lookup"><span data-stu-id="030e8-125">c.</span></span> <span data-ttu-id="030e8-126">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="030e8-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="030e8-127">O que deve conhecer</span><span class="sxs-lookup"><span data-stu-id="030e8-127">What you should know</span></span>

<span data-ttu-id="030e8-128">**Em massa atualizações**: ao criar ou atualizar localizações com nome, para as atualizações em massa, pode carregar ou transferir um ficheiro CSV com intervalos IP Olá.</span><span class="sxs-lookup"><span data-stu-id="030e8-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="030e8-129">Um carregamento adiciona os intervalos IP Olá na lista de toohello Olá ficheiros em vez de substituir a lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="030e8-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Olá carregar e transferir ligações](./media/active-directory-named-locations/09.png)


<span data-ttu-id="030e8-131">**Limitações**: pode definir um máximo de 60 localizações com nome, com um tooeach de intervalo atribuído de IP dos mesmos.</span><span class="sxs-lookup"><span data-stu-id="030e8-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="030e8-132">Se tiver apenas uma localização com nome configurada, pode definir too500 intervalos IP para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="030e8-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="030e8-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="030e8-133">Next steps</span></span>

<span data-ttu-id="030e8-134">toolearn mais informações sobre eventos de risco, consulte [eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="030e8-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

