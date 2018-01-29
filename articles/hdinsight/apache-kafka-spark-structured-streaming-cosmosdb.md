---
title: "Apache Spark transmissão em fluxo estruturada do Kafka para Azure Cosmos DB - o Azure HDInsight | Microsoft Docs"
description: "Saiba como utilizar o Apache Spark estruturados de transmissão em fluxo para ler os dados do Apache Kafka e, em seguida, guarde-o para a base de dados do Azure Cosmos. Neste exemplo, transmitir dados através de um bloco de notas do Jupyter do Spark no HDInsight."
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
ms.date: 01/16/2018
ms.author: larryfr
ms.openlocfilehash: 55d0fb91c8a8b995a5b9369d762f5bd87cb086c9
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2018
---
# <a name="use-spark-structured-streaming-with-kafka-and-azure-cosmos-db"></a>Utilizar o Spark estruturado de transmissão em fluxo com DB Kafka e Cosmos do Azure

Saiba como utilizar o Spark estruturados de transmissão em fluxo para ler os dados do Apache Kafka no Azure HDInsight e, em seguida, guardar os dados numa base de dados do Azure Cosmos.

BD do Cosmos do Azure é uma base de dados globalmente distribuído, com vários modelo. Este exemplo utiliza um modelo de base de dados de API do SQL Server. Para obter mais informações, consulte o [bem-vindo ao Azure Cosmos DB](../cosmos-db/introduction.md) documento.

