---
title: ferramentas de aaaData Lake para Visual Studio com a Hortonworks Sandbox - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá ferramentas do Azure Data Lake para Visual Studio com sandbox de Hortonworks Olá em execução numa local VM. Com estas ferramentas, pode criar e executar tarefas do Hive e do Pig em sandbox Olá e o resultado da tarefa de vista e o histórico."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Utilize Olá do Azure Data Lake tools para Visual Studio com Olá Hortonworks Sandbox

Azure Data Lake inclui ferramentas para trabalhar com clusters do Hadoop genéricos. Este documento fornece passos Olá necessitam as ferramentas do Data Lake de Olá toouse com Olá Hortonworks Sandbox em execução numa máquina virtual local.

Utilizar Olá Hortonworks Sandbox permite-lhe toowork com o Hadoop localmente no seu ambiente de desenvolvimento. Depois de ter programado uma solução e pretender toodeploy-lo em escala, em seguida, pode mover o cluster do HDInsight tooan.

## <a name="prerequisites"></a>Pré-requisitos

* Olá Hortonworks Sandbox, em execução numa máquina virtual no seu ambiente de desenvolvimento. Este documento foi escrito e testado com sandbox Olá em execução no Oracle VirtualBox. Para informações sobre como configurar sandbox Olá, consulte Olá [introdução ao sandbox de Hortonworks Olá.](hdinsight-hadoop-emulator-get-started.md) documento.

* Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (qualquer edição).

