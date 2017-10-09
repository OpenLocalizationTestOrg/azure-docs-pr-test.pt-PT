---
title: aaaIoT fluxos de dados em tempo real e do Azure Stream Analytics | Microsoft Docs
description: "Etiquetas do sensor da IoT e transmissão de dados com análises de transmissão e processamento de dados em tempo real"
keywords: "solução iot, começar com iot"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Introdução aos dados de tooprocess Azure Stream Analytics dos dispositivos de IoT
Neste tutorial, ficará a saber como dados toogather de lógica de processamento de fluxo do toocreate de dispositivos Internet das coisas (IoT). Utilizamos uma toodemonstrate cenário do mundo real, Internet das coisas (IoT) utilize como toobuild solução rapidamente e de forma económica.

## <a name="prerequisites"></a>Pré-requisitos
* [Subscrição do Azure](https://azure.microsoft.com/pricing/free-trial/)
* A consulta de exemplos e os ficheiros de dados estão disponíveis para transferência em [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Cenário
Contoso, que é uma empresa no espaço de automatização industriais Olá, tem totalmente automatizado respetivo processo de fabrico. fábrica, Olá este maquinaria tem sensores que são capazes de emitem transmissões de dados em tempo real. Neste cenário, um gestor do piso de produção pretende toohave em tempo real conhecimentos aprofundados sobre toolook de dados de sensor Olá de padrões e executar ações nos mesmos. Utilizaremos Olá idioma de consulta de análise de fluxo (SAQL) através de padrões interessantes de toofind dados de sensor Olá de transmissão em fluxo recebida Olá de dados.

Aqui, os dados estão a ser gerados a partir de um dispositivo Sensor Tag da Texas Instruments.

![Sensor Tag da Texas Instruments](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

payload de Olá de dados de Olá está no formato JSON e assemelha Olá seguinte:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

Num cenário real, pode ter centenas destes sensores a gerar eventos como uma transmissão. Idealmente, um dispositivo de gateway iria executar código toopush estes eventos demasiado[Event Hubs do Azure](https://azure.microsoft.com/services/event-hubs/) ou [os Hubs IoT do Azure](https://azure.microsoft.com/services/iot-hub/). A tarefa de Stream Analytics seria estes eventos provenientes dos Hubs de eventos de inserção e executar consultas de análise em tempo real contra fluxos Olá. Em seguida, poderia enviar Olá resultados tooone de Olá [suportado saídas](stream-analytics-define-outputs.md).

Para facilitar a utilização, este guia de introdução fornece um ficheiro de dados de exemplo, que foi capturado a partir de dispositivos Sensor Tag reais. Pode executar consultas em dados de exemplo de Olá e ver os resultados. Nos tutoriais subsequentes, ficará a saber como tooconnect sua tooinputs e saídas da tarefa e implementá-las toohello serviço do Azure.

## <a name="create-a-stream-analytics-job"></a>Criar uma tarefa do Stream Analytics
1. No Olá [portal do Azure](http://portal.azure.com), clique em Olá sinal de adição e, em seguida, escreva **STREAM ANALYTICS** no direito de toohello Olá texto janela. Em seguida, selecione **tarefa do Stream Analytics** na lista de resultados de Olá.
   
    ![Criar uma nova tarefa do Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Introduza um nome exclusivo de tarefa e certifique-se de que subscrição Olá é Olá uma correta para a tarefa. Crie um novo grupo de recursos ou selecione um existente na sua subscrição.
3. Em seguida, selecione uma localização para a sua tarefa. Para velocidade de processamento e redução de custos na transferência de dados selecionando Olá é recomendada a mesma localização do grupo de recursos de Olá e conta de armazenamento pretendido.
   
    ![Detalhes para criar uma nova tarefa do Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > Deve criar esta conta de armazenamento apenas uma vez por região. Este armazenamento será partilhado com todas as tarefas do Stream Analytics que são criadas nessa região.
   > 
   > 
4. Olá tooplace de caixa de verificação a tarefa no seu dashboard e, em seguida, clique em **criar**.
   
    ![criação da tarefa em curso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Deverá ver uma 'implementação iniciada...' apresentados numa Olá superior direito da janela do browser. Logo que irá alterar janela tooa concluída conforme mostrado abaixo.
   
    ![criação da tarefa em curso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Criar uma consulta do Azure Stream Analytics
Depois da tarefa é criada tooopen do tempo e compilação uma consulta. Pode aceder facilmente a tarefa ao clicar em mosaico Olá para o mesmo.

![Mosaico da Tarefa](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

No Olá **tarefa topologia** painel clique Olá **consulta** caixa toogo toohello Editor de consultas. Olá **consulta** editor permite-lhe consulta tooenter T-SQL que efetua a transformação Olá através de dados de eventos recebidos Olá.

![Caixa de consulta](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Consulta: Arquivar os dados não processados
forma mais simples de Olá da consulta é uma consulta pass-through que arquiva todos os dados de entrada tooits, designados de saída. Transferir o ficheiro de dados de exemplo de Olá de [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa localização no seu computador. 

1. Cole a consulta de Olá do ficheiro de PassThrough.txt Olá. 
   
    ![Fluxo de entrada de teste](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Entrada de tooyour seguinte do Olá três pontos de clique e selecione **carregar dados de exemplo do ficheiro** caixa.
   
    ![Fluxo de entrada de teste](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Um painel abre-se no Olá direito como resultado, dados Olá selecione HelloWorldASA inputstream. JSON da sua localização transferida o ficheiro em clique em **OK** em Olá parte inferior do painel de Olá.
   
    ![Fluxo de entrada de teste](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Em seguida, clique em Olá **testar** gear na parte superior Olá deixado área da janela de Olá e processam a consulta de teste no conjunto de dados de exemplo de Olá. Uma janela de resultados abrirá abaixo a consulta como Olá processamento estar concluído.
   
    ![Resultados do teste](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Consulta: Dados de Olá com base numa condição de filtro
Vamos tentar resultados de Olá toofilter baseados numa condição. Gostaríamos tooshow resultados para apenas esses eventos provenientes do "sensorA". consulta de Olá está no ficheiro de Filtering.txt Olá.

![Filtragem de um fluxo de dados](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Tenha em atenção que Olá consulta maiúsculas e minúsculas compara um valor de cadeia. Clique em Olá **teste** gear novamente a consulta de Olá tooexecute. consulta de Olá deverá devolver 389 linhas de 1860 eventos.

![Segundos resultados de saída do teste de consulta](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Consulta: Alerta tootrigger um fluxo de trabalho de negócio
Vamos tornar a nossa consulta mais detalhada. Para cada tipo de sensor, pretende toomonitor temperatura média por segundo 30 janela e ver os resultados apenas se a temperatura média Olá estiver acima 100 graus. Iremos escrever seguinte Olá consulta e, em seguida, clique em **teste** resultados de Olá toosee. consulta de Olá está no ficheiro de ThresholdAlerting.txt Olá.

![Consulta do filtro de 30 segundos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Deverá ver os resultados que contêm apenas 245 linhas e nomes de sensores em que a temperatura média de Olá é maior que 100. Esta consulta grupos fluxo Olá de eventos por **dspl**, que é superior a nome do sensor Olá, um **janela em cascata** de 30 segundos. Consultas temporais tem estado como pretendemos tooprogress de tempo. Ao utilizar Olá **TIMESTAMP BY** cláusula, especificámos Olá **OUTPUTTIME** vezes tooassociate de coluna com todos os cálculos temporais. Para obter informações detalhadas, leia os artigos do Olá MSDN sobre [tempo gestão](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [funções modos de janela](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Consulta: Detetar a ausência de eventos
Como pode vamos escrever uma consulta toofind uma falta de eventos de entrada? Vamos determinar Olá última vez que um sensor enviou dados e, em seguida, não enviar eventos para Olá minuto seguinte. consulta de Olá está no ficheiro de AbsenseOfEvent.txt Olá.

![Detetar a ausência de eventos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Aqui, utilizamos uma **externa à esquerda** associar toohello dados mesmos fluxo (associação automática). Para uma associação **NTERNA**, só é apresentado um resultado quando é encontrada uma correspondência.  Para um **externa à esquerda** associação, se um evento de Olá à esquerda do lado da associação de Olá correspondência, é apresentada uma linha que tem um valor nulo para Olá todas as colunas do lado direito de Olá é devolvida. Esta técnica é muito útil toofind uma ausência de eventos. Para obter mais informações sobre [JOIN (ASSOCIAÇÃO)](https://msdn.microsoft.com/library/azure/dn835026.aspx), veja a nossa documentação MSDN.

## <a name="conclusion"></a>Conclusão
Olá objetivo deste tutorial é toodemonstrate como toowrite diferentes consultas de idioma de consulta do Stream Analytics e ver resultados no browser Olá. No entanto, isto é apenas o início. O Stream Analytics tem muitas outras funcionalidades. Stream Analytics suporta uma variedade de entradas e saídas e pode, mesmo que utilize funciona no Azure Machine Learning toomake, uma ferramenta robusta para analisar fluxos de dados. Pode iniciar tooexplore mais sobre o Stream Analytics, utilizando a nossa [mapa de aprendizagem](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Para obter mais informações sobre como consultas de toowrite, leia o artigo de Olá sobre [padrões de consulta comuns](stream-analytics-stream-analytics-query-patterns.md).

