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
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="78a5e-105">Escrever tooHDFS do Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a5e-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="78a5e-106">Saiba como toouse Storm toowrite dados toohello armazenamento compatível com HDFS utilizado pelo Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78a5e-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="78a5e-107">HDInsight pode utilizar ambas Storage do Azure e do Azure Data Lake armazenam como armazenamento HDFS comptabile.</span><span class="sxs-lookup"><span data-stu-id="78a5e-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="78a5e-108">Storm fornece um [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente que escreve tooHDFS de dados.</span><span class="sxs-lookup"><span data-stu-id="78a5e-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="78a5e-109">Este documento fornece informações sobre como escrever tooeither tipo de armazenamento de Olá HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="78a5e-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="78a5e-110">exemplo de Olá topologia utilizada neste documento baseia-se nos componentes que estão incluídos com o Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78a5e-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="78a5e-111">Pode necessitar de modificação toowork com o Azure Data Lake Store quando utilizado com outros clusters do Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="78a5e-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="78a5e-112">Obter o código de Olá</span><span class="sxs-lookup"><span data-stu-id="78a5e-112">Get hello code</span></span>

<span data-ttu-id="78a5e-113">projeto de Olá que contém esta topologia está disponível como uma transferência a partir do [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="78a5e-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="78a5e-114">toocompile este projeto, terá de seguir a configuração para o seu ambiente de desenvolvimento de Olá:</span><span class="sxs-lookup"><span data-stu-id="78a5e-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="78a5e-115">[1.8 do Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="78a5e-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="78a5e-116">HDInsight 3.5 ou superior necessário Java 8.</span><span class="sxs-lookup"><span data-stu-id="78a5e-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="78a5e-117">Maven 3</span><span class="sxs-lookup"><span data-stu-id="78a5e-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="78a5e-118">Olá seguintes variáveis de ambiente podem ser definidas quando instalar o Java e Olá JDK na sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="78a5e-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="78a5e-119">No entanto, deve verificar que existe e que contêm valores corretos a Olá para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="78a5e-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="78a5e-120">`JAVA_HOME`-devem apontar toohello diretório onde hello JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="78a5e-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="78a5e-121">`PATH`-deve conter Olá seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="78a5e-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="78a5e-122">`JAVA_HOME`(ou um caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="78a5e-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="78a5e-123">`JAVA_HOME\bin`(ou um caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="78a5e-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="78a5e-124">diretório de olá onde Maven está instalado.</span><span class="sxs-lookup"><span data-stu-id="78a5e-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="78a5e-125">Como toouse Olá HdfsBolt com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="78a5e-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78a5e-126">Antes de utilizar Olá HdfsBolt Storm no HDInsight, primeiro tem de utilizar uma ficheiros jar do script ação toocopy necessário para Olá `extpath` para Storm.</span><span class="sxs-lookup"><span data-stu-id="78a5e-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="78a5e-127">Para obter mais informações, consulte Olá [configurar clusters de Olá](#configure) secção.</span><span class="sxs-lookup"><span data-stu-id="78a5e-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="78a5e-128">Olá HdfsBolt utiliza o esquema do ficheiro Olá que forneçam toounderstand como toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="78a5e-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="78a5e-129">Com o HDInsight, utilize um dos Olá esquemas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="78a5e-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="78a5e-130">`wasb://`: Utilizada com uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="78a5e-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="78a5e-131">`adl://`: Utilizada com o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="78a5e-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="78a5e-132">Olá tabela seguinte fornece exemplos de como utilizar o esquema do ficheiro de Olá para diferentes cenários:</span><span class="sxs-lookup"><span data-stu-id="78a5e-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="78a5e-133">Esquema</span><span class="sxs-lookup"><span data-stu-id="78a5e-133">Scheme</span></span> | <span data-ttu-id="78a5e-134">Notas</span><span class="sxs-lookup"><span data-stu-id="78a5e-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="78a5e-135">conta do storage predefinida Olá é um contentor de BLOBs numa conta do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="78a5e-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="78a5e-136">conta do storage predefinida Olá é um diretório no Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="78a5e-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="78a5e-137">Durante a criação do cluster, especifique o diretório de Olá no Data Lake Store é Olá raiz do HDFS do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="78a5e-138">Por exemplo, Olá `/clusters/myclustername/` diretório.</span><span class="sxs-lookup"><span data-stu-id="78a5e-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="78a5e-139">Uma conta do storage do Azure (adicionais) de não predefinida associada ao cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="78a5e-140">raiz de Olá da Olá utilizados pelo cluster Olá do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="78a5e-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="78a5e-141">Este esquema permite-lhe dados tooaccess localizados fora do diretório de Olá que contém o sistema de ficheiros do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="78a5e-142">Para obter mais informações, consulte Olá [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) referência em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="78a5e-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="78a5e-143">Configuração de exemplo</span><span class="sxs-lookup"><span data-stu-id="78a5e-143">Example configuration</span></span>

<span data-ttu-id="78a5e-144">Olá YAML seguinte é um excerpt de Olá `resources/writetohdfs.yaml` ficheiros incluídos no exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="78a5e-145">Este ficheiro define a topologia do Storm Olá utilizando Olá [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework para o Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="78a5e-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="78a5e-146">Este YAML define Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="78a5e-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="78a5e-147">`syncPolicy`: Define quando os ficheiros estão synched/descarregados toohello sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="78a5e-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="78a5e-148">Neste exemplo, todas as cadeias de identificação de 1000.</span><span class="sxs-lookup"><span data-stu-id="78a5e-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="78a5e-149">`fileNameFormat`: Define Olá ficheiro e caminho o nome padrão toouse quando escrever ficheiros.</span><span class="sxs-lookup"><span data-stu-id="78a5e-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="78a5e-150">Neste exemplo, o caminho de Olá é fornecido no tempo de execução utilizando um filtro, não sendo extensão de ficheiro Olá `.txt`.</span><span class="sxs-lookup"><span data-stu-id="78a5e-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="78a5e-151">`recordFormat`: Define o formato interno do Olá dos ficheiros de Olá escrito.</span><span class="sxs-lookup"><span data-stu-id="78a5e-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="78a5e-152">Neste exemplo, os campos são delimitados por Olá `|` caráter.</span><span class="sxs-lookup"><span data-stu-id="78a5e-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="78a5e-153">`rotationPolicy`: Define quando toorotate ficheiros.</span><span class="sxs-lookup"><span data-stu-id="78a5e-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="78a5e-154">Neste exemplo, é efetuada sem rotação.</span><span class="sxs-lookup"><span data-stu-id="78a5e-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="78a5e-155">`hdfs-bolt`: Utiliza Olá componentes anteriores como parâmetros de configuração para Olá `HdfsBolt` classe.</span><span class="sxs-lookup"><span data-stu-id="78a5e-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="78a5e-156">Para obter mais informações sobre a estrutura do Flux de Olá, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="78a5e-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="78a5e-157">Configurar o cluster de Olá</span><span class="sxs-lookup"><span data-stu-id="78a5e-157">Configure hello cluster</span></span>

<span data-ttu-id="78a5e-158">Por predefinição, o Storm no HDInsight não inclui os componentes de Olá que HdfsBolt utiliza toocommunicate com o Storage do Azure ou de Data Lake Store no classpath do Storm.</span><span class="sxs-lookup"><span data-stu-id="78a5e-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="78a5e-159">Tooadd de ação de script de utilização Olá seguinte, estes componentes toohello `extlib` diretório para Storm no cluster:</span><span class="sxs-lookup"><span data-stu-id="78a5e-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="78a5e-160">| URI de script | Nós tooapply que | Os parâmetros | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Nenhum |</span><span class="sxs-lookup"><span data-stu-id="78a5e-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="78a5e-161">Para informações sobre como utilizar este script com o cluster, consulte Olá [HDInsight personalizar clusters com ações de script](./hdinsight-hadoop-customize-cluster-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="78a5e-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="78a5e-162">Criar e da topologia de Olá do pacote</span><span class="sxs-lookup"><span data-stu-id="78a5e-162">Build and package hello topology</span></span>

1. <span data-ttu-id="78a5e-163">Transferir o projeto de exemplo de Olá da [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="78a5e-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="78a5e-164">Numa linha de comandos, terminal ou sessão de shell, alteração diretórios toohello raiz da Olá transferir o projeto.</span><span class="sxs-lookup"><span data-stu-id="78a5e-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="78a5e-165">toobuild e pacote Olá topologia, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="78a5e-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="78a5e-166">Depois de concluída a compilação de Olá e empacotamento, há um novo diretório designado `target`, que contém um ficheiro denominado `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="78a5e-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="78a5e-167">Este ficheiro contém a topologia de Olá compilada.</span><span class="sxs-lookup"><span data-stu-id="78a5e-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="78a5e-168">Implementar e executar a topologia de Olá</span><span class="sxs-lookup"><span data-stu-id="78a5e-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="78a5e-169">Utilize Olá cluster de HDInsight do comando toocopy Olá topologia toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="78a5e-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="78a5e-170">Substitua **utilizador** com o nome de utilizador do SSH Olá utilizado ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="78a5e-171">Substitua **CLUSTERNAME** com nome Olá cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="78a5e-172">Quando lhe for pedido, introduza a palavra-passe de Olá utilizada durante a criação de utilizador do SSH Olá para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="78a5e-173">Se tiver utilizado uma chave pública em vez de uma palavra-passe, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello correspondentes à chave privada.</span><span class="sxs-lookup"><span data-stu-id="78a5e-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78a5e-174">Para obter mais informações sobre como utilizar `scp` com o HDInsight, consulte [utilizar o SSH com o HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78a5e-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="78a5e-175">Após a conclusão do carregamento de Olá, utilize Olá seguir tooconnect toohello cluster do HDInsight através de SSH.</span><span class="sxs-lookup"><span data-stu-id="78a5e-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="78a5e-176">Substitua **utilizador** com o nome de utilizador do SSH Olá utilizado ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="78a5e-177">Substitua **CLUSTERNAME** com nome Olá cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="78a5e-178">Quando lhe for pedido, introduza a palavra-passe de Olá utilizada durante a criação de utilizador do SSH Olá para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="78a5e-179">Se tiver utilizado uma chave pública em vez de uma palavra-passe, poderá ser necessário toouse Olá `-i` parâmetro toospecify Olá caminho toohello correspondentes à chave privada.</span><span class="sxs-lookup"><span data-stu-id="78a5e-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="78a5e-180">Para obter mais informações, veja [Utilizar SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78a5e-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="78a5e-181">Assim que estiver ligado, de seguinte de Olá utilize comandos toocreate um ficheiro denominado `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="78a5e-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="78a5e-182">Olá de utilização seguintes texto como conteúdo Olá Olá `dev.properties` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="78a5e-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="78a5e-183">Este exemplo assume que o cluster utiliza uma conta de armazenamento do Azure como armazenamento de predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="78a5e-184">Se o cluster utiliza o Azure Data Lake Store, utilize `hdfs.url: adl:///` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="78a5e-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="78a5e-185">ficheiro de Olá toosave, utilize __Ctrl + X__, em seguida, __Y__e, finalmente, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="78a5e-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="78a5e-186">os valores de Olá neste ficheiro definidos Olá Data Lake store URL e o nome de diretório de Olá que dados são escritos para.</span><span class="sxs-lookup"><span data-stu-id="78a5e-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="78a5e-187">Utilize Olá topologia de Olá toostart de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="78a5e-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="78a5e-188">Este comando inicia a topologia de Olá utilizando a estrutura de Flux de Olá submetendo-nó Nimbus toohello cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="78a5e-189">topologia de Olá é definida pela Olá `writetohdfs.yaml` ficheiros incluídos no jar Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="78a5e-190">Olá `dev.properties` ficheiro é transmitido como um filtro e valores de Olá contidos no ficheiro de Olá são lidas pelas topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="78a5e-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="78a5e-191">Ver dados de saída</span><span class="sxs-lookup"><span data-stu-id="78a5e-191">View output data</span></span>

<span data-ttu-id="78a5e-192">dados de Olá tooview, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="78a5e-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="78a5e-193">É apresentada uma lista dos ficheiros de Olá criada por esta topologia.</span><span class="sxs-lookup"><span data-stu-id="78a5e-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="78a5e-194">Olá lista seguinte é um exemplo de dados de Olá retuned por comandos anteriores Olá:</span><span class="sxs-lookup"><span data-stu-id="78a5e-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="78a5e-195">Parar a topologia de Olá</span><span class="sxs-lookup"><span data-stu-id="78a5e-195">Stop hello topology</span></span>

<span data-ttu-id="78a5e-196">Topologias do Storm executam até parado ou cluster Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="78a5e-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="78a5e-197">toostop Olá topologia, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="78a5e-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="78a5e-198">Elimina o cluster</span><span class="sxs-lookup"><span data-stu-id="78a5e-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="78a5e-199">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="78a5e-199">Next steps</span></span>

<span data-ttu-id="78a5e-200">Agora que aprendeu como toouse Storm toowrite tooAzure armazenamento e o Azure Data Lake Store, detetar outros [Storm exemplos para o HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="78a5e-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

