---
title: aaaInstall e utilize Giraph no HDInsight (Hadoop) - Azure | Microsoft Docs
description: "Saiba como tooinstall Giraph no HDInsight baseado em Linux clusters utilizando ações de Script. Ações de script permitem-lhe cluster de Olá toocustomize durante a criação, alteração da configuração de cluster ou instalar os serviços e utilitários."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="bad40-104">Instalar Giraph em clusters do HDInsight Hadoop e utilizar Giraph tooprocess em grande escala gráficos</span><span class="sxs-lookup"><span data-stu-id="bad40-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="bad40-105">Saiba como tooinstall Apache Giraph num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bad40-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="bad40-106">funcionalidade de ação de script de Olá do HDInsight permite-lhe toocustomize cluster executando um script de bash.</span><span class="sxs-lookup"><span data-stu-id="bad40-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="bad40-107">Scripts podem ser utilizados toocustomize clusters durante e após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="bad40-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bad40-108">passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Linux.</span><span class="sxs-lookup"><span data-stu-id="bad40-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="bad40-109">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="bad40-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bad40-110">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="bad40-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="bad40-111"><a name="whatis"></a>O que é Giraph</span><span class="sxs-lookup"><span data-stu-id="bad40-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="bad40-112">[Apache Giraph](http://giraph.apache.org/) permite-lhe o gráfico de tooperform processamento ao utilizar o Hadoop e pode ser utilizado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bad40-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="bad40-113">Relações entre objetos de modelo de gráficos.</span><span class="sxs-lookup"><span data-stu-id="bad40-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="bad40-114">Por exemplo, Olá ligações entre routers numa rede grande como Olá Internet ou relações entre as pessoas em redes sociais.</span><span class="sxs-lookup"><span data-stu-id="bad40-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="bad40-115">Processamento de gráfico permite-lhe tooreason sobre Olá as relações entre objetos de um gráfico, tais como:</span><span class="sxs-lookup"><span data-stu-id="bad40-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="bad40-116">Identificar potenciais amigos com base na sua relações atuais.</span><span class="sxs-lookup"><span data-stu-id="bad40-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="bad40-117">Identificação Olá mais curta rota entre dois computadores numa rede.</span><span class="sxs-lookup"><span data-stu-id="bad40-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="bad40-118">Calcular a posição da página Olá das páginas Web.</span><span class="sxs-lookup"><span data-stu-id="bad40-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="bad40-119">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados - Support Microsoft ajuda-o tooisolate e resolver problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="bad40-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="bad40-120">Componentes personalizados, tais como Giraph, recebem suporte comercialmente razoáveis toohelp toofurther poderá resolver o problema de Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="bad40-121">Microsoft Support poderá tooresolving capaz de problema de Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="bad40-122">Caso contrário, tem de consultar Comunidades de open source para onde se encontra profundo conhecimentos para que a tecnologia.</span><span class="sxs-lookup"><span data-stu-id="bad40-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="bad40-123">Por exemplo, existem vários sites de Comunidade que podem ser utilizadas, como: [fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Também projetos do Apache tem sites de projeto no [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="bad40-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="bad40-124">O script de Olá faz</span><span class="sxs-lookup"><span data-stu-id="bad40-124">What hello script does</span></span>

