---
title: "aaaTroubleshoot Storm através do Azure HDInsight | Microsoft Docs"
description: Obtenha respostas toocommon perguntas sobre como utilizar o Apache Storm com o Azure HDInsight.
keywords: "FAQ do HDInsight, Storm, do Azure, manual, problemas comuns de resolução de problemas"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Resolver problemas de Storm através do Azure HDInsight

Saiba mais sobre os principais problemas de Olá e as resoluções para trabalhar com payloads do Apache Storm no Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Como posso aceder Olá IU do Storm num cluster
Tem duas opções para aceder ao hello IU do Storm num browser:

### <a name="ambari-ui"></a>IU do Ambari
1. Aceda toohello Ambari dashboard.
2. Na lista de Olá de serviços, selecione **Storm**.
3. No Olá **ligações rápidas** menu, selecione **IU do Storm**.

### <a name="direct-link"></a>Ligação direta
Pode aceder Olá IU do Storm em Olá seguinte URL:

https://\<nome DNS de cluster\>/stormui

Exemplo:

 https://stormcluster.azurehdinsight.NET/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Como transferir informações de ponto de verificação do Storm event hub spout a partir de uma topologia tooanother

Quando desenvolver topologias ler a partir do Event Hubs do Azure utilizando Olá o ficheiro. JAR do HDInsight Storm event hub spout, tem de implementar uma topologia que tenha Olá mesmo nome num cluster de novo. No entanto, tem de manter os dados de ponto de verificação de Olá foi consolidada tooApache ZooKeeper no cluster antigo Olá.

### <a name="where-checkpoint-data-is-stored"></a>Armazenar dados de ponto de verificação
Dados de ponto de verificação para desvios são armazenados pelo Olá event hub spout no ZooKeeper em dois caminhos de raiz:
- Pontos de verificação do Nontransactional spout são armazenados no /eventhubspout.
- Dados de ponto de verificação de spout transacional são armazenados na / transacional.

