---
title: "aaaScale quotas e limites no laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooscale um laboratório no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="cc542-103">Quotas e limites de escala no DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="cc542-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="cc542-104">À medida que trabalha no DevTest Labs, poderá reparar que existem determinada toosome de limites de predefinição recursos do Azure, o que podem afetar o serviço de DevTest Labs Olá.</span><span class="sxs-lookup"><span data-stu-id="cc542-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="cc542-105">Estes limites são referidos tooas **quotas**.</span><span class="sxs-lookup"><span data-stu-id="cc542-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="cc542-106">Olá serviço DevTest Labs não impõe quaisquer quotas.</span><span class="sxs-lookup"><span data-stu-id="cc542-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="cc542-107">Quaisquer quotas que podem surgir são restrições predefinidas de Olá subscrição global do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc542-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="cc542-108">Pode utilizar cada recurso do Azure, até atingir a quota.</span><span class="sxs-lookup"><span data-stu-id="cc542-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="cc542-109">Cada subscrição tem quotas separadas e utilização é controlada por subscrição.</span><span class="sxs-lookup"><span data-stu-id="cc542-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="cc542-110">Por exemplo, cada subscrição tem uma quota de predefinição de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="cc542-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="cc542-111">Por isso, se estiver a criar VMs no seu laboratório com quatro núcleos, em seguida, pode criar apenas cinco VMs.</span><span class="sxs-lookup"><span data-stu-id="cc542-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="cc542-112">[Subscrição e limites de serviço da Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits) lista algumas das quotas mais comuns de Olá para recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc542-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="cc542-113">Olá recursos normalmente utilizados num laboratório de e para que poderá encontrar quotas incluem núcleos VM, endereços IP públicos, interface de rede, discos geridos, atribuição de função RBAC e circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cc542-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="cc542-114">Ver a sua utilização e quotas</span><span class="sxs-lookup"><span data-stu-id="cc542-114">View your usage and quotas</span></span>
<span data-ttu-id="cc542-115">Estes passos mostram como tooview Olá as quotas atuais na sua subscrição para recursos do Azure específicos e toosee que percentagem de cada quota que utilizou.</span><span class="sxs-lookup"><span data-stu-id="cc542-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="cc542-116">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cc542-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="cc542-117">Selecione **mais serviços**e, em seguida, selecione **faturação** da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc542-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="cc542-118">No painel de faturação Olá, selecione uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="cc542-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="cc542-119">Selecione **utilização + quotas**.</span><span class="sxs-lookup"><span data-stu-id="cc542-119">Select **Usage + quotas**.</span></span>

   ![Botão de utilização e quotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="cc542-121">Olá utilização + quotas é apresentado o painel, listagem diferentes recursos disponíveis nessa percentagem de subscrição e Olá de quota de Olá que está a ser utilizado por recurso.</span><span class="sxs-lookup"><span data-stu-id="cc542-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Quotas e utilização](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="cc542-123">Pedir mais recursos na sua subscrição</span><span class="sxs-lookup"><span data-stu-id="cc542-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="cc542-124">Se atingir um limite de quota, limite predefinido de Olá de um recurso de uma subscrição pode ser aumentado segurança limite máximo de tooa, conforme descrito em [subscrição do Azure e limites de serviço](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="cc542-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="cc542-125">Estes passos mostram como toorequest uma quota aumentar através de Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cc542-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="cc542-126">Selecione **mais serviços**, selecione **faturação**e, em seguida, selecione **utilização + quotas**.</span><span class="sxs-lookup"><span data-stu-id="cc542-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="cc542-127">Na utilização de Olá + painel de quotas, selecione Olá **pedido aumentar** botão.</span><span class="sxs-lookup"><span data-stu-id="cc542-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Botão de aumento de pedido](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="cc542-129">toocomplete e submeter pedido Olá, preencha as informações Olá necessário em todos os três separadores de Olá **novo pedido de suporte** formulário.</span><span class="sxs-lookup"><span data-stu-id="cc542-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Formulário de pedido de aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="cc542-131">[Noções sobre Azure limites e aumenta](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fornece mais informações sobre como contactar o suporte do Azure toorequest uma quota de aumento.</span><span class="sxs-lookup"><span data-stu-id="cc542-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="cc542-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cc542-132">Next steps</span></span>
* <span data-ttu-id="cc542-133">Explorar Olá [Galeria de modelo de início rápido do DevTest Labs do Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="cc542-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
