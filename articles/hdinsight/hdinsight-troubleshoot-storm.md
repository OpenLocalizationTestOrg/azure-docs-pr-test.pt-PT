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
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="15939-104">Resolver problemas de Storm através do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="15939-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="15939-105">Saiba mais sobre os principais problemas de Olá e as resoluções para trabalhar com payloads do Apache Storm no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="15939-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="15939-106">Como posso aceder Olá IU do Storm num cluster</span><span class="sxs-lookup"><span data-stu-id="15939-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="15939-107">Tem duas opções para aceder ao hello IU do Storm num browser:</span><span class="sxs-lookup"><span data-stu-id="15939-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="15939-108">IU do Ambari</span><span class="sxs-lookup"><span data-stu-id="15939-108">Ambari UI</span></span>
1. <span data-ttu-id="15939-109">Aceda toohello Ambari dashboard.</span><span class="sxs-lookup"><span data-stu-id="15939-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="15939-110">Na lista de Olá de serviços, selecione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="15939-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="15939-111">No Olá **ligações rápidas** menu, selecione **IU do Storm**.</span><span class="sxs-lookup"><span data-stu-id="15939-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="15939-112">Ligação direta</span><span class="sxs-lookup"><span data-stu-id="15939-112">Direct link</span></span>
<span data-ttu-id="15939-113">Pode aceder Olá IU do Storm em Olá seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="15939-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="15939-114">https://\<nome DNS de cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="15939-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="15939-115">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="15939-115">Example:</span></span>

 <span data-ttu-id="15939-116">https://stormcluster.azurehdinsight.NET/stormui</span><span class="sxs-lookup"><span data-stu-id="15939-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="15939-117">Como transferir informações de ponto de verificação do Storm event hub spout a partir de uma topologia tooanother</span><span class="sxs-lookup"><span data-stu-id="15939-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="15939-118">Quando desenvolver topologias ler a partir do Event Hubs do Azure utilizando Olá o ficheiro. JAR do HDInsight Storm event hub spout, tem de implementar uma topologia que tenha Olá mesmo nome num cluster de novo.</span><span class="sxs-lookup"><span data-stu-id="15939-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="15939-119">No entanto, tem de manter os dados de ponto de verificação de Olá foi consolidada tooApache ZooKeeper no cluster antigo Olá.</span><span class="sxs-lookup"><span data-stu-id="15939-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="15939-120">Armazenar dados de ponto de verificação</span><span class="sxs-lookup"><span data-stu-id="15939-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="15939-121">Dados de ponto de verificação para desvios são armazenados pelo Olá event hub spout no ZooKeeper em dois caminhos de raiz:</span><span class="sxs-lookup"><span data-stu-id="15939-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="15939-122">Pontos de verificação do Nontransactional spout são armazenados no /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="15939-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="15939-123">Dados de ponto de verificação de spout transacional são armazenados na / transacional.</span><span class="sxs-lookup"><span data-stu-id="15939-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="15939-124">Como toorestore</span><span class="sxs-lookup"><span data-stu-id="15939-124">How toorestore</span></span>
