---
title: aaaProcess eventos provenientes dos Hubs de eventos com o Storm no HDInsight com o Java | Microsoft Docs
description: Saiba como tooprocess dados de Event Hubs com uma topologia do Storm de Java criados com o Maven.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Processar eventos provenientes dos Hubs de eventos do Azure com o Storm no HDInsight (Java)

Saiba como toouse os Hubs de eventos do Azure com o Storm no HDInsight. Este exemplo utiliza dados de tooread e de escrita de componentes baseada em Java em Event Hubs do Azure.

Os Hubs de eventos do Azure permite-lhe tooprocess quantidades enormes de dados a partir de Web sites, aplicações e dispositivos. Olá spout de Hub de eventos torna mais fácil toouse Apache Storm no HDInsight tooanalyze estes dados em tempo real. Também pode escrever dados tooEvent Hubs a partir de Storm através da utilização de Olá bolt Event Hubs.

## <a name="prerequisites"></a>Pré-requisitos

* Um Apache Storm no clusters do HDInsight versão 3.6. Para obter mais informações, consulte [introdução ao Storm num cluster do HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

* Um [Hub de eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Oracle Java Developer Kit (JDK) versão 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, tal como [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): Maven é um sistema de compilação do projeto para projetos de Java.

* Num editor de texto ou o ambiente de desenvolvimento integrado (IDE).

    > [!NOTE]
    > O editor ou IDE pode ter funcionalidades específicas para trabalhar com o Maven, que não esteja endereçada neste documento. Para obter informações sobre as capacidades de Olá do ambiente de edição, consulte a documentação Olá produto Olá que estiver a utilizar.

    * Um cliente SSH. Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Olá `ssh` e `scp` comandos. Estes são o cluster do HDInsight utilizados toocopy ficheiros toohello. No Windows, pode obter estas através de Bash no Windows 10.

## <a name="understanding-hello-example"></a>Exemplo de Olá compreender

Olá [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) exemplo contém duas topologias:

Olá `resources/writer.yaml` topologia escreve dados aleatórios tooan Hub de eventos do Azure. dados de Olá são gerados pelo Olá `DeviceSpout` componente, e é um ID de dispositivo aleatórias e o valor de dispositivo. Por isso, é simulando algum hardware que emite um ID de cadeia e um valor numérico.

Thee `resources/reader.yaml` topologia lê dados a partir do Hub de eventos (escritos pelo EventHubWriter, dados de Olá) analisa os dados JSON Olá e, em seguida, regista Olá `deviceId` e `deviceValue` dados.

dados de Olá estão formatados como um documento JSON antes de que é escrito tooEvent Hub e, quando lidos pelo leitor Olá é analisado fora JSON e para cadeias de identificação. formato JSON Olá é o seguinte:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Configuração do projeto

Olá `POM.xml` ficheiro contém informações de configuração para este projeto Maven. peças interessantes Olá são:

#### <a name="event-hub-components"></a>Componentes de Hub de eventos

componente de Olá que lê e escreve os Hubs de eventos de tooAzure está localizado na Olá [HDInsight repositório](https://github.com/hdinsight/mvn-rep). Olá seguintes secções Olá `POM.xml` carga Olá componentes de ficheiros deste repositório

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Olá EventHubs Storm Spout dependência

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Este xml define uma dependência para o pacote eventhubs de Olá, que contém um spout para ler a partir do Event Hubs e um bolt para escrever tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Este xml configura Olá projeto toogenerate o resultado para Java 8, que é utilizada pelo HDInsight 3.5 ou superior.

#### <a name="hello-maven-shade-plugin"></a>Olá maven-shade-Plug-in

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

Este xml configura a saída do Olá solução toopackage Olá para um jar uber. jar Olá contém o código de projeto Olá e dependências necessárias. Também é utilizado para:

* Mudar o nome dos ficheiros de licença para dependências Olá.
* Exclua/assinaturas de segurança.
* Certifique-se de que múltiplas implementações de Olá mesmo interface são intercaladas numa entrada.

Estas definições de configuração evitar erros durante a execução.

#### <a name="topology-definitions"></a>Definições de topologia

Este exemplo utiliza Olá [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework. Esta estrutura utiliza topologias de Olá YAML toodefine. das principais vantagens Olá é que não rígido codificação topologia Olá no código de Java. Uma vez que a definição de Olá YAML, pode alterá-la antes de submeter a topologia de Olá, sem ter toorecompile tudo.

__Writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__Reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Conte topologia Olá Hub de eventos

No momento de execução Olá `dev.properties` ficheiro é utilizado toopass Olá Hub de eventos configuração toohello topologia. Olá exemplo seguinte é Olá predefinido conteúdo de Olá ficheiro:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Configurar variáveis de ambiente

Olá seguintes variáveis de ambiente podem ser definidas quando instalar o Java e Olá JDK na sua estação de trabalho de desenvolvimento. No entanto, deve verificar que existe e que contêm valores corretos a Olá para o seu sistema.

* **JAVA_HOME** -devem apontar diretório toohello onde o ambiente de tempo de execução Java de Olá (JRE) está instalado. Por exemplo, uma distribuição Unix ou Linux, deve ter um valor semelhante demasiado`/usr/lib/jvm/java-7-oracle`. No Windows, este seria tem um valor semelhante demasiado`c:\Program Files (x86)\Java\jre1.7`
* **CAMINHO** -deve conter Olá seguintes caminhos:

  * **JAVA_HOME** (ou um caminho equivalente Olá)
  * **JAVA_HOME\bin** (ou um caminho equivalente Olá)
  * diretório de olá onde está instalado o Maven

## <a name="configure-event-hub"></a>Configurar o Hub de eventos

Os Event Hubs é a origem de dados de Olá para este exemplo. Utilize os seguintes passos toocreate um Hub de eventos de Olá.

1. De Olá [Portal clássico do Azure](https://manage.windowsazure.com), selecione **novo** > **Service Bus** > **Hub de eventos**  >  **Criação personalizada**.

2. No Olá **adicionar um novo Hub de eventos** ecrã, introduza um **nome do Hub de eventos**. Selecione Olá **região** toocreate Olá hub e, em seguida, crie um espaço de nomes ou selecione um existente. Por fim, clique em Olá **seta** toocontinue.

    ![Assistente página 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Selecione Olá mesmo **localização** como Storm no latência de tooreduce de servidor do HDInsight e os custos.

3. No Olá **configurar Hub de eventos** ecrã, introduza Olá **contagem de partição** e **mensagem retenção** valores. Neste exemplo, utilize e uma retenção de mensagem de 1 de uma contagem de partição de 10. Tenha em atenção contagem da partição Olá porque precisa de mais tarde este valor.

    ![Assistente página 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Depois de hub de eventos de Olá tiver sido criada, selecione Olá espaço de nomes, selecione **Event Hubs**e, em seguida, selecione o hub de eventos de Olá que criou anteriormente.
5. Selecione **configurar**, em seguida, crie duas novas políticas de acesso utilizando Olá seguintes informações:

    <table>
    <tr><th>Nome</th><th>Permissões</th></tr>
    <tr><td>Escritor</td><td>Enviar</td></tr>
    <tr><td>Leitor</td><td>Escutar</td></tr>
    </table>

    Depois de criar permissões Olá, selecione Olá **guardar** ícone em Olá parte inferior da página Olá. Estas políticas de acesso partilhado são utilizado tooread e escrever tooEvent Hub.

    ![políticas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Depois de guardar as políticas de Olá, utilizar Olá **gerador de chaves de acesso partilhado** na parte inferior de Olá de Olá página tooretrieve Olá chave Olá **escritor** e **leitor** políticas. Guarde estas chaves.

## <a name="download-and-build-hello-project"></a>Transferir e criar o projeto de Olá

1. Transferir o projeto de Olá a partir do GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Pode transferir o pacote de Olá como um arquivo zip, ou utilizar [git](https://git-scm.com/) localmente o projeto de Olá tooclone.

2. Modificar Olá `dev.properties` ficheiro com a configuração de Olá para o seu Hub de eventos.

3. Utilize Olá toobuild e pacote projeto Olá os seguintes:

        mvn package

    Este comando descarrega dependências necessárias, compilações, e, em seguida, pacotes hello projeto. saída de Olá é armazenada no Olá **/de destino** diretório como **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Testar localmente

Uma vez que estes topologias apenas de leitura e escrita tooEvent Hubs, pode testá-los localmente, se tiver um [ambiente de desenvolvimento do Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Utilize Olá passos toorun localmente num ambiente de desenvolvimento de Olá os seguintes:

1. Execute o escritor de Olá:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Execute o leitor de Olá:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Topologia de Olá executar no modo local (não distribuído).
> * `-R /writer.yaml`: Carregar a definição da topologia Olá de Olá `resources` empacotada num jar Olá. Se a topologia de Olá é um ficheiro no sistema de ficheiros local Olá, especifique Olá caminho tooit como o parâmetro último Olá.
> * `--filter dev.properties`: Utilize conteúdo Olá `dev.properties` toofill valores Olá nas definições da topologia Olá. Por exemplo, `${eventhub.read.policy.name}`.

O resultado é consola toohello com sessão iniciada ao executar localmente. Utilize __Ctrl + C__ topologia de Olá toostop.

## <a name="deploy-hello-topologies"></a>Implementar topologias Olá

1. Utilize o SCP toocopy Olá jar pacote tooyour cluster do HDInsight. Substitua o nome de utilizador com o utilizador do SSH Olá para o cluster. Substitua CLUSTERNAME pelo nome de Olá do cluster do HDInsight:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Se utilizou uma palavra-passe para a sua conta do SSH, são palavra-passe do pedido tooenter Olá. Se tiver utilizado uma chave SSH com a conta de Olá, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello ficheiro de chave. Por exemplo, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Este comando cópias Olá ficheiro toohello diretório raiz do seu utilizador SSH no cluster de Olá.

2. Assim que o ficheiro Olá concluiu o carregamento, utilize o SSH tooconnect toohello HDInsight cluster. Substitua **USERNAME** nome Olá de início de sessão SSH. Substitua **CLUSTERNAME** com o nome de cluster do HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Se utilizou uma palavra-passe para a sua conta do SSH, são palavra-passe do pedido tooenter Olá. Se tiver utilizado uma chave SSH com a conta de Olá, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello ficheiro de chave. Olá exemplo seguinte carrega chave privada do Olá de `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Utilize Olá seguintes topologias de Olá toostart de comando:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Submete Olá topologia toohello serviço de Nimbus, que é iniciada, em nós de trabalho de Olá num cluster de Olá.

4. dados de Olá registado tooview, aceda toohttps://CLUSTERNAME.azurehdinsight.net/stormui, onde __CLUSTERNAME__ é Olá nome do cluster do HDInsight. Selecione as topologias de Olá e desagregar toohello componentes. Selecione Olá __porta__ entrada para uma instância de um componente tooview registou informações.

5. Utilize Olá seguintes topologias de Olá toostop de comandos:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Elimina o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passos seguintes

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)
