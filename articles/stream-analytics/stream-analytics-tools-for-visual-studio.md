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
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Utilizar o Azure Stream Analytics Tools para Visual Studio
## <a name="introduction"></a>Introdução
Neste tutorial, saiba como toouse Azure Stream Analytics Tools para Visual Studio toocreate, criar, testar localmente, gerir e depurar as tarefas do Stream Analytics. 

Depois de concluir este tutorial, será capaz de:
* Familiarize com o Stream Analytics Tools para Visual Studio.
* Configurar e implementar uma tarefa de Stream Analytics.
* Teste a sua tarefa localmente com dados de exemplo local.
* Utilize monitorização tootroubleshoot problemas.
* Exporte tooprojects de tarefas existente.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:
* Conclua os passos de Olá que preceder "Criar uma tarefa de Stream Analytics" no Olá [criar uma solução de IoT utilizando o tutorial do Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Utilize o Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012. Enterprise (Ultimate/Premium), Professional e Community são suportadas as edições. Não é suportada a edição Express. Visual Studio 2017 não é suportada. 
* Olá de utilização do Azure SDK para .NET versão 2.7.1 ou posterior. Instalá-lo utilizando Olá [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Instalar Olá [Stream Analytics Tools para Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Criar um projeto do Stream Analytics
1. No Visual Studio, clique em Olá **ficheiro** menu e selecione **novo projeto**. 

2. Na lista de modelos de Olá Olá esquerda, selecione **Stream Analytics** e, em seguida, clique em **aplicação do Azure Stream Analytics**.

3. Introduza o projeto de Olá **nome**, **localização**, e **nome da solução** para outros projetos.

    ![Nova janela do projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    A **utilização** projeto é gerado no **Explorador de soluções**.

    ![Utilização projeto gerado no Explorador de soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Selecione a subscrição correta Olá
1. No Visual Studio, clique em Olá **vista** menu e abra **Explorador de servidores**.

2. Inicie sessão com a sua conta do Azure. 

## <a name="define-hello-input-sources"></a>Definir origens de entrada Olá
1.  No **Explorador de soluções**, expanda Olá **entradas** nós e mudar o nome **Input** demasiado**EntryStream.json**. Faça duplo clique em **EntryStream.json**.
2.  Olá **Alias de entrada** está agora **EntryStream**. alias de Olá de entrada é utilizada no script de consulta Olá. 
3.  No **tipo de origem**, selecione **fluxo de dados**.
4.  No **origem**, selecione **Hub de eventos**.
5.  No **espaço de nomes do Service Bus**, selecione Olá **TollData** opção.
6.  No **nome do Hub de eventos**, selecione **entrada**.
7.  No **nome de política do Hub de eventos**, selecione **RootManageSharedAccessKey** (Olá o valor predefinido).
8.  No **formato de serialização de eventos**, selecione **Json**. 
9.  No **codificação**, selecione **UTF8**. As definições devem aspeto Olá captura de ecrã a seguir:

    ![Janela de entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. Assistente de Olá toofinish, clique em **guardar**. Agora pode adicionar outro fluxo de saída do Olá toocreate origem de entrada. Contexto Olá **entradas** nós e selecione **Novo Item**.

    ![Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Na janela de Olá, selecione **Azure Stream Analytics entrada**e alterar Olá **nome** demasiado**ExitStream.json**. Clique em **Adicionar**.

    ![Adicionar Novo Item janela](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Faça duplo clique em **ExitStream.json** no projeto Olá e Olá siga os mesmos passos como fez para o fluxo de entrada Olá. Ser tooenter se **sair** para Olá **nome do Hub de eventos** conforme mostrado na seguinte captura de ecrã de Olá:

    ![Janela de ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Agora que definiu dois fluxos de entrada:

    ![Fluxos de entrada de entrada e saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Em seguida, adicione a entrada de dados de referência para o ficheiro de blob Olá que contém dados de registo carro.

13. Contexto Olá **entradas** no projeto Olá e, em seguida, Olá siga os mesmos passos como fez para entradas de fluxo de Olá nó. No **Alias de entrada**, introduza **registo**e, em **tipo de origem**, selecione **referência a dados**.

    ![Janela de registo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. No **conta de armazenamento**, selecione Olá **tolldata** opção. No **contentor**, selecione **tolldata**e, em **padrão do caminho**, introduza **registration.json**. Este nome de ficheiro é sensível a maiúsculas e minúsculas e deve estar em minúscula.
15. Assistente de Olá toofinish, clique em **guardar**.

Agora todas as entradas de Olá são definidas.

## <a name="define-hello-output"></a>Definir a saída de Olá
1.  No **Explorador de soluções**, expanda Olá **entradas** nós e faça duplo clique **Output.json**.

2.  No **Alias de saída**, introduza **saída**. 
3.  No **Sink**, selecione **base de dados SQL**.
4.  No **base de dados**, selecione **TollDataDB**.
5.  No **nome de utilizador**, introduza **tolladmin**. 
6.  No **palavra-passe**, introduza **123toll!**.
7.  No **tabela**, introduza **TollDataRefJoin**.
8.  Clique em **Guardar**.

    ![Janela de saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Criar uma consulta do Stream Analytics
Este tutorial tenta tooanswer várias questões empresariais a que os dados tootoll relacionados. É também constrói as consultas de análises de fluxo que podem ser utilizadas em respostas relevantes do Stream Analytics tooprovide.
Antes de iniciar a tarefa de Stream Analytics primeiro, vamos explorar uma sintaxe de consulta cenário e Olá simple.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Introdução toohello idioma de consulta do Stream Analytics
Imaginemos que tem de toocount Olá diversas veículos que introduza uma booth de utilização. Uma vez neste exemplo é um fluxo contínuo de eventos, terá de toodefine um período de tempo. Modificar Olá pergunta toobe "veículos quantos introduza uma booth de utilização a cada três minutos?" Este toocount de forma dados são frequentemente referido tooas Olá em cascata contagem.

Observe a consulta de Stream Analytics Olá que responde a esta pergunta:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Do Stream Analytics utiliza uma linguagem de consulta que é como o SQL e adiciona alguns extensões toospecify relacionados com o tempo aspetos da consulta de Olá.

Para obter mais informações, consulte [tempo gestão](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [modos de janela](https://msdn.microsoft.com/library/azure/dn835019.aspx) construções utilizadas numa consulta Olá da MSDN.

Agora que tem de escrever a primeira consulta do Stream Analytics, é tempo tootest-lo. Utilize ficheiros de dados de exemplo de Olá localizados na pasta TollApp no Olá seguinte caminho:

.. \TollApp\TollApp\Data

Esta pasta contém Olá os seguintes ficheiros:
*   Entry.JSON
*   Exit.JSON
*   Registration.JSON

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Número da contagem Olá de veículos introduzir um booth de utilização
No projeto Olá, faça duplo clique em **Script.asaql** tooopen script Olá Olá **Editor de consultas**. Copie e cole o script de Olá na secção anterior Olá no editor de Olá. Olá Editor de consultas suporta IntelliSense, cores da sintaxe e o marcador de erro Olá.

![Editor de consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Testar localmente as consultas de análises de fluxo

1. toocompile Olá consulta toosee se existir um erro de sintaxe, faça duplo clique projeto Olá e selecione **criar**. 

2. toovalidate esta consulta em relação a dados de exemplo, pode utilizar os dados de exemplo local. Entrada de Olá com o botão direito e selecione **Adicionar entrada local**.

    ![Adicionar a entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Na janela de pop-up Olá, selecione os dados de exemplo de Olá o caminho local. Clique em **Guardar**.

    ![Adicionar a janela de entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Um ficheiro denominado **local_EntryStream.json** é adicionada automaticamente a pasta de entradas de tooyour.

    ![Pasta de tooinputs adicionada do ficheiro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. No Olá **Editor de consultas**, clique em **executar localmente**. Ou pode premir a tecla F5 de Olá.

    ![Executar localmente](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Saída de execução local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Prima qualquer saída de Olá tooview chave na Olá **ASA Local executar resultado** janela no Visual Studio. 

    ![Janela de resultados de execução Local ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Clique em **Abrir pasta do resultado** ficheiros de saída de Olá toocheck ambos no formato CSV e JSON.

    ![Abra a saída de resultado pasta](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Dados de entrada do exemplo Olá
Também pode dados de entrada de exemplo do ficheiro local do tooa origens de entrada. 
1. Clique no ficheiro de configuração de entrada de Olá e selecione **dados de exemplo**. 

   ![Dados de Exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Pode apresentar exemplos apenas o hub de eventos ou o IoT hub por agora. Não são suportadas outras origens de entrada.

2. Na janela de pop-up Olá, introduza o caminho local utilizado de Olá toosave dados de exemplo de Olá. Clique em **exemplo**.

    ![Janela de dados de exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Pode ver o progresso de Olá na Olá **saída** janela. 

    ![Janela de saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Submeter um tooAzure de consulta do Stream Analytics
1. No Olá **Editor de consultas**, clique em **submeter tooAzure** no editor de scripts Olá.

    ![Submeter tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Selecione **criar uma nova tarefa de análise do Azure Stream**. Introduza Olá **nome da tarefa**e selecione Olá correto **subscrição**. Clique em **submeter**.

    ![Janela de tarefa de envio](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Iniciar uma tarefa
Agora que a tarefa é criada, a vista de tarefas Olá automaticamente é aberta. 
1. Olá toostart da tarefa, clique em Olá **seta verde** botão.

    ![Iniciar uma tarefa](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Selecione predefinição Olá e clique em **iniciar**.
 
    ![Janela de tarefa de início](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    tarefa de Olá **estado** alterações demasiado**executar**, e **eventos de entrada** e **eventos de saída** aparecer.

    ![Estado em execução no resumo da tarefa](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Resultados da verificação de Olá no Visual Studio
1. No Visual Studio, abra **Explorador de servidores** e rato Olá **TollDataRefJoin** tabela.
2. Selecione **Mostrar dados de tabela** saída de Olá toosee do seu trabalho.
   
    ![Seleção de mostrar os dados da tabela no Explorador de servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Vista Olá tarefa métricas
Algumas estatísticas básicas tarefa podem ser encontradas na **métricas de tarefa**. 

![Janela de métricas de tarefa](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Tarefa de Olá lista no Explorador de servidores
No **Explorador de servidores**, clique em **tarefas do Stream Analytics** e, em seguida, clique em **atualizar**. tarefa de Olá é apresentado em **tarefas do Stream Analytics**.

![Tarefas do Stream Analytics listadas no Explorador de servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Vista de tarefas Olá aberta
Vista de tarefas do tooopen Olá, expanda o nó de tarefa e faça duplo clique Olá **tarefas vista** nó.

![Nó de vista de tarefas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Exportar um projeto de tooa tarefa existente
Existem duas formas pode exportar um projeto de tooa tarefa existente.

No **Explorador de servidores**, contexto Olá tarefa no nó Olá **tarefas do Stream Analytics** nó e selecione **exportar tooNew Stream Analytics projeto**.

![Exportar tooNew projeto do Stream Analytics](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

projeto de Olá é gerado no **Explorador de soluções**.

![Projeto gerado no Explorador de soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Também pode utilizar a vista de tarefas Olá e clique em **gerar projeto**.

![Gerar o projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Problemas e limitações conhecidos
 
- Não são suportadas para a saída do Power BI e de saída do Azure data Lake Store.
- Não há nenhum suporte do editor para adicionar ou alterar funções definidas pelo utilizador do JavaScript.

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar através da utilização do Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