<span data-ttu-id="15939-125">scripts de Olá tooget e as bibliotecas que utiliza dados tooexport fora ZooKeeper e, em seguida, importar Olá dados back-tooZooKeeper com um novo nome, consulte [exemplos de HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="15939-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="15939-126">pasta de lib Olá tem ficheiros. JAR que contém a implementação de Olá para a operação de exportação/importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="15939-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="15939-127">pasta de bash Olá tem um script de exemplo que demonstra como dados tooexport Olá servidor ZooKeeper no cluster antigo Olá e, em seguida, importe-o servidor de ZooKeeper back toohello no novo cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="15939-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="15939-128">Executar Olá [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script de tooexport de nós de ZooKeeper Olá e, em seguida, importar dados.</span><span class="sxs-lookup"><span data-stu-id="15939-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="15939-129">Atualização Olá script toohello Hortonworks Data Platform (HDP) versão correta.</span><span class="sxs-lookup"><span data-stu-id="15939-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="15939-130">(Estamos a trabalhar efetuar estes scripts genérico no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15939-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="15939-131">Genéricos podem executar scripts de qualquer nó no cluster de Olá sem modificações por utilizador Olá.)</span><span class="sxs-lookup"><span data-stu-id="15939-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="15939-132">comando de exportação de Olá escreve Olá metadados tooan sistema de ficheiros distribuído do Apache Hadoop (HDFS) caminho (na loja Blob Storage do Azure ou do Azure Data Lake Store) numa localização que definir.</span><span class="sxs-lookup"><span data-stu-id="15939-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="15939-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="15939-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="15939-134">Exportar metadados de deslocamento</span><span class="sxs-lookup"><span data-stu-id="15939-134">Export offset metadata</span></span>
1. <span data-ttu-id="15939-135">Utilize o cluster do SSH toogo toohello ZooKeeper num cluster de Olá do ponto de verificação que Olá deslocamento tem toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="15939-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="15939-136">Olá executar seguinte comando (depois de atualizar Olá cadeia de versão HDP) tooexport ZooKeeper deslocamento dados toohello /stormmetadta/zkdata HDFS caminho:</span><span class="sxs-lookup"><span data-stu-id="15939-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="15939-137">Importar metadados de deslocamento</span><span class="sxs-lookup"><span data-stu-id="15939-137">Import offset metadata</span></span>
1. <span data-ttu-id="15939-138">Utilize o cluster do SSH toogo toohello ZooKeeper num cluster de Olá do ponto de verificação que Olá deslocamento tem toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="15939-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="15939-139">Execute hello os seguintes comandos (depois de atualizar a cadeia de versão Olá HDP) tooimport ZooKeeper deslocamento de dados de Olá HDFS caminho/stormmetadata/zkdata toohello ZooKeeper servidor no cluster de destino Olá:</span><span class="sxs-lookup"><span data-stu-id="15939-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="15939-140">Eliminar os metadados de deslocamento para que as topologias podem começar a processar dados a partir do início de Olá ou de um timestamp escolhe esse utilizador Olá</span><span class="sxs-lookup"><span data-stu-id="15939-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="15939-141">Utilize o cluster do SSH toogo toohello ZooKeeper num cluster de Olá do ponto de verificação que Olá deslocamento tem toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="15939-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="15939-142">Execute hello os seguintes comandos (depois de atualizar a cadeia de versão Olá HDP) toodelete todos os dados em cluster atual Olá de deslocamento de ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="15939-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="15939-143">Como localizar o binários de Storm num cluster</span><span class="sxs-lookup"><span data-stu-id="15939-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="15939-144">Os binários de Storm para a pilha HDP atual Olá são /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="15939-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="15939-145">localização de Olá é Olá mesmo para nós principais e nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="15939-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="15939-146">Podem existir vários binários para versões HDP específicas no /usr/hdp (por exemplo, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="15939-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="15939-147">pasta de /usr/hdp/current/storm-client Olá é symlinked toohello versão mais recente que está em execução no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="15939-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="15939-148">Para obter mais informações, consulte [Connect tooan cluster do HDInsight utilizando SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="15939-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="15939-149">Como determinar a topologia de implementação de Olá de um cluster do Storm</span><span class="sxs-lookup"><span data-stu-id="15939-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="15939-150">Em primeiro lugar, identifique todos os componentes que são instalados com o HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="15939-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="15939-151">Um cluster do Storm é constituída por quatro categorias de nó:</span><span class="sxs-lookup"><span data-stu-id="15939-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="15939-152">Nós de gateway</span><span class="sxs-lookup"><span data-stu-id="15939-152">Gateway nodes</span></span>
* <span data-ttu-id="15939-153">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="15939-153">Head nodes</span></span>
* <span data-ttu-id="15939-154">Nós de zooKeeper</span><span class="sxs-lookup"><span data-stu-id="15939-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="15939-155">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="15939-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="15939-156">Nós de gateway</span><span class="sxs-lookup"><span data-stu-id="15939-156">Gateway nodes</span></span>
<span data-ttu-id="15939-157">Um nó de gateway é um gateway e o serviço de proxy inverso que permite o serviço de gestão de Ambari Active Directory do acesso público tooan.</span><span class="sxs-lookup"><span data-stu-id="15939-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="15939-158">Ele também faz eleição de leader do Ambari.</span><span class="sxs-lookup"><span data-stu-id="15939-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="15939-159">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="15939-159">Head nodes</span></span>
<span data-ttu-id="15939-160">Nós principais do Storm executam Olá os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="15939-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="15939-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="15939-161">Nimbus</span></span>
* <span data-ttu-id="15939-162">Servidor do Ambari</span><span class="sxs-lookup"><span data-stu-id="15939-162">Ambari server</span></span>
* <span data-ttu-id="15939-163">Servidor de métricas do Ambari</span><span class="sxs-lookup"><span data-stu-id="15939-163">Ambari Metrics server</span></span>
* <span data-ttu-id="15939-164">Recoletor de métricas do Ambari</span><span class="sxs-lookup"><span data-stu-id="15939-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="15939-165">Nós de zooKeeper</span><span class="sxs-lookup"><span data-stu-id="15939-165">ZooKeeper nodes</span></span>
<span data-ttu-id="15939-166">O HDInsight inclui um quórum de ZooKeeper três nós.</span><span class="sxs-lookup"><span data-stu-id="15939-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="15939-167">tamanho de quórum Olá é fixo e não pode ser reconfigurado.</span><span class="sxs-lookup"><span data-stu-id="15939-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="15939-168">Serviços de Storm num cluster de Olá são quórum de ZooKeeper tooautomatically configurada utilize Olá.</span><span class="sxs-lookup"><span data-stu-id="15939-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="15939-169">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="15939-169">Worker nodes</span></span>
<span data-ttu-id="15939-170">Nós de trabalho do Storm executam Olá os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="15939-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="15939-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="15939-171">Supervisor</span></span>
* <span data-ttu-id="15939-172">Trabalho Java as máquinas virtuais (JVMs), para a execução de topologias</span><span class="sxs-lookup"><span data-stu-id="15939-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="15939-173">Agente do Ambari</span><span class="sxs-lookup"><span data-stu-id="15939-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="15939-174">Como localizar o Storm event hub spout os binários para o desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="15939-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="15939-175">Para obter mais informações sobre como utilizar os ficheiros do Storm event hub spout. JAR com a topologia, consulte Olá os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="15939-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="15939-176">Topologia baseada em Java</span><span class="sxs-lookup"><span data-stu-id="15939-176">Java-based topology</span></span>
[<span data-ttu-id="15939-177">Processar eventos provenientes dos Hubs de eventos do Azure com o Storm no HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="15939-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="15939-178">C#-com base topologia (Mono nos clusters do HDInsight 3.4 + Linux Storm)</span><span class="sxs-lookup"><span data-stu-id="15939-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
<span data-ttu-id="15939-179">[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology) (Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight [C#])</span><span class="sxs-lookup"><span data-stu-id="15939-179">[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)</span></span>
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="15939-180">Hub de eventos mais recente do Storm spout binários para clusters do HDInsight 3.5 + Linux Storm</span><span class="sxs-lookup"><span data-stu-id="15939-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="15939-181">toolearn como toouse Olá mais recente Storm event hub spout que funciona com o HDInsight 3.5 + clusters do Linux Storm, consulte Olá mvn-repo [ficheiro Leia-me](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="15939-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="15939-182">Exemplos de código de origem</span><span class="sxs-lookup"><span data-stu-id="15939-182">Source code examples</span></span>
<span data-ttu-id="15939-183">Consulte [exemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) como tooread e escrita do Hub de eventos do Azure com uma topologia de Apache Storm (escrita em Java) num cluster do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15939-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="15939-184">Como localizar o ficheiros de configuração de Storm Log4J em clusters</span><span class="sxs-lookup"><span data-stu-id="15939-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="15939-185">ficheiros de configuração de tooidentify Apache Log4J para serviços do Storm.</span><span class="sxs-lookup"><span data-stu-id="15939-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="15939-186">Em nós principais</span><span class="sxs-lookup"><span data-stu-id="15939-186">On head nodes</span></span>
<span data-ttu-id="15939-187">configuração de Olá Nimbus Log4J é lida /usr/hdp/\<versão HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="15939-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="15939-188">Em nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="15939-188">On worker nodes</span></span>
<span data-ttu-id="15939-189">configuração de supervisor Log4J Olá é lida /usr/hdp/\<versão HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="15939-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="15939-190">ficheiro de configuração de trabalho Log4J Olá é lida /usr/hdp/\<versão HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="15939-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="15939-191">Exemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="15939-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

