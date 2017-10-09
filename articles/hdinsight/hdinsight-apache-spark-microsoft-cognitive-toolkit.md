---
title: aaaMicrosoft Toolkit cognitivos com o Azure HDInsight Spark para aprender profunda | Microsoft Docs
description: "Saiba como um treinado Microsoft cognitivos Toolkit profunda modelo learning pode ser aplicados tooa conjunto de dados utilizando Olá Spark Python API num cluster Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Utilizar cognitivos Toolkit de modelo com o cluster Azure HDInsight Spark profunda

Neste artigo, Olá os seguintes passos.

1. Execute um script personalizado de tooinstall Toolkit de cognitivos num cluster do Azure HDInsight Spark.

2. Carregar um toosee de cluster do Spark toohello do Jupyter bloco de notas como tooapply um treinado cognitivos Toolkit de aprendizagem toofiles de modelo numa conta de armazenamento de Blobs do Azure utilizando Olá profunda [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Pré-requisitos

* **Uma subscrição do Azure**. Antes de começar este tutorial, tem de ter uma subscrição do Azure. Veja o artigo [Crie hoje a sua conta do Azure gratuita](https://azure.microsoft.com/free).

* **Cluster do HDInsight Spark do Azure**. Para este artigo, crie um cluster do Spark 2.0. Para obter instruções, consulte [cluster Criar Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Como fluxo esta solução?

Esta solução é dividida entre este artigo e um bloco de notas do Jupyter que carregar como parte deste tutorial. Neste artigo, conclua Olá os seguintes passos:

* Execute uma ação de script num cluster do HDInsight Spark tooinstall Toolkit de cognitivos e Python pacotes.
* Carregue o bloco de notas do Jupyter Olá que executa Olá solução toohello cluster do HDInsight Spark.

Olá restantes passos descritos no bloco de notas do Jupyter Olá.

- Carregar imagens de exemplo para um conjunto de dados do Spark Resiliant distribuída ou RDD
   - Carregar módulos e definir predefinições
   - Transferir o conjunto de dados de Olá localmente no cluster do Spark Olá
   - Converter o conjunto de dados de Olá num RDD
- Imagens de modelo de pontuação Olá através de um modelo treinado do Toolkit cognitivos
   - Transferir o cluster do Spark toohello Olá preparado Toolkit cognitivos modelo
   - Definir toobe funções utilizada por nós de trabalho
   - Imagens de modelo de pontuação Olá em nós de trabalho
   - Avaliar a precisão do modelo


## <a name="install-microsoft-cognitive-toolkit"></a>Instalar o Toolkit de cognitivos

Pode instalar o Toolkit de cognitivos num cluster do Spark através da ação de script. Ação de script utiliza os componentes de tooinstall scripts personalizados num cluster de Olá que não estão disponíveis por predefinição. Pode utilizar scripts personalizados do Olá de Olá Portal do Azure, utilizando o SDK .NET do HDInsight, ou com o Azure PowerShell. Também pode utilizar Olá script tooinstall Olá toolkit como parte da criação do cluster ou depois do cluster de Olá se encontra em execução. 

Neste artigo, utilizamos Olá portal tooinstall Olá toolkit, depois de Olá cluster ter sido criado. Para outro formas toorun Olá script personalizado, consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Utilizar Olá Portal do Azure

Para obter instruções sobre como toouse Olá Portal do Azure toorun script ação, consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Certifique-se de que fornecer Olá seguir entradas tooinstall Toolkit de cognitivos.

* Forneça um valor para o nome de ação de script de Olá.

* Para **Bash script URI**, introduza `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Certifique-se execute o script Olá apenas no Olá nós head e de trabalho e desmarque Olá todas as outras caixas de verificação.

* Clique em **Criar**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Carregar Olá Jupyter bloco de notas tooAzure cluster do HDInsight Spark

Olá toouse Toolkit cognitivos Microsoft com o cluster do Azure HDInsight Spark Olá, tem de carregar o bloco de notas do Jupyter Olá **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello cluster de Azure HDInsight Spark. Este bloco de notas está disponível no GitHub em [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Repositório do GitHub clone Olá [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Para obter instruções tooclone, consulte [um repositório de clonagem](https://help.github.com/articles/cloning-a-repository/).

2. A partir do Olá Portal do Azure, abra o painel do cluster de Spark Olá que já aprovisionada, clique em **Cluster Dashboard**e, em seguida, clique em **bloco de notas do Jupyter**.

    Também pode iniciar o bloco de notas do Jupyter Olá acedendo toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`. Substitua \<clustername > com o nome de Olá de cluster do HDInsight.

3. No bloco de notas do Jupyter Olá, clique em **carregar** no Olá canto superior direito e, em seguida, navegue até localização toohello onde clonou o repositório do GitHub Olá.

    ![Carregar tooAzure de bloco de notas do Jupyter cluster do HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure de bloco de notas do Jupyter carregar cluster do HDInsight Spark")

4. Clique em **carregar** novamente.

5. Depois do bloco de notas do Olá é carregado, clique no nome de Olá do bloco de notas do Olá e, em seguida, siga Olá as instruções no bloco de notas do Olá próprio no como tooload Olá conjunto de dados e executar tutorial Olá.

## <a name="see-also"></a>Consultar também
* [Descrição geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de registos de sites com o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análise de dados telemétricos do Application Insight com o Spark no HDInsight](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicações
* [Criar uma aplicação autónoma com o Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar tarefas remotamente num cluster do Spark com o Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Utilizar o plug-in ferramentas do HDInsight para o IntelliJ IDEA toocreate e submeter aplicações do Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizar o plug-in ferramentas do HDInsight para aplicações do Spark IntelliJ IDEA toodebug remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utilizar pacotes externos com blocos de notas do Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerir recursos
* [Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
