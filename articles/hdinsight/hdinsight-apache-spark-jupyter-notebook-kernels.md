---
title: clusters aaaKernels para bloco de notas do Jupyter no Spark no Azure HDInsight | Microsoft Docs
description: "Saiba mais sobre a kernels PySpark, PySpark3 e Spark Olá para bloco de notas do Jupyter disponível com clusters do Spark no Azure HDInsight."
keywords: Bloco de notas do jupyter no spark, spark do jupyter
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Kernels para bloco de notas do Jupyter nos clusters do Spark no Azure HDInsight 

Clusters do HDInsight Spark fornecem kernels que pode utilizar com o bloco de notas do Jupyter Olá no Spark para testar as suas aplicações. Um kernel é um programa que executa e interpreta o seu código. três kernels Olá são:

- **PySpark** – para aplicações escritas no Python2
- **PySpark3** – para aplicações escritas no Python3
- **O Spark** – para aplicações escritas no Scala

Neste artigo, saiba como toouse estes kernels e os benefícios de Olá de utilizá-los.

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte [clusters do Apache Spark criar no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Criar um bloco de notas do Jupyter no Spark HDInsight

1. De Olá [portal do Azure](https://portal.azure.com/), abra o seu cluster.  Consulte [clusters lista e mostrar](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) para obter instruções de Olá. cluster Olá está aberto num novo painel do portal.

2. De Olá **ligações rápidas** secção, clique em **Cluster dashboards** tooopen Olá **Cluster dashboards** painel.  Se não vir **ligações rápidas**, clique em **descrição geral** no menu à esquerda do Olá no painel de Olá.

    ![Bloco de notas do Jupyter no Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "bloco de notas do Jupyter no Spark") 

3. Clique em **bloco de notas do Jupyter**. Se lhe for solicitado, introduza as credenciais de administrador Olá para cluster Olá.
   
   > [!NOTE]
   > Também pode aceder notas do Jupyter Olá no cluster do Spark por abrir Olá seguinte URL no browser. Substitua **CLUSTERNAME** com o nome de Olá do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Clique em **novo**e, em seguida, clique em **Pyspark**, **PySpark3**, ou **Spark** toocreate um bloco de notas. Utilize o kernel do Spark Olá para aplicações de Scala, kernel do PySpark para aplicações de Python2 e PySpark3 kernel para aplicações de Python3.
   
    ![Kernels para bloco de notas do Jupyter no Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Kernels para bloco de notas do Jupyter no Spark") 

4. Um bloco de notas abre-se com o kernel Olá que selecionou.

## <a name="benefits-of-using-hello-kernels"></a>Vantagens da utilização kernels Olá

Seguem-se alguns benefícios da utilização kernels novo Olá com o bloco de notas do Jupyter nos clusters do Spark HDInsight.

- **Configuração predefinida contextos**. Com **PySpark**, **PySpark3**, ou Olá **Spark** kernels, não precisa de contextos de Spark ou Hive da Olá tooset explicitamente antes de começar a trabalhar com as suas aplicações. Estes estiverem disponíveis por predefinição. Estes contextos são:
   
   * **sc** – para o contexto do Spark
   * **sqlContext** – para o contexto de ramo de registo

    Por isso, não tem instruções de toorun como Olá contextos de Olá tooset os seguintes:

        sc = SparkContext('yarn-client') sqlContext = HiveContext(sc)

    Em vez disso, pode utilizar diretamente Olá contextos na sua aplicação da configuração predefinida.

- **Magia de células**. Olá kernel do PySpark fornece algumas predefinidas "magia", que são comandos especiais que pode chamar com `%%` (por exemplo, `%%MAGIC` <args>). comando mágica Olá tem de ser Olá primeiro numa célula de código e permitir várias linhas de conteúdo. word mágica Olá deverá ser Olá primeiro numa célula de Olá. Adicionar nada antes de magic Olá, mesmo comentários, causa um erro.     Para obter mais informações sobre a magia, consulte [aqui](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Olá tabela seguinte lista magia diferentes Olá disponível através de kernels Olá.

   | Magic | Exemplo | Descrição |
   | --- | --- | --- |
   | Ajuda |`%%help` |Gera uma tabela de todos os magia disponíveis Olá com exemplo e descrição |
   | informações |`%%info` |Informações da sessão para o ponto final de Livy atual Olá saídas |
   | Configurar |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Configura os parâmetros de Olá para criar uma sessão. Olá sinalizador force (-f) é obrigatório se já tiver sido criada uma sessão, que garante que sessão Olá é removido e recriado. Observe [POST /sessions de Livy corpo do pedido](https://github.com/cloudera/livy#request-body) para obter uma lista de parâmetros válidos. Os parâmetros devem ser transmitidos como uma cadeia JSON e tem de estar na linha seguinte Olá após magic Olá, conforme apresentado na coluna de exemplo de Olá. |
   | SQL Server |`%%sql -o <variable name>`<br> `SHOW TABLES` |Executa uma consulta do Hive contra Olá sqlContext. Se hello `-o` parâmetro é transmitido, Olá resultado de Olá consulta é continuado no Olá % % contexto de Python local como uma [Pandas](http://pandas.pydata.org/) dataframe. |
   | local |`%%local`<br>`a=1` |Todo o código de Olá linhas subsequentes é executado localmente. Código tem de ser válido Python2 código mesmo independentemente kernel Olá que estiver a utilizar. Sim, mesmo se tiver selecionado **PySpark3** ou **Spark** kernels ao criar o bloco de notas Olá, se utilizar Olá `%%local` mágica numa célula, nessa célula só podem ter código Python2 válido... |
   | registos |`%%logs` |Saídas hello registos para a sessão de Livy atual Olá. |
   | eliminar |`%%delete -f -s <session number>` |Elimina uma sessão do ponto final de Livy atual Olá específica. Tenha em atenção que não é possível eliminar a sessão de Olá iniciada para o kernel Olá próprio. |
   | Limpeza |`%%cleanup -f` |Elimina todas as sessões de Olá Olá atual Livy ponto final, incluindo sessão este bloco de notas. imposição de Olá sinalizador -f é obrigatório. |

   > [!NOTE]
   > Além disso toohello magia adicionado pelo kernel do PySpark Olá, também pode utilizar Olá [incorporada IPython magia](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), incluindo `%%sh`. Pode utilizar Olá `%%sh` mágica toorun scripts e bloco de código no Olá headnode de cluster.
   >
   >
2. **Auto visualização**. Olá **Pyspark** kernel automaticamente visualiza saída Olá de consultas do Hive e do SQL Server. Pode escolher entre vários tipos diferentes de visualizações incluindo tabela circular, linha, área, a barra.

## <a name="parameters-supported-with-hello-sql-magic"></a>Parâmetros suportados com Olá % % magic de sql
Olá `%%sql` magic suporta diferentes parâmetros que pode utilizar o tipo de Olá toocontrol de saída que recebe quando executar consultas. Olá, a tabela seguinte apresenta uma lista de saída de Olá.

| Parâmetro | Exemplo | Descrição |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Utilize este parâmetro toopersist Olá resultado de Olá consulta, Olá % % contexto de Python local, como um [Pandas](http://pandas.pydata.org/) dataframe. Olá o nome da variável de dataframe Olá é o nome da variável Olá que especificar. |
| -q |`-q` |Utilize este tooturn desativar visualizações para célula Olá. Se não quiser tooauto-visualizar conteúdo Olá de uma célula e deseje toocapture-o como um dataframe, em seguida, utilize `-q -o <VARIABLE>`. Se quiser tooturn desativar visualizações sem capturar resultados Olá (por exemplo, para executar uma consulta SQL, como um `CREATE TABLE` instrução), utilize `-q` sem especificar um `-o` argumento. |
| -m |`-m <METHOD>` |Onde **método** está **demorar** ou **exemplo** (predefinição é **demorar**). Se o método de Olá **demorar**, kernel Olá escolhe elementos de Olá parte superior do conjunto de dados de resultados de Olá especificado pelo MAXROWS (descrito mais à frente nesta tabela). Se o método de Olá **exemplo**, kernel Olá aleatoriamente amostras de elementos de conjunto de dados de Olá demasiado de acordo com`-r` parâmetro, descrito a seguir nesta tabela. |
| -r |`-r <FRACTION>` |Aqui **FRAÇÃO** é um número de vírgula flutuante entre 0,0 e 1,0. Se o método de exemplo de Olá para consulta SQL Olá é `sample`, então kernel Olá aleatoriamente amostras fração de especificado Olá dos elementos de Olá do resultado de Olá definido para si. Por exemplo, se executar uma consulta SQL com argumentos de Olá `-m sample -r 0.01`, em seguida, 1 a % de linhas de resultado Olá aleatoriamente servem como amostra. |
| -n |`-n <MAXROWS>` |**MAXROWS** é um valor de número inteiro. kernel Olá limita Olá número de linhas de saída demasiado**MAXROWS**. Se **MAXROWS** é como um número negativo **-1**, em seguida, Olá número de linhas no conjunto de resultados de Olá não é limitado. |

**Exemplo:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

declaração de Olá acima Olá seguintes:

* Seleciona todos os registos da **hivesampletable**.
* Uma vez que utilizamos - q, desligar automaticamente visualização.
* Uma vez que utilizamos `-m sample -r 0.1 -n 500` aleatoriamente de exemplo 10% de linhas Olá Olá hivesampletable e Olá, limites de tamanho de Olá resultado conjunto too500 linhas.
* Por fim, porque é utilizado `-o query2` também economizam saída Olá para um dataframe chamado **query2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Considerações ao utilizar Olá kernels novo

Qualquer kernel utilizar, deixar os blocos de notas Olá executar consome recursos do cluster Olá.  Com estas kernels porque contextos de Olá são a configuração predefinidos, basta sair blocos de notas Olá não kill contexto Olá e, por conseguinte, os recursos do cluster Olá continuar toobe em utilização. Uma boa prática é toouse Olá **fechar e parar** opção a partir do bloco de notas de Olá **ficheiro** menu quando tiver terminado de utilizar o bloco de notas Olá, que inutilizam contexto Olá e, em seguida, sai Olá bloco de notas.     

## <a name="show-me-some-examples"></a>Mostrar alguns exemplos

Quando abre um bloco de notas do Jupyter, verá duas pastas disponíveis no nível de raiz de Olá.

* Olá **PySpark** pasta tem blocos de notas do exemplo Olá que utilize novo **Python** kernel.
* Olá **Scala** pasta tem blocos de notas do exemplo Olá que utilize novo **Spark** kernel.

Pode abrir Olá **00 - [leia-ME primeiro] funcionalidades de Kernel do Spark Magic** bloco de notas do Olá **PySpark** ou **Spark** toolearn pasta sobre a magia diferentes Olá disponíveis. Também pode utilizar Olá outros blocos de notas do exemplo disponíveis em Olá duas pastas toolearn como tooachieve diferentes cenários de utilização de blocos de notas do Jupyter com clusters do HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>Onde estão armazenados os blocos de notas Olá?

Blocos de notas do Jupyter são guardados toohello conta de armazenamento associada ao cluster Olá em Olá **/HdiNotebooks** pasta.  Blocos de notas, ficheiros de texto e pastas que criar a partir de dentro do Jupyter são acessíveis a partir da conta de armazenamento Olá.  Por exemplo, se utilizar o Jupyter toocreate uma pasta **myfolder** e um bloco de notas **myfolder/mynotebook.ipynb**, pode aceder nesse bloco de notas em `/HdiNotebooks/myfolder/mynotebook.ipynb` na conta do storage Olá.  Olá inversa também se aplica, ou seja, se carregar um bloco de notas diretamente a conta de armazenamento tooyour em `/HdiNotebooks/mynotebook1.ipynb`, o bloco de notas do Olá é também visível a partir do Jupyter.  Blocos de notas permanecem na conta do storage Olá, mesmo depois do cluster Olá é eliminado.

blocos de notas são guardados toohello conta de armazenamento de forma de Olá é compatível com HDFS. Deste modo, se lhe SSH no cluster Olá, que pode utilizar comandos de gestão de ficheiros conforme mostrado no seguinte fragmento de Olá:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


No caso de existirem problemas de acesso à conta de armazenamento Olá para cluster Olá, blocos de notas Olá também são guardados no Olá headnode `/var/lib/jupyter`.

## <a name="supported-browser"></a>Browser suportado

Blocos de notas do Jupyter nos clusters do Spark HDInsight são suportados apenas no Google Chrome.

## <a name="feedback"></a>Comentários
kernels novo Olá estão em fase de evolução e serão madura ao longo do tempo. Isto pode significar que APIs alterar como estes kernels madura. Agradecemos quaisquer comentários que tenham ao utilizar estas kernels de novo. Isto é útil em formação de versão final do Olá destes kernels. Pode deixar os seus comentários comentários em Olá **comentários** secção na parte inferior de Olá deste artigo.

## <a name="seealso"></a>Ver também
* [Descrição geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de registos de sites com o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicações
* [Criar uma aplicação autónoma com o Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar tarefas remotamente num cluster do Spark com o Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Utilizar o plug-in ferramentas do HDInsight para o IntelliJ IDEA toocreate e submeter aplicações do Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizar o plug-in ferramentas do HDInsight para aplicações do Spark IntelliJ IDEA toodebug remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Utilizar pacotes externos com blocos de notas do Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerir recursos
* [Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight](hdinsight-apache-spark-job-debugging.md)
