---
title: "aaaCreate o fluxo de trabalho primeiro entre aplicações em nuvem & serviços em nuvem - Azure Logic Apps | Microsoft Docs"
description: "Crie e execute fluxos de trabalho no Azure Logic Apps para automatizar processos empresariais para cenários de integração de sistemas e integração de aplicações empresariais (EAI)."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "fluxo de trabalho, aplicações na cloud, serviços cloud, processos empresariais, integração de sistemas, integração de aplicações empresariais, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="9df18-104">Criar a sua primeira aplicação de lógica processos de tooautomate de fluxo de trabalho entre aplicações em nuvem e de serviços cloud</span><span class="sxs-lookup"><span data-stu-id="9df18-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="9df18-105">Sem que seja necessário escrever qualquer código, pode automatizar processos empresariais mais fácil e rapidamente se criar e executar fluxos de trabalho com o [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9df18-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="9df18-106">Este primeiro exemplo mostra como toocreate um fluxo de trabalho de aplicação lógica básica que verifica um RSS feed para novo conteúdo num Web site.</span><span class="sxs-lookup"><span data-stu-id="9df18-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="9df18-107">Quando novos itens de aparecem no feed do Web site Olá, a aplicação de lógica de Olá envia e-mail de uma conta do Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="9df18-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="9df18-108">toocreate e execute uma aplicação lógica, terá destes itens:</span><span class="sxs-lookup"><span data-stu-id="9df18-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="9df18-109">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9df18-109">An Azure subscription.</span></span> <span data-ttu-id="9df18-110">Se não tiver uma subscrição, pode [começar com uma conta do Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9df18-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="9df18-111">Caso contrário, pode [inscrever-se numa subscrição Pay As You Go](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="9df18-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="9df18-112">A subscrição do Azure é utilizada para faturar a utilização da aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="9df18-113">Saiba como funciona a [medição da utilização](../logic-apps/logic-apps-pricing.md) e os [preços](https://azure.microsoft.com/pricing/details/logic-apps) no Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="9df18-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="9df18-114">Além disso, este exemplo requer os itens seguintes</span><span class="sxs-lookup"><span data-stu-id="9df18-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="9df18-115">Uma conta do Outlook.com, do Office 365 Outlook ou do Gmail</span><span class="sxs-lookup"><span data-stu-id="9df18-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="9df18-116">Se tiver uma [conta Microsoft](https://account.microsoft.com/account) pessoal, também tem uma conta do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="9df18-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="9df18-117">Caso contrário, se tiver uma conta escolar ou profissional do Azure, tem uma conta do **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="9df18-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="9df18-118">Um tooa de ligação do feed RSS do Web site.</span><span class="sxs-lookup"><span data-stu-id="9df18-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="9df18-119">Este exemplo utiliza Olá [RSS para stories superiores do feed do Web site de CNN.com Olá](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="9df18-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="9df18-120">Adicionar um acionador que inicia o fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="9df18-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="9df18-121">A [ *acionador* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia o fluxo de trabalho de aplicação de lógica e é o primeiro item de Olá que necessita da sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="9df18-122">Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="9df18-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="9df18-123">No menu à esquerda Olá, escolha **novo** > **integração empresarial com** > **aplicação lógica** conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="9df18-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portal do Azure, Novo, Integração Empresarial, Aplicação Lógica](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="9df18-125">Também pode optar por **novo**, em seguida, na caixa de pesquisa de Olá, escreva `logic app`, e prima Enter.</span><span class="sxs-lookup"><span data-stu-id="9df18-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="9df18-126">Em seguida, escolha **Aplicação Lógica** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="9df18-127">Dê um nome à aplicação lógica e selecione a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9df18-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="9df18-128">Agora, crie ou selecione um grupo de recursos do Azure, que o ajuda a organizar e gerir recursos do Azure relacionados.</span><span class="sxs-lookup"><span data-stu-id="9df18-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="9df18-129">Por fim, selecione a localização do Centro de dados de Olá para alojar a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="9df18-130">Quando estiver pronto, selecione **Pin toodashboard** e, em seguida, **criar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Detalhes da aplicação lógica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="9df18-132">Quando seleciona **Pin toodashboard**, a aplicação lógica aparece no Olá dashboard do Azure após a implementação e abre-se automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9df18-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="9df18-133">Se a sua aplicação lógica não aparece no dashboard de Olá, no Olá **todos os recursos** mosaico, escolha **Consulte mais**e selecione a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="9df18-134">Ou no menu à esquerda Olá, escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="9df18-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="9df18-135">Em **Integração Empresarial**, escolha **Aplicações Lógicas** e selecione a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="9df18-136">Quando abre pela primeira vez a sua aplicação lógica para Olá, Olá Designer de aplicação lógica mostra modelos que pode utilizar tooget foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="9df18-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="9df18-137">Por agora, escolha **Aplicação Lógica Vazia**, para que possa criá-la do zero.</span><span class="sxs-lookup"><span data-stu-id="9df18-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="9df18-138">Olá Designer de aplicação lógica abre-se e mostra os serviços disponíveis e *acionadores* que pode utilizar na sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="9df18-139">Na caixa de pesquisa de Olá, escreva `RSS`e selecione este acionador: **RSS - quando um item de feed é publicado**</span><span class="sxs-lookup"><span data-stu-id="9df18-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Acionador RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="9df18-141">Introduza a ligação de Olá feed do Web site Olá RSS que pretende que o tootrack.</span><span class="sxs-lookup"><span data-stu-id="9df18-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="9df18-142">Também pode alterar a **Frequência** e o **Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="9df18-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="9df18-143">Estas definições determinam a frequência com que a aplicação lógica verifica novos itens e devolve todos os itens encontrados durante esse intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="9df18-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="9df18-144">Neste exemplo, vamos verifique todos os dias para stories superiores publicados Web site CNN toohello.</span><span class="sxs-lookup"><span data-stu-id="9df18-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Configurar o acionador com o feed RSS, a frequência e o intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="9df18-146">Guarde o seu trabalho por agora.</span><span class="sxs-lookup"><span data-stu-id="9df18-146">Save your work for now.</span></span> <span data-ttu-id="9df18-147">(Na barra de comando estruturador Olá, escolha **guardar**.)</span><span class="sxs-lookup"><span data-stu-id="9df18-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Guardar a aplicação lógica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="9df18-149">Quando guardar, a sua aplicação lógica vai em direto, mas atualmente, a aplicação lógica só verifica a existência de novos itens na Olá especificado RSS feed.</span><span class="sxs-lookup"><span data-stu-id="9df18-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="9df18-150">Neste exemplo mais útil, que vamos adicionar uma ação que executa a sua aplicação lógica após o acionador toomake é acionado.</span><span class="sxs-lookup"><span data-stu-id="9df18-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="9df18-151">Adicionar uma ação que responde tooyour acionador</span><span class="sxs-lookup"><span data-stu-id="9df18-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="9df18-152">Uma [*ação*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa realizada pelo fluxo de trabalho da sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="9df18-153">Depois de adicionar uma aplicação de lógica do acionador tooyour, pode adicionar operações de tooperform uma ação com dados gerados pelo que trigger.</span><span class="sxs-lookup"><span data-stu-id="9df18-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="9df18-154">Para o nosso exemplo, iremos agora adicionar uma ação que envia correio eletrónico quando novos itens são apresentados no feed RSS do Web site Olá.</span><span class="sxs-lookup"><span data-stu-id="9df18-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="9df18-155">No estruturador de Olá, sob o acionador, escolha **novo passo** > **adicionar uma ação** conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="9df18-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Adicionar uma ação](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="9df18-157">Olá designer mostra [conectores disponíveis](../connectors/apis-list.md) , de modo a que possa selecionar uma ação tooperform quando o acionador é acionado.</span><span class="sxs-lookup"><span data-stu-id="9df18-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="9df18-158">Com base na sua conta de e-mail, siga os passos de Olá para o Outlook ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="9df18-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="9df18-159">Introduza toosend e-mail da sua conta do Outlook, na caixa de pesquisa de Olá, `outlook`.</span><span class="sxs-lookup"><span data-stu-id="9df18-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="9df18-160">Em **Serviços**, escolha **Outlook.com**, para contas Microsoft pessoais, ou **Office 365 Outlook**, para contas escolares ou profissionais do Azure.</span><span class="sxs-lookup"><span data-stu-id="9df18-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="9df18-161">Em **Ações**, selecione **Enviar e-mail**.</span><span class="sxs-lookup"><span data-stu-id="9df18-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selecionar a ação "Enviar e-mail" do Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="9df18-163">Introduza toosend e-mail da sua conta do Gmail, na caixa de pesquisa de Olá, `gmail`.</span><span class="sxs-lookup"><span data-stu-id="9df18-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="9df18-164">Em **Ações**, selecione **Enviar e-mail**.</span><span class="sxs-lookup"><span data-stu-id="9df18-164">Under **Actions**, select **Send email**.</span></span>

       ![Escolher "Gmail - Enviar e-mail”](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="9df18-166">Quando lhe for pedida credenciais, inicie sessão com Olá nome de utilizador e palavra-passe para a sua conta de e-mail.</span><span class="sxs-lookup"><span data-stu-id="9df18-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="9df18-167">Forneça detalhes de Olá para esta ação, como o endereço de correio eletrónico de destino Olá e escolha os parâmetros de Olá para Olá tooinclude de dados no e-mail de Olá, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9df18-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Selecione os dados tooinclude por correio eletrónico](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="9df18-169">Por isso, se optou pelo Outlook, a sua aplicação lógica poderá ser semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9df18-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Aplicação lógica concluída](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="9df18-171">Guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="9df18-171">Save your changes.</span></span> <span data-ttu-id="9df18-172">(Na barra de comando estruturador Olá, escolha **guardar**.)</span><span class="sxs-lookup"><span data-stu-id="9df18-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="9df18-173">Pode agora executar manualmente a sua aplicação lógica para testes.</span><span class="sxs-lookup"><span data-stu-id="9df18-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="9df18-174">Na barra de comando estruturador Olá, escolha **executar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="9df18-175">Caso contrário, pode permitir que a aplicação lógica, certifique-se Olá especificado feed RSS com base numa agenda Olá que configurou.</span><span class="sxs-lookup"><span data-stu-id="9df18-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="9df18-176">Se a sua aplicação lógica localiza novos itens, a aplicação de lógica de Olá envia correio eletrónico que inclui os dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="9df18-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="9df18-177">Se não for encontrados nenhuma novos itens, a sua aplicação lógica ignora ação Olá que envia correio eletrónico.</span><span class="sxs-lookup"><span data-stu-id="9df18-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="9df18-178">toomonitor e verifique a sua aplicação lógica do executar e acionar o histórico de, no menu aplicação lógica, escolha **descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="9df18-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitorizar e ver o histórico de execuções e acionadores da aplicação lógica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="9df18-180">Se não encontrar dados Olá que espera que, na barra de comando Olá, tente escolher **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="9df18-181">mais sobre o estado da sua aplicação lógica toolearn ou execute e acionar histórico ou toodiagnose a sua aplicação lógica, consulte [resolver problemas da aplicação lógica](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="9df18-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="9df18-182">A aplicação lógica continua a ser executada até que a desative.</span><span class="sxs-lookup"><span data-stu-id="9df18-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="9df18-183">Escolha tooturn desativar a aplicação por agora, no menu aplicação lógica, **descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="9df18-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="9df18-184">Na barra de comando Olá, escolha **desativar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="9df18-185">Parabéns! Acabou de configurar e executar a sua primeira aplicação lógica básica.</span><span class="sxs-lookup"><span data-stu-id="9df18-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="9df18-186">Também ficou a saber como pode criar facilmente fluxos de trabalho que automatizam processos e integram aplicações na cloud e serviços cloud, tudo sem ter de escrever código.</span><span class="sxs-lookup"><span data-stu-id="9df18-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="9df18-187">Gerir a aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="9df18-187">Manage your logic app</span></span>

<span data-ttu-id="9df18-188">toomanage a aplicação, pode realizar tarefas como verificar o estado de Olá, editar, ver o histórico, desativar ou eliminar a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="9df18-189">Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="9df18-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="9df18-190">No menu à esquerda Olá, escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="9df18-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="9df18-191">Em **Integração Empresarial**, escolha **Aplicações Lógicas**.</span><span class="sxs-lookup"><span data-stu-id="9df18-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="9df18-192">Selecione a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="9df18-192">Select your logic app.</span></span> 

   <span data-ttu-id="9df18-193">No menu de aplicação de lógica de Olá, pode encontrar estas tarefas de gestão de aplicação lógica:</span><span class="sxs-lookup"><span data-stu-id="9df18-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="9df18-194">Tarefa</span><span class="sxs-lookup"><span data-stu-id="9df18-194">Task</span></span>|<span data-ttu-id="9df18-195">Passos</span><span class="sxs-lookup"><span data-stu-id="9df18-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="9df18-196">Ver o estado da aplicação, o histórico de execuções e informações gerais</span><span class="sxs-lookup"><span data-stu-id="9df18-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="9df18-197">Escolha **Descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="9df18-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="9df18-198">Editar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="9df18-198">Edit your app</span></span> | <span data-ttu-id="9df18-199">Escolha **Estruturador da Aplicação Lógica**.</span><span class="sxs-lookup"><span data-stu-id="9df18-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="9df18-200">Ver a definição de JSON do fluxo de trabalho da aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="9df18-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="9df18-201">Escolha **Vista de Código da Aplicação Lógica**.</span><span class="sxs-lookup"><span data-stu-id="9df18-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="9df18-202">Ver operações realizadas na aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="9df18-202">View operations performed on your logic app</span></span> | <span data-ttu-id="9df18-203">Escolha **Registo de atividades**.</span><span class="sxs-lookup"><span data-stu-id="9df18-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="9df18-204">Ver as versões passadas da aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="9df18-204">View past versions for your logic app</span></span> | <span data-ttu-id="9df18-205">Escolha **Versões**.</span><span class="sxs-lookup"><span data-stu-id="9df18-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="9df18-206">Desativar temporariamente a aplicação</span><span class="sxs-lookup"><span data-stu-id="9df18-206">Turn off your app temporarily</span></span> | <span data-ttu-id="9df18-207">Escolha **descrição geral**, em seguida, na barra de comando Olá, escolha **desativar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="9df18-208">Eliminar a aplicação</span><span class="sxs-lookup"><span data-stu-id="9df18-208">Delete your app</span></span> | <span data-ttu-id="9df18-209">Escolha **descrição geral**, em seguida, na barra de comando Olá, escolha **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="9df18-210">Introduza o nome da sua aplicação lógica e selecione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9df18-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="9df18-211">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="9df18-211">Get help</span></span>

<span data-ttu-id="9df18-212">perguntas tooask, responda às perguntas e saiba que outras Azure Logic Apps os utilizadores estão a fazer, visite Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="9df18-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="9df18-213">toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador do Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="9df18-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9df18-214">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9df18-214">Next steps</span></span>

*  [<span data-ttu-id="9df18-215">Adicionar condições e executar fluxos de trabalho</span><span class="sxs-lookup"><span data-stu-id="9df18-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="9df18-216">Modelos de aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="9df18-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  <span data-ttu-id="9df18-217">[Create logic apps from Azure Resource Manager templates](../logic-apps/logic-apps-arm-provision.md) (Criar aplicações lógicas a partir de modelos do Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="9df18-217">[Create logic apps from Azure Resource Manager templates](../logic-apps/logic-apps-arm-provision.md)</span></span>