### <a name="how-toorestore"></a>Como toorestore
scripts de Olá tooget e as bibliotecas que utiliza dados tooexport fora ZooKeeper e, em seguida, importar Olá dados back-tooZooKeeper com um novo nome, consulte [exemplos de HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

pasta de lib Olá tem ficheiros. JAR que contém a implementação de Olá para a operação de exportação/importação de Olá. pasta de bash Olá tem um script de exemplo que demonstra como dados tooexport Olá servidor ZooKeeper no cluster antigo Olá e, em seguida, importe-o servidor de ZooKeeper back toohello no novo cluster de Olá.

Executar Olá [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script de tooexport de nós de ZooKeeper Olá e, em seguida, importar dados. Atualização Olá script toohello Hortonworks Data Platform (HDP) versão correta. (Estamos a trabalhar efetuar estes scripts genérico no HDInsight. Genéricos podem executar scripts de qualquer nó no cluster de Olá sem modificações por utilizador Olá.)

comando de exportação de Olá escreve Olá metadados tooan sistema de ficheiros distribuído do Apache Hadoop (HDFS) caminho (na loja Blob Storage do Azure ou do Azure Data Lake Store) numa localização que definir.

### <a name="examples"></a>Exemplos

#### <a name="export-offset-metadata"></a>Exportar metadados de deslocamento
1. Utilize o cluster do SSH toogo toohello ZooKeeper num cluster de Olá do ponto de verificação que Olá deslocamento tem toobe exportado.
2. Olá executar seguinte comando (depois de atualizar Olá cadeia de versão HDP) tooexport ZooKeeper deslocamento dados toohello /stormmetadta/zkdata HDFS caminho:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importar metadados de deslocamento
1. Utilize o cluster do SSH toogo toohello ZooKeeper num cluster de Olá do ponto de verificação que Olá deslocamento tem toobe exportado.
2. Execute hello os seguintes comandos (depois de atualizar a cadeia de versão Olá HDP) tooimport ZooKeeper deslocamento de dados de Olá HDFS caminho/stormmetadata/zkdata toohello ZooKeeper servidor no cluster de destino Olá:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Eliminar os metadados de deslocamento para que as topologias podem começar a processar dados a partir do início de Olá ou de um timestamp escolhe esse utilizador Olá
1. Utilize o cluster do SSH toogo toohello ZooKeeper num cluster de Olá do ponto de verificação que Olá deslocamento tem toobe exportado.
2. Execute hello os seguintes comandos (depois de atualizar a cadeia de versão Olá HDP) toodelete todos os dados em cluster atual Olá de deslocamento de ZooKeeper:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Como localizar o binários de Storm num cluster
Os binários de Storm para a pilha HDP atual Olá são /usr/hdp/current/storm-client. localização de Olá é Olá mesmo para nós principais e nós de trabalho.
 
Podem existir vários binários para versões HDP específicas no /usr/hdp (por exemplo, /usr/hdp/2.5.0.1233/storm). pasta de /usr/hdp/current/storm-client Olá é symlinked toohello versão mais recente que está em execução no cluster de Olá.

Para obter mais informações, consulte [Connect tooan cluster do HDInsight utilizando SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Como determinar a topologia de implementação de Olá de um cluster do Storm
Em primeiro lugar, identifique todos os componentes que são instalados com o HDInsight Storm. Um cluster do Storm é constituída por quatro categorias de nó:

* Nós de gateway
* Nós de cabeçalho
* Nós de zooKeeper
* Nós de trabalho
 
### <a name="gateway-nodes"></a>Nós de gateway
Um nó de gateway é um gateway e o serviço de proxy inverso que permite o serviço de gestão de Ambari Active Directory do acesso público tooan. Ele também faz eleição de leader do Ambari.
 
### <a name="head-nodes"></a>Nós de cabeçalho
Nós principais do Storm executam Olá os seguintes serviços:
* Nimbus
* Servidor do Ambari
* Servidor de métricas do Ambari
* Recoletor de métricas do Ambari
 
### <a name="zookeeper-nodes"></a>Nós de zooKeeper
O HDInsight inclui um quórum de ZooKeeper três nós. tamanho de quórum Olá é fixo e não pode ser reconfigurado.
 
Serviços de Storm num cluster de Olá são quórum de ZooKeeper tooautomatically configurada utilize Olá.
 
### <a name="worker-nodes"></a>Nós de trabalho
Nós de trabalho do Storm executam Olá os seguintes serviços:
* Supervisor
* Trabalho Java as máquinas virtuais (JVMs), para a execução de topologias
* Agente do Ambari
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Como localizar o Storm event hub spout os binários para o desenvolvimento
 
Para obter mais informações sobre como utilizar os ficheiros do Storm event hub spout. JAR com a topologia, consulte Olá os seguintes recursos.
 
### <a name="java-based-topology"></a>Topologia baseada em Java
[Processar eventos provenientes dos Hubs de eventos do Azure com o Storm no HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>C#-com base topologia (Mono nos clusters do HDInsight 3.4 + Linux Storm)
[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology) (Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight [C#])
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Hub de eventos mais recente do Storm spout binários para clusters do HDInsight 3.5 + Linux Storm
toolearn como toouse Olá mais recente Storm event hub spout que funciona com o HDInsight 3.5 + clusters do Linux Storm, consulte Olá mvn-repo [ficheiro Leia-me](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Exemplos de código de origem
Consulte [exemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) como tooread e escrita do Hub de eventos do Azure com uma topologia de Apache Storm (escrita em Java) num cluster do Azure HDInsight.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Como localizar o ficheiros de configuração de Storm Log4J em clusters
 
ficheiros de configuração de tooidentify Apache Log4J para serviços do Storm.
 
### <a name="on-head-nodes"></a>Em nós principais
configuração de Olá Nimbus Log4J é lida /usr/hdp/\<versão HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Em nós de trabalho
configuração de supervisor Log4J Olá é lida /usr/hdp/\<versão HDP\>/storm/log4j2/cluster.xml.
 
ficheiro de configuração de trabalho Log4J Olá é lida /usr/hdp/\<versão HDP\>/storm/log4j2/worker.xml.
 
Exemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

