---
title: Exemplos de aaaStorm-starter no Apache Storm no HDInsight - Azure | Microsoft Docs
description: "Saiba como análise de macrodados toodo e processamento de dados em tempo real com Apache Storm e Olá exemplos de storm-starter no HDInsight."
keywords: storm-starter, exemplo do apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Introdução ao Apache Storm no HDInsight com exemplos de storm-starter Olá

Saiba como toouse Apache Storm no HDInsight com Olá exemplos de storm-starter.

O Apache Storm é um sistema de cálculo dimensionável, tolerante a falhas, distribuído e em tempo real para o processamento de fluxos de dados. Com o Storm no Azure HDInsight, pode criar um cluster do Storm baseado na nuvem que executa a análise de macrodados em tempo real.

> [!IMPORTANT]
> Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Estar familiarizado com o SSH e o SCP**. Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Criar um cluster do Storm

Utilize Olá os seguintes passos toocreate um Storm num cluster do HDInsight:

1. De Olá [portal do Azure](https://portal.azure.com), selecione **+ novo**, **Intelligence + análise**e, em seguida, selecione **HDInsight**.

    ![Criar um cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. De Olá **Noções básicas** painel, introduza Olá seguintes informações:

    * **Nome do cluster**: nome de Olá do cluster do HDInsight Olá.
    * **Subscrição**: selecione Olá toouse de subscrição.
    * **Nome de utilizador de início de sessão do cluster** e **palavra-passe de início de sessão do Cluster**: início de sessão de Olá ao aceder ao cluster Olá através de HTTPS. Utiliza estas credenciais tooaccess os serviços, tais como Olá IU da Web do Ambari ou a REST API.
    * **Secure Shell (SSH) username**: início de sessão de Olá utilizado ao aceder ao cluster Olá através de SSH. Por predefinição, palavra-passe de Olá é Olá igual a palavra-passe de início de sessão do Olá cluster.
    * **Grupo de recursos**: Olá recursos grupo toocreate Olá cluster.
    * **Localização**: Olá região do Azure toocreate Olá cluster.

    ![Selecionar subscrição](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Selecione **tipo de Cluster**, e, em seguida, o conjunto Olá seguindo os valores do Olá **configuração de Cluster** painel:

    * **Tipo de Cluster**: Storm

    * **Sistema operativo**: Linux

    * **Versão**: Storm 1.1.0 (HDI 3.6)

    * **Escalão do Cluster**: Standard

    Por último, utilize Olá **selecione** botão toosave definições.

    ![Selecionar tipo de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Depois de selecionar o tipo de cluster Olá, utilize Olá __selecione__ botão de tipo de cluster de Olá tooset. Em seguida, utilize Olá __seguinte__ configuração básica do botão toofinish.

5. De Olá **armazenamento** painel, selecione ou crie uma conta de armazenamento. Para obter os passos de Olá neste documento, deixe Olá outros campos neste painel, os valores predefinidos de Olá. Olá utilize __seguinte__ configuração de armazenamento de toosave do botão.

    ![Configurar as definições de conta de armazenamento Olá para o HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. De Olá **resumo** painel, reveja Olá configuração para o cluster de Olá. Olá utilize __editar__ liga toochange quaisquer definições que estão incorretas. Por fim, utilize o cluster do the__Create__ botão toocreate Olá.

    ![Resumo da configuração do cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Pode demorar até o cluster de Olá too20 minutos toocreate.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Executar um exemplo do storm-starter no HDInsight

1. Ligar o cluster do HDInsight toohello utilizando SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Se utilizou uma palavra-passe toosecure a conta de utilizador do SSH, é pedido tooentê-lo. Se tiver utilizado uma chave pública, poderá precisar de utilizar Olá `-i` parâmetro toospecify Olá chave privada correspondente. Por exemplo, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilize o seguinte comando toostart uma topologia de exemplo de Olá:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > Em versões anteriores do HDInsight, o nome de classe de Olá da topologia de Olá é `storm.starter.WordCountTopology` em vez de `org.apache.storm.starter.WordCountTopology`.

    Este comando inicia a topologia do WordCount de exemplo de Olá no cluster de Olá, com um nome amigável "WordCount". Gerar aleatoriamente frases e a ocorrência de Olá de contagem de cada palavra nas frases Olá.

    > [!NOTE]
    > Ao submeter o seu próprio cluster do toohello topologias, terá primeiro de copiar ficheiros de jar Olá que contém o cluster de Olá antes de utilizar Olá `storm` comando. Olá utilize `scp` o ficheiro de Olá toocopy de comandos. Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > Olá exemplo de WordCount e outros exemplos de storm-starter já estão incluídos no seu cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Se estiver interessado em Ver origem Olá para obter exemplos de storm-starter Olá, pode encontrar o código de Olá no [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Esta ligação é para o Storm 1.1.x, que é fornecido com o HDInsight 3.6. Para outras versões do Storm, utilize Olá __ramo__ botão, Olá parte superior do Olá página tooselect uma versão diferente do Storm.

## <a name="monitor-hello-topology"></a>Topologia de Olá do monitor

Olá IU do Storm fornece uma interface web para trabalhar com topologias em execução e está incluído no cluster do HDInsight.

Utilize Olá topologia de Olá passos toomonitor Olá IU do Storm a utilizar os seguintes:

1. Olá toodisplay IU do Storm, abra um web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui. Substitua **CLUSTERNAME** com o nome de Olá do cluster.

    > [!NOTE]
    > Se lhe for perguntado tooprovide um nome de utilizador e palavra-passe, introduza o administrador de clusters de Olá (administrador) e a palavra-passe que utilizou quando criar cluster de Olá.

2. Em **resumo da topologia**, selecione Olá **wordcount** entrada no Olá **nome** coluna. Informações sobre a topologia de Olá são apresentadas.

    ![Dashboard do Storm com informações de topologia do WordCount do storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Esta página fornece Olá seguintes informações:

    * **Estatísticas de topologia** -informações básicas sobre desempenho Olá da topologia, organizadas em intervalos de tempo.

        > [!NOTE]
        > Selecionar um intervalo de tempo de Olá de alterações de janela do tempo específico das informações apresentadas noutras secções da página Olá.

    * **Spouts** -informações básicas sobre spouts, incluindo Olá último erro devolvido por cada spout.

    * **Bolts** – informações básicas sobre bolts.

    * **Configuração da topologia** -informações detalhadas sobre a configuração da topologia Olá.

    Esta página também fornece ações que podem ser executadas na topologia de Olá:

    * **Ativar** – retoma o processamento de uma topologia desativada.

    * **Desativar** – coloca em pausa uma topologia em execução.

    * **Rebalancear** -ajusta o paralelismo Olá da topologia de Olá. Deve rebalancear as topologias em execução depois de ter alterado o número de Olá de nós no cluster de Olá. Reequilíbrio ajusta o paralelismo toocompensate para o número de Olá maior/menor de nós no cluster de Olá. Para obter mais informações, consulte [compreender o paralelismo Olá de uma topologia do Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **Kill** -termina uma topologia do Storm após Olá especificado tempo limite.

3. Nesta página, selecione uma entrada de Olá **Spouts** ou **Bolts** secção. Informações sobre o componente selecionado Olá são apresentadas.

    ![Dashboard do Storm com informações sobre os componentes selecionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Esta página apresenta Olá seguintes informações:

    * **Estatísticas de spout/Bolt** -informações básicas sobre o desempenho do componente de Olá, organizadas em intervalos de tempo.

        > [!NOTE]
        > Selecionar um intervalo de tempo de Olá de alterações de janela do tempo específico das informações apresentadas noutras secções da página Olá.

    * **Estatísticas de entrada** (apenas bolt) – informações sobre componentes que produzem os dados consumidos pelo bolt Olá.

    * **Estatísticas de saída** – Informações sobre dados emitidos por este bolt.

    * **Executores** – Informações sobre as instâncias deste componente.

    * **Erros** – Erros produzidos por este componente.

4. Quando visualiza detalhes de Olá de um spout ou bolt, selecione uma entrada de Olá **porta** coluna na Olá **executores** secção tooview detalhes de uma instância específica do componente de Olá.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    Neste exemplo, Olá word **sete** Ocorreu 1493957 vezes. Esta contagem é o número de vezes word Olá foi detetado desde que esta topologia foi iniciada.

## <a name="stop-hello-topology"></a>Parar a topologia de Olá

Devolver toohello **resumo da topologia** página topologia da contagem word Olá e, em seguida, selecione Olá **Kill** botão de Olá **ações de topologia** secção. Quando lhe for pedido, introduza 10 Olá segundos toowait antes de parar a topologia de Olá. Após o período de tempo limite de Olá, topologia Olá já não é apresentada quando visitar Olá **IU do Storm** secção do dashboard de Olá.

## <a name="delete-hello-cluster"></a>Eliminar cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Caso se depare com um problema com a criação de um cluster do HDInsight, veja [aceder aos requisitos de controlo](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Passos seguintes

Neste tutorial do Apache Storm, aprendeu as noções básicas de Olá do trabalho com o Storm no HDInsight. Seguidamente, saiba como demasiado[topologias baseadas em Java desenvolver com o Maven](hdinsight-storm-develop-java-topology.md).

Se já estiver familiarizado com o desenvolvimento de topologias baseadas em Java e pretender toodeploy um tooHDInsight de topologia existentes, consulte [implementar e gerir topologias Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Se for um programador do .NET, pode criar topologias C# ou C#/Java híbridas com o Visual Studio. Para obter mais informações, veja [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio (Desenvolver topologias C# para Apache Storm no HDInsight com ferramentas do Hadoop para o Visual Studio)](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Para topologias de exemplo que podem ser utilizadas com o Storm no HDInsight, consulte Olá exemplos a seguir:

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
