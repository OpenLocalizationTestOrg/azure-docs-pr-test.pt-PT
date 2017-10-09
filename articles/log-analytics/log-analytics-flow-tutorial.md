---
title: aaaAutomate processa do Log Analytics do Azure com o Microsoft Flow
description: "Saiba como pode utilizar o Microsoft Flow tooquickly automatizar processos repetíveis utilizando o conector do Olá Log Analytics do Azure."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="939a6-103">Automatizar processos de análise de registos com o conector de Olá Flow da Microsoft</span><span class="sxs-lookup"><span data-stu-id="939a6-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="939a6-104">[Microsoft Flow](https://ms.flow.microsoft.com) permite-lhe toocreate automatizada fluxos de trabalho com centenas de ações para uma variedade de serviços.</span><span class="sxs-lookup"><span data-stu-id="939a6-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="939a6-105">Resultado de uma ação pode ser utilizado como entrada tooanother, permitindo-lhe toocreate integração entre diferentes serviços.</span><span class="sxs-lookup"><span data-stu-id="939a6-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="939a6-106">conector do Log Analytics do Azure Olá Microsoft Flow permitem-lhe toobuild fluxos de trabalho que incluem dados obtidos através de pesquisas de registo na análise de registos.</span><span class="sxs-lookup"><span data-stu-id="939a6-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="939a6-107">Por exemplo, pode utilizar dados de análise de registos do Microsoft Flow toouse uma notificação por e-mail a partir do Office 365, criar um erro no Visual Studio Team Services ou publicar uma mensagem Slack.</span><span class="sxs-lookup"><span data-stu-id="939a6-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="939a6-108">Pode acionar um fluxo de trabalho por um agendamento simple ou a partir de qualquer ação num serviço ligado, tais como quando é recebido um e-mail ou um tweet.</span><span class="sxs-lookup"><span data-stu-id="939a6-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="939a6-109">conector de Log Analytics do Azure de Olá Microsoft Flow requer a sua área de trabalho toobe atualizado toohello nova análise de registos a linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="939a6-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="939a6-110">Pode saber mais sobre o novo idioma de Olá e obter Olá procedimento tooupgrade sua área de trabalho em [atualizar a sua pesquisa de registo de toonew de área de trabalho do Log Analytics do Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="939a6-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="939a6-111">tutorial de Olá neste artigo mostra como toocreate um fluxo que envia automaticamente Olá resultados da pesquisa de análise de registos de registo por e-mail, apenas um exemplo de como pode utilizar a análise de registos Flow da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="939a6-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="939a6-112">Passo 1: Criar um fluxo</span><span class="sxs-lookup"><span data-stu-id="939a6-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="939a6-113">A iniciar sessão demasiado[Microsoft Flow](http://flow.microsoft.com)e selecione **flui My**.</span><span class="sxs-lookup"><span data-stu-id="939a6-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="939a6-114">Clique em **+ criar em branco**.</span><span class="sxs-lookup"><span data-stu-id="939a6-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="939a6-115">Passo 2: Criar um acionador para o fluxo</span><span class="sxs-lookup"><span data-stu-id="939a6-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="939a6-116">Clique em **pesquisa centenas de conectores e acionadores**.</span><span class="sxs-lookup"><span data-stu-id="939a6-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="939a6-117">Tipo **agenda** na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="939a6-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="939a6-118">Selecione **agenda**e, em seguida, selecione **agenda - periodicidade**.</span><span class="sxs-lookup"><span data-stu-id="939a6-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="939a6-119">No Olá **frequência** selecione **dia** e no Olá **intervalo** box, introduza **1**.</span><span class="sxs-lookup"><span data-stu-id="939a6-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="939a6-120">![Caixa de diálogo de Acionador de Flow Microsoft](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="939a6-121">Passo 3: Adicionar uma ação de análise de registos</span><span class="sxs-lookup"><span data-stu-id="939a6-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="939a6-122">Clique em **+ novo passo**e, em seguida, clique em **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="939a6-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="939a6-123">Procurar **Iniciar análise**.</span><span class="sxs-lookup"><span data-stu-id="939a6-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="939a6-124">Clique em **Log Analytics do Azure – execute a consulta e visualizar os resultados**.</span><span class="sxs-lookup"><span data-stu-id="939a6-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="939a6-125">![Execute a janela de consulta de análise de registos](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="939a6-126">Passo 4: Configurar a ação de análise de registos de Olá</span><span class="sxs-lookup"><span data-stu-id="939a6-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="939a6-127">Especifique os detalhes de Olá para a sua área de trabalho, incluindo Olá ID de subscrição, grupo de recursos e o nome da área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="939a6-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="939a6-128">Adicionar Olá seguir toohello de consulta de análise de registos **consulta** janela.</span><span class="sxs-lookup"><span data-stu-id="939a6-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="939a6-129">Esta é apenas uma consulta de exemplo e pode substituir qualquer outra que devolve dados.</span><span class="sxs-lookup"><span data-stu-id="939a6-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="939a6-130">Selecione **HTML tabela** para Olá **tipo de gráfico**.</span><span class="sxs-lookup"><span data-stu-id="939a6-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="939a6-131">![Ação de análise do registo](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="939a6-132">Passo 5: Configurar o e-mail de toosend Olá fluxo</span><span class="sxs-lookup"><span data-stu-id="939a6-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="939a6-133">Clique em **novo passo**e, em seguida, clique em **+ adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="939a6-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="939a6-134">Procurar **Outlook do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="939a6-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="939a6-135">Clique em **Office 365 Outlook – enviar um e-mail**.</span><span class="sxs-lookup"><span data-stu-id="939a6-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="939a6-136">![Janela de seleção do Outlook do Office 365](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="939a6-137">Especifique o endereço de correio eletrónico Olá de um destinatário no Olá **para** janela e um assunto de correio eletrónico de Olá no **requerente**.</span><span class="sxs-lookup"><span data-stu-id="939a6-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="939a6-138">Clique em qualquer local no Olá **corpo** caixa.</span><span class="sxs-lookup"><span data-stu-id="939a6-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="939a6-139">A **conteúdo dinâmico** é aberta a janela com os valores das ações de anteriores.</span><span class="sxs-lookup"><span data-stu-id="939a6-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="939a6-140">Selecione **corpo**.</span><span class="sxs-lookup"><span data-stu-id="939a6-140">Select **Body**.</span></span>  <span data-ttu-id="939a6-141">Este é Olá os resultados da consulta Olá Olá ação de análise de registos.</span><span class="sxs-lookup"><span data-stu-id="939a6-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="939a6-142">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="939a6-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="939a6-143">No Olá **é HTML** caixa, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="939a6-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="939a6-144">![Janela de configuração de e-mail do Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="939a6-145">Passo 6: Guardar e testar o fluxo</span><span class="sxs-lookup"><span data-stu-id="939a6-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="939a6-146">No Olá **nome de fluxo** caixa, adicionar um nome para o fluxo e, em seguida, clique em **criar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="939a6-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="939a6-147">![Guardar fluxo](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="939a6-148">fluxo de Olá está agora criado e será executado após um dia em que é a agenda de Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="939a6-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="939a6-149">tooimmediately teste Olá fluxo, clique em **executar agora** e, em seguida, **executar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="939a6-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="939a6-150">![Executar o fluxo](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="939a6-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="939a6-151">Quando o fluxo de Olá estiver concluída, verifique o correio de Olá de destinatário Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="939a6-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="939a6-152">Deve ter recebido uma mensagem com um corpo semelhante toohello seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="939a6-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![E-mail de exemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="939a6-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="939a6-154">Next steps</span></span>

- <span data-ttu-id="939a6-155">Saiba mais sobre [pesquisas de registo na análise de registos](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="939a6-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="939a6-156">Saiba mais sobre [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="939a6-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



