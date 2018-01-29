---
title: "Utilizar Caffe no Azure HDInsight Spark para aprender profunda distribuída | Microsoft Docs"
description: "Utilizar Caffe no Azure HDInsight Spark para aprender profunda distribuída"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: 7565efd82945f21b83471ee66098cd476b7bb59f
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/08/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Utilizar Caffe no Azure HDInsight Spark para aprender profunda distribuída


## <a name="introduction"></a>Introdução

Learning profunda está a afetar tudo healthcare para transportes para fabrico e muito mais. As empresas ativa para avançada de aprendizagem resolver problemas de disco rígidos, como [imagem classificação](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [reconhecimento de voz](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), reconhecimento de objeto e tradução do computador. 

Existem [muitas arquiteturas populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), incluindo [Toolkit de cognitivos](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe é uma das estruturas de não simbólico rede neuronal (imperativo) mais famosa e amplamente utilizado em várias áreas, incluindo problemas de visão do computador. Além disso, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina Caffe Apache spark, caso em que profundo learning pode ser facilmente utilizado num cluster de Hadoop existente. Pode utilizar profunda learning, juntamente com os pipelines de ETL de Spark, reduzir a complexidade de sistema e latência de aprendizagem solução completa.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) é uma nuvem Hadoop oferta que fornece clusters de análise de open source para otimizado para Spark, Hive, Hadoop, HBase, Storm, Kafka e servidor R. HDInsight é copiado por um SLA de 99,9%. Cada uma destas tecnologias de macrodados e aplicações de ISV é facilmente implementável como clusters geridos com segurança e monitorização para empresas.

Este artigo demonstra como instalar [Caffe no Spark](https://github.com/yahoo/CaffeOnSpark) para um cluster do HDInsight. Este artigo utiliza também a demonstração MNIST incorporada para mostrar como utilizar Learning profunda distribuídas através do HDInsight Spark nas CPUs.

Existem quatro passos principais para obtê-lo a trabalham no HDInsight.

1. Instale as dependências necessárias em todos os nós
2. Criar Caffe no Spark para o HDInsight no nó principal
3. Distribuir as bibliotecas necessárias para todos os nós de trabalho
4. Componha um modelo de Caffe e executá-lo de forma distribuída.

Uma vez que o HDInsight é uma solução de PaaS, oferece funcionalidades ótimos plataforma - para que seja fácil efetuar algumas tarefas. Uma das funcionalidades que utilizamos descontos elevados nesta mensagem de blogue denomina [ação de Script](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), com o qual pode executar comandos da shell para personalizar nós de cluster (nó principal, nó de trabalho ou nó de extremidade).

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a>Passo 1: Instalar dependências necessárias em todos os nós

Para começar, precisamos de instalar as dependências, que é necessário. O site Caffe e [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) oferece algumas wiki úteis para instalar as dependências para o Spark no modo YARN. Também o HDInsight utiliza o Spark no modo YARN. No entanto, precisamos de adicionar alguns dependências mais para a plataforma do HDInsight. Para tal, utilize uma ação de script e execute-a em todos os nós principais e nós de trabalho. Esta ação de script demora cerca de 20 minutos, como dessas dependências dependem também outros pacotes. Deve colocá-la em algumas localização que esteja acessível ao cluster do HDInsight, como uma localização do GitHub ou a conta de armazenamento de BLOBS predefinido.

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


Existem dois passos a ação de script. O primeiro passo é instalar as bibliotecas necessárias. As bibliotecas de incluem as bibliotecas necessárias para compilar Caffe (por exemplo, gflags, glog) e em execução Caffe (por exemplo, numpy). Estamos a utilizar libatlas para a otimização de CPU, mas pode seguir sempre CaffeOnSpark wiki sobre como instalar outras bibliotecas de otimização, tais como MKL ou CUDA (para a GPU).

O segundo passo é para transferir, de compilação e instalar protobuf 2.5.0 para Caffe durante o tempo de execução. Protobuf 2.5.0 [é necessário](https://github.com/yahoo/CaffeOnSpark/issues/87); no entanto, esta versão não está disponível como um pacote no Ubuntu 16, pelo que temos de compilá-la a partir do código de origem. Existem também alguns recursos na Internet no como compilá-la. Para obter mais informações, consulte [aqui](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html).

Para começar a utilizar, pode apenas executar esta ação de script contra o cluster para todos os nós de trabalho e nós principais (para o HDInsight 3.5). Pode executar as ações de script num cluster existente ou utilize ações do script durante a criação do cluster. Para obter mais informações sobre as ações de script, consulte a documentação [aqui](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions).

![Ações de script para instalar dependências](./media/apache-spark-deep-learning-caffe/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a>Passo 2: Criar Caffe no Spark para o HDInsight no nó principal

O segundo passo é criar Caffe no headnode e, em seguida, distribuir as bibliotecas compiladas para todos os nós de trabalho. Neste passo, terá [ssh no seu headnode](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix). Depois disso, tem de seguir a [CaffeOnSpark criar processo](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn). Segue-se o script que pode utilizar para criar CaffeOnSpark com alguns passos adicionais. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Terá de fazer mais do que o que indica a documentação do CaffeOnSpark. As alterações são:
- Altere a CPU apenas e utilizar libatlas para esta finalidade específica.
- Coloque os conjuntos de dados para o armazenamento de BLOBS, que é uma localização partilhada que está acessível para todos os nós de trabalho para utilização posterior.
- Colocar as bibliotecas de Caffe compiladas para o BLOB storage e mais tarde copiar esses bibliotecas para todos os nós utilizando ações de script para evitar o tempo de compilação adicionais.


### <a name="troubleshooting-an-ant-buildexception-has-occurred-exec-returned-2"></a>Resolução de problemas: Uma BuildException Ant ocorreu: exec devolvido: 2

Quando tenta primeiro criar CaffeOnSpark, por vezes, diz

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Limpar o repositório de código por "tornar limpa" e, em seguida, execute "faça criar" para resolver este problema, desde que tenham as dependências corretas.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Resolução de problemas: Limite de ligação do repositório de Maven

Por vezes, maven fornece um erro de tempo limite de ligação, semelhante à seguinte fragmento:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Tem a novamente após alguns minutos.


### <a name="troubleshooting-test-failure-for-caffe"></a>Resolução de problemas: Falha teste para Caffe

Provavelmente, verá uma falha de teste ao efetuar a verificação final CaffeOnSpark. Isto é provavelmente relacionado com codificação UTF-8, mas não deve afetar a utilização de Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a>Passo 3: Distribuir as bibliotecas necessárias para todos os nós de trabalho

O passo seguinte é para distribuir as bibliotecas (basicamente as bibliotecas na CaffeOnSpark/caffe-público/distribuir/lib/e CaffeOnSpark/caffe-distri/distribuir/lib /) para todos os nós. No passo 2, vamos colocar as bibliotecas no armazenamento de BLOBS e neste passo, utilizamos ações de script para copiá-los para todos os nós principais e nós de trabalho.

Para tal, execute uma ação de script, conforme mostrado no seguinte fragmento:

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Certifique-se que precisa de ponto para a localização correta específico para o cluster)

Porque no passo 2, iremos colocá-la no armazenamento de BLOBS, que está acessível para todos os nós, este passo é apenas copiá-los para todos os nós.

## <a name="step-4-compose-a-caffe-model-and-run-it-in-a-distributed-manner"></a>Passo 4: Compor um modelo de Caffe e executá-lo de forma distribuída

Está instalada Caffe depois de executar os passos anteriores. O passo seguinte é escrever um modelo de Caffe. 

Caffe utilizando uma "expressivas arquitetura", onde para composição um modelo, apenas terá de definir um ficheiro de configuração e sem codificação em todos os (na maioria dos casos). Por isso, vamos ver não existe. 

O modelo, que vamos dar formação sobre é um modelo de exemplo para formação MNIST. A base de dados MNIST dígitos handwritten tem um conjunto de preparação de 60 000 exemplos e um conjunto de teste de 10 000 exemplos. É um subconjunto de um conjunto maior disponível a partir do NIST. Os dígitos foram normalizado de tamanho e centrado numa imagem de tamanho fixo. CaffeOnSpark tem alguns scripts para transferir o conjunto de dados e convertê-lo num formato correto.

CaffeOnSpark fornece alguns exemplos de topologias de rede para formação MNIST. Tem uma estrutura nice de divisão a arquitetura de rede (a topologia da rede) e a otimização. Neste caso, existem dois ficheiros necessários: 

o ficheiro de "pelo solucionador" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) é utilizado para a otimização de supervisionar e gerar parâmetro atualizações. Por exemplo, define se CPU ou para a GPU é utilizado, o que é momentum, o número de iterações são, etc. Também define que topologia de rede neuron deve o programa utilizar (que é o segundo ficheiro que é necessário). Para mais informações sobre Solver, consulte [Caffe documentação](http://caffe.berkeleyvision.org/tutorial/solver.html).

Para este exemplo, uma vez que estamos a utilizar CPU em vez de GPU, iremos deve alterar a última linha para:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuração de Caffe](./media/apache-spark-deep-learning-caffe/Caffe-1.png)

Pode alterar outras linhas conforme necessário.

O segundo ficheiro (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define como rede neuron aspeto e a entrada relevante e ficheiro de saída. Também é necessário atualizar o ficheiro para refletir a localização de dados de formação. Altere a parte seguinte do lenet_memory_train_test.prototxt (tem de apontar para a localização correta específica para o cluster):

- Altere o "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" para "wasb: / / / projetos/machine_learning/image_dataset/mnist_train_lmdb"
- Altere "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" para "wasb: / / / projetos/machine_learning/image_dataset/mnist_test_lmdb"

![Configuração de Caffe](./media/apache-spark-deep-learning-caffe/Caffe-2.png)

Para obter mais informações sobre como definir a rede, verifique o [Caffe documentação MNIST conjunto de dados](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

Neste artigo, vamos utilizar este exemplo MNIST. Execute os seguintes comandos a partir do nó principal:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

O comando anterior distribui os ficheiros necessários (lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt) para cada contentor YARN. O comando define também o caminho de cada controlador de Spark/executor relevante para LD_LIBRARY_PATH. LD_LIBRARY_PATH está definido no fragmento de código anterior e aponta para a localização que tenha CaffeOnSpark bibliotecas. 

## <a name="monitoring-and-troubleshooting"></a>Monitorização e resolução de problemas

Uma vez que estamos a utilizar o modo de cluster YARN, caso em que o controlador de Spark será agendado para um contentor arbitrário (e um nó de trabalho arbitrários) deverá apenas ver na consola do exportar algo semelhante ao seguinte:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Se pretender saber o que aconteceu, normalmente, terá de obter o Spark o registo do controlador, que tem mais informações. Neste caso, terá de ir para a IU do YARN para localizar os registos YARN relevantes. Pode obter a IU do YARN por este URL: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![IU DO YARN](./media/apache-spark-deep-learning-caffe/YARN-UI-1.png)

Pode demorar uma vista de olhos quantidade de recursos é atribuídos para esta aplicação em particular. Pode clicar na ligação "Programador" e, em seguida, verá que para esta aplicação, existem 9 contentores em execução. Vamos pedir o YARN para fornecer 8 executores, não sendo outro contentor para o processo de controladores. 

![YARN Programador](./media/apache-spark-deep-learning-caffe/YARN-Scheduler.png)

Poderá verificar os registos de controlador ou registos do contentor se existirem falhas. Registos de controladores, pode clique o ID da aplicação na IU do YARN, em seguida, clique no botão "Iniciar". Os registos de controladores são escritos em stderr.

![IU DO YARN 2](./media/apache-spark-deep-learning-caffe/YARN-UI-2.png)

Por exemplo, poderá ver alguns do erro abaixo dos registos de controladores, com a indicação de que alocar o executor demasiados.

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

Por vezes, o problema pode ocorrer num executores em vez de controladores. Neste caso, terá de verificar os registos do contentor. Pode obter sempre os registos do contentor e, em seguida, obter o contentor de falha. Por exemplo, poderá cumprir esta falha ao executar Caffe.

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

Neste caso, terá de obter o ID de contentor com falhas (no caso de acima, está container_1485916338528_0008_05_000005). Em seguida, tem de executar 

    yarn logs -containerId container_1485916338528_0008_03_000005

de headnode. Após verificar a falha de contentor, este é causado utilizando o modo GPU (onde deve utilizar o modo de CPU em vez disso) no lenet_memory_solver.prototxt.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Obter resultados

Uma vez que vamos são alocar 8 executores e a topologia de rede é simple, apenas deve demorar cerca de 30 minutos para o resultado da execução. Na linha de comandos, pode ver que vamos colocar o modelo para wasb:///mnist.model e colocar os resultados para uma pasta denominada wasb: / / / mnist_features_result.

Pode obter os resultados ao executar

    hadoop fs -cat hdfs:///mnist_features_result/*

e o resultado semelhante:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

O SampleID representa o ID no conjunto de dados MNIST e a etiqueta é o número que identifica o modelo.


## <a name="conclusion"></a>Conclusão

Nesta documentação, tentou instalar CaffeOnSpark com a execução de um exemplo simples. HDInsight é uma plataforma de computação distribuída completa de nuvem gerido e é o melhor local para executar o machine learning e análise avançadas cargas de trabalho num grande conjunto de dados e de aprendizagem profunda distribuída, pode utilizar Caffe no Spark do HDInsight para executar tarefas de aprendizagem profunda.


## <a name="seealso"></a>Ver também
* [Descrição geral: Apache Spark no Azure HDInsight](apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC](apache-spark-ipython-notebook-machine-learning.md)
* [Spark com Machine Learning: Utilizar o Spark no HDInsight para prever resultados de inspeções alimentares](apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Gerir recursos
* [Gerir recursos para o cluster do Apache Spark no Azure HDInsight](apache-spark-resource-manager.md)

