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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="7f955-103">Processar eventos provenientes dos Hubs de eventos do Azure com o Storm no HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="7f955-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="7f955-104">Saiba como toouse os Hubs de eventos do Azure com o Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f955-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="7f955-105">Este exemplo utiliza dados de tooread e de escrita de componentes baseada em Java em Event Hubs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f955-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="7f955-106">Os Hubs de eventos do Azure permite-lhe tooprocess quantidades enormes de dados a partir de Web sites, aplicações e dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7f955-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="7f955-107">Olá spout de Hub de eventos torna mais fácil toouse Apache Storm no HDInsight tooanalyze estes dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="7f955-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="7f955-108">Também pode escrever dados tooEvent Hubs a partir de Storm através da utilização de Olá bolt Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7f955-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f955-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f955-109">Prerequisites</span></span>

* <span data-ttu-id="7f955-110">Um Apache Storm no clusters do HDInsight versão 3.6.</span><span class="sxs-lookup"><span data-stu-id="7f955-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="7f955-111">Para obter mais informações, consulte [introdução ao Storm num cluster do HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7f955-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7f955-112">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="7f955-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7f955-113">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="7f955-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7f955-114">Um [Hub de eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="7f955-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="7f955-115">[Oracle Java Developer Kit (JDK) versão 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, tal como [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="7f955-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="7f955-116">[Maven](https://maven.apache.org/download.cgi): Maven é um sistema de compilação do projeto para projetos de Java.</span><span class="sxs-lookup"><span data-stu-id="7f955-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="7f955-117">Num editor de texto ou o ambiente de desenvolvimento integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="7f955-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f955-118">O editor ou IDE pode ter funcionalidades específicas para trabalhar com o Maven, que não esteja endereçada neste documento.</span><span class="sxs-lookup"><span data-stu-id="7f955-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="7f955-119">Para obter informações sobre as capacidades de Olá do ambiente de edição, consulte a documentação Olá produto Olá que estiver a utilizar.</span><span class="sxs-lookup"><span data-stu-id="7f955-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="7f955-120">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="7f955-120">An SSH client.</span></span> <span data-ttu-id="7f955-121">Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7f955-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="7f955-122">Olá `ssh` e `scp` comandos.</span><span class="sxs-lookup"><span data-stu-id="7f955-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="7f955-123">Estes são o cluster do HDInsight utilizados toocopy ficheiros toohello.</span><span class="sxs-lookup"><span data-stu-id="7f955-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="7f955-124">No Windows, pode obter estas através de Bash no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7f955-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="7f955-125">Exemplo de Olá compreender</span><span class="sxs-lookup"><span data-stu-id="7f955-125">Understanding hello example</span></span>

<span data-ttu-id="7f955-126">Olá [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) exemplo contém duas topologias:</span><span class="sxs-lookup"><span data-stu-id="7f955-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="7f955-127">Olá `resources/writer.yaml` topologia escreve dados aleatórios tooan Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f955-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="7f955-128">dados de Olá são gerados pelo Olá `DeviceSpout` componente, e é um ID de dispositivo aleatórias e o valor de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7f955-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="7f955-129">Por isso, é simulando algum hardware que emite um ID de cadeia e um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="7f955-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="7f955-130">Thee `resources/reader.yaml` topologia lê dados a partir do Hub de eventos (escritos pelo EventHubWriter, dados de Olá) analisa os dados JSON Olá e, em seguida, regista Olá `deviceId` e `deviceValue` dados.</span><span class="sxs-lookup"><span data-stu-id="7f955-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="7f955-131">dados de Olá estão formatados como um documento JSON antes de que é escrito tooEvent Hub e, quando lidos pelo leitor Olá é analisado fora JSON e para cadeias de identificação.</span><span class="sxs-lookup"><span data-stu-id="7f955-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="7f955-132">formato JSON Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7f955-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="7f955-133">Configuração do projeto</span><span class="sxs-lookup"><span data-stu-id="7f955-133">Project configuration</span></span>

<span data-ttu-id="7f955-134">Olá `POM.xml` ficheiro contém informações de configuração para este projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="7f955-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="7f955-135">peças interessantes Olá são:</span><span class="sxs-lookup"><span data-stu-id="7f955-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="7f955-136">Componentes de Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="7f955-136">Event Hub components</span></span>

<span data-ttu-id="7f955-137">componente de Olá que lê e escreve os Hubs de eventos de tooAzure está localizado na Olá [HDInsight repositório](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="7f955-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="7f955-138">Olá seguintes secções Olá `POM.xml` carga Olá componentes de ficheiros deste repositório</span><span class="sxs-lookup"><span data-stu-id="7f955-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="7f955-139">Olá EventHubs Storm Spout dependência</span><span class="sxs-lookup"><span data-stu-id="7f955-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="7f955-140">Este xml define uma dependência para o pacote eventhubs de Olá, que contém um spout para ler a partir do Event Hubs e um bolt para escrever tooit.</span><span class="sxs-lookup"><span data-stu-id="7f955-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="7f955-141">Este xml configura Olá projeto toogenerate o resultado para Java 8, que é utilizada pelo HDInsight 3.5 ou superior.</span><span class="sxs-lookup"><span data-stu-id="7f955-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="7f955-142">Olá maven-shade-Plug-in</span><span class="sxs-lookup"><span data-stu-id="7f955-142">hello maven-shade-plugin</span></span>

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

<span data-ttu-id="7f955-143">Este xml configura a saída do Olá solução toopackage Olá para um jar uber.</span><span class="sxs-lookup"><span data-stu-id="7f955-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="7f955-144">jar Olá contém o código de projeto Olá e dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="7f955-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="7f955-145">Também é utilizado para:</span><span class="sxs-lookup"><span data-stu-id="7f955-145">It is also used to:</span></span>

* <span data-ttu-id="7f955-146">Mudar o nome dos ficheiros de licença para dependências Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="7f955-147">Exclua/assinaturas de segurança.</span><span class="sxs-lookup"><span data-stu-id="7f955-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="7f955-148">Certifique-se de que múltiplas implementações de Olá mesmo interface são intercaladas numa entrada.</span><span class="sxs-lookup"><span data-stu-id="7f955-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="7f955-149">Estas definições de configuração evitar erros durante a execução.</span><span class="sxs-lookup"><span data-stu-id="7f955-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="7f955-150">Definições de topologia</span><span class="sxs-lookup"><span data-stu-id="7f955-150">Topology definitions</span></span>

<span data-ttu-id="7f955-151">Este exemplo utiliza Olá [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="7f955-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="7f955-152">Esta estrutura utiliza topologias de Olá YAML toodefine.</span><span class="sxs-lookup"><span data-stu-id="7f955-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="7f955-153">das principais vantagens Olá é que não rígido codificação topologia Olá no código de Java.</span><span class="sxs-lookup"><span data-stu-id="7f955-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="7f955-154">Uma vez que a definição de Olá YAML, pode alterá-la antes de submeter a topologia de Olá, sem ter toorecompile tudo.</span><span class="sxs-lookup"><span data-stu-id="7f955-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="7f955-155">__Writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="7f955-155">__writer.yaml__:</span></span>

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

<span data-ttu-id="7f955-156">__Reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="7f955-156">__reader.yaml__:</span></span>

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

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="7f955-157">Conte topologia Olá Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="7f955-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="7f955-158">No momento de execução Olá `dev.properties` ficheiro é utilizado toopass Olá Hub de eventos configuração toohello topologia.</span><span class="sxs-lookup"><span data-stu-id="7f955-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="7f955-159">Olá exemplo seguinte é Olá predefinido conteúdo de Olá ficheiro:</span><span class="sxs-lookup"><span data-stu-id="7f955-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="7f955-160">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="7f955-160">Configure environment variables</span></span>

<span data-ttu-id="7f955-161">Olá seguintes variáveis de ambiente podem ser definidas quando instalar o Java e Olá JDK na sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7f955-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="7f955-162">No entanto, deve verificar que existe e que contêm valores corretos a Olá para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="7f955-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="7f955-163">**JAVA_HOME** -devem apontar diretório toohello onde o ambiente de tempo de execução Java de Olá (JRE) está instalado.</span><span class="sxs-lookup"><span data-stu-id="7f955-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="7f955-164">Por exemplo, uma distribuição Unix ou Linux, deve ter um valor semelhante demasiado`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="7f955-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="7f955-165">No Windows, este seria tem um valor semelhante demasiado`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="7f955-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="7f955-166">**CAMINHO** -deve conter Olá seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="7f955-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="7f955-167">**JAVA_HOME** (ou um caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="7f955-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="7f955-168">**JAVA_HOME\bin** (ou um caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="7f955-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="7f955-169">diretório de olá onde está instalado o Maven</span><span class="sxs-lookup"><span data-stu-id="7f955-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="7f955-170">Configurar o Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="7f955-170">Configure Event Hub</span></span>

<span data-ttu-id="7f955-171">Os Event Hubs é a origem de dados de Olá para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="7f955-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="7f955-172">Utilize os seguintes passos toocreate um Hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="7f955-173">De Olá [Portal clássico do Azure](https://manage.windowsazure.com), selecione **novo** > **Service Bus** > **Hub de eventos**  >  **Criação personalizada**.</span><span class="sxs-lookup"><span data-stu-id="7f955-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="7f955-174">No Olá **adicionar um novo Hub de eventos** ecrã, introduza um **nome do Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="7f955-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="7f955-175">Selecione Olá **região** toocreate Olá hub e, em seguida, crie um espaço de nomes ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="7f955-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="7f955-176">Por fim, clique em Olá **seta** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7f955-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![Assistente página 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="7f955-178">Selecione Olá mesmo **localização** como Storm no latência de tooreduce de servidor do HDInsight e os custos.</span><span class="sxs-lookup"><span data-stu-id="7f955-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="7f955-179">No Olá **configurar Hub de eventos** ecrã, introduza Olá **contagem de partição** e **mensagem retenção** valores.</span><span class="sxs-lookup"><span data-stu-id="7f955-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="7f955-180">Neste exemplo, utilize e uma retenção de mensagem de 1 de uma contagem de partição de 10.</span><span class="sxs-lookup"><span data-stu-id="7f955-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="7f955-181">Tenha em atenção contagem da partição Olá porque precisa de mais tarde este valor.</span><span class="sxs-lookup"><span data-stu-id="7f955-181">Note hello partition count because you need this value later.</span></span>

    ![Assistente página 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="7f955-183">Depois de hub de eventos de Olá tiver sido criada, selecione Olá espaço de nomes, selecione **Event Hubs**e, em seguida, selecione o hub de eventos de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7f955-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="7f955-184">Selecione **configurar**, em seguida, crie duas novas políticas de acesso utilizando Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="7f955-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="7f955-185">Nome</span><span class="sxs-lookup"><span data-stu-id="7f955-185">Name</span></span></th><th><span data-ttu-id="7f955-186">Permissões</span><span class="sxs-lookup"><span data-stu-id="7f955-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="7f955-187">Escritor</span><span class="sxs-lookup"><span data-stu-id="7f955-187">Writer</span></span></td><td><span data-ttu-id="7f955-188">Enviar</span><span class="sxs-lookup"><span data-stu-id="7f955-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="7f955-189">Leitor</span><span class="sxs-lookup"><span data-stu-id="7f955-189">Reader</span></span></td><td><span data-ttu-id="7f955-190">Escutar</span><span class="sxs-lookup"><span data-stu-id="7f955-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="7f955-191">Depois de criar permissões Olá, selecione Olá **guardar** ícone em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="7f955-192">Estas políticas de acesso partilhado são utilizado tooread e escrever tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="7f955-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![políticas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="7f955-194">Depois de guardar as políticas de Olá, utilizar Olá **gerador de chaves de acesso partilhado** na parte inferior de Olá de Olá página tooretrieve Olá chave Olá **escritor** e **leitor** políticas.</span><span class="sxs-lookup"><span data-stu-id="7f955-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="7f955-195">Guarde estas chaves.</span><span class="sxs-lookup"><span data-stu-id="7f955-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="7f955-196">Transferir e criar o projeto de Olá</span><span class="sxs-lookup"><span data-stu-id="7f955-196">Download and build hello project</span></span>

1. <span data-ttu-id="7f955-197">Transferir o projeto de Olá a partir do GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="7f955-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="7f955-198">Pode transferir o pacote de Olá como um arquivo zip, ou utilizar [git](https://git-scm.com/) localmente o projeto de Olá tooclone.</span><span class="sxs-lookup"><span data-stu-id="7f955-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="7f955-199">Modificar Olá `dev.properties` ficheiro com a configuração de Olá para o seu Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="7f955-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="7f955-200">Utilize Olá toobuild e pacote projeto Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7f955-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="7f955-201">Este comando descarrega dependências necessárias, compilações, e, em seguida, pacotes hello projeto.</span><span class="sxs-lookup"><span data-stu-id="7f955-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="7f955-202">saída de Olá é armazenada no Olá **/de destino** diretório como **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="7f955-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="7f955-203">Testar localmente</span><span class="sxs-lookup"><span data-stu-id="7f955-203">Test locally</span></span>

<span data-ttu-id="7f955-204">Uma vez que estes topologias apenas de leitura e escrita tooEvent Hubs, pode testá-los localmente, se tiver um [ambiente de desenvolvimento do Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="7f955-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="7f955-205">Utilize Olá passos toorun localmente num ambiente de desenvolvimento de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7f955-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="7f955-206">Execute o escritor de Olá:</span><span class="sxs-lookup"><span data-stu-id="7f955-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="7f955-207">Execute o leitor de Olá:</span><span class="sxs-lookup"><span data-stu-id="7f955-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="7f955-208">`--local`: Topologia de Olá executar no modo local (não distribuído).</span><span class="sxs-lookup"><span data-stu-id="7f955-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="7f955-209">`-R /writer.yaml`: Carregar a definição da topologia Olá de Olá `resources` empacotada num jar Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="7f955-210">Se a topologia de Olá é um ficheiro no sistema de ficheiros local Olá, especifique Olá caminho tooit como o parâmetro último Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="7f955-211">`--filter dev.properties`: Utilize conteúdo Olá `dev.properties` toofill valores Olá nas definições da topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="7f955-212">Por exemplo, `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="7f955-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="7f955-213">O resultado é consola toohello com sessão iniciada ao executar localmente.</span><span class="sxs-lookup"><span data-stu-id="7f955-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="7f955-214">Utilize __Ctrl + C__ topologia de Olá toostop.</span><span class="sxs-lookup"><span data-stu-id="7f955-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="7f955-215">Implementar topologias Olá</span><span class="sxs-lookup"><span data-stu-id="7f955-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="7f955-216">Utilize o SCP toocopy Olá jar pacote tooyour cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f955-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="7f955-217">Substitua o nome de utilizador com o utilizador do SSH Olá para o cluster.</span><span class="sxs-lookup"><span data-stu-id="7f955-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="7f955-218">Substitua CLUSTERNAME pelo nome de Olá do cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7f955-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="7f955-219">Se utilizou uma palavra-passe para a sua conta do SSH, são palavra-passe do pedido tooenter Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="7f955-220">Se tiver utilizado uma chave SSH com a conta de Olá, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello ficheiro de chave.</span><span class="sxs-lookup"><span data-stu-id="7f955-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="7f955-221">Por exemplo, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="7f955-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="7f955-222">Este comando cópias Olá ficheiro toohello diretório raiz do seu utilizador SSH no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="7f955-223">Assim que o ficheiro Olá concluiu o carregamento, utilize o SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7f955-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="7f955-224">Substitua **USERNAME** nome Olá de início de sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="7f955-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="7f955-225">Substitua **CLUSTERNAME** com o nome de cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7f955-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="7f955-226">Se utilizou uma palavra-passe para a sua conta do SSH, são palavra-passe do pedido tooenter Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="7f955-227">Se tiver utilizado uma chave SSH com a conta de Olá, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello ficheiro de chave.</span><span class="sxs-lookup"><span data-stu-id="7f955-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="7f955-228">Olá exemplo seguinte carrega chave privada do Olá de `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="7f955-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="7f955-229">Utilize Olá seguintes topologias de Olá toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="7f955-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="7f955-230">`--remote`: Submete Olá topologia toohello serviço de Nimbus, que é iniciada, em nós de trabalho de Olá num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7f955-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="7f955-231">dados de Olá registado tooview, aceda toohttps://CLUSTERNAME.azurehdinsight.net/stormui, onde __CLUSTERNAME__ é Olá nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f955-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="7f955-232">Selecione as topologias de Olá e desagregar toohello componentes.</span><span class="sxs-lookup"><span data-stu-id="7f955-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="7f955-233">Selecione Olá __porta__ entrada para uma instância de um componente tooview registou informações.</span><span class="sxs-lookup"><span data-stu-id="7f955-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="7f955-234">Utilize Olá seguintes topologias de Olá toostop de comandos:</span><span class="sxs-lookup"><span data-stu-id="7f955-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="7f955-235">Elimina o cluster</span><span class="sxs-lookup"><span data-stu-id="7f955-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="7f955-236">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7f955-236">Next steps</span></span>

* [<span data-ttu-id="7f955-237">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f955-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
