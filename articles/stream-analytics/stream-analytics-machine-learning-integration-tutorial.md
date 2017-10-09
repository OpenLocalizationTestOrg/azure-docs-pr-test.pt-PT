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
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Efetuar análise de dados de sentimento utilizando o Azure Stream Analytics e o Azure Machine Learning
Este artigo descreve como tooquickly configurar uma tarefa de Stream Analytics do Azure simples que integra o Azure Machine Learning. Utilizar um modelo de análise de dados de sentimento do Machine Learning de Olá dados de texto de transmissão em fluxo em tooanalyze de galeria da Cortana Intelligence e determinar a classificação de dados de sentimento Olá em tempo real. Utilizar Olá Cortana Intelligence Suite permite-lhe realizar esta tarefa sem se preocupar intricacies Olá da criação de um modelo de análise de dados de sentimento.

Pode aplicar a saber de tooscenarios este artigo como estas:

* A analisar o sentimento em tempo real no Twitter dados de transmissão em fluxo.
* Analisar registos de cliente chats com a equipa de suporte.
* Comentários nos fóruns, blogues e vídeos de avaliação. 
* Muitos outros em tempo real, preditivos classificação cenários.

Um cenário do mundo real, teria de obter dados de Olá diretamente a partir de um fluxo de dados do Twitter. tutorial de Olá toosimplify, escritos-la para que hello tarefa de análise de transmissão em fluxo obtém tweets de um ficheiro CSV no Blob storage do Azure. Pode criar o seu próprio ficheiro CSV, ou pode utilizar um ficheiro CSV de exemplo, conforme mostrado no Olá seguinte imagem:

