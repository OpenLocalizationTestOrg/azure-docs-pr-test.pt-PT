---
title: aaaAutomate Azure Application Insights processa utilizando as Logic Apps.
description: "Saiba como rapidamente pode automatizar processos repetíveis, adicionando a aplicação de lógica de tooyour do Olá Application Insights conector."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="93f86-103">Automatizar processos de Application Insights utilizando as Logic Apps</span><span class="sxs-lookup"><span data-stu-id="93f86-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="93f86-104">Localizar sozinho repetidamente executar Olá mesmas consultas no seu toocheck de dados de telemetria se o serviço está a funcionar corretamente?</span><span class="sxs-lookup"><span data-stu-id="93f86-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="93f86-105">É procura o tooautomate estas consultas para localizar tendências e anomalias e, em seguida, criar os seus fluxos de trabalho em torno deles? conector do Azure Application Insights (pré-visualização) Olá para aplicações lógicas é ferramenta certa Olá para esta finalidade.</span><span class="sxs-lookup"><span data-stu-id="93f86-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="93f86-106">Esta integração, pode automatizar processos várias sem ter de escrever uma única linha de código.</span><span class="sxs-lookup"><span data-stu-id="93f86-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="93f86-107">Pode criar uma aplicação lógica com Olá Application Insights conector tooquickly automatizar qualquer processo do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="93f86-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="93f86-108">Pode adicionar, bem como as ações adicionais.</span><span class="sxs-lookup"><span data-stu-id="93f86-108">You can add additional actions as well.</span></span> <span data-ttu-id="93f86-109">funcionalidade de Logic Apps Olá do App Service do Azure disponibiliza a centenas de ações.</span><span class="sxs-lookup"><span data-stu-id="93f86-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="93f86-110">Por exemplo, utilizando uma aplicação lógica, pode automaticamente enviar uma notificação por e-mail ou criar um erro no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="93f86-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="93f86-111">Também pode utilizar um dos Olá muitas disponíveis [modelos](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp acelerar o processo de Olá de criar a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="93f86-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="93f86-112">Criar uma aplicação lógica para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="93f86-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="93f86-113">Neste tutorial, saiba como toocreate uma aplicação lógica que utiliza Olá análise autocluster algoritmo toogroup atributos nos dados de Olá para uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="93f86-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="93f86-114">fluxo de Olá envia automaticamente resultados Olá por e-mail, apenas um exemplo de como pode utilizar o Application Insights Analytics e Logic Apps em conjunto.</span><span class="sxs-lookup"><span data-stu-id="93f86-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="93f86-115">Passo 1: Criar uma aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="93f86-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="93f86-116">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93f86-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="93f86-117">No Olá **novo** painel, selecione **Web + móvel**e, em seguida, selecione **aplicação lógica**.</span><span class="sxs-lookup"><span data-stu-id="93f86-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Nova janela de aplicação lógica](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="93f86-119">Passo 2: Criar um acionador para a sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="93f86-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="93f86-120">No Olá **Designer de aplicação lógica** janela em **começar com um acionador comuns**, selecione **periodicidade**.</span><span class="sxs-lookup"><span data-stu-id="93f86-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Janela do estruturador de aplicação lógica](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="93f86-122">No Olá **frequência** caixa, selecione **dia** e, em seguida, no Olá **intervalo** caixa, escreva **1**.</span><span class="sxs-lookup"><span data-stu-id="93f86-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Designer de aplicação lógica "Recurrence" janela](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="93f86-124">Passo 3: Adicionar uma ação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="93f86-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="93f86-125">Clique em **novo passo**e, em seguida, clique em **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="93f86-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="93f86-126">No Olá **escolher uma ação** caixa de pesquisa, escreva **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="93f86-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="93f86-127">Em **ações**, clique em **pré-visualização de consulta do Azure Application Insights – análise visualizar**.</span><span class="sxs-lookup"><span data-stu-id="93f86-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    !["Escolher uma ação" janela do Designer de aplicação lógica](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="93f86-129">Passo 4: Ligar o recurso do Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="93f86-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="93f86-130">toocomplete neste passo, precisará de uma ID da aplicação e uma chave de API para o seu recurso.</span><span class="sxs-lookup"><span data-stu-id="93f86-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="93f86-131">Pode obtê-los de Olá portal do Azure, conforme mostrado no Olá diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="93f86-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID da aplicação Olá portal do Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="93f86-133">Forneça um nome para a ligação, o ID da aplicação Olá e a chave de API de Olá.</span><span class="sxs-lookup"><span data-stu-id="93f86-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Janela de ligação de fluxo de Designer da aplicação lógica](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="93f86-135">Passo 5: Especificar Olá consulta de análise e tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="93f86-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="93f86-136">No seguinte exemplo de Olá, consulta Olá seleciona Olá falhada pedidos dentro Olá último dia e está correlacionada com exceções que ocorreram como parte da operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="93f86-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="93f86-137">Análise de está correlacionada com pedidos de Olá falhou, com base no identificador de operation_Id Olá.</span><span class="sxs-lookup"><span data-stu-id="93f86-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="93f86-138">consulta de Olá segmenta, em seguida, resultados de Olá utilizando Olá autocluster algoritmo.</span><span class="sxs-lookup"><span data-stu-id="93f86-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="93f86-139">Quando criar as suas próprias consultas, certifique-se de que estão a funcionar corretamente no Analytics antes de o adicionar tooyour fluxo.</span><span class="sxs-lookup"><span data-stu-id="93f86-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="93f86-140">No Olá **consulta** caixa, adicione a seguinte consulta de análise de Olá:</span><span class="sxs-lookup"><span data-stu-id="93f86-140">In hello **Query** box, add hello following Analytics query:</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. <span data-ttu-id="93f86-141">No Olá **tipo de gráfico** caixa, selecione **Html tabela**.</span><span class="sxs-lookup"><span data-stu-id="93f86-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Janela de configuração de consulta de análise](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="93f86-143">Passo 6: Configurar o e-mail de toosend de aplicação de lógica de Olá</span><span class="sxs-lookup"><span data-stu-id="93f86-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="93f86-144">Clique em **novo passo**e, em seguida, selecione **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="93f86-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="93f86-145">Na caixa de pesquisa de Olá, escreva **Outlook do Office 365**.</span><span class="sxs-lookup"><span data-stu-id="93f86-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="93f86-146">Clique em **Office 365 Outlook – enviar um e-mail**.</span><span class="sxs-lookup"><span data-stu-id="93f86-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Seleção de Outlook do Office 365](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="93f86-148">No Olá **enviar um e-mail** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="93f86-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="93f86-149">a.</span><span class="sxs-lookup"><span data-stu-id="93f86-149">a.</span></span> <span data-ttu-id="93f86-150">Escreva o endereço de e-mail Olá do destinatário Olá.</span><span class="sxs-lookup"><span data-stu-id="93f86-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="93f86-151">b.</span><span class="sxs-lookup"><span data-stu-id="93f86-151">b.</span></span> <span data-ttu-id="93f86-152">Escreva um assunto de correio eletrónico de Olá.</span><span class="sxs-lookup"><span data-stu-id="93f86-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="93f86-153">c.</span><span class="sxs-lookup"><span data-stu-id="93f86-153">c.</span></span> <span data-ttu-id="93f86-154">Clique em qualquer local no Olá **corpo** caixa e, em seguida, no Olá dinâmica conteúdo menu que se abre no Olá direito, selecione **corpo**.</span><span class="sxs-lookup"><span data-stu-id="93f86-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="93f86-155">d.</span><span class="sxs-lookup"><span data-stu-id="93f86-155">d.</span></span> <span data-ttu-id="93f86-156">Clique em **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="93f86-156">Click **Show advanced options**.</span></span>

      ![Configuração do Outlook do Office 365](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="93f86-158">No menu de conteúdo dinâmico de Olá, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="93f86-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="93f86-159">a.</span><span class="sxs-lookup"><span data-stu-id="93f86-159">a.</span></span> <span data-ttu-id="93f86-160">Selecione **nome do anexo**.</span><span class="sxs-lookup"><span data-stu-id="93f86-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="93f86-161">b.</span><span class="sxs-lookup"><span data-stu-id="93f86-161">b.</span></span> <span data-ttu-id="93f86-162">Selecione **anexo conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="93f86-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="93f86-163">c.</span><span class="sxs-lookup"><span data-stu-id="93f86-163">c.</span></span> <span data-ttu-id="93f86-164">No Olá **é HTML** caixa, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="93f86-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Ecrã de configuração de e-mail do Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="93f86-166">Passo 7: Guardar e testar a sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="93f86-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="93f86-167">Clique em **guardar** toosave as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="93f86-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="93f86-168">Pode aguardar a aplicação de lógica Olá acionador toorun Olá, ou pode executar imediatamente aplicação de lógica de Olá selecionando **executar**.</span><span class="sxs-lookup"><span data-stu-id="93f86-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Ecrã de criação de aplicação lógica](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="93f86-170">Quando é executada a sua aplicação lógica, os destinatários Olá especificado na lista de correio eletrónico Olá irão receber um e-mail que se assemelha Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="93f86-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Mensagem de correio eletrónico de aplicação lógica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="93f86-172">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="93f86-172">Next steps</span></span>

- <span data-ttu-id="93f86-173">Saiba mais sobre como criar [as consultas de análises](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="93f86-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="93f86-174">Saiba mais sobre [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="93f86-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





