---
title: "aaaAzure integração análises de transmissão e Machine Learning | Microsoft Docs"
description: "Como toouse uma função definida pelo utilizador e a aprendizagem uma tarefa de Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="af495-103">Efetuar análise de dados de sentimento utilizando o Azure Stream Analytics e o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="af495-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="af495-104">Este artigo descreve como tooquickly configurar uma tarefa de Stream Analytics do Azure simples que integra o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="af495-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="af495-105">Utilizar um modelo de análise de dados de sentimento do Machine Learning de Olá dados de texto de transmissão em fluxo em tooanalyze de galeria da Cortana Intelligence e determinar a classificação de dados de sentimento Olá em tempo real.</span><span class="sxs-lookup"><span data-stu-id="af495-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="af495-106">Utilizar Olá Cortana Intelligence Suite permite-lhe realizar esta tarefa sem se preocupar intricacies Olá da criação de um modelo de análise de dados de sentimento.</span><span class="sxs-lookup"><span data-stu-id="af495-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="af495-107">Pode aplicar a saber de tooscenarios este artigo como estas:</span><span class="sxs-lookup"><span data-stu-id="af495-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="af495-108">A analisar o sentimento em tempo real no Twitter dados de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="af495-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="af495-109">Analisar registos de cliente chats com a equipa de suporte.</span><span class="sxs-lookup"><span data-stu-id="af495-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="af495-110">Comentários nos fóruns, blogues e vídeos de avaliação.</span><span class="sxs-lookup"><span data-stu-id="af495-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="af495-111">Muitos outros em tempo real, preditivos classificação cenários.</span><span class="sxs-lookup"><span data-stu-id="af495-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="af495-112">Um cenário do mundo real, teria de obter dados de Olá diretamente a partir de um fluxo de dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="af495-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="af495-113">tutorial de Olá toosimplify, escritos-la para que hello tarefa de análise de transmissão em fluxo obtém tweets de um ficheiro CSV no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="af495-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="af495-114">Pode criar o seu próprio ficheiro CSV, ou pode utilizar um ficheiro CSV de exemplo, conforme mostrado no Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="af495-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![exemplo de tweets num ficheiro CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="af495-116">tarefa de análise de transmissão em fluxo Olá que criar aplica-se modelo de análise de dados de sentimento Olá como uma função definida pelo utilizador (UDF) nos dados de texto de exemplo de Olá do arquivo de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="af495-117">saída de Olá (resultado Olá da análise de dados de sentimento Olá) é escrita toohello mesmo arquivo de blob num ficheiro CSV diferente.</span><span class="sxs-lookup"><span data-stu-id="af495-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="af495-118">Olá figura seguinte demonstra esta configuração.</span><span class="sxs-lookup"><span data-stu-id="af495-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="af495-119">Conforme indicado, num cenário mais realistas, pode substituir o armazenamento de Blobs com transmissão em fluxo de dados do Twitter de uma entrada de Event Hubs do Azure.</span><span class="sxs-lookup"><span data-stu-id="af495-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="af495-120">Além disso, foi possível criar um [Microsoft Power BI](https://powerbi.microsoft.com/) visualização em tempo real de dados de sentimento do agregado Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Descrição geral de integração do Stream Analytics Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="af495-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="af495-122">Prerequisites</span></span>
<span data-ttu-id="af495-123">Antes de começar, certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="af495-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="af495-124">Uma subscrição ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="af495-124">An active Azure subscription.</span></span>
* <span data-ttu-id="af495-125">Um ficheiro CSV com alguns dados na mesma.</span><span class="sxs-lookup"><span data-stu-id="af495-125">A CSV file with some data in it.</span></span> <span data-ttu-id="af495-126">Pode transferir ficheiro Olá apresentado anteriormente da [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ou pode criar os seus próprios ficheiros.</span><span class="sxs-lookup"><span data-stu-id="af495-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="af495-127">Para este artigo, partimos do pressuposto que está a utilizar ficheiro de Olá a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="af495-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="af495-128">Um nível elevado, as tarefas de Olá toocomplete demonstrada neste artigo, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="af495-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="af495-129">Criar uma conta de armazenamento do Azure e um contentor de blob storage e carregar um contentor de toohello do ficheiro de entrada CSV formatado.</span><span class="sxs-lookup"><span data-stu-id="af495-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="af495-130">Adicione um modelo de análise de dados de sentimento da área de trabalho do Olá galeria da Cortana Intelligence tooyour Azure Machine Learning e implementar este modelo como um serviço web na área de trabalho do Olá Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="af495-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="af495-131">Crie uma tarefa de Stream Analytics que chama este serviço web como uma função de dados de sentimento do ordem toodetermine para Olá a entrada de texto.</span><span class="sxs-lookup"><span data-stu-id="af495-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="af495-132">Iniciar a tarefa de Stream Analytics Olá e verifique a saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="af495-133">Criar um contentor de armazenamento e carregue o ficheiro de entrada do Olá CSV</span><span class="sxs-lookup"><span data-stu-id="af495-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="af495-134">Para este passo, pode utilizar qualquer ficheiro CSV, tais como Olá um disponível a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="af495-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="af495-135">No portal do Azure Olá, clique em **novo** &gt; **armazenamento** &gt; **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="af495-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![Criar nova conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="af495-137">Forneça um nome (`samldemo` no exemplo de Olá).</span><span class="sxs-lookup"><span data-stu-id="af495-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="af495-138">nome de Olá pode utilizar apenas letras minúsculas e números, e tem de ser exclusivo em todo o Azure.</span><span class="sxs-lookup"><span data-stu-id="af495-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="af495-139">Especifique um grupo de recursos existente e especifique uma localização.</span><span class="sxs-lookup"><span data-stu-id="af495-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="af495-140">Para a localização, recomendamos que todos os recursos de Olá criados nesta utilização tutorial Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="af495-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![forneça detalhes da conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="af495-142">No portal do Azure Olá, selecione a conta de armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="af495-143">No painel de conta de armazenamento Olá, clique em **contentores** e, em seguida, clique em  **+ &nbsp;contentor** toocreate o blob storage.</span><span class="sxs-lookup"><span data-stu-id="af495-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![Criar contentor de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="af495-145">Forneça um nome para o contentor de Olá (`azuresamldemoblob` no exemplo de Olá) e certifique-se de que **aceder tipo** estiver definido demasiado**Blob**.</span><span class="sxs-lookup"><span data-stu-id="af495-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="af495-146">Quando tiver terminado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="af495-146">When you're done, click **OK**.</span></span>

    ![Especifique os detalhes do contentor de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="af495-148">No Olá **contentores** painel, selecione Olá novo contentor, que abre painel Olá para esse contentor.</span><span class="sxs-lookup"><span data-stu-id="af495-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="af495-149">Clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="af495-149">Click **Upload**.</span></span>

    ![Botão 'Carregar' para um contentor](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="af495-151">No Olá **carregar blob** painel, especifique um ficheiro CSV Olá que pretende que toouse para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="af495-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="af495-152">Para **Blob tipo**, selecione **BLOBs de blocos** e conjunto Olá bloco tamanho too4 MB, que é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="af495-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![carregar ficheiro de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="af495-154">Clique em Olá **carregar** botão na Olá parte inferior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="af495-155">Adicionar modelo de análise de dados de sentimento Olá de Olá galeria da Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="af495-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="af495-156">Agora que os dados de exemplo de Olá num blob, pode ativar o modelo de análise de dados de sentimento Olá na galeria da Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="af495-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="af495-157">Aceda toohello [modelo de Análise Preditiva sentimento](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) página Olá galeria da Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="af495-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="af495-158">Clique em **abrir no Studio**.</span><span class="sxs-lookup"><span data-stu-id="af495-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, abra o Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="af495-160">Inicie sessão na área de trabalho do toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="af495-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="af495-161">Selecione uma localização.</span><span class="sxs-lookup"><span data-stu-id="af495-161">Select a location.</span></span>

4. <span data-ttu-id="af495-162">Clique em **executar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="af495-163">Olá processo é executado, que demora um minuto.</span><span class="sxs-lookup"><span data-stu-id="af495-163">hello process runs, which takes about a minute.</span></span>

   ![Execute experimentação no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="af495-165">Depois do processo de Olá foi executada com êxito, selecione **implementar serviço Web** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![implementar experimentação no Machine Learning Studio como um serviço web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="af495-167">toovalidate Olá dados de sentimento do modelo de análise é toouse pronto, clique em Olá **teste** botão.</span><span class="sxs-lookup"><span data-stu-id="af495-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="af495-168">Forneça o texto de entrada, tais como "Posso adoram Microsoft".</span><span class="sxs-lookup"><span data-stu-id="af495-168">Provide text input such as "I love Microsoft".</span></span> 

   ![teste de experimentação no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="af495-170">Se o teste de Olá funciona, consulte um resultado toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="af495-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![resultados do teste no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="af495-172">No Olá **aplicações** coluna, clique em Olá **Excel 2010 ou anterior livro** toodownload ligação um livro do Excel.</span><span class="sxs-lookup"><span data-stu-id="af495-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="af495-173">livro Olá contém a chave de Olá uma API e o URL de Olá terá tooset posterior se a tarefa de Stream Analytics Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, leitura rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="af495-175">Criar uma tarefa de Stream Analytics utiliza o modelo de Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="af495-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="af495-176">Agora, pode criar uma tarefa de Stream Analytics que lê tweets de exemplo de Olá de um ficheiro CSV Olá no blob storage.</span><span class="sxs-lookup"><span data-stu-id="af495-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="af495-177">Criar tarefa de Olá</span><span class="sxs-lookup"><span data-stu-id="af495-177">Create hello job</span></span>

1. <span data-ttu-id="af495-178">Aceda toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af495-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="af495-179">Clique em **novo** > **Internet das coisas** > **tarefa do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="af495-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Caminho do portal do Azure para obter tooa nova tarefa de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="af495-181">Tarefa de Olá nome `azure-sa-ml-demo`, especifique uma subscrição, especifique um grupo de recursos existente ou crie um novo e selecione Olá localização para a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![Especifique as definições para a nova tarefa de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="af495-183">Configurar a entrada da tarefa de Olá</span><span class="sxs-lookup"><span data-stu-id="af495-183">Configure hello job input</span></span>
<span data-ttu-id="af495-184">tarefa de Olá obtém a entrada de um ficheiro CSV Olá que carregou anteriormente tooblob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af495-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="af495-185">Depois da tarefa de Olá tiver sido criada, em **tarefa topologia** no painel de tarefas Olá, clique em Olá **entradas** caixa.</span><span class="sxs-lookup"><span data-stu-id="af495-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Caixa de 'Entradas' no painel de tarefas do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="af495-187">No Olá **entradas** painel, clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="af495-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   !['Adicionar' botão para adicionar uma tarefa de Stream Analytics toohello entrada](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="af495-189">Preencha Olá **nova entrada** painel com estes valores:</span><span class="sxs-lookup"><span data-stu-id="af495-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="af495-190">**Alias de entrada**: Utilize o nome de Olá `datainput`.</span><span class="sxs-lookup"><span data-stu-id="af495-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="af495-191">**Tipo de origem**: selecione **fluxo de dados**.</span><span class="sxs-lookup"><span data-stu-id="af495-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="af495-192">**Origem**: selecione **armazenamento de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="af495-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="af495-193">**Opção de importar**: selecione **armazenamento de BLOBs de utilização da subscrição atual**.</span><span class="sxs-lookup"><span data-stu-id="af495-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="af495-194">**Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="af495-194">**Storage account**.</span></span> <span data-ttu-id="af495-195">Selecione a conta de armazenamento de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af495-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="af495-196">**Contentor**.</span><span class="sxs-lookup"><span data-stu-id="af495-196">**Container**.</span></span> <span data-ttu-id="af495-197">Contentor de Olá selecione que criou anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="af495-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="af495-198">**Formato de serialização de eventos**.</span><span class="sxs-lookup"><span data-stu-id="af495-198">**Event serialization format**.</span></span> <span data-ttu-id="af495-199">Selecione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="af495-199">Select **CSV**.</span></span>

    ![Definições para a nova entrada de tarefa](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="af495-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="af495-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="af495-202">Configurar o resultado da tarefa Olá</span><span class="sxs-lookup"><span data-stu-id="af495-202">Configure hello job output</span></span>
<span data-ttu-id="af495-203">tarefa de Olá envia resultados toohello mesmo onde obtém entrada de armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="af495-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="af495-204">Em **tarefa topologia** no painel de tarefas Olá, clique em Olá **saídas** caixa.</span><span class="sxs-lookup"><span data-stu-id="af495-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Criar nova saída da tarefa de análise de transmissão em fluxo](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="af495-206">No Olá **saídas** painel, clique em **+ adicionar**e, em seguida, adicione uma saída com o alias de Olá `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="af495-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="af495-207">Para **Sink**, selecione **armazenamento de BLOBs**.</span><span class="sxs-lookup"><span data-stu-id="af495-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="af495-208">Em seguida, preencha restante Olá Olá saída definições utilizando Olá mesmos valores que utilizou para armazenamento de BLOBs de Olá para a entrada:</span><span class="sxs-lookup"><span data-stu-id="af495-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="af495-209">**Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="af495-209">**Storage account**.</span></span> <span data-ttu-id="af495-210">Selecione a conta de armazenamento de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af495-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="af495-211">**Contentor**.</span><span class="sxs-lookup"><span data-stu-id="af495-211">**Container**.</span></span> <span data-ttu-id="af495-212">Contentor de Olá selecione que criou anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="af495-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="af495-213">**Formato de serialização de eventos**.</span><span class="sxs-lookup"><span data-stu-id="af495-213">**Event serialization format**.</span></span> <span data-ttu-id="af495-214">Selecione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="af495-214">Select **CSV**.</span></span>

   ![Definições do novo resultado da tarefa](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="af495-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="af495-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="af495-217">Adicionar a função de Machine Learning Olá</span><span class="sxs-lookup"><span data-stu-id="af495-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="af495-218">Anteriormente publicou um serviço web do Machine Learning modelo tooa.</span><span class="sxs-lookup"><span data-stu-id="af495-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="af495-219">No nosso cenário, quando é executada a tarefa de análise de fluxo de Olá, envia cada tweet de exemplo do serviço web de entrada toohello de Olá para análise de dados de sentimento.</span><span class="sxs-lookup"><span data-stu-id="af495-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="af495-220">Olá serviço web Machine Learning devolve um sentimento (`positive`, `neutral`, ou `negative`) e uma probabilidade de tweet Olá a ser positivo.</span><span class="sxs-lookup"><span data-stu-id="af495-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="af495-221">Esta secção do tutorial Olá, é possível definir uma função na tarefa de análise de fluxo de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="af495-222">função de Olá pode ser invocado toosend um serviço de web de toohello tweet e voltar a resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="af495-223">Certifique-se de que tem Olá web service URL e API a chave que transferiu anteriormente no livro do Excel Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="af495-224">Devolva o painel de descrição geral de tarefa toohello.</span><span class="sxs-lookup"><span data-stu-id="af495-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="af495-225">Em **definições**, selecione **funções** e, em seguida, clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="af495-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Adicionar uma tarefa de Stream Analytics toohello função](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="af495-227">Introduza `sentiment` como Olá funcione alias e preencher rest Olá do painel de Olá utilizando estes valores:</span><span class="sxs-lookup"><span data-stu-id="af495-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="af495-228">**Tipo de função**: selecione **do Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="af495-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="af495-229">**Opção de importar**: selecione **importação de uma subscrição diferente**.</span><span class="sxs-lookup"><span data-stu-id="af495-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="af495-230">Isto fornece uma oportunidade tooenter Olá URL e a chave.</span><span class="sxs-lookup"><span data-stu-id="af495-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="af495-231">**URL**: colar em Olá URL do serviço web.</span><span class="sxs-lookup"><span data-stu-id="af495-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="af495-232">**Chave**: colar na chave de API de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-232">**Key**: Paste in hello API key.</span></span>
  
    ![Definições para adicionar uma tarefa de Stream Analytics toohello do Machine Learning função](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="af495-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="af495-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="af495-235">Criar uma consulta tootransform Olá de dados</span><span class="sxs-lookup"><span data-stu-id="af495-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="af495-236">Do Stream Analytics utiliza uma entrada de Olá tooexamine consulta declarativa, baseado em SQL e processá-la.</span><span class="sxs-lookup"><span data-stu-id="af495-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="af495-237">Nesta secção, vai criar uma consulta que lê cada tweet da entrada e, em seguida, invoca o Analysis Services função Olá Machine Learning tooperform sentimento.</span><span class="sxs-lookup"><span data-stu-id="af495-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="af495-238">consulta de Olá, em seguida, envia Olá toohello de resultado de saída que definido (armazenamento de BLOBs).</span><span class="sxs-lookup"><span data-stu-id="af495-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="af495-239">Devolva o painel de descrição geral de tarefa toohello.</span><span class="sxs-lookup"><span data-stu-id="af495-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="af495-240">Em **tarefa topologia**, clique em Olá **consulta** caixa.</span><span class="sxs-lookup"><span data-stu-id="af495-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Criar uma consulta para a tarefa de análise de transmissão em fluxo](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="af495-242">Introduza Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="af495-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="af495-243">consulta de Olá invoca a função de Olá que criou anteriormente (`sentiment`) no ordem tooperform sentimento de análise em cada tweet Olá de entrada.</span><span class="sxs-lookup"><span data-stu-id="af495-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="af495-244">Clique em **guardar** consulta de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="af495-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="af495-245">Iniciar a tarefa de Stream Analytics Olá e verifique a saída de Olá</span><span class="sxs-lookup"><span data-stu-id="af495-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="af495-246">É agora possível iniciar a tarefa de Stream Analytics Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="af495-247">Iniciar a tarefa de Olá</span><span class="sxs-lookup"><span data-stu-id="af495-247">Start hello job</span></span>
1. <span data-ttu-id="af495-248">Devolva o painel de descrição geral de tarefa toohello.</span><span class="sxs-lookup"><span data-stu-id="af495-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="af495-249">Clique em **iniciar** , Olá parte superior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-249">Click **Start** at hello top of hello blade.</span></span>

    ![Criar uma consulta para a tarefa de análise de transmissão em fluxo](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="af495-251">No Olá **iniciar tarefa**, selecione **personalizada**e, em seguida, selecione toowhen anterior de um dia que carregou o armazenamento de tooblob Olá CSV ficheiros.</span><span class="sxs-lookup"><span data-stu-id="af495-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="af495-252">Quando tiver terminado, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="af495-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="af495-253">Verifique a saída de Olá</span><span class="sxs-lookup"><span data-stu-id="af495-253">Check hello output</span></span>
1. <span data-ttu-id="af495-254">Tarefa de Olá permitem executar alguns minutos até ver a atividade na Olá **monitorização** caixa.</span><span class="sxs-lookup"><span data-stu-id="af495-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="af495-255">Se tiver uma ferramenta que normalmente utiliza conteúdo de Olá tooexamine do armazenamento de BLOBs, utilize essa Olá de tooexamine ferramenta `azuresamldemoblob` contentor.</span><span class="sxs-lookup"><span data-stu-id="af495-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="af495-256">Em alternativa, Olá os seguintes passos no portal do Azure de Olá:</span><span class="sxs-lookup"><span data-stu-id="af495-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="af495-257">No portal de Olá, determinar Olá `samldemo` armazenamento conta e, dentro da conta de Olá, determinar Olá `azuresamldemoblob` contentor.</span><span class="sxs-lookup"><span data-stu-id="af495-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="af495-258">Pode ver dois ficheiros no contentor de Olá: Olá ficheiro que contém tweets de exemplo de Olá e um ficheiro CSV gerado pela tarefa de Stream Analytics Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="af495-259">Clique no ficheiro de Olá gerado e, em seguida, selecione **transferir**.</span><span class="sxs-lookup"><span data-stu-id="af495-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Transferir o resultado da tarefa CSV do armazenamento de BLOBs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="af495-261">Abra Olá gerou um ficheiro CSV.</span><span class="sxs-lookup"><span data-stu-id="af495-261">Open hello generated CSV file.</span></span> <span data-ttu-id="af495-262">Verá algo semelhante Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="af495-262">You see something like hello following example:</span></span>  
   
   ![Veja aprendizagem do Stream Analytics, CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="af495-264">Veja as métricas</span><span class="sxs-lookup"><span data-stu-id="af495-264">View metrics</span></span>
<span data-ttu-id="af495-265">Também pode ver as métricas relacionadas com a função do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="af495-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="af495-266">Olá métricas relacionadas com a função a seguir é apresentado no Olá **monitorização** caixa no painel de tarefas Olá:</span><span class="sxs-lookup"><span data-stu-id="af495-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="af495-267">**Pedidos de função** indica Olá número de pedidos enviados tooa serviço web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="af495-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="af495-268">**Eventos de função** indica Olá número dos eventos num pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="af495-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="af495-269">Por predefinição, cada tooa pedido de serviço web Machine Learning contém too1, 000 eventos de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="af495-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="af495-270">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="af495-270">Next steps</span></span>

* [<span data-ttu-id="af495-271">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af495-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="af495-272">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af495-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="af495-273">Integrar o REST API e Machine Learning</span><span class="sxs-lookup"><span data-stu-id="af495-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="af495-274">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af495-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



