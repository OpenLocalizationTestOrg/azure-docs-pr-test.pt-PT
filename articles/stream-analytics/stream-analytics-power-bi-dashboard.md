---
title: dashboard de BI aaaPower no Azure Stream Analytics | Microsoft Docs
description: "Utilize um em tempo real transmissão em fluxo Power BI dashboard toogather business intelligence e analisar dados de elevado volume de uma tarefa de Stream Analytics."
keywords: "dashboard de análise, dashboard em tempo real"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="4a4ad-104">Stream Analytics e o Power BI: um dashboard de análise em tempo real para transmissão em fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="4a4ad-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="4a4ad-105">O Azure Stream Analytics permite-lhe tootake partido de uma das Olá esquerda ferramentas de business intelligence, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="4a4ad-106">Neste artigo, saiba como criar ferramentas de business intelligence, utilizando o Power BI como uma saída para as tarefas do Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="4a4ad-107">Também saber como toocreate e utilizar um dashboard em tempo real.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="4a4ad-108">Este artigo continua a partir do Olá Stream Analytics [deteção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="4a4ad-109">Isto baseia-se no fluxo de trabalho Olá criado este tutorial e adiciona um Power BI para que pode visualizar as chamadas telefónicas fraudulentas que são detetadas por uma tarefa de análise de transmissão em fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="4a4ad-110">Pode ver [um vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que ilustra este cenário.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4a4ad-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4a4ad-111">Prerequisites</span></span>

