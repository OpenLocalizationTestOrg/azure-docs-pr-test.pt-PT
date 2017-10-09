---
title: "aaaPorts utilizada pelos serviços do Hadoop no HDInsight - Azure | Microsoft Docs"
description: "Uma lista de portas utilizadas pelos serviços de Hadoop em execução no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Portas utilizadas pelos serviços do Hadoop no HDInsight

Este documento fornece uma lista de portas de Olá utilizada pelos serviços do Hadoop em execução em clusters do HDInsight baseado em Linux. Também fornece informações sobre as portas utilizadas tooconnect toohello cluster através de SSH.

## <a name="public-ports-vs-non-public-ports"></a>Portas públicas vs portas não público

HDInsight baseado em Linux clusters apenas expõem três portas publicamente no Olá internet; 22, 23 e 443. Estas portas são cluster de Olá toosecurely utilizados acesso através de SSH e expostos através do protocolo HTTPS seguro Olá de serviços.

Internamente, o HDInsight é implementado por várias máquinas virtuais do Azure (nós Olá num cluster de Olá) em execução numa rede Virtual do Azure. De dentro da rede virtual Olá, pode aceder às portas não expostas através de Olá internet. Por exemplo, se ligar tooone de nós principais Olá através do SSH, a partir do nó principal Olá pode, em seguida, diretamente aceder a serviços em execução em nós de cluster Olá.

> [!IMPORTANT]
> Se não especificar uma rede Virtual do Azure como uma opção de configuração para o HDInsight, é criada uma automaticamente. No entanto, não é possível associar outra rede virtual de toothis máquinas (como outras máquinas virtuais do Azure ou no seu computador de desenvolvimento do cliente).