Spark estruturado de transmissão em fluxo é um motor de processamento de fluxo incorporado no Spark SQL. Permite-lhe express computações de transmissão em fluxo a mesma que a computação do batch em dados estáticos. Para obter mais informações sobre a transmissão em fluxo estruturada, consulte o [estruturados de transmissão em fluxo guia de programação [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) em Apache.org.

> [!IMPORTANT]
> Neste exemplo utilizado 2.1 do Spark no HDInsight 3.6. Transmissão em fluxo estruturada é considerado __alpha__ no Spark 2.1.
>
> Os passos neste documento, criar um grupo de recursos do Azure que contém tanto o Spark no HDInsight e um Kafka num cluster do HDInsight. Esses clusters são ambos localizado dentro de uma rede Virtual do Azure, que permite que o cluster do Spark comunicar diretamente com o Kafka do cluster.
>
> Quando tiver terminado com os passos neste documento, lembre-se eliminar os clusters para evitar encargos em excesso.

## <a name="create-the-clusters"></a>Criar os clusters

Apache Kafka no HDInsight fornece acesso para os mediadores Kafka através da internet pública. Tudo o que sua Kafka tem de ser na mesma rede virtual do Azure que os nós do Kafka cluster. Neste exemplo, clusters Kafka tanto Spark estão localizados numa rede virtual do Azure. O diagrama seguinte mostra como a comunicação flua entre os clusters:

![Diagrama de clusters do Spark e Kafka uma Azure virtual network](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> O serviço de Kafka está limitado a comunicação na rede virtual. Outros serviços em cluster, como SSH e Ambari, podem ser acedidos através da internet. Para obter mais informações sobre as portas públicas disponíveis com o HDInsight, consulte [portas e os URIs utilizados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Pode criar uma Azure virtual network, Kafka, e clusters do Spark manualmente, é mais fáceis de utilizar um modelo Azure Resource Manager. Utilize os seguintes passos para implementar uma Azure virtual network, Kafka e Spark clusters a sua subscrição do Azure.

1. Utilize o botão seguinte para iniciar sessão no Azure e abrir o modelo no portal do Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fhdinsight-spark-scala-kafka-cosmosdb%2Fmaster%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/> </a>

    O modelo Azure Resource Manager está localizado no repositório de GitHub para este projeto ([https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb)).

    Este modelo cria os seguintes recursos:

    * Um Kafka no cluster de HDInsight 3.6.

    * Spark no HDInsight 3.6 cluster.

    * Uma rede Virtual do Azure, que contém os clusters do HDInsight.

    * Uma base de dados da API do Azure Cosmos BD SQL.

    > [!IMPORTANT]
    > O bloco de notas de transmissão em fluxo estruturado utilizado neste exemplo requer o Spark no HDInsight 3.6. Se utilizar uma versão anterior do Spark no HDInsight, receber erros ao utilizar o bloco de notas.

2. Utilize as seguintes informações para preencher as entradas no **implementação personalizada** secção:
   
    ![Implementação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Grupo de recursos**: criar um grupo ou selecione um existente. Este grupo contém o cluster do HDInsight.

    * **Localização**: selecione uma localização geograficamente perto de si.

    * **Nome do Cluster de base**: este valor é utilizado como o nome de base para o Spark e Kafka clusters. Por exemplo, introduzir **hdi** cria um Spark cluster spark hdi__ com o nome e um cluster de Kafka denominado **kafka hdi**.

    * **Nome de utilizador de início de sessão do cluster**: O nome de utilizador de administrador para os clusters do Spark e Kafka.

    * **Palavra-passe de início de sessão do cluster**: A palavra-passe de utilizador do administrador para os clusters do Spark e Kafka.

    * **Nome de utilizador SSH**: O utilizador SSH para criar para os clusters do Spark e Kafka.

    * **Palavra-passe SSH**: A palavra-passe para o utilizador SSH para os clusters do Spark e Kafka.

3. Leia o **termos e condições**e, em seguida, selecione **concordo com os termos e condições indicadas acima**.

4. Por fim, verifique **afixar ao dashboard** e, em seguida, selecione **Compra**. Demora cerca de 20 minutos para criar os clusters.

Depois de criar os recursos, é apresentada uma página de resumo.

![Informações do grupo de recursos para a vnet e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Tenha em atenção que os nomes dos clusters de HDInsight são **spark BASENAME** e **kafka BASENAME**, onde BASENAME é o nome fornecido para o modelo. Utilize estes nomes em passos posteriores quando ligar para os clusters.

## <a name="get-the-kafka-brokers"></a>Obter o Kafka mediadores

O código neste exemplo liga-se em anfitriões do Kafka cluster Kafka mediador. Para localizar os endereços dos dois anfitriões de Mediador de Kafka, utilize o seguinte exemplo do PowerShell ou Bash:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
```

Quando lhe for pedido, introduza a palavra-passe para a conta de início de sessão (administrador) do cluster

> [!NOTE]
> Neste exemplo espera `$CLUSTERNAME` para conter o nome do Kafka cluster.
>
> Este exemplo utiliza o [jq](https://stedolan.github.io/jq/) utilitário para analisar os dados para fora do documento JSON.

O resultado é semelhante ao seguinte texto:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Guarde esta informação, como é utilizado nas secções seguintes deste documento.

## <a name="get-the-notebooks"></a>Obter os blocos de notas

O código de exemplo descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka-cosmosdb).

## <a name="upload-the-notebooks"></a>Carregar os blocos de notas

Utilize os seguintes passos para carregar os blocos de notas do projeto para o Spark no HDInsight cluster:

1. No seu browser, ligue para o bloco de notas do Jupyter no cluster do Spark. No seguinte URL, substitua `CLUSTERNAME` com o nome do seu __Spark__ cluster:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Quando lhe for pedido, introduza o início de sessão do cluster (admin) e a palavra-passe utilizada quando criou o cluster.

2. Do lado direito superior da página, utilize o __carregar__ botão para carregar o __fluxo-taxi-data-para-kafka.ipynb__ ficheiro para o cluster. Selecione __abra__ para iniciar o carregamento.

3. Localizar o __fluxo-taxi-data-para-kafka.ipynb__ entrada na lista de blocos de notas e selecione __carregar__ botão junto-lo.

4. Repita os passos 1 a 3 para carregar o __Stream-data-from-Kafka-to-Cosmos-DB.ipynb__ bloco de notas.

## <a name="load-taxi-data-into-kafka"></a>Dados de carregamento de taxi para Kafka

Depois dos ficheiros tiverem sido carregados, selecione o __fluxo-taxi-data-para-kafka.ipynb__ entrada para abrir o bloco de notas. Siga os passos para carregar dados para Kafka o bloco de notas.

## <a name="process-taxi-data-using-spark-structured-streaming"></a>Processo taxi dados com o Spark estruturados de transmissão em fluxo

A partir da home page do bloco de notas do Jupyter, selecione o __Stream-data-from-Kafka-to-Cosmos-DB.ipynb__ entrada. Siga os passos no bloco de notas para os dados de fluxo do Kafka e para a base de dados do Cosmos do Azure com o Spark estruturados de transmissão em fluxo.

## <a name="next-steps"></a>Passos Seguintes

Agora que aprendeu como utilizar o Spark estruturados de transmissão em fluxo, consulte os seguintes documentos para obter mais informações sobre como trabalhar com o Spark, Kafka e base de dados do Azure Cosmos:

* [Como utilizar o Spark transmissão em fluxo (DStream) com Kafka](hdinsight-apache-spark-with-kafka.md).
* [Começar a utilizar o bloco de notas do Jupyter e Spark no HDInsight](spark/apache-spark-jupyter-spark-sql.md)
* [Bem-vindo ao Azure Cosmos DB](../cosmos-db/introduction.md)
