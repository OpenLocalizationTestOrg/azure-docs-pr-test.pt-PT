---
title: "aaaTesting o serviço de dados oferecem para Olá Marketplace | Microsoft Docs"
description: "Compreenda como tootest o serviço de dados oferecem para Olá Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="41695-103">Testar a sua oferta de serviço de dados no modo de transição</span><span class="sxs-lookup"><span data-stu-id="41695-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="41695-104">**Neste momento, estamos já não integração qualquer nova editores de serviço de dados. Novo dataservices não irá obter aprovada para listagem.**</span><span class="sxs-lookup"><span data-stu-id="41695-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="41695-105">Se tiver uma aplicação de negócio de SaaS que gostaria de toopublish pode encontrar mais informações no AppSource [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="41695-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="41695-106">Se tiver um aplicações IaaS ou para programadores de serviço teria como toopublish no Azure Marketplace pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="41695-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="41695-107">Depois de concluir os primeiros dois passos, Olá de [criar a sua conta Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) e [criar a sua oferta de serviço de dados de mensagens em fila no Portal de publicação](marketplace-publishing-data-service-creation.md) está pronto para disponibilizar a oferta Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41695-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="41695-108">Este tópico irá guiá-lo Olá pela primeira vez, intermediária, passo chamada "transição"</span><span class="sxs-lookup"><span data-stu-id="41695-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="41695-109">Significa que implementar a sua oferta no privado "sandbox", onde pode testar e verificar a respetiva funcionalidade antes de enviar-tooproduction de teste.</span><span class="sxs-lookup"><span data-stu-id="41695-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="41695-110">oferta de Olá será apresentado tal como qualquer cliente de tooa que implementou, de transição.</span><span class="sxs-lookup"><span data-stu-id="41695-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="41695-111">Passo 1.</span><span class="sxs-lookup"><span data-stu-id="41695-111">Step 1.</span></span> <span data-ttu-id="41695-112">Enviar a sua oferta toostaging</span><span class="sxs-lookup"><span data-stu-id="41695-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="41695-113">Enviar a sua oferta toostaging permite-lhe oferta de Olá tootest antes de ficar disponíveis toofuture subscritores.</span><span class="sxs-lookup"><span data-stu-id="41695-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="41695-114">Pode ver como oferta irá aparecer e funcionar os subscrever tooyour dados.</span><span class="sxs-lookup"><span data-stu-id="41695-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="41695-116">Início de sessão para Olá [Portal de publicação](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="41695-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="41695-117">Selecione **serviços de dados** na janela de navegação esquerdo Olá</span><span class="sxs-lookup"><span data-stu-id="41695-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="41695-118">Selecione a sua oferta pretende toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="41695-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="41695-119">Verá Olá acima ecrã.</span><span class="sxs-lookup"><span data-stu-id="41695-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="41695-120">Clique em **Push tooStaging** botão.</span><span class="sxs-lookup"><span data-stu-id="41695-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="41695-121">Se existirem problemas com Olá oferta necessário toobe concluída toostaging toopushing anterior, verá uma lista apresentada.</span><span class="sxs-lookup"><span data-stu-id="41695-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="41695-122">Corrija estes itens clicando em cada item na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="41695-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="41695-123">Quando todas as correções efetuadas, clique em **Push tooStaging** botão novamente.</span><span class="sxs-lookup"><span data-stu-id="41695-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="41695-124">Se existirem sem problemas com a sua oferta verá a janela de pop-up de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="41695-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="41695-125">Se não tiver planeamento/não aprovado toosurface oferta no Portal do Azure (atualmente limitou capacidade), em seguida, janela de pop-up Olá apenas fechar.</span><span class="sxs-lookup"><span data-stu-id="41695-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="41695-126">tootest os dados de serviço no Portal do Azure (no portal do adição toohello DataMarket), terá de tootest um ID de subscrição do Azure com.</span><span class="sxs-lookup"><span data-stu-id="41695-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="41695-127">Este ID de subscrição irá identificar a conta de Olá que será permitido tootest oferta.</span><span class="sxs-lookup"><span data-stu-id="41695-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="41695-128">Cortar e colar o ID de subscrição e clique em Olá toocontinue de marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="41695-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="41695-130">Estes IDs de subscrições do Azure só são necessárias para teste e transição em Olá [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="41695-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="41695-131">Não são necessária tootest no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41695-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="41695-132">Olá aparecimento do ecrã que aparece mostra que a publicação está a decorrer, apresentando Olá "em curso" ícone realçado amarelo abaixo.</span><span class="sxs-lookup"><span data-stu-id="41695-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="41695-133">Enviar toostaging demora entre 10 too15 minutos.</span><span class="sxs-lookup"><span data-stu-id="41695-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="41695-134">Se demora mais, atualize primeiro o seu browser (prima F5 no IE).</span><span class="sxs-lookup"><span data-stu-id="41695-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="41695-135">Em casos raros olá onde a oferta é ainda enviar toostaging depois de uma hora, clique em contactar Olá nos toolet-na saber que existe um problema de ligação.</span><span class="sxs-lookup"><span data-stu-id="41695-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="41695-137">Quando terminar de Olá Push tooStaging Olá "em curso" ícone deixa de mover e Olá será possível atualizar o estado demasiado "teste".</span><span class="sxs-lookup"><span data-stu-id="41695-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="41695-138">Está agora pronto tootest oferta.</span><span class="sxs-lookup"><span data-stu-id="41695-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="41695-139">Passo 2.</span><span class="sxs-lookup"><span data-stu-id="41695-139">Step 2.</span></span> <span data-ttu-id="41695-140">Testar a sua oferta faseada DataMarket</span><span class="sxs-lookup"><span data-stu-id="41695-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="41695-141">Clique em seguinte texto Olá de ligação de Olá **"consulte o seu serviço oferecem em..."**</span><span class="sxs-lookup"><span data-stu-id="41695-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="41695-142">ecrã de Olá toodisplay que Olá subscritor verá quando a sua oferta fica tooproduction e aparecerá na DataMarket.</span><span class="sxs-lookup"><span data-stu-id="41695-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="41695-144">Testar ou certifique-se de que cada um dos itens de 12 Olá marcada acima tooensure todos os logótipos os preços/transações, texto, imagens, documentação e as ligações estão corretos e a funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="41695-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="41695-145">Este é um tooensure boa altura quaisquer valores de teste que introduziu ao criar a sua oferta foram substituídos por valores reais.</span><span class="sxs-lookup"><span data-stu-id="41695-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="41695-146">Logótipo da oferta</span><span class="sxs-lookup"><span data-stu-id="41695-146">Offer logo</span></span>
2. <span data-ttu-id="41695-147">Nome da oferta</span><span class="sxs-lookup"><span data-stu-id="41695-147">Offer name</span></span>
3. <span data-ttu-id="41695-148">Web site da empresa de publicador, nome/link tooyour</span><span class="sxs-lookup"><span data-stu-id="41695-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="41695-149">Categorias de pesquisa para a sua oferta</span><span class="sxs-lookup"><span data-stu-id="41695-149">Search categories for your offer</span></span>
5. <span data-ttu-id="41695-150">Subscritores de tooassist de ligação de suporte da oferta</span><span class="sxs-lookup"><span data-stu-id="41695-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="41695-151">Contextual descrição para a sua oferta</span><span class="sxs-lookup"><span data-stu-id="41695-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="41695-152">Plano de oferta que mostram os detalhes de faturação</span><span class="sxs-lookup"><span data-stu-id="41695-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="41695-153">Ligação tooimplementation código</span><span class="sxs-lookup"><span data-stu-id="41695-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="41695-154">Imagens de exemplo que ilustram a utilização de dados da oferta</span><span class="sxs-lookup"><span data-stu-id="41695-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="41695-155">Metadados de entrada/saída para cada serviço dentro de oferta de Olá</span><span class="sxs-lookup"><span data-stu-id="41695-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="41695-156">Termos do oferta de utilização</span><span class="sxs-lookup"><span data-stu-id="41695-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="41695-157">Pré-visualização de dados da oferta de Olá</span><span class="sxs-lookup"><span data-stu-id="41695-157">Preview of hello offer's data</span></span>

<span data-ttu-id="41695-158">Por fim, verifique o serviço de Olá funcionará através de Olá Datamarket clicando Olá hiperligação "EXPLORAR este conjunto de dados".</span><span class="sxs-lookup"><span data-stu-id="41695-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="41695-159">Irá abrir uma nova janela na ferramenta de Olá chamamos "Explorador de serviço", de modo pode pré-visualizar resultados Olá de uma consulta relativamente ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="41695-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="41695-160">Nesta janela, pode introduzir Olá parâmetros necessitam e ver resultados de Olá apresentados por uma consulta relativamente ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="41695-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="41695-161">Além disso, apresentado é o URL de Olá na sua consulta.</span><span class="sxs-lookup"><span data-stu-id="41695-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="41695-162">Ser se tooreview Olá descrição textual do serviço de Olá apresentada na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="41695-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="41695-163">E se a oferta é composta por mais do que um serviço chamar, clique em Olá nos separadores na Olá inferior tooswitch toohello seguinte serviço tooreview e testar.</span><span class="sxs-lookup"><span data-stu-id="41695-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="41695-164">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="41695-164">Next step</span></span>
<span data-ttu-id="41695-165">Se estiver a ter problemas e precisar de ajuda para resolvê-los contacte [suporte do Editor de Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="41695-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="41695-166">Se estiver satisfeito e toopublish pronto a oferta leia Olá [aprovação do pedido tooPush tooProduction](marketplace-publishing-push-to-production.md) documentação.</span><span class="sxs-lookup"><span data-stu-id="41695-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="41695-167">Veja Também</span><span class="sxs-lookup"><span data-stu-id="41695-167">See Also</span></span>
* [<span data-ttu-id="41695-168">Introdução: Como toopublish toohello uma oferta Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="41695-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

