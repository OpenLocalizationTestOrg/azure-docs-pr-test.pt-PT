---
title: "aaaApache Spark estruturados transmissão em fluxo com Kafka - Azure HDInsight | Microsoft Docs"
description: "Saiba como toouse Apache Spark transmissão em fluxo (DStream) tooget dados ou a sair Apache Kafka. Neste exemplo, transmitir dados através de um bloco de notas do Jupyter do Spark no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="e9253-104">Utilizar o Spark estruturados transmissão em fluxo com Kafka (pré-visualização) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9253-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="e9253-105">Saiba como toouse dados Apache Kafka no Azure HDInsight Spark estruturados de transmissão em fluxo tooread.</span><span class="sxs-lookup"><span data-stu-id="e9253-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="e9253-106">Spark estruturado de transmissão em fluxo é um motor de processamento de fluxo incorporado no Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="e9253-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="e9253-107">Permite-lhe computações de transmissão em fluxo tooexpress Olá igual ao cálculo de batch nos dados estáticos.</span><span class="sxs-lookup"><span data-stu-id="e9253-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="e9253-108">Para obter mais informações sobre a transmissão em fluxo estruturada, consulte Olá [estruturados de transmissão em fluxo guia de programação [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="e9253-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9253-109">Neste exemplo utilizado 2.1 do Spark no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e9253-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="e9253-110">Transmissão em fluxo estruturada é considerado __alpha__ no Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="e9253-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="e9253-111">passos de Olá neste documento, criar um grupo de recursos do Azure que contém tanto o Spark no HDInsight e um Kafka num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9253-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="e9253-112">Esses clusters são ambos localizado dentro de uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Spark comunicam com Olá Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="e9253-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="e9253-113">Quando tiver terminado com os passos de Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.</span><span class="sxs-lookup"><span data-stu-id="e9253-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="e9253-114">Criar clusters Olá</span><span class="sxs-lookup"><span data-stu-id="e9253-114">Create hello clusters</span></span>

<span data-ttu-id="e9253-115">Apache Kafka no HDInsight fornece acesso toohello Kafka mediadores Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="e9253-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="e9253-116">Olá tudo o que Olá, talks tooKafka tem de estar na mesma rede virtual do Azure como nós de Olá num cluster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="e9253-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="e9253-117">Para este exemplo Olá Kafka e clusters do Spark estão localizados numa rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9253-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="e9253-118">Olá diagrama seguinte mostra como flui de comunicação entre clusters de Olá:</span><span class="sxs-lookup"><span data-stu-id="e9253-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clusters do Spark e Kafka uma Azure virtual network](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="e9253-120">Olá serviço Kafka é limitado toocommunication dentro da rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="e9253-121">Outros serviços em cluster Olá, tal como pode ser acedido através de SSH e Ambari, Olá internet.</span><span class="sxs-lookup"><span data-stu-id="e9253-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="e9253-122">Para obter mais informações sobre portas pública Olá disponíveis com o HDInsight, consulte [portas e os URIs utilizados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e9253-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="e9253-123">Apesar de poder criar uma Azure virtual network, Kafka e Spark clusters manualmente, é mais fácil toouse um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9253-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="e9253-124">Seguinte de Olá utilize os passos toodeploy uma Azure virtual network, Kafka, e clusters do Spark tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9253-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="e9253-125">Utilize Olá seguinte botão toosign no tooAzure e o modelo de Olá aberta no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9253-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="e9253-126">Olá modelo Azure Resource Manager está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="e9253-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="e9253-127">Este modelo cria Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="e9253-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="e9253-128">Um Kafka no cluster de HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="e9253-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="e9253-129">Spark no HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="e9253-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="e9253-130">Uma rede Virtual do Azure, que contém os clusters do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e9253-131">Olá estruturados transmissão em fluxo bloco de notas utilizado neste exemplo requer o Spark no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e9253-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="e9253-132">Se utilizar uma versão anterior do Spark no HDInsight, receber erros ao utilizar o bloco de notas do Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="e9253-133">Olá utilize seguindo entradas de Olá toopopulate de informações do Olá **implementação personalizada** painel:</span><span class="sxs-lookup"><span data-stu-id="e9253-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implementação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="e9253-135">**Grupo de recursos**: criar um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="e9253-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="e9253-136">Este grupo contém o cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="e9253-137">**Localização**: selecione uma tooyou fechar geograficamente da localização.</span><span class="sxs-lookup"><span data-stu-id="e9253-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="e9253-138">**Nome do Cluster de base**: este valor é utilizado como nome de base de Olá para clusters do Spark e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="e9253-139">Por exemplo, introduzir **hdi** cria um Spark cluster spark hdi__ com o nome e um cluster de Kafka denominado **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="e9253-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="e9253-140">**Nome de utilizador de início de sessão do cluster**: nome de utilizador de admin Olá para clusters do Spark e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e9253-141">**Palavra-passe de início de sessão do cluster**: palavra-passe utilizador de administrador de Olá para clusters do Spark e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e9253-142">**Nome de utilizador SSH**: Olá toocreate de utilizador do SSH para clusters do Spark e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e9253-143">**Palavra-passe SSH**: Olá palavra-passe do utilizador do SSH Olá para clusters do Spark e Kafka Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="e9253-144">Olá leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições indicadas acima**.</span><span class="sxs-lookup"><span data-stu-id="e9253-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="e9253-145">Por fim, verifique **Pin toodashboard** e, em seguida, selecione **Compra**.</span><span class="sxs-lookup"><span data-stu-id="e9253-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e9253-146">Demora cerca de 20 minutos toocreate clusters Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="e9253-147">Depois de tem sido criados recursos Olá, está redirecionado toohello painel do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e9253-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Painel do grupo de recursos para vnet Olá e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e9253-149">Tenha em atenção que os nomes de Olá dos clusters do HDInsight Olá são **spark BASENAME** e **kafka BASENAME**, onde BASENAME nome Olá fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="e9253-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="e9253-150">Ao ligar a toohello clusters é utilizar estes nomes em passos posteriores.</span><span class="sxs-lookup"><span data-stu-id="e9253-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="e9253-151">Obter Olá Kafka mediadores</span><span class="sxs-lookup"><span data-stu-id="e9253-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="e9253-152">Olá código neste exemplo liga-se toohello Kafka mediador anfitriões Olá Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="e9253-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="e9253-153">toofind Olá anfitriões de Mediador Kafka, utilize Olá seguinte o exemplo do PowerShell ou Bash:</span><span class="sxs-lookup"><span data-stu-id="e9253-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="e9253-154">Neste exemplo espera `$PASSWORD` toocontain Olá palavra-passe início de sessão de cluster Olá e `$CLUSTERNAME` toocontain nome Olá Olá Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="e9253-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="e9253-155">Este exemplo utiliza Olá [jq](https://stedolan.github.io/jq/) dados de tooparse utilitário fora do documento JSON de Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="e9253-156">Olá de saída é semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="e9253-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="e9253-157">Guarde esta informação, como é utilizado em Olá seguintes secções deste documento.</span><span class="sxs-lookup"><span data-stu-id="e9253-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="e9253-158">Obter os blocos de notas Olá</span><span class="sxs-lookup"><span data-stu-id="e9253-158">Get hello notebooks</span></span>

<span data-ttu-id="e9253-159">código de Olá, por exemplo Olá descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="e9253-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="e9253-160">Carregar os blocos de notas Olá</span><span class="sxs-lookup"><span data-stu-id="e9253-160">Upload hello notebooks</span></span>

<span data-ttu-id="e9253-161">Utilize Olá seguintes blocos de notas do passos tooupload Olá de Olá projeto tooyour Spark num cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e9253-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="e9253-162">No seu browser, ligue toohello de notas do Jupyter no cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="e9253-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="e9253-163">Substituir o URL, a seguir no Olá `CLUSTERNAME` com o nome de Olá do Kafka cluster:</span><span class="sxs-lookup"><span data-stu-id="e9253-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="e9253-164">Quando lhe for pedido, introduza o início de sessão do cluster de Olá (administrador) e palavra-passe utilizada quando criou o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="e9253-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="e9253-165">A partir de Olá superior direita da página Olá, utilize Olá __carregar__ Olá do botão tooupload __fluxo-Tweets-To_Kafka.ipynb__ cluster toohello de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e9253-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="e9253-166">Selecione __abra__ carregamento de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="e9253-166">Select __Open__ toostart hello upload.</span></span>

    ![Utilize Olá carregamento botão tooselect e carregar um bloco de notas](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selecione o ficheiro de KafkaStreaming.ipynb Olá](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="e9253-169">Determinar Olá __fluxo-Tweets-To_Kafka.ipynb__ entrada na lista de Olá de blocos de notas e selecione __carregar__ botão junto-lo.</span><span class="sxs-lookup"><span data-stu-id="e9253-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Carregamento de Olá Utilize botão junto tooupload de entrada de KafkaStreaming.ipynb Olá-servidor de bloco de notas toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="e9253-171">Repita os passos 1 a 3 Olá de tooload __Spark-estruturados-transmissão em fluxo-do-Kafka.ipynb__ bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="e9253-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="e9253-172">Carregar tweets para Kafka</span><span class="sxs-lookup"><span data-stu-id="e9253-172">Load tweets into Kafka</span></span>

<span data-ttu-id="e9253-173">Depois de tem sido carregados ficheiros Olá, selecione Olá __fluxo-Tweets-To_Kafka.ipynb__ entrada tooopen Olá bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="e9253-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="e9253-174">Siga os passos de Olá no Olá bloco de notas tooload tweets em Kafka.</span><span class="sxs-lookup"><span data-stu-id="e9253-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="e9253-175">Tweets processo com o Spark estruturados de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="e9253-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="e9253-176">A partir da home page do bloco de notas do Jupyter Olá, selecione Olá __Spark-estruturados-transmissão em fluxo-do-Kafka.ipynb__ entrada.</span><span class="sxs-lookup"><span data-stu-id="e9253-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="e9253-177">Siga os passos de Olá Olá bloco de notas tooload tweets do Kafka utilizando Spark estruturados de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="e9253-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9253-178">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e9253-178">Next steps</span></span>

<span data-ttu-id="e9253-179">Agora que aprendeu como toouse Spark estruturados de transmissão em fluxo, consulte Olá toolearn documentos mais sobre como trabalhar com o Spark e Kafka os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e9253-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="e9253-180">[Como toouse Spark transmissão em fluxo (DStream) com Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="e9253-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="e9253-181">Começar a utilizar o bloco de notas do Jupyter e Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9253-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)