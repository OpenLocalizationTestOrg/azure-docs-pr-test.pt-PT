---
title: aaaSubscription e de conta para VMs com Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá chaves design e implementação diretrizes para as subscrições e contas no Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="9a59a-103">Diretrizes de contas e subscrição do Azure para VMs com Linux</span><span class="sxs-lookup"><span data-stu-id="9a59a-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="9a59a-104">Este artigo foca-se em compreender o crescimentos de gestão de subscrição e a conta de tooapproach como o seu ambiente e a base de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="9a59a-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="9a59a-105">Diretrizes de implementação para as subscrições e contas</span><span class="sxs-lookup"><span data-stu-id="9a59a-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="9a59a-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="9a59a-106">Decisions:</span></span>

* <span data-ttu-id="9a59a-107">O conjunto de subscrições e contas precisa toohost a carga de trabalho IT ou infraestrutura?</span><span class="sxs-lookup"><span data-stu-id="9a59a-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="9a59a-108">Como toobreak baixo Olá hierarquia toofit sua organização?</span><span class="sxs-lookup"><span data-stu-id="9a59a-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="9a59a-109">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="9a59a-109">Tasks:</span></span>

* <span data-ttu-id="9a59a-110">Definir a sua hierarquia de organização lógica como gostaria de toomanage-lo a partir de um nível de subscrição.</span><span class="sxs-lookup"><span data-stu-id="9a59a-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="9a59a-111">toomatch esta hierarquia lógica, definir as contas de Olá necessários e as subscrições em cada conta.</span><span class="sxs-lookup"><span data-stu-id="9a59a-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="9a59a-112">Crie conjunto de Olá de subscrições e contas de utilizar a Convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="9a59a-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="9a59a-113">Subscrições e contas</span><span class="sxs-lookup"><span data-stu-id="9a59a-113">Subscriptions and accounts</span></span>
<span data-ttu-id="9a59a-114">toowork com o Azure, terá de uma ou mais subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a59a-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="9a59a-115">Recursos como máquinas virtuais (VMs) ou rede virtual existir nessas subscrições.</span><span class="sxs-lookup"><span data-stu-id="9a59a-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="9a59a-116">Os clientes empresariais têm normalmente uma inscrição Enterprise, o que é Olá mais alto recurso na hierarquia de Olá, não sendo tooone associado ou mais contas.</span><span class="sxs-lookup"><span data-stu-id="9a59a-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="9a59a-117">Para consumidores e os clientes sem uma inscrição Enterprise, o recurso de mais alto de Olá é conta Olá.</span><span class="sxs-lookup"><span data-stu-id="9a59a-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="9a59a-118">As subscrições são tooaccounts associados e pode existir uma ou mais subscrições por conta.</span><span class="sxs-lookup"><span data-stu-id="9a59a-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="9a59a-119">Registos do Azure informações ao nível da subscrição de Olá de faturação.</span><span class="sxs-lookup"><span data-stu-id="9a59a-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="9a59a-120">Devido a toohello limite dos níveis de hierarquia de duas na relação de subscrição de conta/Olá, é importante tooalign Olá Convenção de nomenclatura subscrições e contas toohello necessidades de faturação.</span><span class="sxs-lookup"><span data-stu-id="9a59a-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="9a59a-121">Por exemplo, se uma empresa global utiliza o Azure, pode optar por utilizar toohave uma conta por região e tem subscrições geridos de Olá nível Região:</span><span class="sxs-lookup"><span data-stu-id="9a59a-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="9a59a-122">Por exemplo, poderá utilizar Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="9a59a-122">For instance, you might use hello following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="9a59a-123">Se uma região decidir toohave mais do que grupo específico de tooa associada uma subscrição, convenção de nomenclatura de Olá deve incorporar um tooencode de forma Olá dados adicionais sobre a conta de Olá ou o nome da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="9a59a-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="9a59a-124">Esta organização permite massaging faturação dados toogenerate Olá novos níveis da hierarquia durante a faturação relatórios:</span><span class="sxs-lookup"><span data-stu-id="9a59a-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="9a59a-125">organização Olá foi aspeto Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9a59a-125">hello organization could look like hello following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="9a59a-126">Fornecemos faturação detalhada através de um ficheiro transferível para uma única conta ou para todas as contas de um contrato enterprise.</span><span class="sxs-lookup"><span data-stu-id="9a59a-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a59a-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a59a-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

