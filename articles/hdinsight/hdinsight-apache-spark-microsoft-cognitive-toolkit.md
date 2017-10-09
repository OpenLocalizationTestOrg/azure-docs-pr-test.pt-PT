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
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="d2e03-103">Utilizar cognitivos Toolkit de modelo com o cluster Azure HDInsight Spark profunda</span><span class="sxs-lookup"><span data-stu-id="d2e03-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="d2e03-104">Neste artigo, Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="d2e03-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="d2e03-105">Execute um script personalizado de tooinstall Toolkit de cognitivos num cluster do Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d2e03-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="d2e03-106">Carregar um toosee de cluster do Spark toohello do Jupyter bloco de notas como tooapply um treinado cognitivos Toolkit de aprendizagem toofiles de modelo numa conta de armazenamento de Blobs do Azure utilizando Olá profunda [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="d2e03-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2e03-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d2e03-107">Prerequisites</span></span>

* <span data-ttu-id="d2e03-108">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d2e03-108">**An Azure subscription**.</span></span> <span data-ttu-id="d2e03-109">Antes de começar este tutorial, tem de ter uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e03-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="d2e03-110">Veja o artigo [Crie hoje a sua conta do Azure gratuita](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="d2e03-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="d2e03-111">**Cluster do HDInsight Spark do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d2e03-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="d2e03-112">Para este artigo, crie um cluster do Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="d2e03-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="d2e03-113">Para obter instruções, consulte [cluster Criar Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d2e03-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="d2e03-114">Como fluxo esta solução?</span><span class="sxs-lookup"><span data-stu-id="d2e03-114">How does this solution flow?</span></span>

<span data-ttu-id="d2e03-115">Esta solução é dividida entre este artigo e um bloco de notas do Jupyter que carregar como parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d2e03-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="d2e03-116">Neste artigo, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d2e03-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="d2e03-117">Execute uma ação de script num cluster do HDInsight Spark tooinstall Toolkit de cognitivos e Python pacotes.</span><span class="sxs-lookup"><span data-stu-id="d2e03-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="d2e03-118">Carregue o bloco de notas do Jupyter Olá que executa Olá solução toohello cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d2e03-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="d2e03-119">Olá restantes passos descritos no bloco de notas do Jupyter Olá.</span><span class="sxs-lookup"><span data-stu-id="d2e03-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="d2e03-120">Carregar imagens de exemplo para um conjunto de dados do Spark Resiliant distribuída ou RDD</span><span class="sxs-lookup"><span data-stu-id="d2e03-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="d2e03-121">Carregar módulos e definir predefinições</span><span class="sxs-lookup"><span data-stu-id="d2e03-121">Load modules and define presets</span></span>
   - <span data-ttu-id="d2e03-122">Transferir o conjunto de dados de Olá localmente no cluster do Spark Olá</span><span class="sxs-lookup"><span data-stu-id="d2e03-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="d2e03-123">Converter o conjunto de dados de Olá num RDD</span><span class="sxs-lookup"><span data-stu-id="d2e03-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="d2e03-124">Imagens de modelo de pontuação Olá através de um modelo treinado do Toolkit cognitivos</span><span class="sxs-lookup"><span data-stu-id="d2e03-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="d2e03-125">Transferir o cluster do Spark toohello Olá preparado Toolkit cognitivos modelo</span><span class="sxs-lookup"><span data-stu-id="d2e03-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="d2e03-126">Definir toobe funções utilizada por nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="d2e03-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="d2e03-127">Imagens de modelo de pontuação Olá em nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="d2e03-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="d2e03-128">Avaliar a precisão do modelo</span><span class="sxs-lookup"><span data-stu-id="d2e03-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="d2e03-129">Instalar o Toolkit de cognitivos</span><span class="sxs-lookup"><span data-stu-id="d2e03-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="d2e03-130">Pode instalar o Toolkit de cognitivos num cluster do Spark através da ação de script.</span><span class="sxs-lookup"><span data-stu-id="d2e03-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="d2e03-131">Ação de script utiliza os componentes de tooinstall scripts personalizados num cluster de Olá que não estão disponíveis por predefinição.</span><span class="sxs-lookup"><span data-stu-id="d2e03-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="d2e03-132">Pode utilizar scripts personalizados do Olá de Olá Portal do Azure, utilizando o SDK .NET do HDInsight, ou com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2e03-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="d2e03-133">Também pode utilizar Olá script tooinstall Olá toolkit como parte da criação do cluster ou depois do cluster de Olá se encontra em execução.</span><span class="sxs-lookup"><span data-stu-id="d2e03-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="d2e03-134">Neste artigo, utilizamos Olá portal tooinstall Olá toolkit, depois de Olá cluster ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="d2e03-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="d2e03-135">Para outro formas toorun Olá script personalizado, consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d2e03-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="d2e03-136">Utilizar Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2e03-136">Using hello Azure Portal</span></span>

<span data-ttu-id="d2e03-137">Para obter instruções sobre como toouse Olá Portal do Azure toorun script ação, consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="d2e03-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="d2e03-138">Certifique-se de que fornecer Olá seguir entradas tooinstall Toolkit de cognitivos.</span><span class="sxs-lookup"><span data-stu-id="d2e03-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="d2e03-139">Forneça um valor para o nome de ação de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d2e03-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="d2e03-140">Para **Bash script URI**, introduza `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="d2e03-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="d2e03-141">Certifique-se execute o script Olá apenas no Olá nós head e de trabalho e desmarque Olá todas as outras caixas de verificação.</span><span class="sxs-lookup"><span data-stu-id="d2e03-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="d2e03-142">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d2e03-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="d2e03-143">Carregar Olá Jupyter bloco de notas tooAzure cluster do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="d2e03-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="d2e03-144">Olá toouse Toolkit cognitivos Microsoft com o cluster do Azure HDInsight Spark Olá, tem de carregar o bloco de notas do Jupyter Olá **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello cluster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d2e03-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="d2e03-145">Este bloco de notas está disponível no GitHub em [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="d2e03-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="d2e03-146">Repositório do GitHub clone Olá [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="d2e03-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="d2e03-147">Para obter instruções tooclone, consulte [um repositório de clonagem](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="d2e03-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="d2e03-148">A partir do Olá Portal do Azure, abra o painel do cluster de Spark Olá que já aprovisionada, clique em **Cluster Dashboard**e, em seguida, clique em **bloco de notas do Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="d2e03-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="d2e03-149">Também pode iniciar o bloco de notas do Jupyter Olá acedendo toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="d2e03-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="d2e03-150">Substitua \<clustername > com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2e03-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="d2e03-151">No bloco de notas do Jupyter Olá, clique em **carregar** no Olá canto superior direito e, em seguida, navegue até localização toohello onde clonou o repositório do GitHub Olá.</span><span class="sxs-lookup"><span data-stu-id="d2e03-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="d2e03-152">![Carregar tooAzure de bloco de notas do Jupyter cluster do HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure de bloco de notas do Jupyter carregar cluster do HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="d2e03-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="d2e03-153">Clique em **carregar** novamente.</span><span class="sxs-lookup"><span data-stu-id="d2e03-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="d2e03-154">Depois do bloco de notas do Olá é carregado, clique no nome de Olá do bloco de notas do Olá e, em seguida, siga Olá as instruções no bloco de notas do Olá próprio no como tooload Olá conjunto de dados e executar tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="d2e03-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2e03-155">Consultar também</span><span class="sxs-lookup"><span data-stu-id="d2e03-155">See also</span></span>
* [<span data-ttu-id="d2e03-156">Descrição geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d2e03-157">Cenários</span><span class="sxs-lookup"><span data-stu-id="d2e03-157">Scenarios</span></span>
* [<span data-ttu-id="d2e03-158">Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI</span><span class="sxs-lookup"><span data-stu-id="d2e03-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d2e03-159">Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC</span><span class="sxs-lookup"><span data-stu-id="d2e03-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d2e03-160">Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares</span><span class="sxs-lookup"><span data-stu-id="d2e03-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d2e03-161">Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real</span><span class="sxs-lookup"><span data-stu-id="d2e03-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d2e03-162">Análise de registos de sites com o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="d2e03-163">Análise de dados telemétricos do Application Insight com o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d2e03-164">Criar e executar aplicações</span><span class="sxs-lookup"><span data-stu-id="d2e03-164">Create and run applications</span></span>
* [<span data-ttu-id="d2e03-165">Criar uma aplicação autónoma com o Scala</span><span class="sxs-lookup"><span data-stu-id="d2e03-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d2e03-166">Executar tarefas remotamente num cluster do Spark com o Livy</span><span class="sxs-lookup"><span data-stu-id="d2e03-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d2e03-167">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="d2e03-167">Tools and extensions</span></span>
* [<span data-ttu-id="d2e03-168">Utilizar o plug-in ferramentas do HDInsight para o IntelliJ IDEA toocreate e submeter aplicações do Spark Scala</span><span class="sxs-lookup"><span data-stu-id="d2e03-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d2e03-169">Utilizar o plug-in ferramentas do HDInsight para aplicações do Spark IntelliJ IDEA toodebug remotamente</span><span class="sxs-lookup"><span data-stu-id="d2e03-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d2e03-170">Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d2e03-171">Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d2e03-172">Utilizar pacotes externos com blocos de notas do Jupyter</span><span class="sxs-lookup"><span data-stu-id="d2e03-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="d2e03-173">Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="d2e03-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="d2e03-174">Gerir recursos</span><span class="sxs-lookup"><span data-stu-id="d2e03-174">Manage resources</span></span>
* [<span data-ttu-id="d2e03-175">Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d2e03-176">Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2e03-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