<span data-ttu-id="4a4ad-112">Antes de começar, certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="4a4ad-113">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-113">An Azure account.</span></span>
* <span data-ttu-id="4a4ad-114">Uma conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-114">An account for Power BI.</span></span> <span data-ttu-id="4a4ad-115">Pode utilizar uma conta profissional ou de uma conta profissional.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="4a4ad-116">Uma versão completa do Olá [deteção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="4a4ad-117">tutorial de Olá inclui uma aplicação que gera metadados fictícios de atribuição de chamada telefónica.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="4a4ad-118">Tutorial de Olá, pode criar um hub de eventos e enviar Olá hub de eventos de toohello de dados de chamada telefónica de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="4a4ad-119">Escrever uma consulta que Deteta chamadas fraudulentas (chamadas a partir do Olá igual número em Olá mesmo tempo em localizações diferentes).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="4a4ad-120">Adicionar a saída do Power BI</span><span class="sxs-lookup"><span data-stu-id="4a4ad-120">Add Power BI output</span></span>
<span data-ttu-id="4a4ad-121">Tutorial de deteção de fraudes em tempo real de Olá, saída Olá é enviada tooAzure o Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="4a4ad-122">Nesta secção, adicione uma saída que envia informações tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="4a4ad-123">No portal do Azure Olá, abra a tarefa de análise de transmissão em fluxo Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="4a4ad-124">Se utilizou o nome sugerido Olá, tarefa Olá é denominada `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="4a4ad-125">Selecione Olá **saídas** caixa no meio de Olá do dashboard de tarefa Olá e, em seguida, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="4a4ad-126">Para **Alias de saída**, introduza `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="4a4ad-127">Pode utilizar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-127">You can use a different name.</span></span> <span data-ttu-id="4a4ad-128">Se o fizer, tome nota do mesmo, porque tem o nome de Olá mais tarde.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="4a4ad-129">Em **Sink**, selecione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-129">Under **Sink**, select **Power BI**.</span></span>

   ![Criar um resultado para o Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="4a4ad-131">Clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-131">Click **Authorize**.</span></span>

    <span data-ttu-id="4a4ad-132">Abre uma janela onde pode fornecer as suas credenciais do Azure para uma conta escolar ou profissional.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Introduza as credenciais de acesso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="4a4ad-134">Introduza as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-134">Enter your credentials.</span></span> <span data-ttu-id="4a4ad-135">Tenha em atenção, em seguida, quando introduzir as suas credenciais, está também a dar permissão toohello análise de transmissão em fluxo de trabalho tooaccess sua área de Power BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="4a4ad-136">Quando estiver a devolvidos toohello **nova saída** painel, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="4a4ad-137">**Área de trabalho de grupo**: selecione uma área de trabalho no seu inquilino do Power BI onde pretende que o conjunto de dados do toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="4a4ad-138">**Nome do conjunto de dados**: introduza `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="4a4ad-139">Pode utilizar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-139">You can use a different name.</span></span> <span data-ttu-id="4a4ad-140">Se o fizer, anote-lo para utilizar mais tarde.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="4a4ad-141">**Nome de tabela**: introduza `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="4a4ad-142">Atualmente, o resultado de Power BI de tarefas do Stream Analytics pode ter apenas uma tabela num conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Área de trabalho do PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="4a4ad-144">Se o Power BI tem um conjunto de dados e a tabela que tenham Olá mesmos nomes que Olá aqueles que especificou na tarefa de Stream Analytics Olá, Olá existentes será substituído.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="4a4ad-145">Recomendamos que não explicitamente crie este conjunto de dados e a tabela na sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="4a4ad-146">Estes são criados automaticamente quando iniciar a tarefa de Stream Analytics e a tarefa de Olá começa a saída de bombagem para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="4a4ad-147">Se a consulta da tarefa não devolve quaisquer resultados, Olá conjunto de dados e a tabela não são criados.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="4a4ad-148">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-148">Click **Create**.</span></span>

<span data-ttu-id="4a4ad-149">Olá conjunto de dados é criado com Olá seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="4a4ad-150">**defaultRetentionPolicy: BasicFIFO**: os dados são FIFO, com um máximo de 200 000 linhas.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="4a4ad-151">**defaultMode: pushStreaming**: Olá conjunto de dados suporta a transmissão em fluxo de mosaicos e visuais baseados no relatório tradicionais (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="4a4ad-152">Push).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-152">push).</span></span>

<span data-ttu-id="4a4ad-153">Atualmente, não é possível criar conjuntos de dados com outros sinalizadores.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="4a4ad-154">Para obter mais informações sobre conjuntos de dados do Power BI, consulte Olá [API de REST do Power BI](https://msdn.microsoft.com/library/mt203562.aspx) referência.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="4a4ad-155">Escrever Olá consulta</span><span class="sxs-lookup"><span data-stu-id="4a4ad-155">Write hello query</span></span>

1. <span data-ttu-id="4a4ad-156">Fechar Olá **saídas** painel e retorno toohello painel de tarefas.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="4a4ad-157">Clique em Olá **consulta** caixa.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="4a4ad-158">Introduza Olá seguinte de consulta.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-158">Enter hello following query.</span></span> <span data-ttu-id="4a4ad-159">Esta consulta é semelhante toohello associação automática consulta que criou no tutorial de deteção de fraudes Olá.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="4a4ad-160">Olá diferença é que esta consulta envia resultados toohello novo de saída que criou (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="4a4ad-161">Se não nome Olá entrada `CallStream` tutorial de deteção de fraudes Olá, substitua o nome para `CallStream` no Olá **FROM** e **associar** cláusulas na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="4a4ad-162">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="4a4ad-163">Consulta de Olá de teste</span><span class="sxs-lookup"><span data-stu-id="4a4ad-163">Test hello query</span></span>
<span data-ttu-id="4a4ad-164">Esta secção é opcional mas recomendado.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="4a4ad-165">Se a aplicação de TelcoStreaming Olá não está em execução atualmente, inicie-o seguindo estes passos:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="4a4ad-166">Abra uma janela de comando.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-166">Open a command window.</span></span>
    * <span data-ttu-id="4a4ad-167">Aceda a pasta toohello onde são Olá telcogenerator.exe e ficheiros de telcodatagen.exe.config modificadas.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="4a4ad-168">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="4a4ad-169">No Olá **consulta** painel, clique em Olá pontos seguinte toohello `CallStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="4a4ad-170">Especifique que pretende que o visão de três minutos de dados e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="4a4ad-171">Aguarde até que está a notificado de que os dados de Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="4a4ad-172">Clique em **teste** e certifique-se de que está a obter resultados.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="4a4ad-173">Executar tarefa de Olá</span><span class="sxs-lookup"><span data-stu-id="4a4ad-173">Run hello job</span></span>

1. <span data-ttu-id="4a4ad-174">Certifique-se de que aplicações de TelcoStreaming Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="4a4ad-175">Fechar Olá **consulta** painel.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="4a4ad-176">No painel de tarefas Olá, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-176">In hello job blade, click **Start**.</span></span>

    ![Iniciar a tarefa de Stream Analytics Olá](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="4a4ad-178">A tarefa de análise de transmissão em fluxo inicia à procura de chamadas fraudulentas no fluxo de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="4a4ad-179">tarefa de Olá também cria Olá conjunto de dados e tabela no Power BI e começa a enviar dados sobre Olá chamadas fraudulentas toothem.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="4a4ad-180">Criar o dashboard de Olá no Power BI</span><span class="sxs-lookup"><span data-stu-id="4a4ad-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="4a4ad-181">Aceda demasiado[Powerbi.com](https://powerbi.com) e inicie sessão com a sua conta escolar ou profissional.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="4a4ad-182">Se a consulta da tarefa do Stream Analytics Olá produz resultados, verá que o conjunto de dados já está a ser criado:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Conjunto de dados de transmissão em fluxo no Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="4a4ad-184">Na área de trabalho, clique em  **+ &nbsp;criar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![botão para criar Olá na área de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="4a4ad-186">Criar um novo dashboard e dê-lhe nome `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Criar um dashboard e atribua um nome na área de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="4a4ad-188">Na Olá parte superior da janela de Olá, clique em **adicionar mosaico**, selecione **dados de transmissão em fluxo personalizados**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Personalizada conjunto de dados de transmissão em fluxo](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="4a4ad-190">Em **YOUR DATSETS**, selecione o conjunto de dados e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![O conjunto de dados de transmissão em fluxo](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="4a4ad-192">Em **tipo de visualização**, selecione **cartão**e, em seguida, no Olá **campos** lista, selecione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Detalhes de visualização do novo mosaico](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="4a4ad-194">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-194">Click **Next**.</span></span>

8. <span data-ttu-id="4a4ad-195">Preencha os detalhes de mosaico, como um título e subtítulo do.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-195">Fill in tile details like a title and subtitle.</span></span>

    ![Título e subtítulo do novo mosaico](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="4a4ad-197">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-197">Click **Apply**.</span></span>

    <span data-ttu-id="4a4ad-198">Tem agora um contador de fraude!</span><span class="sxs-lookup"><span data-stu-id="4a4ad-198">Now you have a fraud counter!</span></span>

    ![Contador de fraude](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="4a4ad-200">Olá siga os passos novamente tooadd um mosaico (começando com o passo 4).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="4a4ad-201">Neste momento, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-201">This time, do hello following:</span></span>

    * <span data-ttu-id="4a4ad-202">Quando obtiver demasiado**tipo de visualização**, selecione **gráfico de linhas**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="4a4ad-203">Adicionar um eixo e selecione **windowend**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="4a4ad-204">Adicione um valor e selecione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="4a4ad-205">Para **toodisplay de janela de tempo**, selecione Olá últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Criar o mosaico de gráfico de linha](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="4a4ad-207">Clique em **seguinte**, adicionar um título e subtítulo do e, em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="4a4ad-208">dashboard do Power BI Olá agora dá-lhe duas vistas dos dados sobre chamadas fraudulentas como detetado na Olá dados de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Terminou o dashboard do Power BI que mostra dois mosaicos para chamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="4a4ad-210">Mais informações sobre o Power BI</span><span class="sxs-lookup"><span data-stu-id="4a4ad-210">Learn more about Power BI</span></span>

<span data-ttu-id="4a4ad-211">Este tutorial demonstra como toocreate apenas alguns tipos de visualizações para um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="4a4ad-212">Power BI pode ajudar a criar outras ferramentas de cliente business intelligence para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="4a4ad-213">Para obter mais ideias, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="4a4ad-214">Para obter outro exemplo de um dashboard do Power BI, veja Olá [introdução ao Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vídeo.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="4a4ad-215">Para obter mais informações sobre como configurar a análise de transmissão em fluxo de saída tooPower BI tarefa e utilizar grupos de Power BI, reveja Olá [Power BI](stream-analytics-define-outputs.md#power-bi) secção Olá [Stream Analytics produz](stream-analytics-define-outputs.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="4a4ad-216">Para obter informações sobre como utilizar o Power BI geralmente, consulte [Dashboards no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="4a4ad-217">Saiba mais sobre as melhores práticas e limitações</span><span class="sxs-lookup"><span data-stu-id="4a4ad-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="4a4ad-218">Atualmente, Power BI pode ser chamado aproximadamente uma vez por segundo.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="4a4ad-219">Os visuais de transmissão em fluxo suportam pacotes de 15 KB.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="4a4ad-220">Para além disso, os visuais de transmissão em fluxo falharem (mas push continua toowork).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="4a4ad-221">Devido a estas limitações, Power BI presta-se mais naturalmente toocases onde o Azure Stream Analytics does uma redução de carregamento de dados significativos.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="4a4ad-222">Recomendamos que utilize uma janela em cascata ou Hopping janela tooensure push de dados é, no máximo, um push por segundo, e que a consulta lands dentro de requisitos de débito Olá.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="4a4ad-223">Pode utilizar Olá seguir equação toocompute Olá valor toogive a janela em segundos:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="4a4ad-225">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-225">For example:</span></span>

* <span data-ttu-id="4a4ad-226">Terá de 1000 dispositivos enviar dados em intervalos de um segundo.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="4a4ad-227">Estão a utilizar Olá Power BI SKU Pro que suporte 1.000.000 linhas por hora.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="4a4ad-228">Pretende que quantidade de Olá toopublish de dados de média por dispositivo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="4a4ad-229">Como resultado, torna-se equação de Olá:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-229">As a result, hello equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="4a4ad-231">Tendo em conta esta configuração, pode alterar seguinte toohello da consulta original do Olá:</span><span class="sxs-lookup"><span data-stu-id="4a4ad-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="4a4ad-232">Renovar autorização</span><span class="sxs-lookup"><span data-stu-id="4a4ad-232">Renew authorization</span></span>
<span data-ttu-id="4a4ad-233">Se a palavra-passe de Olá tiver sido alterado desde a tarefa foi criada ou pela última vez autenticada, terá de tooreauthenticate sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="4a4ad-234">Se o Azure multi-factor Authentication está configurado no seu inquilino do Azure Active Directory (Azure AD), também tem de autorização de Power BI toorenew em duas semanas.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="4a4ad-235">Se não renovar, pode ver sintomas como uma falta de saída da tarefa ou um `Authenticate user error` nos registos de operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="4a4ad-236">Da mesma forma, se uma tarefa é iniciado depois de Olá token tiver expirado, ocorre um erro e Olá tarefa falhar.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="4a4ad-237">tooresolve este problema, parar a tarefa de Olá que está a executar e aceda tooyour de saída do Power BI.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="4a4ad-238">tooavoid perda de dados, selecione de Olá **renovar autorização** associar e, em seguida, reinicie a tarefa de Olá **hora da última paragem**.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="4a4ad-239">Após ter sido atualizada autorização Olá com o Power BI, um alerta de verde é apresentado no Olá autorização área tooreflect problema Olá foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="4a4ad-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="4a4ad-240">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="4a4ad-240">Get help</span></span>
<span data-ttu-id="4a4ad-241">Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="4a4ad-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a4ad-242">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4a4ad-242">Next steps</span></span>
* [<span data-ttu-id="4a4ad-243">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4a4ad-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4a4ad-244">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4a4ad-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4a4ad-245">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4a4ad-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4a4ad-246">Referência de linguagem de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4a4ad-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4a4ad-247">Referência da API de REST de gestão do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="4a4ad-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