* Olá [Azure SDK para .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou posterior.

* Olá [do Azure Data Lake tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Configurar palavras-passe para a sandbox Olá

Certifique-se de que Olá que hortonworks Sandbox está em execução. Em seguida, siga os passos de Olá Olá [começar Olá Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento. Estes passos configurar Olá palavra-passe para Olá SSH `root` conta e Olá Ambari `admin` conta. Estas palavras-passe é utilizados quando se liga toohello sandbox a partir do Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Ligar sandbox de toohello Olá ferramentas

1. Abra o Visual Studio, selecione **vista**e, em seguida, selecione **Explorador de servidores**.

2. De **Explorador de servidores**, contexto Olá **HDInsight** entrada e, em seguida, selecione **ligar tooHDInsight emulador**.

    ![Captura de ecrã do Explorador de servidores, com Connect tooHDInsight emulador realçado](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. De Olá **ligar tooHDInsight emulador** caixa de diálogo, introduza a palavra-passe de Olá que configurou para Ambari.

    ![Captura de ecrã da caixa de diálogo, com a caixa de texto de palavra-passe realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Selecione **seguinte** toocontinue.

4. Olá utilize **palavra-passe** palavra-passe campo tooenter Olá configurado para Olá `root` conta. Deixe Olá outros campos no valor predefinido de Olá.

    ![Captura de ecrã da caixa de diálogo, com a caixa de texto de palavra-passe realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Selecione **seguinte** toocontinue.

5. Aguarde que a validação de Olá toofinish de serviços. Em alguns casos, validação pode falhar e solicitar a configuração de Olá tooupdate. Se a validação falhar, selecione **atualização**e aguarde que a configuração de Olá e verificação para Olá serviço toofinish.

    ![Captura de ecrã da caixa de diálogo, com o botão de atualização realçado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > processo de atualização de Olá utiliza Ambari toomodify Olá Hortonworks Sandbox configuração toowhat é esperado pelas ferramentas de Data Lake Olá para Visual Studio.

6. Depois de concluir a validação, selecione **concluir** toocomplete configuração.
    ![Captura de ecrã da caixa de diálogo, com o botão Concluir realçado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > Consoante a velocidade de Olá do ambiente de desenvolvimento e da quantidade de Olá de memória alocada a máquina virtual de toohello, pode demorar vários minutos tooconfigure e confirme Olá serviços.

Depois de seguir estes passos, tem agora um **HDInsight local cluster** entrada existente no Explorador de servidores, sob Olá **HDInsight** secção.

## <a name="write-a-hive-query"></a>Escrever uma consulta do Hive

Ramo de registo fornece um idioma de consulta como o SQL Server (HiveQL) para trabalhar com dados estruturados. Utilize Olá toolearn passos como toorun a pedido consulta contra o cluster local Olá a seguir.

1. No **Explorador de servidores**, faça duplo clique entrada Olá para o cluster local Olá que adicionou anteriormente e, em seguida, selecione **escrever uma consulta do Hive**.

    ![Captura de ecrã do Explorador de servidores, com uma consulta do Hive realçado de escrita](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    É apresentada uma nova janela de consulta. Aqui, pode rapidamente escrever e submeter um cluster local de toohello de consulta.

2. Na nova janela de consulta Olá, introduza Olá os seguintes comandos:

        select count(*) from sample_08;

    consulta do toorun Olá, selecione **submeter** em Olá parte superior da janela de Olá. Deixe Olá outros valores (**Batch** e nome do servidor), os valores predefinidos de Olá.

    ![Captura de ecrã da janela de consulta, com o botão para submeter Olá realçado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    Também pode utilizar o menu pendente de Olá junto demasiado**submeter** tooselect **avançadas**. Opções avançadas permitem-lhe opções adicionais tooprovide ao submeter a tarefa de Olá.

    ![Caixa de diálogo de captura de ecrã de submeter Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Depois de submeter a consulta de Olá, é apresentado o estado da tarefa Olá. Estado da tarefa Olá apresenta informações sobre a tarefa de Olá como processado por Hadoop. **Estado da tarefa** fornece Olá estado da tarefa de Olá. Estado de Olá é atualizado periodicamente, ou pode utilizar Olá atualizar ícone toorefresh Olá estado manualmente.

    ![Caixa de diálogo de captura de ecrã da vista de tarefas, com o estado da tarefa realçado](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Depois de Olá **estado da tarefa** alterações demasiado**concluído**, é apresentado um direcionado Acíclico gráfico (DAG). Este diagrama descreve o caminho de execução de Olá foi determinado pelo Tez ao processar a consulta do Hive de Olá. Tez é o motor de execução de predefinição do Olá para o ramo de registo no cluster local Olá.

    > [!NOTE]
    > Tez também é predefinido Olá quando estiver a utilizar clusters do HDInsight baseado em Linux. Não é predefinido Olá no HDInsight baseado em Windows. toouse-lo, tem de adicionar a linha de Olá `set hive.execution.engine = tez;` toohello início da sua consulta do Hive.

    Olá utilize **resultado da tarefa** saída de Olá tooview de ligação. Neste caso, é 823, número de Olá de linhas na tabela de sample_08 Olá. Pode ver informações de diagnóstico sobre a tarefa de Olá utilizando Olá **registo da tarefa** e **transferir o registo de YARN** ligações.

4. Também pode executar tarefas do Hive interativamente alterando Olá **Batch** campo demasiado**interativo**. Em seguida, selecione **executar**.

    ![Captura de ecrã de interativa e executar botões realçados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Uma consulta interativa fluxos Olá registo de saídas gerado durante o processamento toohello **HiveServer2 saída** janela.

    > [!NOTE]
    > Olá informações é Olá, mesmo que esteja disponível a partir do Olá **registo da tarefa** ligação depois de terminar uma tarefa.

    ![Captura de ecrã do registo de saída](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Criar um projeto do Hive

Também pode criar um projeto que contém vários scripts Hive. Utilize um projeto quando ter relacionados scripts ou pretender toostore scripts num sistema de controlo de versão.

1. No Visual Studio, selecione **ficheiro**, **novo**e, em seguida, **projeto**.

2. Na lista de Olá de projetos, expanda **modelos**, expanda **do Azure Data Lake**e, em seguida, selecione **ramo de registo (HDInsight)**. Na lista de Olá dos modelos, selecione **do Hive de exemplo**. Introduza um nome e localização e, em seguida, selecione **OK**.

    ![Janela de captura de ecrã do novo projeto, com o Azure Data Lake, HIVE, do Hive de exemplo e OK realçado](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Olá **do Hive de exemplo** projeto contém dois scripts, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**. Pode submeter estes scripts utilizando Olá mesmo **submeter** botão na Olá parte superior da janela de Olá.

## <a name="create-a-pig-project"></a>Criar um projeto do Pig

Enquanto o ramo de registo fornece uma linguagem semelhante a SQL para trabalhar com dados estruturados, Pig funciona efetuando transformações de dados. PIg fornece um idioma (Pig Latin) que permite-lhe toodevelop um pipeline de transformações. toouse Pig com o cluster local Olá, siga estes passos:

1. Abra o Visual Studio e selecione **ficheiro**, **novo**e, em seguida, **projeto**. Na lista de Olá de projetos, expanda **modelos**, expanda **do Azure Data Lake**e, em seguida, selecione **Pig (HDInsight)**. Na lista de Olá dos modelos, selecione **Pig aplicação**. Introduza um nome, localização e, em seguida, selecione **OK**.

    ![Janela de captura de ecrã do novo projeto, com o Azure Data Lake, Pig, Pig aplicação e OK realçado](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Introduza Olá seguir texto como conteúdo Olá Olá **script.pig** ficheiro que foi criado com este projeto.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Enquanto o Pig utiliza um idioma diferente de ramo de registo, como executar tarefas de Olá é consistente entre ambos os idiomas, através de Olá **submeter** botão. Selecionar Olá pendente junto a **submeter** apresenta uma caixa de diálogo de submissão avançada para o Pig.

    ![Caixa de diálogo de captura de ecrã de submeter Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. Também é apresentado o estado da tarefa Olá e de saída, Olá mesmo como uma consulta do Hive.

    ![Captura de ecrã de uma tarefa Pig concluída](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Ver tarefas

Ferramentas do Data Lake também permitem-lhe tooeasily ver informações sobre as tarefas que foram executadas no Hadoop. Os seguintes passos toosee Olá as tarefas que foram executadas no cluster local Olá Olá de utilização.

1. De **Explorador de servidores**, clique no cluster local Olá e, em seguida, selecione **ver tarefas**. É apresentada uma lista de tarefas que foram submetidos toohello cluster.

    ![Captura de ecrã do Explorador de servidores, com as tarefas da vista realçados](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Na lista de Olá de tarefas, selecione um detalhes da tarefa tooview Olá.

    ![Captura de ecrã da tarefa de Browser, uma das tarefas de Olá realçadas](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    informação de Olá apresentada é semelhante toowhat que consulte depois de executar uma consulta do Hive ou Pig, incluindo ligações tooview Olá saída e o registo de informações.

3. Também pode modificar e submeta novamente a tarefa de Olá aqui.

## <a name="view-hive-databases"></a>Ver as bases de dados do Hive

1. No **Explorador de servidores**, expanda Olá **HDInsight local cluster** entrada e, em seguida, expanda **bases de dados do Hive**. Olá **predefinido** e **xademo** bases de dados no cluster local Olá são apresentados. Uma base de dados de expansão mostra tabelas de Olá na base de dados de Olá.

    ![Captura de ecrã do Explorador de servidores, com bases de dados expandidos](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Expandir uma tabela mostra colunas Olá para essa tabela. tooquickly ver dados de Olá, uma tabela com o botão direito e selecione **vista primeiras 100 linhas**.

    ![Captura de ecrã do Explorador de servidores, com a tabela expandido e vista primeiras 100 linhas selecionadas](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Propriedades de base de dados e tabela

Pode ver as propriedades de Olá de uma base de dados ou tabela. Selecionar **propriedades** apresenta os detalhes do item de Olá selecionado na janela de propriedades de Olá. Por exemplo, consulte as informações de Olá mostradas na seguinte captura de ecrã de Olá:

![Janela de captura de ecrã de propriedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Criar uma tabela

toocreate uma tabela, faça duplo clique uma base de dados e, em seguida, selecione **Create Table**.

![Captura de ecrã do Explorador de servidores, com Create Table realçado](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Em seguida, pode criar tabela Olá utilizando um formulário. Na parte inferior de Olá de Olá seguinte captura de ecrã, pode ver Olá HiveQL não processado que é utilizado toocreate Olá tabela.

![Captura de ecrã do formulário Olá utilizado toocreate uma tabela](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Passos seguintes

* [Learning ropes Olá de Olá Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Tutorial do Hadoop - introdução HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
