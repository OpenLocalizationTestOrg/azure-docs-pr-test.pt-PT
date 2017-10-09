---
title: "recomendações de custo de Advisor aaaAzure | Microsoft Docs"
description: "Utilize o custo de Olá toooptimize Azure Advisor das implementações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="f9b60-103">Recomendações de custo do Assistente</span><span class="sxs-lookup"><span data-stu-id="f9b60-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="f9b60-104">Ajuda-o Advisor otimizar e reduzir o Azure geral passam por identificar recursos inativos e subutilizados.</span><span class="sxs-lookup"><span data-stu-id="f9b60-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="f9b60-105">Pode obter custo recomendações da Olá **custo** separador no dashboard do Olá do Advisor.</span><span class="sxs-lookup"><span data-stu-id="f9b60-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Separador de custo do Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="f9b60-107">Otimizar a máquina virtual passam por redimensionamento subutilizadas instâncias</span><span class="sxs-lookup"><span data-stu-id="f9b60-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="f9b60-108">Apesar de determinados cenários de aplicação podem resultar numa utilização baixa por predefinição, muitas vezes, pode poupar dinheiro ao gerir tamanho Olá e o número de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f9b60-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="f9b60-109">Advisor monitoriza a utilização da máquina virtual nos últimos 14 dias e, em seguida, identifica as máquinas virtuais de baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="f9b60-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="f9b60-110">Máquinas virtuais cuja utilização do CPU é 5 porcento ou menos e utilização de rede é 7 MB ou menos, de quatro ou mais dias são considerados máquinas de virtuais baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="f9b60-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="f9b60-111">Apresenta o Advisor Olá custo estimado continuar toorun a máquina virtual, para que possa escolher tooshut-pendente ou redimensioná-la.</span><span class="sxs-lookup"><span data-stu-id="f9b60-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Advisor custo recomendações para redimensionar máquinas virtuais](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="f9b60-113">Utilizar uma solução económica toomanage desempenho objetivos várias bases de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f9b60-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="f9b60-114">Advisor identifica as instâncias do SQL Server que podem beneficiar do criar conjuntos de bases de dados elásticas.</span><span class="sxs-lookup"><span data-stu-id="f9b60-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="f9b60-115">Conjuntos de bases de dados elásticas fornecem uma solução simples e rentável toomanage objetivos de desempenho de Olá de várias bases de dados que tenham diferentes padrões de utilização.</span><span class="sxs-lookup"><span data-stu-id="f9b60-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="f9b60-116">Para obter mais informações sobre conjuntos elásticos do Azure, consulte [o que é um conjunto elástico do Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="f9b60-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Advisor custo recomendações para conjuntos de bases de dados elásticas](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="f9b60-118">Como tooaccess custo recomendações no Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="f9b60-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="f9b60-119">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9b60-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f9b60-120">No painel esquerdo Olá, clique em **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="f9b60-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="f9b60-121">Olá serviço em Painel de menu, **monitorização e gestão**, clique em **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="f9b60-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="f9b60-122">dashboard de Advisor Olá é apresentado.</span><span class="sxs-lookup"><span data-stu-id="f9b60-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="f9b60-123">No dashboard do Advisor Olá, clique em Olá **custo** separador.</span><span class="sxs-lookup"><span data-stu-id="f9b60-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="f9b60-124">Selecione a subscrição Olá para o qual pretende tooreceive recomendações e, em seguida, clique em **obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="f9b60-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="f9b60-125">tooaccess recomendações do assistente, tem primeiro *registar a sua subscrição* com o Advisor.</span><span class="sxs-lookup"><span data-stu-id="f9b60-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="f9b60-126">Uma subscrição é registada quando um *subscrição proprietário* inicia Olá Olá de dashboard e os cliques em Advisor **obter recomendações** botão.</span><span class="sxs-lookup"><span data-stu-id="f9b60-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="f9b60-127">Este é um *operação única*.</span><span class="sxs-lookup"><span data-stu-id="f9b60-127">This is a *one-time operation*.</span></span> <span data-ttu-id="f9b60-128">Depois de subscrição de Olá está registada, pode aceder recomendações do assistente como *proprietário*, *contribuinte*, ou *leitor* para uma subscrição, um grupo de recursos, ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="f9b60-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9b60-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f9b60-129">Next steps</span></span>

<span data-ttu-id="f9b60-130">toolearn mais informações sobre as recomendações do Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="f9b60-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="f9b60-131">Introdução tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="f9b60-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="f9b60-132">Introdução</span><span class="sxs-lookup"><span data-stu-id="f9b60-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="f9b60-133">Recomendações de desempenho do Assistente</span><span class="sxs-lookup"><span data-stu-id="f9b60-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="f9b60-134">Recomendações de elevada disponibilidade do Assistente</span><span class="sxs-lookup"><span data-stu-id="f9b60-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="f9b60-135">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="f9b60-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