![exemplo de tweets num ficheiro CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

tarefa de análise de transmissão em fluxo Olá que criar aplica-se modelo de análise de dados de sentimento Olá como uma função definida pelo utilizador (UDF) nos dados de texto de exemplo de Olá do arquivo de blob Olá. saída de Olá (resultado Olá da análise de dados de sentimento Olá) é escrita toohello mesmo arquivo de blob num ficheiro CSV diferente. 

Olá figura seguinte demonstra esta configuração. Conforme indicado, num cenário mais realistas, pode substituir o armazenamento de Blobs com transmissão em fluxo de dados do Twitter de uma entrada de Event Hubs do Azure. Além disso, foi possível criar um [Microsoft Power BI](https://powerbi.microsoft.com/) visualização em tempo real de dados de sentimento do agregado Olá.    

![Descrição geral de integração do Stream Analytics Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, certifique-se de que tem o seguinte Olá:

* Uma subscrição ativa do Azure.
* Um ficheiro CSV com alguns dados na mesma. Pode transferir ficheiro Olá apresentado anteriormente da [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ou pode criar os seus próprios ficheiros. Para este artigo, partimos do pressuposto que está a utilizar ficheiro de Olá a partir do GitHub.

Um nível elevado, as tarefas de Olá toocomplete demonstrada neste artigo, Olá seguintes:

1. Criar uma conta de armazenamento do Azure e um contentor de blob storage e carregar um contentor de toohello do ficheiro de entrada CSV formatado.
3. Adicione um modelo de análise de dados de sentimento da área de trabalho do Olá galeria da Cortana Intelligence tooyour Azure Machine Learning e implementar este modelo como um serviço web na área de trabalho do Olá Machine Learning.
5. Crie uma tarefa de Stream Analytics que chama este serviço web como uma função de dados de sentimento do ordem toodetermine para Olá a entrada de texto.
6. Iniciar a tarefa de Stream Analytics Olá e verifique a saída de Olá.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Criar um contentor de armazenamento e carregue o ficheiro de entrada do Olá CSV
Para este passo, pode utilizar qualquer ficheiro CSV, tais como Olá um disponível a partir do GitHub.

1. No portal do Azure Olá, clique em **novo** &gt; **armazenamento** &gt; **conta de armazenamento**.

   ![Criar nova conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Forneça um nome (`samldemo` no exemplo de Olá). nome de Olá pode utilizar apenas letras minúsculas e números, e tem de ser exclusivo em todo o Azure. 

3. Especifique um grupo de recursos existente e especifique uma localização. Para a localização, recomendamos que todos os recursos de Olá criados nesta utilização tutorial Olá mesma localização.

    ![forneça detalhes da conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. No portal do Azure Olá, selecione a conta de armazenamento de Olá. No painel de conta de armazenamento Olá, clique em **contentores** e, em seguida, clique em  **+ &nbsp;contentor** toocreate o blob storage.

    ![Criar contentor de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Forneça um nome para o contentor de Olá (`azuresamldemoblob` no exemplo de Olá) e certifique-se de que **aceder tipo** estiver definido demasiado**Blob**. Quando tiver terminado, clique em **OK**.

    ![Especifique os detalhes do contentor de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. No Olá **contentores** painel, selecione Olá novo contentor, que abre painel Olá para esse contentor.

7. Clique em **Carregar**.

    ![Botão 'Carregar' para um contentor](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. No Olá **carregar blob** painel, especifique um ficheiro CSV Olá que pretende que toouse para este tutorial. Para **Blob tipo**, selecione **BLOBs de blocos** e conjunto Olá bloco tamanho too4 MB, que é suficiente para este tutorial.

    ![carregar ficheiro de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Clique em Olá **carregar** botão na Olá parte inferior do painel de Olá.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Adicionar modelo de análise de dados de sentimento Olá de Olá galeria da Cortana Intelligence

Agora que os dados de exemplo de Olá num blob, pode ativar o modelo de análise de dados de sentimento Olá na galeria da Cortana Intelligence.

1. Aceda toohello [modelo de Análise Preditiva sentimento](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) página Olá galeria da Cortana Intelligence.  

2. Clique em **abrir no Studio**.  
   
   ![Stream Analytics Machine Learning, abra o Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Inicie sessão na área de trabalho do toogo toohello. Selecione uma localização.

4. Clique em **executar** em Olá parte inferior da página Olá. Olá processo é executado, que demora um minuto.

   ![Execute experimentação no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Depois do processo de Olá foi executada com êxito, selecione **implementar serviço Web** em Olá parte inferior da página Olá.

   ![implementar experimentação no Machine Learning Studio como um serviço web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate Olá dados de sentimento do modelo de análise é toouse pronto, clique em Olá **teste** botão. Forneça o texto de entrada, tais como "Posso adoram Microsoft". 

   ![teste de experimentação no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Se o teste de Olá funciona, consulte um resultado toohello semelhante seguinte exemplo:

   ![resultados do teste no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. No Olá **aplicações** coluna, clique em Olá **Excel 2010 ou anterior livro** toodownload ligação um livro do Excel. livro Olá contém a chave de Olá uma API e o URL de Olá terá tooset posterior se a tarefa de Stream Analytics Olá.

    ![Stream Analytics Machine Learning, leitura rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Criar uma tarefa de Stream Analytics utiliza o modelo de Machine Learning Olá

Agora, pode criar uma tarefa de Stream Analytics que lê tweets de exemplo de Olá de um ficheiro CSV Olá no blob storage. 

### <a name="create-hello-job"></a>Criar tarefa de Olá

1. Aceda toohello [portal do Azure](https://portal.azure.com).  

2. Clique em **novo** > **Internet das coisas** > **tarefa do Stream Analytics**. 

   ![Caminho do portal do Azure para obter tooa nova tarefa de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Tarefa de Olá nome `azure-sa-ml-demo`, especifique uma subscrição, especifique um grupo de recursos existente ou crie um novo e selecione Olá localização para a tarefa de Olá.

   ![Especifique as definições para a nova tarefa de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Configurar a entrada da tarefa de Olá
tarefa de Olá obtém a entrada de um ficheiro CSV Olá que carregou anteriormente tooblob armazenamento.

1. Depois da tarefa de Olá tiver sido criada, em **tarefa topologia** no painel de tarefas Olá, clique em Olá **entradas** caixa.  
   
   ![Caixa de 'Entradas' no painel de tarefas do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. No Olá **entradas** painel, clique em **+ adicionar**.

   !['Adicionar' botão para adicionar uma tarefa de Stream Analytics toohello entrada](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Preencha Olá **nova entrada** painel com estes valores:

    * **Alias de entrada**: Utilize o nome de Olá `datainput`.
    * **Tipo de origem**: selecione **fluxo de dados**.
    * **Origem**: selecione **armazenamento de BLOBs**.
    * **Opção de importar**: selecione **armazenamento de BLOBs de utilização da subscrição atual**. 
    * **Conta de armazenamento**. Selecione a conta de armazenamento de Olá que criou anteriormente.
    * **Contentor**. Contentor de Olá selecione que criou anteriormente (`azuresamldemoblob`).
    * **Formato de serialização de eventos**. Selecione **CSV**.

    ![Definições para a nova entrada de tarefa](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Clique em **Criar**.

### <a name="configure-hello-job-output"></a>Configurar o resultado da tarefa Olá
tarefa de Olá envia resultados toohello mesmo onde obtém entrada de armazenamento de Blobs. 

1. Em **tarefa topologia** no painel de tarefas Olá, clique em Olá **saídas** caixa.  
  
   ![Criar nova saída da tarefa de análise de transmissão em fluxo](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. No Olá **saídas** painel, clique em **+ adicionar**e, em seguida, adicione uma saída com o alias de Olá `datamloutput`. 

3. Para **Sink**, selecione **armazenamento de BLOBs**. Em seguida, preencha restante Olá Olá saída definições utilizando Olá mesmos valores que utilizou para armazenamento de BLOBs de Olá para a entrada:

    * **Conta de armazenamento**. Selecione a conta de armazenamento de Olá que criou anteriormente.
    * **Contentor**. Contentor de Olá selecione que criou anteriormente (`azuresamldemoblob`).
    * **Formato de serialização de eventos**. Selecione **CSV**.

   ![Definições do novo resultado da tarefa](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Clique em **Criar**.   


### <a name="add-hello-machine-learning-function"></a>Adicionar a função de Machine Learning Olá 
Anteriormente publicou um serviço web do Machine Learning modelo tooa. No nosso cenário, quando é executada a tarefa de análise de fluxo de Olá, envia cada tweet de exemplo do serviço web de entrada toohello de Olá para análise de dados de sentimento. Olá serviço web Machine Learning devolve um sentimento (`positive`, `neutral`, ou `negative`) e uma probabilidade de tweet Olá a ser positivo. 

Esta secção do tutorial Olá, é possível definir uma função na tarefa de análise de fluxo de Olá. função de Olá pode ser invocado toosend um serviço de web de toohello tweet e voltar a resposta Olá. 

1. Certifique-se de que tem Olá web service URL e API a chave que transferiu anteriormente no livro do Excel Olá.

2. Devolva o painel de descrição geral de tarefa toohello.

3. Em **definições**, selecione **funções** e, em seguida, clique em **+ adicionar**.

   ![Adicionar uma tarefa de Stream Analytics toohello função](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Introduza `sentiment` como Olá funcione alias e preencher rest Olá do painel de Olá utilizando estes valores:

    * **Tipo de função**: selecione **do Azure ML**.
    * **Opção de importar**: selecione **importação de uma subscrição diferente**. Isto fornece uma oportunidade tooenter Olá URL e a chave.
    * **URL**: colar em Olá URL do serviço web.
    * **Chave**: colar na chave de API de Olá.
  
    ![Definições para adicionar uma tarefa de Stream Analytics toohello do Machine Learning função](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Clique em **Criar**.

### <a name="create-a-query-tootransform-hello-data"></a>Criar uma consulta tootransform Olá de dados

Do Stream Analytics utiliza uma entrada de Olá tooexamine consulta declarativa, baseado em SQL e processá-la. Nesta secção, vai criar uma consulta que lê cada tweet da entrada e, em seguida, invoca o Analysis Services função Olá Machine Learning tooperform sentimento. consulta de Olá, em seguida, envia Olá toohello de resultado de saída que definido (armazenamento de BLOBs).

1. Devolva o painel de descrição geral de tarefa toohello.

2.  Em **tarefa topologia**, clique em Olá **consulta** caixa.

    ![Criar uma consulta para a tarefa de análise de transmissão em fluxo](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Introduza Olá seguinte consulta:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    consulta de Olá invoca a função de Olá que criou anteriormente (`sentiment`) no ordem tooperform sentimento de análise em cada tweet Olá de entrada. 

4. Clique em **guardar** consulta de Olá toosave.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Iniciar a tarefa de Stream Analytics Olá e verifique a saída de Olá

É agora possível iniciar a tarefa de Stream Analytics Olá.

### <a name="start-hello-job"></a>Iniciar a tarefa de Olá
1. Devolva o painel de descrição geral de tarefa toohello.

2. Clique em **iniciar** , Olá parte superior do painel de Olá.

    ![Criar uma consulta para a tarefa de análise de transmissão em fluxo](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. No Olá **iniciar tarefa**, selecione **personalizada**e, em seguida, selecione toowhen anterior de um dia que carregou o armazenamento de tooblob Olá CSV ficheiros. Quando tiver terminado, clique em **iniciar**.  


### <a name="check-hello-output"></a>Verifique a saída de Olá
1. Tarefa de Olá permitem executar alguns minutos até ver a atividade na Olá **monitorização** caixa. 

2. Se tiver uma ferramenta que normalmente utiliza conteúdo de Olá tooexamine do armazenamento de BLOBs, utilize essa Olá de tooexamine ferramenta `azuresamldemoblob` contentor. Em alternativa, Olá os seguintes passos no portal do Azure de Olá:

    1. No portal de Olá, determinar Olá `samldemo` armazenamento conta e, dentro da conta de Olá, determinar Olá `azuresamldemoblob` contentor. Pode ver dois ficheiros no contentor de Olá: Olá ficheiro que contém tweets de exemplo de Olá e um ficheiro CSV gerado pela tarefa de Stream Analytics Olá.
    2. Clique no ficheiro de Olá gerado e, em seguida, selecione **transferir**. 

   ![Transferir o resultado da tarefa CSV do armazenamento de BLOBs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Abra Olá gerou um ficheiro CSV. Verá algo semelhante Olá seguinte exemplo:  
   
   ![Veja aprendizagem do Stream Analytics, CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Veja as métricas
Também pode ver as métricas relacionadas com a função do Azure Machine Learning. Olá métricas relacionadas com a função a seguir é apresentado no Olá **monitorização** caixa no painel de tarefas Olá:

* **Pedidos de função** indica Olá número de pedidos enviados tooa serviço web Machine Learning.  
* **Eventos de função** indica Olá número dos eventos num pedido de Olá. Por predefinição, cada tooa pedido de serviço web Machine Learning contém too1, 000 eventos de cópia de segurança.  


## <a name="next-steps"></a>Passos seguintes

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Integrar o REST API e Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)