<span data-ttu-id="bad40-125">Este script executa Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="bad40-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="bad40-126">Instala Giraph demasiado`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="bad40-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="bad40-127">Olá cópias `giraph-examples.jar` armazenamento de ficheiros toodefault (WASB) para o cluster:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="bad40-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="bad40-128"><a name="install"></a>Instalar Giraph utilizando ações de Script</span><span class="sxs-lookup"><span data-stu-id="bad40-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="bad40-129">Um tooinstall de script de exemplo Giraph num cluster do HDInsight está disponível em Olá seguinte localização:</span><span class="sxs-lookup"><span data-stu-id="bad40-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="bad40-130">Esta secção fornece instruções sobre como toouse Olá script de exemplo ao criar o cluster de Olá utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bad40-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="bad40-131">Uma ação de script pode ser aplicada utilizando qualquer um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="bad40-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="bad40-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bad40-132">Azure PowerShell</span></span>
> * <span data-ttu-id="bad40-133">Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bad40-133">hello Azure CLI</span></span>
> * <span data-ttu-id="bad40-134">Olá SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="bad40-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="bad40-135">Modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bad40-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="bad40-136">Também pode aplicar tooalready de ações de script clusters em execução.</span><span class="sxs-lookup"><span data-stu-id="bad40-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="bad40-137">Para obter mais informações, consulte [HDInsight personalizar clusters com ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bad40-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="bad40-138">Iniciar criação de um cluster, utilizando os passos de Olá no [clusters do HDInsight baseado em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md), mas não concluir a criação.</span><span class="sxs-lookup"><span data-stu-id="bad40-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="bad40-139">No Olá **configuração opcional** painel, selecione **ações de Script**e forneça Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="bad40-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="bad40-140">**NOME**: introduza um nome amigável para a ação de script de Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="bad40-141">**URI de SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="bad40-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="bad40-142">**HEAD**: esta entrada de verificação</span><span class="sxs-lookup"><span data-stu-id="bad40-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="bad40-143">**TRABALHO**: deixe esta entrada desmarcada</span><span class="sxs-lookup"><span data-stu-id="bad40-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="bad40-144">**ZOOKEEPER**: deixe esta entrada desmarcada</span><span class="sxs-lookup"><span data-stu-id="bad40-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="bad40-145">**Os parâmetros**: deixe este campo em branco</span><span class="sxs-lookup"><span data-stu-id="bad40-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="bad40-146">Na parte inferior de Olá de Olá **ações de Script**, utilize Olá **selecione** configuração de Olá toosave do botão.</span><span class="sxs-lookup"><span data-stu-id="bad40-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="bad40-147">Por último, utilize Olá **selecione** botão na parte inferior de Olá de Olá **configuração opcional** painel toosave Olá opcional as informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="bad40-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="bad40-148">Continuar a criar cluster Olá, conforme descrito em [clusters do HDInsight baseado em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bad40-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="bad40-149"><a name="usegiraph"></a>Como utilizar o Giraph no HDInsight?</span><span class="sxs-lookup"><span data-stu-id="bad40-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="bad40-150">Quando o cluster de Olá tiver sido criado, utilize Olá seguinte passos toorun Olá SimpleShortestPathsComputation exemplo incluído com Giraph.</span><span class="sxs-lookup"><span data-stu-id="bad40-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="bad40-151">Este exemplo utiliza básico Olá [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementação para localizar o caminho mais curto do Olá entre objetos de um gráfico.</span><span class="sxs-lookup"><span data-stu-id="bad40-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="bad40-152">Ligar o cluster do HDInsight toohello utilizando SSH:</span><span class="sxs-lookup"><span data-stu-id="bad40-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="bad40-153">Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bad40-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bad40-154">Seguinte de Olá utilize comando toocreate um ficheiro denominado **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="bad40-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="bad40-155">Utilize Olá seguir texto como conteúdo Olá deste ficheiro:</span><span class="sxs-lookup"><span data-stu-id="bad40-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="bad40-156">Estes dados descreve uma relação entre objetos de um gráfico direcionado, utilizando o formato de Olá `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="bad40-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="bad40-157">Cada linha representa uma relação entre um `source_id` objeto e um ou mais `dest_id` objetos.</span><span class="sxs-lookup"><span data-stu-id="bad40-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="bad40-158">Olá `edge_value` pode considerar como força Olá ou distance Olá da ligação de entre `source_id` e `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="bad40-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="bad40-159">Desenhado horizontalmente, e utilizar o valor de Olá (ou ponderação) como distância Olá entre objetos, dados de Olá aspeto que poderão ter Olá diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="bad40-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt desenhado como circles com linhas de variando distância entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="bad40-161">ficheiro de Olá toosave, utilize **Ctrl + X**, em seguida, **Y**e, finalmente, **Enter** nome de ficheiro de Olá tooaccept.</span><span class="sxs-lookup"><span data-stu-id="bad40-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="bad40-162">Utilize Olá os seguintes dados de Olá toostore para o armazenamento primário para o cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="bad40-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="bad40-163">Execute Olá SimpleShortestPathsComputation exemplo, utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="bad40-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="bad40-164">os parâmetros de Olá utilizados com este comando descritos Olá a tabela seguinte:</span><span class="sxs-lookup"><span data-stu-id="bad40-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="bad40-165">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="bad40-165">Parameter</span></span> | <span data-ttu-id="bad40-166">O que faz</span><span class="sxs-lookup"><span data-stu-id="bad40-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="bad40-167">ficheiro jar Olá que contém exemplos de Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="bad40-168">classe de Olá utilizada exemplos de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="bad40-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="bad40-169">exemplo de Olá que é utilizado.</span><span class="sxs-lookup"><span data-stu-id="bad40-169">hello example that is used.</span></span> <span data-ttu-id="bad40-170">Neste exemplo, calcula caminho mais curto do Olá entre 1 de ID e todos os outros IDs no gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="bad40-171">Olá headnode para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="bad40-172">Olá toouse de formato de entrada para dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="bad40-173">ficheiro de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="bad40-174">formato de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-174">hello output format.</span></span> <span data-ttu-id="bad40-175">Neste exemplo, a ID e o valor como texto simples.</span><span class="sxs-lookup"><span data-stu-id="bad40-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="bad40-176">localização de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="bad40-177">Olá número workers toouse.</span><span class="sxs-lookup"><span data-stu-id="bad40-177">hello number of workers toouse.</span></span> <span data-ttu-id="bad40-178">Neste exemplo, 2.</span><span class="sxs-lookup"><span data-stu-id="bad40-178">In this example, 2.</span></span> |

    <span data-ttu-id="bad40-179">Para obter mais informações sobre estes e outros parâmetros utilizados Giraph exemplos, consulte Olá [início rápido de Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="bad40-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="bad40-180">Depois de concluir a tarefa de Olá, Olá estão armazenados no Olá **/example/out/shotestpaths** diretório.</span><span class="sxs-lookup"><span data-stu-id="bad40-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="bad40-181">Olá nomes de ficheiro de saída de começar por **parte-m -** e terminar com um número a indicar Olá em primeiro lugar, segundo, ficheiro etc..</span><span class="sxs-lookup"><span data-stu-id="bad40-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="bad40-182">Utilize Olá resultado do comando tooview Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bad40-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="bad40-183">saída de Olá deve aparecer toohello semelhante seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="bad40-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="bad40-184">exemplo de SimpleShortestPathComputation Olá está hard-coded toostart com 1 de ID de objeto e localizar Olá objetos de tooother de caminho mais curto.</span><span class="sxs-lookup"><span data-stu-id="bad40-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="bad40-185">saída de Olá está num formato de Olá de `destination_id` e `distance`.</span><span class="sxs-lookup"><span data-stu-id="bad40-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="bad40-186">Olá `distance` é Olá valor (ou ponderação) das margens Olá percorrer entre 1 de ID de objeto e ID de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="bad40-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="bad40-187">Visualizar estes dados, pode verificar os resultados de Olá, viaja caminhos mais curto Olá entre 1 de ID e todos os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="bad40-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="bad40-188">caminho mais curto do Olá entre ID 1 e ID 4 é 5.</span><span class="sxs-lookup"><span data-stu-id="bad40-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="bad40-189">Este valor é distância total do Olá entre <span style="color:orange">ID 1 e 3</span>e, em seguida, <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="bad40-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Desenho de objetos como circles com mais curto caminhos desenhados entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="bad40-191">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bad40-191">Next steps</span></span>

* <span data-ttu-id="bad40-192">[Instalar e utilizar Hue nos clusters do HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bad40-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="bad40-193">[Instalar Solr nos clusters do HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bad40-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
