---
title: aaaApache Storm escrever tooStorage/Data Lake Store - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá armazenamento do Apache Storm toowrite toohello compatível com HDFS para o HDInsight. Armazenamento do Azure ou de Azure Data Lake Store fornecer armazenamento de Olá HDFS comptabile para o HDInsight. Este documento e o exemplo de associado Olá, demonstram como componente de HdfsBolt Olá pode ser utilizados toowrite toohello predefinido armazenamento de um cluster Storm no HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Escrever tooHDFS do Apache Storm no HDInsight

Saiba como toouse Storm toowrite dados toohello armazenamento compatível com HDFS utilizado pelo Apache Storm no HDInsight. HDInsight pode utilizar ambas Storage do Azure e do Azure Data Lake armazenam como armazenamento HDFS comptabile. Storm fornece um [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente que escreve tooHDFS de dados. Este documento fornece informações sobre como escrever tooeither tipo de armazenamento de Olá HdfsBolt. 

> [!IMPORTANT]
> exemplo de Olá topologia utilizada neste documento baseia-se nos componentes que estão incluídos com o Storm no HDInsight. Pode necessitar de modificação toowork com o Azure Data Lake Store quando utilizado com outros clusters do Apache Storm.

## <a name="get-hello-code"></a>Obter o código de Olá

projeto de Olá que contém esta topologia está disponível como uma transferência a partir do [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile este projeto, terá de seguir a configuração para o seu ambiente de desenvolvimento de Olá:

* [1.8 do Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior. HDInsight 3.5 ou superior necessário Java 8.

* [Maven 3](https://maven.apache.org/download.cgi)

Olá seguintes variáveis de ambiente podem ser definidas quando instalar o Java e Olá JDK na sua estação de trabalho de desenvolvimento. No entanto, deve verificar que existe e que contêm valores corretos a Olá para o seu sistema.

* `JAVA_HOME`-devem apontar toohello diretório onde hello JDK está instalado.
* `PATH`-deve conter Olá seguintes caminhos:
  
    * `JAVA_HOME`(ou um caminho equivalente Olá).
    * `JAVA_HOME\bin`(ou um caminho equivalente Olá).
    * diretório de olá onde Maven está instalado.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Como toouse Olá HdfsBolt com o HDInsight

> [!IMPORTANT]
> Antes de utilizar Olá HdfsBolt Storm no HDInsight, primeiro tem de utilizar uma ficheiros jar do script ação toocopy necessário para Olá `extpath` para Storm. Para obter mais informações, consulte Olá [configurar clusters de Olá](#configure) secção.

Olá HdfsBolt utiliza o esquema do ficheiro Olá que forneçam toounderstand como toowrite tooHDFS. Com o HDInsight, utilize um dos Olá esquemas os seguintes:

* `wasb://`: Utilizada com uma conta de armazenamento do Azure.
* `adl://`: Utilizada com o Azure Data Lake Store.

Olá tabela seguinte fornece exemplos de como utilizar o esquema do ficheiro de Olá para diferentes cenários:

| Esquema | Notas |
| ----- | ----- |
| `wasb:///` | conta do storage predefinida Olá é um contentor de BLOBs numa conta do Storage do Azure |
| `adl:///` | conta do storage predefinida Olá é um diretório no Azure Data Lake Store. Durante a criação do cluster, especifique o diretório de Olá no Data Lake Store é Olá raiz do HDFS do cluster Olá. Por exemplo, Olá `/clusters/myclustername/` diretório. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Uma conta do storage do Azure (adicionais) de não predefinida associada ao cluster Olá. |
| `adl://STORENAME/` | raiz de Olá da Olá utilizados pelo cluster Olá do Data Lake Store. Este esquema permite-lhe dados tooaccess localizados fora do diretório de Olá que contém o sistema de ficheiros do cluster Olá. |

Para obter mais informações, consulte Olá [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) referência em Apache.org.

### <a name="example-configuration"></a>Configuração de exemplo

Olá YAML seguinte é um excerpt de Olá `resources/writetohdfs.yaml` ficheiros incluídos no exemplo de Olá. Este ficheiro define a topologia do Storm Olá utilizando Olá [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework para o Apache Storm.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Este YAML define Olá seguintes itens:

* `syncPolicy`: Define quando os ficheiros estão synched/descarregados toohello sistema de ficheiros. Neste exemplo, todas as cadeias de identificação de 1000.
* `fileNameFormat`: Define Olá ficheiro e caminho o nome padrão toouse quando escrever ficheiros. Neste exemplo, o caminho de Olá é fornecido no tempo de execução utilizando um filtro, não sendo extensão de ficheiro Olá `.txt`.
* `recordFormat`: Define o formato interno do Olá dos ficheiros de Olá escrito. Neste exemplo, os campos são delimitados por Olá `|` caráter.
* `rotationPolicy`: Define quando toorotate ficheiros. Neste exemplo, é efetuada sem rotação.
* `hdfs-bolt`: Utiliza Olá componentes anteriores como parâmetros de configuração para Olá `HdfsBolt` classe.

Para obter mais informações sobre a estrutura do Flux de Olá, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Configurar o cluster de Olá

Por predefinição, o Storm no HDInsight não inclui os componentes de Olá que HdfsBolt utiliza toocommunicate com o Storage do Azure ou de Data Lake Store no classpath do Storm. Tooadd de ação de script de utilização Olá seguinte, estes componentes toohello `extlib` diretório para Storm no cluster:

| URI de script | Nós tooapply que | Os parâmetros | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Nenhum |

Para informações sobre como utilizar este script com o cluster, consulte Olá [HDInsight personalizar clusters com ações de script](./hdinsight-hadoop-customize-cluster-linux.md) documento.

## <a name="build-and-package-hello-topology"></a>Criar e da topologia de Olá do pacote

1. Transferir o projeto de exemplo de Olá da [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ambiente de desenvolvimento.

2. Numa linha de comandos, terminal ou sessão de shell, alteração diretórios toohello raiz da Olá transferir o projeto. toobuild e pacote Olá topologia, utilize Olá os seguintes comandos:
   
        mvn compile package
   
    Depois de concluída a compilação de Olá e empacotamento, há um novo diretório designado `target`, que contém um ficheiro denominado `StormToHdfs-1.0-SNAPSHOT.jar`. Este ficheiro contém a topologia de Olá compilada.

## <a name="deploy-and-run-hello-topology"></a>Implementar e executar a topologia de Olá

1. Utilize Olá cluster de HDInsight do comando toocopy Olá topologia toohello a seguir. Substitua **utilizador** com o nome de utilizador do SSH Olá utilizado ao criar o cluster de Olá. Substitua **CLUSTERNAME** com nome Olá cluster Olá.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Quando lhe for pedido, introduza a palavra-passe de Olá utilizada durante a criação de utilizador do SSH Olá para cluster Olá. Se tiver utilizado uma chave pública em vez de uma palavra-passe, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello correspondentes à chave privada.
   
   > [!NOTE]
   > Para obter mais informações sobre como utilizar `scp` com o HDInsight, consulte [utilizar o SSH com o HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Após a conclusão do carregamento de Olá, utilize Olá seguir tooconnect toohello cluster do HDInsight através de SSH. Substitua **utilizador** com o nome de utilizador do SSH Olá utilizado ao criar o cluster de Olá. Substitua **CLUSTERNAME** com nome Olá cluster Olá.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Quando lhe for pedido, introduza a palavra-passe de Olá utilizada durante a criação de utilizador do SSH Olá para cluster Olá. Se tiver utilizado uma chave pública em vez de uma palavra-passe, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello correspondentes à chave privada.
   
   Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Assim que estiver ligado, de seguinte de Olá utilize comandos toocreate um ficheiro denominado `dev.properties`:

        nano dev.properties

4. Olá de utilização seguintes texto como conteúdo Olá Olá `dev.properties` ficheiro:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > Este exemplo assume que o cluster utiliza uma conta de armazenamento do Azure como armazenamento de predefinido Olá. Se o cluster utiliza o Azure Data Lake Store, utilize `hdfs.url: adl:///` em vez disso.
    
    ficheiro de Olá toosave, utilize __Ctrl + X__, em seguida, __Y__e, finalmente, __Enter__. os valores de Olá neste ficheiro definidos Olá Data Lake store URL e o nome de diretório de Olá que dados são escritos para.

3. Utilize Olá topologia de Olá toostart de comando a seguir:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Este comando inicia a topologia de Olá utilizando a estrutura de Flux de Olá submetendo-nó Nimbus toohello cluster Olá. topologia de Olá é definida pela Olá `writetohdfs.yaml` ficheiros incluídos no jar Olá. Olá `dev.properties` ficheiro é transmitido como um filtro e valores de Olá contidos no ficheiro de Olá são lidas pelas topologia Olá.

## <a name="view-output-data"></a>Ver dados de saída

dados de Olá tooview, utilize Olá os seguintes comandos:

    hdfs dfs -ls /stormdata/

É apresentada uma lista dos ficheiros de Olá criada por esta topologia.

Olá lista seguinte é um exemplo de dados de Olá retuned por comandos anteriores Olá:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Parar a topologia de Olá

Topologias do Storm executam até parado ou cluster Olá é eliminado. toostop Olá topologia, utilize Olá os seguintes comandos:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Elimina o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passos seguintes

Agora que aprendeu como toouse Storm toowrite tooAzure armazenamento e o Azure Data Lake Store, detetar outros [Storm exemplos para o HDInsight](hdinsight-storm-example-topology.md).

