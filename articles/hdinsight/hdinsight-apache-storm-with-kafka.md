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
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="cc669-105">Utilizar o Apache Kafka (pré-visualização) com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc669-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="cc669-106">Saiba como toouse Apache Storm tooread de e escrevem tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="cc669-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="cc669-107">Este exemplo também demonstra como o sistema utilizado pelo HDInsight de ficheiros de dados toosave um toohello de topologia do Storm compatível com HDFS.</span><span class="sxs-lookup"><span data-stu-id="cc669-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="cc669-108">passos de Olá neste documento, criar um grupo de recursos do Azure que contém tanto um Storm no HDInsight e um Kafka num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc669-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="cc669-109">Esses clusters são ambos localizado dentro de uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Storm comunicam com Olá Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="cc669-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="cc669-110">Quando tiver terminado com os passos de Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.</span><span class="sxs-lookup"><span data-stu-id="cc669-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="cc669-111">Obter o código de Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-111">Get hello code</span></span>

<span data-ttu-id="cc669-112">código de Olá, por exemplo Olá utilizado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="cc669-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="cc669-113">toocompile este projeto, terá de seguir a configuração para o seu ambiente de desenvolvimento de Olá:</span><span class="sxs-lookup"><span data-stu-id="cc669-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="cc669-114">[1.8 do Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="cc669-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="cc669-115">HDInsight 3.5 ou superior necessário Java 8.</span><span class="sxs-lookup"><span data-stu-id="cc669-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="cc669-116">Maven 3</span><span class="sxs-lookup"><span data-stu-id="cc669-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="cc669-117">Um cliente SSH (terá Olá `ssh` e `scp` comandos) – para obter informações, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cc669-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="cc669-118">Num editor de texto ou IDE.</span><span class="sxs-lookup"><span data-stu-id="cc669-118">A text editor or IDE.</span></span>

<span data-ttu-id="cc669-119">Olá seguintes variáveis de ambiente podem ser definidas quando instalar o Java e Olá JDK na sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="cc669-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="cc669-120">No entanto, deve verificar que existe e que contêm valores corretos a Olá para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="cc669-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="cc669-121">`JAVA_HOME`-devem apontar toohello diretório onde hello JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="cc669-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="cc669-122">`PATH`-deve conter Olá seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="cc669-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="cc669-123">`JAVA_HOME`(ou um caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="cc669-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="cc669-124">`JAVA_HOME\bin`(ou um caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="cc669-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="cc669-125">diretório de olá onde Maven está instalado.</span><span class="sxs-lookup"><span data-stu-id="cc669-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="cc669-126">Criar clusters Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-126">Create hello clusters</span></span>

<span data-ttu-id="cc669-127">Apache Kafka no HDInsight fornece acesso toohello Kafka mediadores Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="cc669-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="cc669-128">Olá tudo o que Olá, talks tooKafka tem de estar na mesma rede virtual do Azure como nós de Olá num cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="cc669-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="cc669-129">Para este exemplo Olá Kafka e clusters de Storm estão localizados numa rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc669-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="cc669-130">Olá diagrama seguinte mostra como flui de comunicação entre clusters de Olá:</span><span class="sxs-lookup"><span data-stu-id="cc669-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clusters Storm e Kafka uma Azure virtual network](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="cc669-132">Outros serviços em cluster Olá, tais como podem ser acedido através de SSH e Ambari Olá internet.</span><span class="sxs-lookup"><span data-stu-id="cc669-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="cc669-133">Para obter mais informações sobre portas pública Olá disponíveis com o HDInsight, consulte [portas e os URIs utilizados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="cc669-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="cc669-134">Pode criar uma Azure virtual network, Kafka, e clusters de Storm manualmente, é mais fácil toouse um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc669-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="cc669-135">Seguinte de Olá utilize os passos toodeploy uma Azure virtual network, Kafka, e clusters de Storm tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc669-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="cc669-136">Utilize Olá seguinte botão toosign no tooAzure e o modelo de Olá aberta no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc669-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="cc669-137">Olá modelo Azure Resource Manager está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="cc669-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="cc669-138">Cria Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="cc669-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="cc669-139">Grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="cc669-139">Azure resource group</span></span>
    * <span data-ttu-id="cc669-140">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="cc669-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="cc669-141">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cc669-141">Azure Storage account</span></span>
    * <span data-ttu-id="cc669-142">Kafka no HDInsight versão 3.6 (três nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="cc669-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="cc669-143">Storm no HDInsight versão 3.6 (três nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="cc669-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="cc669-144">disponibilidade de tooguarantee dos Kafka no HDInsight, o cluster tem de conter, pelo menos, três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cc669-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="cc669-145">Este modelo cria um cluster Kafka contém três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cc669-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="cc669-146">Olá utilizar seguindo as entradas do orientações toopopulate Olá do Olá **implementação personalizada** painel:</span><span class="sxs-lookup"><span data-stu-id="cc669-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implementação personalizada do HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="cc669-148">**Grupo de recursos**: criar um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="cc669-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="cc669-149">Este grupo contém o cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="cc669-150">**Localização**: selecione uma tooyou fechar geograficamente da localização.</span><span class="sxs-lookup"><span data-stu-id="cc669-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="cc669-151">**Nome do Cluster de base**: este valor é utilizado como nome de base de Olá para clusters de Storm e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="cc669-152">Por exemplo, introduzir **hdi** cria um cluster do Storm com o nome **storm hdi** e um cluster de Kafka denominado **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="cc669-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="cc669-153">**Nome de utilizador de início de sessão do cluster**: nome de utilizador de admin Olá para clusters de Storm e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="cc669-154">**Palavra-passe de início de sessão do cluster**: palavra-passe utilizador de administrador de Olá para clusters de Storm e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="cc669-155">**Nome de utilizador SSH**: Olá toocreate de utilizador do SSH para clusters de Storm e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="cc669-156">**Palavra-passe SSH**: Olá palavra-passe do utilizador do SSH Olá para clusters de Storm e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="cc669-157">Olá leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições indicadas acima**.</span><span class="sxs-lookup"><span data-stu-id="cc669-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="cc669-158">Por fim, verifique **Pin toodashboard** e, em seguida, selecione **Compra**.</span><span class="sxs-lookup"><span data-stu-id="cc669-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="cc669-159">Demora cerca de 20 minutos toocreate clusters Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="cc669-160">Depois de tem sido criados recursos Olá, é apresentado o painel de Olá Olá grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc669-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Painel do grupo de recursos para vnet Olá e clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="cc669-162">Tenha em atenção que os nomes de Olá dos clusters do HDInsight Olá são **storm BASENAME** e **kafka BASENAME**, onde BASENAME nome Olá fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="cc669-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="cc669-163">Ao ligar a toohello clusters é utilizar estes nomes em passos posteriores.</span><span class="sxs-lookup"><span data-stu-id="cc669-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="cc669-164">Compreender o código de Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-164">Understanding hello code</span></span>

<span data-ttu-id="cc669-165">Este projeto contém duas topologias:</span><span class="sxs-lookup"><span data-stu-id="cc669-165">This project contains two topologies:</span></span>

* <span data-ttu-id="cc669-166">**KafkaWriter**: definidos pela Olá **writer.yaml** ficheiro, esta topologia escreve tooKafka frases aleatória utilizando Olá KafkaBolt fornecido com Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="cc669-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="cc669-167">Esta topologia utiliza personalizadas **SentenceSpout** frases aleatório do componente toogenerate.</span><span class="sxs-lookup"><span data-stu-id="cc669-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="cc669-168">**KafkaReader**: definidos pela Olá **reader.yaml** ficheiro, esta topologia lê dados de Kafka utilizando Olá KafkaSpout fornecido com Apache Storm, em seguida, os registos Olá toostdout de dados.</span><span class="sxs-lookup"><span data-stu-id="cc669-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="cc669-169">Esta topologia utiliza Olá Storm HdfsBolt toowrite dados toodefault um armazenamento de cluster do Storm Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="cc669-170">Flux</span><span class="sxs-lookup"><span data-stu-id="cc669-170">Flux</span></span>

<span data-ttu-id="cc669-171">topologias de Olá são definidas utilizando [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="cc669-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="cc669-172">Flux foi introduzida no Storm 0.10.x e permite-lhe configuração da topologia Olá tooseparate a partir do código Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="cc669-173">Para as topologias que utilizam a estrutura do Flux de Olá, a topologia de Olá está definida num ficheiro YAML.</span><span class="sxs-lookup"><span data-stu-id="cc669-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="cc669-174">ficheiro YAML Olá pode ser incluído como parte da topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="cc669-175">Também pode ser um ficheiro autónomo utilizado ao submeter a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="cc669-176">Flux também suporta a substituição das variáveis em tempo de execução, que é utilizada neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="cc669-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="cc669-177">Olá parâmetros seguintes são definidos em tempo de execução para estes topologias:</span><span class="sxs-lookup"><span data-stu-id="cc669-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="cc669-178">`${kafka.topic}`: nome Olá Olá tópico Kafka que topologias Olá leitura/escritam.</span><span class="sxs-lookup"><span data-stu-id="cc669-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="cc669-179">`${kafka.broker.hosts}`: Olá aloja esse Olá Kafka mediadores executar.</span><span class="sxs-lookup"><span data-stu-id="cc669-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="cc669-180">informações de Mediador de Olá utilizadas pelo Olá KafkaBolt escrever tooKafka.</span><span class="sxs-lookup"><span data-stu-id="cc669-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="cc669-181">`${kafka.zookeeper.hosts}`: anfitriões Olá Zookeeper executado em Olá Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="cc669-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="cc669-182">Para obter mais informações sobre topologias Flux, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="cc669-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="cc669-183">Transferir e compilar o projeto de Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-183">Download and compile hello project</span></span>

1. <span data-ttu-id="cc669-184">No seu ambiente de desenvolvimento, transfira o projeto de Olá de [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra uma linha de comandos e altere a localização de toohello de diretórios que transferiu o projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="cc669-185">De Olá **hdinsight-storm-java-kafka** diretório, utilize seguinte de Olá projeto de Olá toocompile de comandos e cria um pacote de implementação:</span><span class="sxs-lookup"><span data-stu-id="cc669-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="cc669-186">processo de pacote de Olá cria um ficheiro denominado `KafkaTopology-1.0-SNAPSHOT.jar` no Olá `target` diretório.</span><span class="sxs-lookup"><span data-stu-id="cc669-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="cc669-187">Utilize Olá os seguintes comandos toocopy Olá pacote tooyour Storm num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc669-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="cc669-188">Substitua **USERNAME** com o nome de utilizador do SSH Olá para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="cc669-189">Substitua **BASENAME** com o nome de base de Olá utilizado ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="cc669-190">Quando lhe for pedido, introduza a palavra-passe de Olá utilizado aquando da criação de clusters de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="cc669-191">Configurar a topologia de Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-191">Configure hello topology</span></span>

1. <span data-ttu-id="cc669-192">Utilize um dos Olá seguintes métodos toodiscover Olá anfitriões de Mediador Kafka:</span><span class="sxs-lookup"><span data-stu-id="cc669-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

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
    > <span data-ttu-id="cc669-193">Olá Bash exemplo assume que `$CLUSTERNAME` contém Olá nome do cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="cc669-194">Também parte do princípio que [jq](https://stedolan.github.io/jq/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="cc669-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="cc669-195">Quando lhe for pedido, introduza a palavra-passe de Olá para a conta de início de sessão do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="cc669-196">valor de Olá devolvido é semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="cc669-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="cc669-197">Enquanto pode ser mais do que dois mediador anfitriões para o cluster, não precisa de tooprovide uma lista completa de todos os anfitriões tooclients.</span><span class="sxs-lookup"><span data-stu-id="cc669-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="cc669-198">Um ou dois são suficiente.</span><span class="sxs-lookup"><span data-stu-id="cc669-198">One or two is enough.</span></span>

2. <span data-ttu-id="cc669-199">Utilize um dos Olá anfitriões de Kafka Zookeeper métodos toodiscover Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cc669-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

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
    > <span data-ttu-id="cc669-200">Olá Bash exemplo assume que `$CLUSTERNAME` contém Olá nome do cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="cc669-201">Também parte do princípio que [jq](https://stedolan.github.io/jq/) está instalado.</span><span class="sxs-lookup"><span data-stu-id="cc669-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="cc669-202">Quando lhe for pedido, introduza a palavra-passe de Olá para a conta de início de sessão do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="cc669-203">valor de Olá devolvido é semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="cc669-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="cc669-204">Enquanto existirem mais de dois nós de Zookeeper, não precisa de tooprovide uma lista completa de todos os anfitriões tooclients.</span><span class="sxs-lookup"><span data-stu-id="cc669-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="cc669-205">Um ou dois são suficiente.</span><span class="sxs-lookup"><span data-stu-id="cc669-205">One or two is enough.</span></span>

    <span data-ttu-id="cc669-206">Guarde este valor, porque é utilizado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cc669-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="cc669-207">Editar Olá `dev.properties` ficheiro na raiz de Olá do projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="cc669-208">Adicione Olá mediador e linhas com correspondência do Zookeeper anfitriões informações toohello neste ficheiro.</span><span class="sxs-lookup"><span data-stu-id="cc669-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="cc669-209">Olá exemplo seguinte é configurado utilizando os valores de exemplo de Olá dos passos anteriores Olá:</span><span class="sxs-lookup"><span data-stu-id="cc669-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="cc669-210">Guardar Olá `dev.properties` ficheiro e, em seguida, utilize Olá os seguintes comandos tooupload este cluster do Storm toohello:</span><span class="sxs-lookup"><span data-stu-id="cc669-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="cc669-211">Substitua **USERNAME** com o nome de utilizador do SSH Olá para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="cc669-212">Substitua **BASENAME** com o nome de base de Olá utilizado ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="cc669-213">Escritor de Olá de início</span><span class="sxs-lookup"><span data-stu-id="cc669-213">Start hello writer</span></span>

1. <span data-ttu-id="cc669-214">Utilize Olá seguir o cluster do Storm tooconnect toohello utilizando SSH.</span><span class="sxs-lookup"><span data-stu-id="cc669-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="cc669-215">Substitua **USERNAME** com o nome de utilizador SSH Olá utilizado ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="cc669-216">Substitua **BASENAME** com o nome de base Olá utilizado ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="cc669-217">Quando lhe for pedido, introduza a palavra-passe de Olá utilizado aquando da criação de clusters de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="cc669-218">Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cc669-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cc669-219">A partir de Olá ligação SSH, utilize Olá Olá toocreate do comando tópico Kafka utilizado por topologia Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cc669-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="cc669-220">Substitua `$KAFKAZKHOSTS` com Olá Zookeeper informações que obteve na secção anterior Olá do anfitrião.</span><span class="sxs-lookup"><span data-stu-id="cc669-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="cc669-221">A partir do cluster do Olá SSH ligação toohello Storm, utilize Olá topologia de escritor do comando toostart Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cc669-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="cc669-222">os parâmetros de Olá utilizados com este comando são:</span><span class="sxs-lookup"><span data-stu-id="cc669-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="cc669-223">`org.apache.storm.flux.Flux`: Utilize Flux tooconfigure e execute esta topologia.</span><span class="sxs-lookup"><span data-stu-id="cc669-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="cc669-224">`--remote`: Olá topologia tooNimbus de envio.</span><span class="sxs-lookup"><span data-stu-id="cc669-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="cc669-225">topologia de Olá é distribuída entre os nós de trabalho Olá num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="cc669-226">`-R /writer.yaml`: Olá utilize `writer.yaml` topologia de Olá tooconfigure de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="cc669-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="cc669-227">`-R`indica que este recurso está incluído no ficheiro de jar Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="cc669-228">É por isso, na raiz de Olá da jar Olá, `/writer.yaml` é Olá tooit de caminho.</span><span class="sxs-lookup"><span data-stu-id="cc669-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="cc669-229">`--filter`: A preencher a entradas no Olá `writer.yaml` topologia com valores no Olá `dev.properties` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="cc669-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="cc669-230">Olá, por exemplo, o valor de Olá `kafka.topic` entrada no ficheiro de Olá é utilizado tooreplace Olá `${kafka.topic}` entrada na definição de topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="cc669-231">Depois de é iniciado a topologia de Olá, utilize Olá tooverify de comando que está a escrever dados toohello tópico Kafka os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cc669-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="cc669-232">Substitua `$KAFKAZKHOSTS` com Olá Zookeeper informações que obteve na secção anterior Olá do anfitrião.</span><span class="sxs-lookup"><span data-stu-id="cc669-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="cc669-233">Este comando utiliza um script vem incluído no tópico de Olá Kafka toomonitor.</span><span class="sxs-lookup"><span data-stu-id="cc669-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="cc669-234">Após um momento, este deve iniciar aleatórios frases escritos toohello tópico a devolver.</span><span class="sxs-lookup"><span data-stu-id="cc669-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="cc669-235">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="cc669-235">hello output is similar toohello following example:</span></span>

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

    <span data-ttu-id="cc669-236">Utilize Ctrl + c toostop script de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="cc669-237">Início Olá leitor</span><span class="sxs-lookup"><span data-stu-id="cc669-237">Start hello reader</span></span>

1. <span data-ttu-id="cc669-238">A partir do cluster do Olá SSH sessão toohello Storm, utilize Olá topologia de leitor do comando toostart Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cc669-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="cc669-239">Assim que for iniciada a topologia de Olá, abra Olá IU do Storm.</span><span class="sxs-lookup"><span data-stu-id="cc669-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="cc669-240">Este IU da web está localizado em https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="cc669-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="cc669-241">Substitua __BASENAME__ com o nome de base Olá utilizada quando Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="cc669-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="cc669-242">Quando lhe for pedido, utilize o nome de início de sessão de administrador Olá (predefinição, `admin`) e palavra-passe utilizada quando Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="cc669-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="cc669-243">Consulte uma toohello semelhante de página web seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="cc669-243">You see a web page similar toohello following image:</span></span>

    ![IU do Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="cc669-245">Na IU do Storm Olá, selecione Olá __kafka leitor__ ligação no Olá __resumo da topologia__ secção toodisplay informações sobre Olá __kafka leitor__ topologia.</span><span class="sxs-lookup"><span data-stu-id="cc669-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Secção de resumo da topologia da IU da web do Olá Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="cc669-247">informações de toodisplay sobre Olá as instâncias do componente de registo bolt Olá, selecione Olá __registador bolt__ ligação no Olá __Bolts (tempo)__ secção.</span><span class="sxs-lookup"><span data-stu-id="cc669-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Ligação registador bolt Olá bolts secção](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="cc669-249">No Olá __executores__ secção, selecione uma ligação na Olá __porta__ informações de registo de toodisplay coluna sobre esta instância do componente de Olá.</span><span class="sxs-lookup"><span data-stu-id="cc669-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Executores ligação](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="cc669-251">registo de Olá contém um registo de dados de Olá lidos Olá tópico Kafka.</span><span class="sxs-lookup"><span data-stu-id="cc669-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="cc669-252">informações de Olá no registo de Olá são semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="cc669-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="cc669-253">Parar topologias Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-253">Stop hello topologies</span></span>

<span data-ttu-id="cc669-254">A partir de um cluster do Storm do SSH sessão toohello, utilize Olá topologias do Storm comandos toostop Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cc669-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="cc669-255">Eliminar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="cc669-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="cc669-256">Uma vez que os passos neste documento Olá criar ambos Olá de clusters no mesmo grupo de recursos do Azure, pode eliminar o grupo de recursos Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc669-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="cc669-257">Eliminar grupo de recursos de Olá remove todos os recursos que criou ao seguir este documento.</span><span class="sxs-lookup"><span data-stu-id="cc669-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc669-258">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cc669-258">Next steps</span></span>

<span data-ttu-id="cc669-259">Para obter mais topologias de exemplo que podem ser utilizadas com o Storm no HDInsight, consulte [topologias do Storm de exemplo e componentes](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc669-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="cc669-260">Para obter informações sobre como implementar e monitorizar topologias no HDInsight baseado em Linux, consulte [implementar e gerir topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="cc669-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>