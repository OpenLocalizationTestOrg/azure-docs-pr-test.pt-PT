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
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics e o Power BI: um dashboard de análise em tempo real para transmissão em fluxo de dados
O Azure Stream Analytics permite-lhe tootake partido de uma das Olá esquerda ferramentas de business intelligence, [Microsoft Power BI](https://powerbi.com/). Neste artigo, saiba como criar ferramentas de business intelligence, utilizando o Power BI como uma saída para as tarefas do Azure Stream Analytics. Também saber como toocreate e utilizar um dashboard em tempo real.

Este artigo continua a partir do Olá Stream Analytics [deteção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial. Isto baseia-se no fluxo de trabalho Olá criado este tutorial e adiciona um Power BI para que pode visualizar as chamadas telefónicas fraudulentas que são detetadas por uma tarefa de análise de transmissão em fluxo de saída. 

Pode ver [um vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que ilustra este cenário.


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que tem o seguinte Olá:

* Uma conta do Azure.
* Uma conta do Power BI. Pode utilizar uma conta profissional ou de uma conta profissional.
* Uma versão completa do Olá [deteção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial. tutorial de Olá inclui uma aplicação que gera metadados fictícios de atribuição de chamada telefónica. Tutorial de Olá, pode criar um hub de eventos e enviar Olá hub de eventos de toohello de dados de chamada telefónica de transmissão em fluxo. Escrever uma consulta que Deteta chamadas fraudulentas (chamadas a partir do Olá igual número em Olá mesmo tempo em localizações diferentes). 


## <a name="add-power-bi-output"></a>Adicionar a saída do Power BI
Tutorial de deteção de fraudes em tempo real de Olá, saída Olá é enviada tooAzure o Blob storage. Nesta secção, adicione uma saída que envia informações tooPower BI.

1. No portal do Azure Olá, abra a tarefa de análise de transmissão em fluxo Olá que criou anteriormente. Se utilizou o nome sugerido Olá, tarefa Olá é denominada `sa_frauddetection_job_demo`.

2. Selecione Olá **saídas** caixa no meio de Olá do dashboard de tarefa Olá e, em seguida, selecione **+ adicionar**.

3. Para **Alias de saída**, introduza `CallStream-PowerBI`. Pode utilizar um nome diferente. Se o fizer, tome nota do mesmo, porque tem o nome de Olá mais tarde. 

4. Em **Sink**, selecione **Power BI**.

   ![Criar um resultado para o Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Clique em **autorizar**.

    Abre uma janela onde pode fornecer as suas credenciais do Azure para uma conta escolar ou profissional. 

    ![Introduza as credenciais de acesso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Introduza as suas credenciais. Tenha em atenção, em seguida, quando introduzir as suas credenciais, está também a dar permissão toohello análise de transmissão em fluxo de trabalho tooaccess sua área de Power BI.

7. Quando estiver a devolvidos toohello **nova saída** painel, introduza Olá seguintes informações:

    * **Área de trabalho de grupo**: selecione uma área de trabalho no seu inquilino do Power BI onde pretende que o conjunto de dados do toocreate Olá.
    * **Nome do conjunto de dados**: introduza `sa-dataset`. Pode utilizar um nome diferente. Se o fizer, anote-lo para utilizar mais tarde.
    * **Nome de tabela**: introduza `fraudulent-calls`. Atualmente, o resultado de Power BI de tarefas do Stream Analytics pode ter apenas uma tabela num conjunto de dados.

    ![Área de trabalho do PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Se o Power BI tem um conjunto de dados e a tabela que tenham Olá mesmos nomes que Olá aqueles que especificou na tarefa de Stream Analytics Olá, Olá existentes será substituído.
    > Recomendamos que não explicitamente crie este conjunto de dados e a tabela na sua conta do Power BI. Estes são criados automaticamente quando iniciar a tarefa de Stream Analytics e a tarefa de Olá começa a saída de bombagem para o Power BI. Se a consulta da tarefa não devolve quaisquer resultados, Olá conjunto de dados e a tabela não são criados.
    >

8. Clique em **Criar**.

Olá conjunto de dados é criado com Olá seguintes definições:

* **defaultRetentionPolicy: BasicFIFO**: os dados são FIFO, com um máximo de 200 000 linhas.
* **defaultMode: pushStreaming**: Olá conjunto de dados suporta a transmissão em fluxo de mosaicos e visuais baseados no relatório tradicionais (a.k.a. Push).

Atualmente, não é possível criar conjuntos de dados com outros sinalizadores.

Para obter mais informações sobre conjuntos de dados do Power BI, consulte Olá [API de REST do Power BI](https://msdn.microsoft.com/library/mt203562.aspx) referência.


## <a name="write-hello-query"></a>Escrever Olá consulta

1. Fechar Olá **saídas** painel e retorno toohello painel de tarefas.

2. Clique em Olá **consulta** caixa. 

3. Introduza Olá seguinte de consulta. Esta consulta é semelhante toohello associação automática consulta que criou no tutorial de deteção de fraudes Olá. Olá diferença é que esta consulta envia resultados toohello novo de saída que criou (`CallStream-PowerBI`). 

    >[!NOTE]
    >Se não nome Olá entrada `CallStream` tutorial de deteção de fraudes Olá, substitua o nome para `CallStream` no Olá **FROM** e **associar** cláusulas na consulta de Olá.

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

4. Clique em **Guardar**.


## <a name="test-hello-query"></a>Consulta de Olá de teste
Esta secção é opcional mas recomendado. 

1. Se a aplicação de TelcoStreaming Olá não está em execução atualmente, inicie-o seguindo estes passos:

    * Abra uma janela de comando.
    * Aceda a pasta toohello onde são Olá telcogenerator.exe e ficheiros de telcodatagen.exe.config modificadas.
    * Execute Olá os seguintes comandos:

            telcodatagen.exe 1000 .2 2

2. No Olá **consulta** painel, clique em Olá pontos seguinte toohello `CallStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.

3. Especifique que pretende que o visão de três minutos de dados e clique em **OK**. Aguarde até que está a notificado de que os dados de Olá amostragem.

4. Clique em **teste** e certifique-se de que está a obter resultados.


## <a name="run-hello-job"></a>Executar tarefa de Olá

1. Certifique-se de que aplicações de TelcoStreaming Olá está em execução.

2. Fechar Olá **consulta** painel.

3. No painel de tarefas Olá, clique em **iniciar**.

    ![Iniciar a tarefa de Stream Analytics Olá](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

A tarefa de análise de transmissão em fluxo inicia à procura de chamadas fraudulentas no fluxo de entrada Olá. tarefa de Olá também cria Olá conjunto de dados e tabela no Power BI e começa a enviar dados sobre Olá chamadas fraudulentas toothem.


## <a name="create-hello-dashboard-in-power-bi"></a>Criar o dashboard de Olá no Power BI

1. Aceda demasiado[Powerbi.com](https://powerbi.com) e inicie sessão com a sua conta escolar ou profissional. Se a consulta da tarefa do Stream Analytics Olá produz resultados, verá que o conjunto de dados já está a ser criado:

    ![Conjunto de dados de transmissão em fluxo no Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. Na área de trabalho, clique em  **+ &nbsp;criar**.

    ![botão para criar Olá na área de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Criar um novo dashboard e dê-lhe nome `Fraudulent Calls`.

    ![Criar um dashboard e atribua um nome na área de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Na Olá parte superior da janela de Olá, clique em **adicionar mosaico**, selecione **dados de transmissão em fluxo personalizados**e, em seguida, clique em **seguinte**.

    ![Personalizada conjunto de dados de transmissão em fluxo](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. Em **YOUR DATSETS**, selecione o conjunto de dados e, em seguida, clique em **seguinte**.

    ![O conjunto de dados de transmissão em fluxo](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. Em **tipo de visualização**, selecione **cartão**e, em seguida, no Olá **campos** lista, selecione **fraudulentcalls**.

    ![Detalhes de visualização do novo mosaico](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Clique em **Seguinte**.

8. Preencha os detalhes de mosaico, como um título e subtítulo do.

    ![Título e subtítulo do novo mosaico](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Clique em **Aplicar**.

    Tem agora um contador de fraude!

    ![Contador de fraude](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Olá siga os passos novamente tooadd um mosaico (começando com o passo 4). Neste momento, Olá seguintes:

    * Quando obtiver demasiado**tipo de visualização**, selecione **gráfico de linhas**. 
    * Adicionar um eixo e selecione **windowend**. 
    * Adicione um valor e selecione **fraudulentcalls**.
    * Para **toodisplay de janela de tempo**, selecione Olá últimos 10 minutos.

    ![Criar o mosaico de gráfico de linha](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Clique em **seguinte**, adicionar um título e subtítulo do e, em **aplicar**.

    dashboard do Power BI Olá agora dá-lhe duas vistas dos dados sobre chamadas fraudulentas como detetado na Olá dados de transmissão em fluxo.

    ![Terminou o dashboard do Power BI que mostra dois mosaicos para chamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Mais informações sobre o Power BI

Este tutorial demonstra como toocreate apenas alguns tipos de visualizações para um conjunto de dados. Power BI pode ajudar a criar outras ferramentas de cliente business intelligence para a sua organização. Para obter mais ideias, consulte Olá os seguintes recursos:

* Para obter outro exemplo de um dashboard do Power BI, veja Olá [introdução ao Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vídeo.
* Para obter mais informações sobre como configurar a análise de transmissão em fluxo de saída tooPower BI tarefa e utilizar grupos de Power BI, reveja Olá [Power BI](stream-analytics-define-outputs.md#power-bi) secção Olá [Stream Analytics produz](stream-analytics-define-outputs.md) artigo. 
* Para obter informações sobre como utilizar o Power BI geralmente, consulte [Dashboards no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Saiba mais sobre as melhores práticas e limitações
Atualmente, Power BI pode ser chamado aproximadamente uma vez por segundo. Os visuais de transmissão em fluxo suportam pacotes de 15 KB. Para além disso, os visuais de transmissão em fluxo falharem (mas push continua toowork). Devido a estas limitações, Power BI presta-se mais naturalmente toocases onde o Azure Stream Analytics does uma redução de carregamento de dados significativos. Recomendamos que utilize uma janela em cascata ou Hopping janela tooensure push de dados é, no máximo, um push por segundo, e que a consulta lands dentro de requisitos de débito Olá.

Pode utilizar Olá seguir equação toocompute Olá valor toogive a janela em segundos:

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Por exemplo:

* Terá de 1000 dispositivos enviar dados em intervalos de um segundo.
* Estão a utilizar Olá Power BI SKU Pro que suporte 1.000.000 linhas por hora.
* Pretende que quantidade de Olá toopublish de dados de média por dispositivo tooPower BI.

Como resultado, torna-se equação de Olá:

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

Tendo em conta esta configuração, pode alterar seguinte toohello da consulta original do Olá:

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


### <a name="renew-authorization"></a>Renovar autorização
Se a palavra-passe de Olá tiver sido alterado desde a tarefa foi criada ou pela última vez autenticada, terá de tooreauthenticate sua conta do Power BI. Se o Azure multi-factor Authentication está configurado no seu inquilino do Azure Active Directory (Azure AD), também tem de autorização de Power BI toorenew em duas semanas. Se não renovar, pode ver sintomas como uma falta de saída da tarefa ou um `Authenticate user error` nos registos de operação de Olá.

Da mesma forma, se uma tarefa é iniciado depois de Olá token tiver expirado, ocorre um erro e Olá tarefa falhar. tooresolve este problema, parar a tarefa de Olá que está a executar e aceda tooyour de saída do Power BI. tooavoid perda de dados, selecione de Olá **renovar autorização** associar e, em seguida, reinicie a tarefa de Olá **hora da última paragem**.

Após ter sido atualizada autorização Olá com o Power BI, um alerta de verde é apresentado no Olá autorização área tooreflect problema Olá foi resolvido.

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API de REST de gestão do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
