---
title: aaaUse Kafka Apache Storm no HDInsight - Azure | Microsoft Docs
description: "Apache Kafka é instalado com Apache Storm no HDInsight. Saiba como toowrite tooKafka e, em seguida, leitura a partir do mesmo, utilizando Olá KafkaBolt e KafkaSpout componentes fornecidos com o Storm. Também pode aprender como toouse Olá Flux framework toodefine e submeter topologias do Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Utilizar o Apache Kafka (pré-visualização) com o Storm no HDInsight

Saiba como toouse Apache Storm tooread de e escrevem tooApache Kafka. Este exemplo também demonstra como o sistema utilizado pelo HDInsight de ficheiros de dados toosave um toohello de topologia do Storm compatível com HDFS.

> [!NOTE]
> passos de Olá neste documento, criar um grupo de recursos do Azure que contém tanto um Storm no HDInsight e um Kafka num cluster do HDInsight. Esses clusters são ambos localizado dentro de uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Storm comunicam com Olá Kafka cluster.
> 
> Quando tiver terminado com os passos de Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.

## <a name="get-hello-code"></a>Obter o código de Olá

código de Olá, por exemplo Olá utilizado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile este projeto, terá de seguir a configuração para o seu ambiente de desenvolvimento de Olá:

* [1.8 do Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior. HDInsight 3.5 ou superior necessário Java 8.

* [Maven 3](https://maven.apache.org/download.cgi)

* Um cliente SSH (terá Olá `ssh` e `scp` comandos) – para obter informações, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Num editor de texto ou IDE.

Olá seguintes variáveis de ambiente podem ser definidas quando instalar o Java e Olá JDK na sua estação de trabalho de desenvolvimento. No entanto, deve verificar que existe e que contêm valores corretos a Olá para o seu sistema.

* `JAVA_HOME`-devem apontar toohello diretório onde hello JDK está instalado.
* `PATH`-deve conter Olá seguintes caminhos:
  
    * `JAVA_HOME`(ou um caminho equivalente Olá).
    * `JAVA_HOME\bin`(ou um caminho equivalente Olá).
    * diretório de olá onde Maven está instalado.

## <a name="create-hello-clusters"></a>Criar clusters Olá

Apache Kafka no HDInsight fornece acesso toohello Kafka mediadores Olá internet pública. Olá tudo o que Olá, talks tooKafka tem de estar na mesma rede virtual do Azure como nós de Olá num cluster de Kafka. Para este exemplo Olá Kafka e clusters de Storm estão localizados numa rede virtual do Azure. Olá diagrama seguinte mostra como flui de comunicação entre clusters de Olá:

![Diagrama de clusters Storm e Kafka uma Azure virtual network](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Outros serviços em cluster Olá, tais como podem ser acedido através de SSH e Ambari Olá internet. Para obter mais informações sobre portas pública Olá disponíveis com o HDInsight, consulte [portas e os URIs utilizados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Pode criar uma Azure virtual network, Kafka, e clusters de Storm manualmente, é mais fácil toouse um modelo Azure Resource Manager. Seguinte de Olá utilize os passos toodeploy uma Azure virtual network, Kafka, e clusters de Storm tooyour subscrição do Azure.

1. Utilize Olá seguinte botão toosign no tooAzure e o modelo de Olá aberta no Olá portal do Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Olá modelo Azure Resource Manager está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Cria Olá os seguintes recursos:
    
    * Grupo de recursos do Azure
    * Rede Virtual do Azure
    * Conta de armazenamento do Azure
    * Kafka no HDInsight versão 3.6 (três nós de trabalho)
    * Storm no HDInsight versão 3.6 (três nós de trabalho)

  > [!WARNING]
  > disponibilidade de tooguarantee dos Kafka no HDInsight, o cluster tem de conter, pelo menos, três nós de trabalho. Este modelo cria um cluster Kafka contém três nós de trabalho.

2. Olá utilizar seguindo as entradas do orientações toopopulate Olá do Olá **implementação personalizada** painel:
   
    ![Implementação personalizada do HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Grupo de recursos**: criar um grupo ou selecione um existente. Este grupo contém o cluster do HDInsight Olá.
   
    * **Localização**: selecione uma tooyou fechar geograficamente da localização.

    * **Nome do Cluster de base**: este valor é utilizado como nome de base de Olá para clusters de Storm e Kafka Olá. Por exemplo, introduzir **hdi** cria um cluster do Storm com o nome **storm hdi** e um cluster de Kafka denominado **kafka hdi**.
   
    * **Nome de utilizador de início de sessão do cluster**: nome de utilizador de admin Olá para clusters de Storm e Kafka Olá.
   
    * **Palavra-passe de início de sessão do cluster**: palavra-passe utilizador de administrador de Olá para clusters de Storm e Kafka Olá.
    
    * **Nome de utilizador SSH**: Olá toocreate de utilizador do SSH para clusters de Storm e Kafka Olá.
    
    * **Palavra-passe SSH**: Olá palavra-passe do utilizador do SSH Olá para clusters de Storm e Kafka Olá.

3. Olá leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições indicadas acima**.

4. Por fim, verifique **Pin toodashboard** e, em seguida, selecione **Compra**. Demora cerca de 20 minutos toocreate clusters Olá.

Depois de tem sido criados recursos Olá, é apresentado o painel de Olá Olá grupo de recursos.

![Painel do grupo de recursos para vnet Olá e clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Tenha em atenção que os nomes de Olá dos clusters do HDInsight Olá são **storm BASENAME** e **kafka BASENAME**, onde BASENAME nome Olá fornecido toohello modelo. Ao ligar a toohello clusters é utilizar estes nomes em passos posteriores.

## <a name="understanding-hello-code"></a>Compreender o código de Olá

Este projeto contém duas topologias:

* **KafkaWriter**: definidos pela Olá **writer.yaml** ficheiro, esta topologia escreve tooKafka frases aleatória utilizando Olá KafkaBolt fornecido com Apache Storm.

    Esta topologia utiliza personalizadas **SentenceSpout** frases aleatório do componente toogenerate.

* **KafkaReader**: definidos pela Olá **reader.yaml** ficheiro, esta topologia lê dados de Kafka utilizando Olá KafkaSpout fornecido com Apache Storm, em seguida, os registos Olá toostdout de dados.

    Esta topologia utiliza Olá Storm HdfsBolt toowrite dados toodefault um armazenamento de cluster do Storm Olá.
### <a name="flux"></a>Flux

topologias de Olá são definidas utilizando [Flux](https://storm.apache.org/releases/1.1.0/flux.html). Flux foi introduzida no Storm 0.10.x e permite-lhe configuração da topologia Olá tooseparate a partir do código Olá. Para as topologias que utilizam a estrutura do Flux de Olá, a topologia de Olá está definida num ficheiro YAML. ficheiro YAML Olá pode ser incluído como parte da topologia de Olá. Também pode ser um ficheiro autónomo utilizado ao submeter a topologia de Olá. Flux também suporta a substituição das variáveis em tempo de execução, que é utilizada neste exemplo.

Olá parâmetros seguintes são definidos em tempo de execução para estes topologias:

* `${kafka.topic}`: nome Olá Olá tópico Kafka que topologias Olá leitura/escritam.

* `${kafka.broker.hosts}`: Olá aloja esse Olá Kafka mediadores executar. informações de Mediador de Olá utilizadas pelo Olá KafkaBolt escrever tooKafka.

* `${kafka.zookeeper.hosts}`: anfitriões Olá Zookeeper executado em Olá Kafka cluster.

Para obter mais informações sobre topologias Flux, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Transferir e compilar o projeto de Olá

1. No seu ambiente de desenvolvimento, transfira o projeto de Olá de [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra uma linha de comandos e altere a localização de toohello de diretórios que transferiu o projeto de Olá.

2. De Olá **hdinsight-storm-java-kafka** diretório, utilize seguinte de Olá projeto de Olá toocompile de comandos e cria um pacote de implementação:

  ```bash
  mvn clean package
  ```

    processo de pacote de Olá cria um ficheiro denominado `KafkaTopology-1.0-SNAPSHOT.jar` no Olá `target` diretório.

3. Utilize Olá os seguintes comandos toocopy Olá pacote tooyour Storm num cluster do HDInsight. Substitua **USERNAME** com o nome de utilizador do SSH Olá para cluster Olá. Substitua **BASENAME** com o nome de base de Olá utilizado ao criar o cluster de Olá.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Quando lhe for pedido, introduza a palavra-passe de Olá utilizado aquando da criação de clusters de Olá.

## <a name="configure-hello-topology"></a>Configurar a topologia de Olá

1. Utilize um dos Olá seguintes métodos toodiscover Olá anfitriões de Mediador Kafka:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Olá Bash exemplo assume que `$CLUSTERNAME` contém Olá nome do cluster do HDInsight Olá. Também parte do princípio que [jq](https://stedolan.github.io/jq/) está instalado. Quando lhe for pedido, introduza a palavra-passe de Olá para a conta de início de sessão do cluster Olá.

    valor de Olá devolvido é semelhante toohello seguinte texto:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Enquanto pode ser mais do que dois mediador anfitriões para o cluster, não precisa de tooprovide uma lista completa de todos os anfitriões tooclients. Um ou dois são suficiente.

2. Utilize um dos Olá anfitriões de Kafka Zookeeper métodos toodiscover Olá os seguintes:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Olá Bash exemplo assume que `$CLUSTERNAME` contém Olá nome do cluster do HDInsight Olá. Também parte do princípio que [jq](https://stedolan.github.io/jq/) está instalado. Quando lhe for pedido, introduza a palavra-passe de Olá para a conta de início de sessão do cluster Olá.

    valor de Olá devolvido é semelhante toohello seguinte texto:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Enquanto existirem mais de dois nós de Zookeeper, não precisa de tooprovide uma lista completa de todos os anfitriões tooclients. Um ou dois são suficiente.

    Guarde este valor, porque é utilizado mais tarde.

3. Editar Olá `dev.properties` ficheiro na raiz de Olá do projeto de Olá. Adicione Olá mediador e linhas com correspondência do Zookeeper anfitriões informações toohello neste ficheiro. Olá exemplo seguinte é configurado utilizando os valores de exemplo de Olá dos passos anteriores Olá:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Guardar Olá `dev.properties` ficheiro e, em seguida, utilize Olá os seguintes comandos tooupload este cluster do Storm toohello:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Substitua **USERNAME** com o nome de utilizador do SSH Olá para cluster Olá. Substitua **BASENAME** com o nome de base de Olá utilizado ao criar o cluster de Olá.

## <a name="start-hello-writer"></a>Escritor de Olá de início

1. Utilize Olá seguir o cluster do Storm tooconnect toohello utilizando SSH. Substitua **USERNAME** com o nome de utilizador SSH Olá utilizado ao criar o cluster de Olá. Substitua **BASENAME** com o nome de base Olá utilizado ao criar o cluster de Olá.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Quando lhe for pedido, introduza a palavra-passe de Olá utilizado aquando da criação de clusters de Olá.
   
    Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

2. A partir de Olá ligação SSH, utilize Olá Olá toocreate do comando tópico Kafka utilizado por topologia Olá os seguintes:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Substitua `$KAFKAZKHOSTS` com Olá Zookeeper informações que obteve na secção anterior Olá do anfitrião.

2. A partir do cluster do Olá SSH ligação toohello Storm, utilize Olá topologia de escritor do comando toostart Olá os seguintes:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    os parâmetros de Olá utilizados com este comando são:

    * `org.apache.storm.flux.Flux`: Utilize Flux tooconfigure e execute esta topologia.

    * `--remote`: Olá topologia tooNimbus de envio. topologia de Olá é distribuída entre os nós de trabalho Olá num cluster de Olá.

    * `-R /writer.yaml`: Olá utilize `writer.yaml` topologia de Olá tooconfigure de ficheiros. `-R`indica que este recurso está incluído no ficheiro de jar Olá. É por isso, na raiz de Olá da jar Olá, `/writer.yaml` é Olá tooit de caminho.

    * `--filter`: A preencher a entradas no Olá `writer.yaml` topologia com valores no Olá `dev.properties` ficheiro. Olá, por exemplo, o valor de Olá `kafka.topic` entrada no ficheiro de Olá é utilizado tooreplace Olá `${kafka.topic}` entrada na definição de topologia Olá.

5. Depois de é iniciado a topologia de Olá, utilize Olá tooverify de comando que está a escrever dados toohello tópico Kafka os seguintes:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Substitua `$KAFKAZKHOSTS` com Olá Zookeeper informações que obteve na secção anterior Olá do anfitrião.

    Este comando utiliza um script vem incluído no tópico de Olá Kafka toomonitor. Após um momento, este deve iniciar aleatórios frases escritos toohello tópico a devolver. Olá de saída é semelhante toohello seguinte exemplo:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Utilize Ctrl + c toostop script de Olá.

## <a name="start-hello-reader"></a>Início Olá leitor

1. A partir do cluster do Olá SSH sessão toohello Storm, utilize Olá topologia de leitor do comando toostart Olá os seguintes:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Assim que for iniciada a topologia de Olá, abra Olá IU do Storm. Este IU da web está localizado em https://storm-BASENAME.azurehdinsight.net/stormui. Substitua __BASENAME__ com o nome de base Olá utilizada quando Olá cluster foi criado. 

    Quando lhe for pedido, utilize o nome de início de sessão de administrador Olá (predefinição, `admin`) e palavra-passe utilizada quando Olá cluster foi criado. Consulte uma toohello semelhante de página web seguinte imagem:

    ![IU do Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Na IU do Storm Olá, selecione Olá __kafka leitor__ ligação no Olá __resumo da topologia__ secção toodisplay informações sobre Olá __kafka leitor__ topologia.

    ![Secção de resumo da topologia da IU da web do Olá Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. informações de toodisplay sobre Olá as instâncias do componente de registo bolt Olá, selecione Olá __registador bolt__ ligação no Olá __Bolts (tempo)__ secção.

    ![Ligação registador bolt Olá bolts secção](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. No Olá __executores__ secção, selecione uma ligação na Olá __porta__ informações de registo de toodisplay coluna sobre esta instância do componente de Olá.

    ![Executores ligação](./media/hdinsight-apache-storm-with-kafka/executors.png)

    registo de Olá contém um registo de dados de Olá lidos Olá tópico Kafka. informações de Olá no registo de Olá são semelhante toohello seguinte texto:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Parar topologias Olá

A partir de um cluster do Storm do SSH sessão toohello, utilize Olá topologias do Storm comandos toostop Olá os seguintes:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Eliminar cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Uma vez que os passos neste documento Olá criar ambos Olá de clusters no mesmo grupo de recursos do Azure, pode eliminar o grupo de recursos Olá Olá portal do Azure. Eliminar grupo de recursos de Olá remove todos os recursos que criou ao seguir este documento.

## <a name="next-steps"></a>Passos seguintes

Para obter mais topologias de exemplo que podem ser utilizadas com o Storm no HDInsight, consulte [topologias do Storm de exemplo e componentes](hdinsight-storm-example-topology.md).

Para obter informações sobre como implementar e monitorizar topologias no HDInsight baseado em Linux, consulte [implementar e gerir topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)