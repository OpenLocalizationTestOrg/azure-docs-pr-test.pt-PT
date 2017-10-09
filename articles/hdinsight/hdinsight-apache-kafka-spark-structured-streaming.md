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
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Utilizar o Spark estruturados transmissão em fluxo com Kafka (pré-visualização) no HDInsight

Saiba como toouse dados Apache Kafka no Azure HDInsight Spark estruturados de transmissão em fluxo tooread.

Spark estruturado de transmissão em fluxo é um motor de processamento de fluxo incorporado no Spark SQL. Permite-lhe computações de transmissão em fluxo tooexpress Olá igual ao cálculo de batch nos dados estáticos. Para obter mais informações sobre a transmissão em fluxo estruturada, consulte Olá [estruturados de transmissão em fluxo guia de programação [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) em Apache.org.

> [!IMPORTANT]
> Neste exemplo utilizado 2.1 do Spark no HDInsight 3.6. Transmissão em fluxo estruturada é considerado __alpha__ no Spark 2.1.
>
> passos de Olá neste documento, criar um grupo de recursos do Azure que contém tanto o Spark no HDInsight e um Kafka num cluster do HDInsight. Esses clusters são ambos localizado dentro de uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Spark comunicam com Olá Kafka cluster.
>
> Quando tiver terminado com os passos de Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.

## <a name="create-hello-clusters"></a>Criar clusters Olá

Apache Kafka no HDInsight fornece acesso toohello Kafka mediadores Olá internet pública. Olá tudo o que Olá, talks tooKafka tem de estar na mesma rede virtual do Azure como nós de Olá num cluster de Kafka. Para este exemplo Olá Kafka e clusters do Spark estão localizados numa rede virtual do Azure. Olá diagrama seguinte mostra como flui de comunicação entre clusters de Olá:

![Diagrama de clusters do Spark e Kafka uma Azure virtual network](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Olá serviço Kafka é limitado toocommunication dentro da rede virtual Olá. Outros serviços em cluster Olá, tal como pode ser acedido através de SSH e Ambari, Olá internet. Para obter mais informações sobre portas pública Olá disponíveis com o HDInsight, consulte [portas e os URIs utilizados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Apesar de poder criar uma Azure virtual network, Kafka e Spark clusters manualmente, é mais fácil toouse um modelo Azure Resource Manager. Seguinte de Olá utilize os passos toodeploy uma Azure virtual network, Kafka, e clusters do Spark tooyour subscrição do Azure.

1. Utilize Olá seguinte botão toosign no tooAzure e o modelo de Olá aberta no Olá portal do Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Olá modelo Azure Resource Manager está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Este modelo cria Olá os seguintes recursos:

    * Um Kafka no cluster de HDInsight 3.5.
    * Spark no HDInsight 3.6 cluster.
    * Uma rede Virtual do Azure, que contém os clusters do HDInsight Olá.

    > [!IMPORTANT]
    > Olá estruturados transmissão em fluxo bloco de notas utilizado neste exemplo requer o Spark no HDInsight 3.6. Se utilizar uma versão anterior do Spark no HDInsight, receber erros ao utilizar o bloco de notas do Olá.

2. Olá utilize seguindo entradas de Olá toopopulate de informações do Olá **implementação personalizada** painel:
   
    ![Implementação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Grupo de recursos**: criar um grupo ou selecione um existente. Este grupo contém o cluster do HDInsight Olá.

    * **Localização**: selecione uma tooyou fechar geograficamente da localização.

    * **Nome do Cluster de base**: este valor é utilizado como nome de base de Olá para clusters do Spark e Kafka Olá. Por exemplo, introduzir **hdi** cria um Spark cluster spark hdi__ com o nome e um cluster de Kafka denominado **kafka hdi**.

    * **Nome de utilizador de início de sessão do cluster**: nome de utilizador de admin Olá para clusters do Spark e Kafka Olá.

    * **Palavra-passe de início de sessão do cluster**: palavra-passe utilizador de administrador de Olá para clusters do Spark e Kafka Olá.

    * **Nome de utilizador SSH**: Olá toocreate de utilizador do SSH para clusters do Spark e Kafka Olá.

    * **Palavra-passe SSH**: Olá palavra-passe do utilizador do SSH Olá para clusters do Spark e Kafka Olá.

3. Olá leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições indicadas acima**.

4. Por fim, verifique **Pin toodashboard** e, em seguida, selecione **Compra**. Demora cerca de 20 minutos toocreate clusters Olá.

Depois de tem sido criados recursos Olá, está redirecionado toohello painel do grupo de recursos.

![Painel do grupo de recursos para vnet Olá e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Tenha em atenção que os nomes de Olá dos clusters do HDInsight Olá são **spark BASENAME** e **kafka BASENAME**, onde BASENAME nome Olá fornecido toohello modelo. Ao ligar a toohello clusters é utilizar estes nomes em passos posteriores.

## <a name="get-hello-kafka-brokers"></a>Obter Olá Kafka mediadores

Olá código neste exemplo liga-se toohello Kafka mediador anfitriões Olá Kafka cluster. toofind Olá anfitriões de Mediador Kafka, utilize Olá seguinte o exemplo do PowerShell ou Bash:

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
> Neste exemplo espera `$PASSWORD` toocontain Olá palavra-passe início de sessão de cluster Olá e `$CLUSTERNAME` toocontain nome Olá Olá Kafka cluster.
>
> Este exemplo utiliza Olá [jq](https://stedolan.github.io/jq/) dados de tooparse utilitário fora do documento JSON de Olá.

Olá de saída é semelhante toohello seguinte texto:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Guarde esta informação, como é utilizado em Olá seguintes secções deste documento.

## <a name="get-hello-notebooks"></a>Obter os blocos de notas Olá

código de Olá, por exemplo Olá descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Carregar os blocos de notas Olá

Utilize Olá seguintes blocos de notas do passos tooupload Olá de Olá projeto tooyour Spark num cluster do HDInsight:

1. No seu browser, ligue toohello de notas do Jupyter no cluster do Spark. Substituir o URL, a seguir no Olá `CLUSTERNAME` com o nome de Olá do Kafka cluster:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Quando lhe for pedido, introduza o início de sessão do cluster de Olá (administrador) e palavra-passe utilizada quando criou o cluster de Olá.

2. A partir de Olá superior direita da página Olá, utilize Olá __carregar__ Olá do botão tooupload __fluxo-Tweets-To_Kafka.ipynb__ cluster toohello de ficheiros. Selecione __abra__ carregamento de Olá toostart.

    ![Utilize Olá carregamento botão tooselect e carregar um bloco de notas](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selecione o ficheiro de KafkaStreaming.ipynb Olá](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Determinar Olá __fluxo-Tweets-To_Kafka.ipynb__ entrada na lista de Olá de blocos de notas e selecione __carregar__ botão junto-lo.

    ![Carregamento de Olá Utilize botão junto tooupload de entrada de KafkaStreaming.ipynb Olá-servidor de bloco de notas toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Repita os passos 1 a 3 Olá de tooload __Spark-estruturados-transmissão em fluxo-do-Kafka.ipynb__ bloco de notas.

## <a name="load-tweets-into-kafka"></a>Carregar tweets para Kafka

Depois de tem sido carregados ficheiros Olá, selecione Olá __fluxo-Tweets-To_Kafka.ipynb__ entrada tooopen Olá bloco de notas. Siga os passos de Olá no Olá bloco de notas tooload tweets em Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Tweets processo com o Spark estruturados de transmissão em fluxo

A partir da home page do bloco de notas do Jupyter Olá, selecione Olá __Spark-estruturados-transmissão em fluxo-do-Kafka.ipynb__ entrada. Siga os passos de Olá Olá bloco de notas tooload tweets do Kafka utilizando Spark estruturados de transmissão em fluxo.

## <a name="next-steps"></a>Passos seguintes

Agora que aprendeu como toouse Spark estruturados de transmissão em fluxo, consulte Olá toolearn documentos mais sobre como trabalhar com o Spark e Kafka os seguintes:

* [Como toouse Spark transmissão em fluxo (DStream) com Kafka](hdinsight-apache-spark-with-kafka.md).
* [Começar a utilizar o bloco de notas do Jupyter e Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)