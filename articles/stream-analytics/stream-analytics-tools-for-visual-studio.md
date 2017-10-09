---
title: aaaUse Azure Stream Analytics Tools para Visual Studio | Microsoft Docs
description: "Tutorial de introdução para Olá Azure Stream Analytics Tools para Visual Studio"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="6606b-104">Utilizar o Azure Stream Analytics Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6606b-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="6606b-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="6606b-105">Introduction</span></span>
<span data-ttu-id="6606b-106">Neste tutorial, saiba como toouse Azure Stream Analytics Tools para Visual Studio toocreate, criar, testar localmente, gerir e depurar as tarefas do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="6606b-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="6606b-107">Depois de concluir este tutorial, será capaz de:</span><span class="sxs-lookup"><span data-stu-id="6606b-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="6606b-108">Familiarize com o Stream Analytics Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6606b-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="6606b-109">Configurar e implementar uma tarefa de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="6606b-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="6606b-110">Teste a sua tarefa localmente com dados de exemplo local.</span><span class="sxs-lookup"><span data-stu-id="6606b-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="6606b-111">Utilize monitorização tootroubleshoot problemas.</span><span class="sxs-lookup"><span data-stu-id="6606b-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="6606b-112">Exporte tooprojects de tarefas existente.</span><span class="sxs-lookup"><span data-stu-id="6606b-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6606b-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6606b-113">Prerequisites</span></span>
<span data-ttu-id="6606b-114">toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="6606b-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="6606b-115">Conclua os passos de Olá que preceder "Criar uma tarefa de Stream Analytics" no Olá [criar uma solução de IoT utilizando o tutorial do Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="6606b-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="6606b-116">Utilize o Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="6606b-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="6606b-117">Enterprise (Ultimate/Premium), Professional e Community são suportadas as edições.</span><span class="sxs-lookup"><span data-stu-id="6606b-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="6606b-118">Não é suportada a edição Express.</span><span class="sxs-lookup"><span data-stu-id="6606b-118">Express edition is not supported.</span></span> <span data-ttu-id="6606b-119">Visual Studio 2017 não é suportada.</span><span class="sxs-lookup"><span data-stu-id="6606b-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="6606b-120">Olá de utilização do Azure SDK para .NET versão 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6606b-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="6606b-121">Instalá-lo utilizando Olá [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="6606b-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="6606b-122">Instalar Olá [Stream Analytics Tools para Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="6606b-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="6606b-123">Criar um projeto do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="6606b-124">No Visual Studio, clique em Olá **ficheiro** menu e selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="6606b-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="6606b-125">Na lista de modelos de Olá Olá esquerda, selecione **Stream Analytics** e, em seguida, clique em **aplicação do Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6606b-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="6606b-126">Introduza o projeto de Olá **nome**, **localização**, e **nome da solução** para outros projetos.</span><span class="sxs-lookup"><span data-stu-id="6606b-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Nova janela do projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="6606b-128">A **utilização** projeto é gerado no **Explorador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="6606b-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Utilização projeto gerado no Explorador de soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="6606b-130">Selecione a subscrição correta Olá</span><span class="sxs-lookup"><span data-stu-id="6606b-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="6606b-131">No Visual Studio, clique em Olá **vista** menu e abra **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="6606b-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="6606b-132">Inicie sessão com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6606b-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="6606b-133">Definir origens de entrada Olá</span><span class="sxs-lookup"><span data-stu-id="6606b-133">Define hello input sources</span></span>
1.  <span data-ttu-id="6606b-134">No **Explorador de soluções**, expanda Olá **entradas** nós e mudar o nome **Input** demasiado**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="6606b-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="6606b-135">Faça duplo clique em **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="6606b-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="6606b-136">Olá **Alias de entrada** está agora **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="6606b-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="6606b-137">alias de Olá de entrada é utilizada no script de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="6606b-138">No **tipo de origem**, selecione **fluxo de dados**.</span><span class="sxs-lookup"><span data-stu-id="6606b-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="6606b-139">No **origem**, selecione **Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="6606b-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="6606b-140">No **espaço de nomes do Service Bus**, selecione Olá **TollData** opção.</span><span class="sxs-lookup"><span data-stu-id="6606b-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="6606b-141">No **nome do Hub de eventos**, selecione **entrada**.</span><span class="sxs-lookup"><span data-stu-id="6606b-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="6606b-142">No **nome de política do Hub de eventos**, selecione **RootManageSharedAccessKey** (Olá o valor predefinido).</span><span class="sxs-lookup"><span data-stu-id="6606b-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="6606b-143">No **formato de serialização de eventos**, selecione **Json**.</span><span class="sxs-lookup"><span data-stu-id="6606b-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="6606b-144">No **codificação**, selecione **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="6606b-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="6606b-145">As definições devem aspeto Olá captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="6606b-145">Your settings should look like hello following screenshot:</span></span>

    ![Janela de entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="6606b-147">Assistente de Olá toofinish, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="6606b-148">Agora pode adicionar outro fluxo de saída do Olá toocreate origem de entrada.</span><span class="sxs-lookup"><span data-stu-id="6606b-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="6606b-149">Contexto Olá **entradas** nós e selecione **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="6606b-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="6606b-151">Na janela de Olá, selecione **Azure Stream Analytics entrada**e alterar Olá **nome** demasiado**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="6606b-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="6606b-152">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-152">Click **Add**.</span></span>

    ![Adicionar Novo Item janela](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="6606b-154">Faça duplo clique em **ExitStream.json** no projeto Olá e Olá siga os mesmos passos como fez para o fluxo de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="6606b-155">Ser tooenter se **sair** para Olá **nome do Hub de eventos** conforme mostrado na seguinte captura de ecrã de Olá:</span><span class="sxs-lookup"><span data-stu-id="6606b-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Janela de ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="6606b-157">Agora que definiu dois fluxos de entrada:</span><span class="sxs-lookup"><span data-stu-id="6606b-157">Now you have defined two input streams:</span></span>

    ![Fluxos de entrada de entrada e saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="6606b-159">Em seguida, adicione a entrada de dados de referência para o ficheiro de blob Olá que contém dados de registo carro.</span><span class="sxs-lookup"><span data-stu-id="6606b-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="6606b-160">Contexto Olá **entradas** no projeto Olá e, em seguida, Olá siga os mesmos passos como fez para entradas de fluxo de Olá nó.</span><span class="sxs-lookup"><span data-stu-id="6606b-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="6606b-161">No **Alias de entrada**, introduza **registo**e, em **tipo de origem**, selecione **referência a dados**.</span><span class="sxs-lookup"><span data-stu-id="6606b-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Janela de registo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="6606b-163">No **conta de armazenamento**, selecione Olá **tolldata** opção.</span><span class="sxs-lookup"><span data-stu-id="6606b-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="6606b-164">No **contentor**, selecione **tolldata**e, em **padrão do caminho**, introduza **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="6606b-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="6606b-165">Este nome de ficheiro é sensível a maiúsculas e minúsculas e deve estar em minúscula.</span><span class="sxs-lookup"><span data-stu-id="6606b-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="6606b-166">Assistente de Olá toofinish, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="6606b-167">Agora todas as entradas de Olá são definidas.</span><span class="sxs-lookup"><span data-stu-id="6606b-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="6606b-168">Definir a saída de Olá</span><span class="sxs-lookup"><span data-stu-id="6606b-168">Define hello output</span></span>
1.  <span data-ttu-id="6606b-169">No **Explorador de soluções**, expanda Olá **entradas** nós e faça duplo clique **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="6606b-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="6606b-170">No **Alias de saída**, introduza **saída**.</span><span class="sxs-lookup"><span data-stu-id="6606b-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="6606b-171">No **Sink**, selecione **base de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="6606b-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="6606b-172">No **base de dados**, selecione **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="6606b-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="6606b-173">No **nome de utilizador**, introduza **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="6606b-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="6606b-174">No **palavra-passe**, introduza **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="6606b-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="6606b-175">No **tabela**, introduza **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="6606b-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="6606b-176">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-176">Click **Save**.</span></span>

    ![Janela de saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="6606b-178">Criar uma consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="6606b-179">Este tutorial tenta tooanswer várias questões empresariais a que os dados tootoll relacionados.</span><span class="sxs-lookup"><span data-stu-id="6606b-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="6606b-180">É também constrói as consultas de análises de fluxo que podem ser utilizadas em respostas relevantes do Stream Analytics tooprovide.</span><span class="sxs-lookup"><span data-stu-id="6606b-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="6606b-181">Antes de iniciar a tarefa de Stream Analytics primeiro, vamos explorar uma sintaxe de consulta cenário e Olá simple.</span><span class="sxs-lookup"><span data-stu-id="6606b-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="6606b-182">Introdução toohello idioma de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="6606b-183">Imaginemos que tem de toocount Olá diversas veículos que introduza uma booth de utilização.</span><span class="sxs-lookup"><span data-stu-id="6606b-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="6606b-184">Uma vez neste exemplo é um fluxo contínuo de eventos, terá de toodefine um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="6606b-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="6606b-185">Modificar Olá pergunta toobe "veículos quantos introduza uma booth de utilização a cada três minutos?"</span><span class="sxs-lookup"><span data-stu-id="6606b-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="6606b-186">Este toocount de forma dados são frequentemente referido tooas Olá em cascata contagem.</span><span class="sxs-lookup"><span data-stu-id="6606b-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="6606b-187">Observe a consulta de Stream Analytics Olá que responde a esta pergunta:</span><span class="sxs-lookup"><span data-stu-id="6606b-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="6606b-188">Do Stream Analytics utiliza uma linguagem de consulta que é como o SQL e adiciona alguns extensões toospecify relacionados com o tempo aspetos da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="6606b-189">Para obter mais informações, consulte [tempo gestão](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [modos de janela](https://msdn.microsoft.com/library/azure/dn835019.aspx) construções utilizadas numa consulta Olá da MSDN.</span><span class="sxs-lookup"><span data-stu-id="6606b-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="6606b-190">Agora que tem de escrever a primeira consulta do Stream Analytics, é tempo tootest-lo.</span><span class="sxs-lookup"><span data-stu-id="6606b-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="6606b-191">Utilize ficheiros de dados de exemplo de Olá localizados na pasta TollApp no Olá seguinte caminho:</span><span class="sxs-lookup"><span data-stu-id="6606b-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="6606b-192">.. \TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="6606b-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="6606b-193">Esta pasta contém Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="6606b-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="6606b-194">Entry.JSON</span><span class="sxs-lookup"><span data-stu-id="6606b-194">Entry.json</span></span>
*   <span data-ttu-id="6606b-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="6606b-195">Exit.json</span></span>
*   <span data-ttu-id="6606b-196">Registration.JSON</span><span class="sxs-lookup"><span data-stu-id="6606b-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="6606b-197">Número da contagem Olá de veículos introduzir um booth de utilização</span><span class="sxs-lookup"><span data-stu-id="6606b-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="6606b-198">No projeto Olá, faça duplo clique em **Script.asaql** tooopen script Olá Olá **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="6606b-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="6606b-199">Copie e cole o script de Olá na secção anterior Olá no editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="6606b-200">Olá Editor de consultas suporta IntelliSense, cores da sintaxe e o marcador de erro Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Editor de consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="6606b-202">Testar localmente as consultas de análises de fluxo</span><span class="sxs-lookup"><span data-stu-id="6606b-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="6606b-203">toocompile Olá consulta toosee se existir um erro de sintaxe, faça duplo clique projeto Olá e selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="6606b-204">toovalidate esta consulta em relação a dados de exemplo, pode utilizar os dados de exemplo local.</span><span class="sxs-lookup"><span data-stu-id="6606b-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="6606b-205">Entrada de Olá com o botão direito e selecione **Adicionar entrada local**.</span><span class="sxs-lookup"><span data-stu-id="6606b-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Adicionar a entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="6606b-207">Na janela de pop-up Olá, selecione os dados de exemplo de Olá o caminho local.</span><span class="sxs-lookup"><span data-stu-id="6606b-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="6606b-208">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-208">Click **Save**.</span></span>

    ![Adicionar a janela de entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="6606b-210">Um ficheiro denominado **local_EntryStream.json** é adicionada automaticamente a pasta de entradas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="6606b-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Pasta de tooinputs adicionada do ficheiro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="6606b-212">No Olá **Editor de consultas**, clique em **executar localmente**.</span><span class="sxs-lookup"><span data-stu-id="6606b-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="6606b-213">Ou pode premir a tecla F5 de Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-213">Or you can press hello F5 key.</span></span>

    ![Executar localmente](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Saída de execução local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="6606b-216">Prima qualquer saída de Olá tooview chave na Olá **ASA Local executar resultado** janela no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6606b-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Janela de resultados de execução Local ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="6606b-218">Clique em **Abrir pasta do resultado** ficheiros de saída de Olá toocheck ambos no formato CSV e JSON.</span><span class="sxs-lookup"><span data-stu-id="6606b-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Abra a saída de resultado pasta](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="6606b-220">Dados de entrada do exemplo Olá</span><span class="sxs-lookup"><span data-stu-id="6606b-220">Sample hello input data</span></span>
<span data-ttu-id="6606b-221">Também pode dados de entrada de exemplo do ficheiro local do tooa origens de entrada.</span><span class="sxs-lookup"><span data-stu-id="6606b-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="6606b-222">Clique no ficheiro de configuração de entrada de Olá e selecione **dados de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="6606b-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Dados de Exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="6606b-224">Pode apresentar exemplos apenas o hub de eventos ou o IoT hub por agora.</span><span class="sxs-lookup"><span data-stu-id="6606b-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="6606b-225">Não são suportadas outras origens de entrada.</span><span class="sxs-lookup"><span data-stu-id="6606b-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="6606b-226">Na janela de pop-up Olá, introduza o caminho local utilizado de Olá toosave dados de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="6606b-227">Clique em **exemplo**.</span><span class="sxs-lookup"><span data-stu-id="6606b-227">Click **Sample**.</span></span>

    ![Janela de dados de exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="6606b-229">Pode ver o progresso de Olá na Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="6606b-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Janela de saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="6606b-231">Submeter um tooAzure de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="6606b-232">No Olá **Editor de consultas**, clique em **submeter tooAzure** no editor de scripts Olá.</span><span class="sxs-lookup"><span data-stu-id="6606b-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Submeter tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="6606b-234">Selecione **criar uma nova tarefa de análise do Azure Stream**.</span><span class="sxs-lookup"><span data-stu-id="6606b-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="6606b-235">Introduza Olá **nome da tarefa**e selecione Olá correto **subscrição**.</span><span class="sxs-lookup"><span data-stu-id="6606b-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="6606b-236">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="6606b-236">Click **Submit**.</span></span>

    ![Janela de tarefa de envio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="6606b-238">Iniciar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="6606b-238">Start a job</span></span>
<span data-ttu-id="6606b-239">Agora que a tarefa é criada, a vista de tarefas Olá automaticamente é aberta.</span><span class="sxs-lookup"><span data-stu-id="6606b-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="6606b-240">Olá toostart da tarefa, clique em Olá **seta verde** botão.</span><span class="sxs-lookup"><span data-stu-id="6606b-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Iniciar uma tarefa](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="6606b-242">Selecione predefinição Olá e clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Janela de tarefa de início](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="6606b-244">tarefa de Olá **estado** alterações demasiado**executar**, e **eventos de entrada** e **eventos de saída** aparecer.</span><span class="sxs-lookup"><span data-stu-id="6606b-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Estado em execução no resumo da tarefa](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="6606b-246">Resultados da verificação de Olá no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6606b-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="6606b-247">No Visual Studio, abra **Explorador de servidores** e rato Olá **TollDataRefJoin** tabela.</span><span class="sxs-lookup"><span data-stu-id="6606b-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="6606b-248">Selecione **Mostrar dados de tabela** saída de Olá toosee do seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="6606b-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Seleção de mostrar os dados da tabela no Explorador de servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="6606b-250">Vista Olá tarefa métricas</span><span class="sxs-lookup"><span data-stu-id="6606b-250">View hello job metrics</span></span>
<span data-ttu-id="6606b-251">Algumas estatísticas básicas tarefa podem ser encontradas na **métricas de tarefa**.</span><span class="sxs-lookup"><span data-stu-id="6606b-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Janela de métricas de tarefa](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="6606b-253">Tarefa de Olá lista no Explorador de servidores</span><span class="sxs-lookup"><span data-stu-id="6606b-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="6606b-254">No **Explorador de servidores**, clique em **tarefas do Stream Analytics** e, em seguida, clique em **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="6606b-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="6606b-255">tarefa de Olá é apresentado em **tarefas do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6606b-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Tarefas do Stream Analytics listadas no Explorador de servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="6606b-257">Vista de tarefas Olá aberta</span><span class="sxs-lookup"><span data-stu-id="6606b-257">Open hello job view</span></span>
<span data-ttu-id="6606b-258">Vista de tarefas do tooopen Olá, expanda o nó de tarefa e faça duplo clique Olá **tarefas vista** nó.</span><span class="sxs-lookup"><span data-stu-id="6606b-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Nó de vista de tarefas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="6606b-260">Exportar um projeto de tooa tarefa existente</span><span class="sxs-lookup"><span data-stu-id="6606b-260">Export an existing job tooa project</span></span>
<span data-ttu-id="6606b-261">Existem duas formas pode exportar um projeto de tooa tarefa existente.</span><span class="sxs-lookup"><span data-stu-id="6606b-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="6606b-262">No **Explorador de servidores**, contexto Olá tarefa no nó Olá **tarefas do Stream Analytics** nó e selecione **exportar tooNew Stream Analytics projeto**.</span><span class="sxs-lookup"><span data-stu-id="6606b-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Exportar tooNew projeto do Stream Analytics](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="6606b-264">projeto de Olá é gerado no **Explorador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="6606b-264">hello project is generated in **Solution Explorer**.</span></span>

![Projeto gerado no Explorador de soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="6606b-266">Também pode utilizar a vista de tarefas Olá e clique em **gerar projeto**.</span><span class="sxs-lookup"><span data-stu-id="6606b-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Gerar o projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="6606b-268">Problemas e limitações conhecidos</span><span class="sxs-lookup"><span data-stu-id="6606b-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="6606b-269">Não são suportadas para a saída do Power BI e de saída do Azure data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6606b-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="6606b-270">Não há nenhum suporte do editor para adicionar ou alterar funções definidas pelo utilizador do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6606b-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6606b-271">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6606b-271">Next steps</span></span>
* [<span data-ttu-id="6606b-272">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6606b-273">Começar através da utilização do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6606b-274">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6606b-275">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6606b-276">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6606b-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
