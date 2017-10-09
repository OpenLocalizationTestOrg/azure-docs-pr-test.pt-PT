---
title: cluster de recursos de aaaManage para Apache Spark no Azure HDInsight | Microsoft Docs
description: Saiba como toouse gerir os recursos de clusters do Spark no Azure HDInsight para um melhor desempenho.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Gerir os recursos de cluster do Apache Spark no Azure HDInsight 

Neste artigo, ficará a saber como associados a interfaces de Olá tooaccess como Ambari IU, IU do YARN e Olá Spark histórico de servidor com o cluster do Spark. Também ficará a saber sobre como tootune Olá configuração de cluster para um desempenho ideal.

**Pré-requisitos:**

Tem de ter o seguinte Olá:

* Uma subscrição do Azure. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte [clusters do Apache Spark criar no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Como iniciar o Olá IU da Web do Ambari
1. De Olá [Portal do Azure](https://portal.azure.com/), de Olá startboard, clique no mosaico Olá para o cluster do Spark (se o tiver afixado toohello startboard). Também pode navegar tooyour cluster em **Procurar tudo** > **Clusters do HDInsight**.
2. No painel de cluster do Spark de Olá, clique em **Dashboard**. Quando lhe for pedido, introduza as credenciais de administrador Olá para um cluster do Spark Olá.

    ![Inicie o Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "inicie o Gestor de recursos")
3. Isto deve iniciar Olá IU da Web do Ambari, conforme mostrado abaixo.

    ![IU da Web do Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "IU da Web do Ambari")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Como iniciar o Olá Spark histórico de servidor
1. De Olá [Portal do Azure](https://portal.azure.com/), de Olá startboard, clique no mosaico Olá para o cluster do Spark (se o tiver afixado toohello startboard).
2. De Olá cluster painel, em **ligações rápidas**, clique em **Cluster Dashboard**. No Olá **Cluster Dashboard** painel, clique em **Spark histórico servidor**.

    ![Servidor do histórico de spark](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark histórico servidor")

    Quando lhe for pedido, introduza as credenciais de administrador Olá para um cluster do Spark Olá.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Como iniciar a IU do Yarn de Olá?
Pode utilizar Olá IU do YARN toomonitor aplicações que estão atualmente em execução no cluster do Spark Olá.

1. No painel do cluster de Olá, clique em **Cluster Dashboard**e, em seguida, clique em **YARN**.

    ![Iniciar a IU do YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Em alternativa, pode também iniciar Olá IU do YARN de Olá IU do Ambari. toolaunch Olá IU do Ambari, no painel do cluster de Olá, clique em **Cluster Dashboard**e, em seguida, clique em **Dashboard de Cluster do HDInsight**. Na IU do Ambari Olá, clique em **YARN**, clique em **ligações rápidas**, clique em Gestor de recursos do Active Directory Olá e, em seguida, clique em **ResourceManager IU**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>O que é aplicações do Spark toorun Olá cluster ideal configuração?
os parâmetros de chave de Olá três que podem ser utilizados para a configuração de Spark consoante os requisitos da aplicação são `spark.executor.instances`, `spark.executor.cores`, e `spark.executor.memory`. Um Executor é um processo iniciado para uma aplicação de Spark. Este é executado no nó de trabalho de Olá e é responsável toocarry tarefas Olá para aplicação Olá. Olá predefinição o número de executor e tamanhos de executor de Olá para cada cluster é calculado com base no número de Olá de nós de trabalho e o tamanho de nó de trabalho de Olá. Estes são armazenados no `spark-defaults.conf` em nós principais do cluster Olá.

parâmetros de configuração de três Olá podem ser configurados ao nível do cluster Olá (para todas as aplicações que são executadas no cluster de Olá) ou podem ser especificados para cada aplicação individuais bem.

### <a name="change-hello-parameters-using-ambari-ui"></a>Altere os parâmetros de Olá utilizando a IU do Ambari
1. No Olá Ambari IU clique **Spark**, clique em **folhas**e, em seguida, expanda **personalizada spark-predefinições**.

    ![Parâmetros de conjunto com o Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. os valores predefinidos de Olá são executadas em simultâneo no cluster de Olá de aplicações do Spark toohave boa 4. Pode alterações estes valores na interface de utilizador de Olá, conforme mostrado abaixo.

    ![Parâmetros de conjunto com o Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Clique em **guardar** alterações de configuração de Olá toosave. Em Olá parte superior da página Olá, será solicitado toorestart Olá, todos os serviços afectados. Clique em **reiniciar**.

    ![Reinicie os serviços](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Altere os parâmetros de Olá para uma aplicação em execução no bloco de notas do Jupyter
Para aplicações em execução no bloco de notas do Jupyter Olá, pode utilizar Olá `%%configure` mágica alterações de configuração de Olá toomake. Idealmente, tem de se essas alterações no início de Olá da aplicação Olá, antes de executar a sua primeira célula do código. Isto garante que a configuração Olá é aplicado toohello Livy sessão, quando é criada. Se pretender que a configuração de Olá toochange uma fase posterior na aplicação Olá, tem de utilizar Olá `-f` parâmetro. No entanto, por se o fizer, todos os progresso na Olá aplicação serão perdida.

fragmento Olá abaixo mostra como toochange Olá configuração para uma aplicação em execução no Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Parâmetros de configuração tem de ser transmitidos como uma cadeia JSON e tem de estar na linha seguinte Olá após magic Olá, conforme apresentado na coluna de exemplo de Olá.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Parâmetros de Olá de alteração para uma aplicação enviados através de spark-submeter
Os seguintes comandos é um exemplo de como toochange Olá parâmetros de configuração para uma aplicação de batch que é submetido utilizando `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Altere os parâmetros de Olá para uma aplicação submetido utilizando cURL
Os seguintes comandos é um exemplo de como toochange Olá parâmetros de configuração para uma aplicação de batch que é submetido utilizando utilizando cURL.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Como posso alterar estes parâmetros num servidor Thrift de Spark?
Servidor Thrift de Spark fornece o cluster do Spark JDBC/ODBC acesso tooa e é utilizado tooservice consultas do Spark SQL. Ferramentas como o Power BI, Tableau etc. Utilize ODBC protocolo toocommunicate com as consultas de Spark SQL do servidor Thrift de Spark tooexecute como uma aplicação de Spark. Quando é criado um cluster do Spark, duas instâncias do Olá servidor Thrift de Spark são iniciados, e um em cada nó principal. Cada servidor Thrift de Spark é visível como uma aplicação do Spark no Olá IU do YARN.

Utiliza servidor Thrift de Spark Spark alocação dinâmica executor e, por conseguinte, Olá `spark.executor.instances` não é utilizado. Em vez disso, utiliza servidor Thrift de Spark `spark.dynamicAllocation.minExecutors` e `spark.dynamicAllocation.maxExecutors` contagem de executor de Olá toospecify. parâmetros de configuração de Olá `spark.executor.cores` e `spark.executor.memory` é utilizado o tamanho de executor de Olá toomodify. Pode alterar estes parâmetros, como mostrado abaixo.

* Expanda Olá **avançadas sparkconf de thrift de spark** parâmetros de Olá categoria tooupdate `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, e `spark.executor.memory`.

    ![Configurar o servidor thrift de Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Expanda Olá **personalizada spark-thrift-sparkconf** parâmetro de Olá categoria tooupdate `spark.executor.cores`.

    ![Configurar o servidor thrift de Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Como posso alterar Olá controladores de memória de Olá servidor Thrift de Spark?
Memória do servidor Thrift de Spark controlador é configurado too25% do tamanho do nó principal RAM Olá, fornecida Olá tamanho de RAM total do nó principal Olá é superior a 14GB. Pode utilizar Olá configuração de memória do Ambari IU toochange Olá controladores, como mostrado abaixo.

* No Olá Ambari IU clique **Spark**, clique em **folhas**, expanda **avançadas spark env**e, em seguida, forneça o valor de Olá para **spark_thrift_cmd_opts**.

    ![Configurar o servidor thrift de Spark RAM](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>Não utilizo BI com um cluster do Spark. Como devo efetuar recursos Olá novamente?
Uma vez que utilizamos alocação dinâmica Spark, hello apenas os recursos que são consumidos pelo servidor thrift são recursos Olá para Olá duas aplicações modelos de estrutura mestres. tooreclaim Olá, estes recursos que tem de parar serviços do servidor Thrift em execução no cluster de Olá.

1. Olá IU do Ambari, no painel esquerdo do Olá, clique em **Spark**.
2. Na página seguinte Olá, clique em **servidores de Thrift de Spark**.

    ![Reinicie o servidor thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Deverá ver dois headnodes Olá no qual Olá servidor Thrift de Spark está em execução. Clique das Olá headnodes.

    ![Reinicie o servidor thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. página seguinte Olá apresenta uma lista de todos os serviços de Olá em execução nesse headnode. Na lista de Olá clique Olá pendente botão seguinte tooSpark servidor Thrift e, em seguida, clique em **parar**.

    ![Reinicie o servidor thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Repita estes passos em Olá, bem como outra headnode.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>A minha blocos de notas do Jupyter não estão em execução conforme esperado. Como reiniciar o serviço de Olá?
Inicie Olá IU da Web do Ambari, conforme mostrado acima. No painel de navegação esquerdo Olá, clique em **Jupyter**, clique em **serviço ações**e, em seguida, clique em **todas reinicie**. Isto irá iniciar o serviço do Jupyter de Olá em todos os Olá headnodes.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Como saber se estiver a ficar sem recursos?
Inicie Olá IU do Yarn, conforme mostrado acima. Na tabela de métricas de Cluster por cima do ecrã de Olá, verifique os valores de **memória utilizada** e **memória Total** colunas. Se os valores de Olá 2 forem muito fechar, pode não existir suficiente aplicação seguinte do toostart Olá de recursos. Olá mesmo se aplica toohello **VCores utilizado** e **VCores Total** colunas. Além disso, na vista de principais de Olá, se existir uma aplicação stayed no **ACEITES** estado e não vão transitar para **executar** nem **falha** Estado, isto também pode ser uma indicação que não está a obter suficiente toostart de recursos.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Como eliminar uma execução toofree de aplicação dos recursos?
1. No Olá IU do Yarn, a partir do painel esquerdo do Olá, clique em **executar**. Na lista de Olá das aplicações em execução, determinar Olá aplicação toobe desativados e clique em Olá **ID**.

    ![Kill App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")

2. Clique em **Kill aplicação** Olá canto superior direito, em seguida, clique em **OK**.

    ![Kill App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")

## <a name="see-also"></a>Consultar também
* [Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>Para os analistas de dados

* [Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Análise de registos de sites com o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análise de dados telemétricos do Application Insight com o Spark no HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Utilizar Caffe no Azure HDInsight Spark para aprender profunda distribuída](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Para programadores do Spark

* [Criar uma aplicação autónoma com o Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar tarefas remotamente num cluster do Spark com o Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Utilizar o plug-in ferramentas do HDInsight para o IntelliJ IDEA toocreate e submeter aplicações do Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Utilizar o plug-in ferramentas do HDInsight para aplicações do Spark IntelliJ IDEA toodebug remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utilizar pacotes externos com blocos de notas do Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