toojoin máquinas adicionais toohello rede virtual, tem de criar rede virtual Olá pela primeira vez e, em seguida, especifique-o ao criar o cluster do HDInsight. Para obter mais informações, consulte [capacidades de expandir HDInsight utilizando uma rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Portas públicas

Olá, Olá todos os nós no cluster do HDInsight estão localizados numa rede Virtual do Azure e não podem ser acedidos diretamente da internet. Um gateway público fornece toohello de acesso à internet seguintes portas, que são comuns a todos os tipos de cluster do HDInsight.

| Serviço | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Liga-se os clientes toosshd no headnode primário Olá. Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Estabelece ligação toosshd de clientes no nó de extremidade Olá. Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Liga-se os clientes toosshd no headnode secundário Olá. Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |IU da web Ambari. Consulte [gerir HDInsight com Olá IU da Web do Ambari](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |API de REST do Ambari. Consulte [gerir HDInsight com Olá API de REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |API de REST do HCatalog. Consulte [utilizar o Hive com o Curl](hdinsight-hadoop-use-pig-curl.md), [utilizar o Pig com o Curl](hdinsight-hadoop-use-pig-curl.md), [utilizar o MapReduce com Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |Estabelece ligação tooHive através de ODBC. Consulte [tooHDInsight de ligar o Excel com o controlador Microsoft ODBC de Olá](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Estabelece ligação tooHive através de JDBC. Consulte [ligar tooHive no HDInsight com o controlador de ramo de registo JDBC Olá](hdinsight-connect-hive-jdbc-driver.md) |

Olá seguem-se disponível para tipos de cluster específicos:

| Serviço | Porta | Protocolo | Tipo de cluster | Descrição |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |API de REST de HBase. Consulte [introdução ao hbase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |API de REST do Spark. Consulte [tarefas submeter Spark remotamente com o Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |IU da web Storm. Consulte [implementar e gerir topologias Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Autenticação

Todos os serviços publicamente expostos no Olá que Internet têm de ser autenticados:

| Porta | Credenciais |
| --- | --- |
| 22 ou 23 |Olá SSH as credenciais de utilizador especificadas durante a criação do cluster |
| 443 |nome de início de sessão de Olá (predefinição: admin) e palavra-passe que foram definidas durante a criação do cluster |

## <a name="non-public-ports"></a>Portas não público

> [!NOTE]
> Alguns serviços só estão disponíveis em tipos de cluster específicos. Por exemplo, o HBase só está disponível em tipos de cluster de HBase.

> [!IMPORTANT]
> Alguns serviços executam apenas no um headnode de cada vez. Se tentar tooconnect toohello serviço headnode primário Olá e receber um erro 404, tente novamente utilizando headnode secundário Olá.

### <a name="ambari"></a>Ambari

| Serviço | Nós | Porta | Caminho de URL | Protocolo | 
| --- | --- | --- | --- | --- |
| IU da web do Ambari | Nós de cabeçalho | 8080 | / | HTTP |
| API de REST do Ambari | Nós de cabeçalho | 8080 | / api/v1 | HTTP |

Exemplos:

* API de REST do Ambari:`curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>Portas do HDFS

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| IU da web do NameNode |Nós de cabeçalho |30070 |HTTPS |Estado de tooview Web da IU |
| Serviço de metadados NameNode |Nós de cabeçalho |8020 |IPC |Metadados do sistema de ficheiros |
| DataNode |Todos os nós de trabalho |30075 |HTTPS |Estado de tooview de IU Web, os registos, etc. |
| DataNode |Todos os nós de trabalho |30010 |&nbsp; |Transferência de dados |
| DataNode |Todos os nós de trabalho |30020 |IPC |Operações de metadados |
| NameNode secundário |Nós de cabeçalho |50090 |HTTP |Ponto de verificação para metadados NameNode |

### <a name="yarn-ports"></a>Portas YARN

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| IU da web do Gestor de recursos |Nós de cabeçalho |8088 |HTTP |Web da IU para o Resource Manager |
| IU da web do Gestor de recursos |Nós de cabeçalho |8090 |HTTPS |Web da IU para o Resource Manager |
| Interface de administração do Gestor de recursos |Nós de cabeçalho |8141 |IPC |Para as submissões de aplicação (Hive, o servidor do Hive, Pig, etc.) |
| Gestor de recursos de programador |Nós de cabeçalho |8030 |HTTP |Interface administrativa |
| Interface de aplicação do Gestor de recursos |Nós de cabeçalho |8050 |HTTP |Endereço da interface do Gestor de aplicações de Olá |
| NodeManager |Todos os nós de trabalho |30050 |&nbsp; |endereço de Olá do Gestor de contentor Olá |
| IU da web do NodeManager |Todos os nós de trabalho |30060 |HTTP |Interface do Gestor de recursos |
| Linha cronológica endereço |Nós de cabeçalho |10200 |RPC |Olá linha cronológica serviço de RPC de serviço. |
| Linha cronológica IU da web do |Nós de cabeçalho |8181 |HTTP |IU da web de serviço de linha cronológica Olá |

### <a name="hive-ports"></a>Portas de ramo de registo

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| HiveServer2 |Nós de cabeçalho |10001 |Thrift |Serviço para estabelecer a ligação tooHive (Thrift/JDBC) |
| Metastore do Hive |Nós de cabeçalho |9083 |Thrift |Serviço para ligação tooHive metadados (Thrift/JDBC) |

### <a name="webhcat-ports"></a>Portas de WebHCat

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Servidor de WebHCat |Nós de cabeçalho |30111 |HTTP |API Web em cima HCatalog e outros serviços do Hadoop |

### <a name="mapreduce-ports"></a>Portas de MapReduce

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| JobHistory |Nós de cabeçalho |19888 |HTTP |IU da web do MapReduce JobHistory |
| JobHistory |Nós de cabeçalho |10020 |&nbsp; |Servidor de MapReduce JobHistory |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Mapeamento intermédio transferências produz toorequesting Reducers |

### <a name="oozie"></a>Oozie

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Servidor do Oozie |Nós de cabeçalho |11000 |HTTP |URL para o serviço de Oozie |
| Servidor do Oozie |Nós de cabeçalho |11001 |HTTP |Porta para Oozie admin |

### <a name="ambari-metrics"></a>Métricas de Ambari

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Linha cronológica (histórico de aplicação) |Nós de cabeçalho |6188 |HTTP |IU da web de serviço de linha cronológica Olá |
| Linha cronológica (histórico de aplicação) |Nós de cabeçalho |30200 |RPC |IU da web de serviço de linha cronológica Olá |

### <a name="hbase-ports"></a>Portas de HBase

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| HMaster |Nós de cabeçalho |16000 |&nbsp; |&nbsp; |
| Informações de HMaster IU da Web |Nós de cabeçalho |16010 |HTTP |porta de Olá da IU da web do Olá mestre HBase |
| Servidor de região |Todos os nós de trabalho |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |porta Olá que os clientes utilizam tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Portas Kafka

| Serviço | Nós | Porta | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Mediador |Nós de trabalho |9092 |[Protocolo de transmissão Kafka](http://kafka.apache.org/protocol.html) |Utilizado para comunicação de cliente |
| &nbsp; |Nós de zookeeper |2181 |&nbsp; |porta Olá que os clientes utilizam tooconnect tooZookeeper |

### <a name="spark-ports"></a>Portas do Spark

| Serviço | Nós | Porta | Protocolo | Caminho de URL | Descrição |
| --- | --- | --- | --- | --- | --- |
| Servidores de Thrift de Spark |Nós de cabeçalho |10002 |Thrift | &nbsp; | Serviço para estabelecer a ligação tooSpark SQL (Thrift/JDBC) |
| Servidor Livy | Nós de cabeçalho | 8998 | HTTP | /Batches | Serviço para executar instruções, tarefas e aplicações |

Exemplos:

* O Livy: `curl "http://10.0.0.11:8998/batches"`. Neste exemplo, `10.0.0.11` é Olá o endereço IP do headnode Olá que aloja Olá serviço Livy.
