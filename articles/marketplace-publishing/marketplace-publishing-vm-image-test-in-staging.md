---
title: "aaaTest VM oferecem para Olá Marketplace | Microsoft Docs"
description: "Compreenda como tootest a VM de imagem para Olá Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="adf04-103">Testar a sua oferta VM para Olá Azure Marketplace em transição</span><span class="sxs-lookup"><span data-stu-id="adf04-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="adf04-104">Significa que implementar o SKU no privado "sandbox", onde pode testar e validar a sua funcionalidade antes de o implementar toohello Marketplace de teste.</span><span class="sxs-lookup"><span data-stu-id="adf04-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="adf04-105">Olá SKU é apresentado no teste, tal como qualquer cliente de tooa que tenha implementado.</span><span class="sxs-lookup"><span data-stu-id="adf04-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="adf04-106">A imagem VM tem de ser certificadas toobe enviadas por push toostaging.</span><span class="sxs-lookup"><span data-stu-id="adf04-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="adf04-107">Passo 1: Push toostaging sua oferta</span><span class="sxs-lookup"><span data-stu-id="adf04-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="adf04-108">No Olá **publicar** separador, clique em **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="adf04-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![desenho](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="adf04-110">Se o Portal de publicação de Olá notifica-o de erros, corrija-os.</span><span class="sxs-lookup"><span data-stu-id="adf04-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="adf04-111">No Olá **quem pode aceder à sua oferta testada?** caixa de diálogo, introduza a lista de Olá de subscrições do Azure que irá utilizar toopreview oferta no Olá [portal de pré-visualização do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="adf04-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="adf04-112">Em caso de máquinas virtuais e modelos de solução,. **não** subscrições da lista branca do tipo CSP, DreamSpark ou do Azure no Open.</span><span class="sxs-lookup"><span data-stu-id="adf04-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="adf04-113">Em caso de máquinas virtuais, ao clicar no botão de Olá **PUSH tooSTAGING**, Olá os seguintes passos é efetuado por trás de cenas Olá.</span><span class="sxs-lookup"><span data-stu-id="adf04-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="adf04-114">Será progresso de Olá tooview capaz de cada passo no separador de publicar Olá no Olá portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="adf04-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="adf04-115">Tem de verificar esta página num intervalo regular (até que o estado de Olá mostra teste) para qualquer informação de falha que precisam de correção da sua end.</span><span class="sxs-lookup"><span data-stu-id="adf04-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="adf04-116">Em primeiro lugar, o pedido de teste passa toohello equipa de certificação que validar Olá vhd.</span><span class="sxs-lookup"><span data-stu-id="adf04-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="adf04-117">No entanto, se o pedido tem tem apenas alterações de marketing, em seguida, Olá certificação passo é ignorado.</span><span class="sxs-lookup"><span data-stu-id="adf04-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="adf04-118">Após a conclusão da certificação Olá, replicação de início de oferta Olá em todos os Olá centros de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="adf04-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="adf04-119">Geralmente, demora 24-48hours para Olá replicação toocomplete mas poderá demorar até tooa semana, consoante o tamanho do vhd Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="adf04-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="adf04-120">No entanto, se o pedido tem tem apenas alterações de marketing, em seguida, replicação de Olá é mais rápida.</span><span class="sxs-lookup"><span data-stu-id="adf04-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="adf04-121">Quando a replicação de Olá estiver concluída, em seguida, oferta Olá estará disponível no Olá [portal do Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="adf04-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="adf04-122">Em Olá esse tempo Estado ficar TESTADO no Olá portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="adf04-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="adf04-123">Uma oferta pré-configurada está visível no Olá [portal do Azure](http:/portal.azure.com) apenas utilizando Olá indicados de correio eletrónico associados à subscrição Olá preparada com que Olá oferta.</span><span class="sxs-lookup"><span data-stu-id="adf04-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="adf04-124">Inicie sessão no toohello [portal de pré-visualização do Azure](https://portal.azure.com) utilizando um dos Olá subscrições Azure listadas no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="adf04-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="adf04-125">Localizar a sua oferta e validar os pontos de imagem VM:</span><span class="sxs-lookup"><span data-stu-id="adf04-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="adf04-126">Certifique-se de que marketing conteúdo apresentado corretamente no Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="adf04-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="adf04-127">Implementação da imagem VM Olá ponto-a-ponto.</span><span class="sxs-lookup"><span data-stu-id="adf04-127">End-to-end deployment of hello VM image.</span></span>
     
      ![portal de mapa img](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="adf04-129">A oferta irá permanecer na transição até notificar a Microsoft através do Portal de publicação de Olá [**publicar** separador > clique no botão de Olá **"" pedido de aprovação tooPush tooProduction**] que é toopush pronto tooproduction.</span><span class="sxs-lookup"><span data-stu-id="adf04-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="adf04-130">Este é um toohave tempo ideal todos os membros da sua equipa de verificação sobre tudo em preparação para a sua oferta vai listadas.</span><span class="sxs-lookup"><span data-stu-id="adf04-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="adf04-131">Olá plataforma de teste foi concebida para teste Olá oferta no modo de pré-visualização por fabricante Olá.</span><span class="sxs-lookup"><span data-stu-id="adf04-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="adf04-132">É vivamente desencorajar-se utilizar esta platofrm para fins de commerical.</span><span class="sxs-lookup"><span data-stu-id="adf04-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="adf04-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="adf04-133">Next steps</span></span>
<span data-ttu-id="adf04-134">Agora que a oferta é "teste" e testado a sua funcionalidade e conteúdo de marketing, pode avançar publicação final toohello fase, **passo 4**: [implementar toohello sua oferta Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="adf04-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="adf04-135">Consultar também</span><span class="sxs-lookup"><span data-stu-id="adf04-135">See also</span></span>
* [<span data-ttu-id="adf04-136">Introdução: como toopublish toohello uma oferta Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="adf04-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

