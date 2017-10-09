---
title: cluster aaaTroubleshoot problemas com o Apache Spark no Azure HDInsight | Microsoft Docs
description: Saiba mais sobre problemas relacionados tooApache clusters do Spark no Azure HDInsight e como toowork em torno dos.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="d727d-103">Problemas conhecidos para o cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="d727d-104">Este documento mantém um registo dos Olá todos os problemas conhecidos para Olá pré-visualização pública do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d727d-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="d727d-105">O Livy fugas de sessão interativa</span><span class="sxs-lookup"><span data-stu-id="d727d-105">Livy leaks interactive session</span></span>
<span data-ttu-id="d727d-106">Quando o Livy é reiniciado (do Ambari ou devido a reinício da máquina virtual de tooheadnode 0), com uma sessão interativa ainda ativo, uma sessão interativa de tarefa será transmitida.</span><span class="sxs-lookup"><span data-stu-id="d727d-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="d727d-107">Por este motivo, novas tarefas podem bloqueada no Olá aceites estado e não pode ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="d727d-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="d727d-108">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="d727d-108">**Mitigation:**</span></span>

<span data-ttu-id="d727d-109">Utilize Olá problema do procedimento tooworkaround Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d727d-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="d727d-110">SSH para headnode.</span><span class="sxs-lookup"><span data-stu-id="d727d-110">Ssh into headnode.</span></span> <span data-ttu-id="d727d-111">Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d727d-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d727d-112">Olá executar aplicações do comando toofind Olá os seguintes IDs de tarefas interativa Olá trabalhar com o Livy.</span><span class="sxs-lookup"><span data-stu-id="d727d-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="d727d-113">Olá nomes de tarefa de predefinição será o Livy se tarefas de Olá foram começar com uma sessão interativa de Livy sem nomes explícitos especificados para Olá Livy iniciado pelo bloco de notas do Jupyter, o nome da tarefa Olá será início de sessão com remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="d727d-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="d727d-114">Execute Olá os seguintes comandos tookill essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="d727d-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="d727d-115">Novas tarefas iniciará a executar.</span><span class="sxs-lookup"><span data-stu-id="d727d-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="d727d-116">Servidor de histórico de Spark não foi iniciado</span><span class="sxs-lookup"><span data-stu-id="d727d-116">Spark History Server not started</span></span>
<span data-ttu-id="d727d-117">Servidor do histórico de Spark não está iniciado automaticamente depois de um cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="d727d-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="d727d-118">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="d727d-118">**Mitigation:**</span></span> 

<span data-ttu-id="d727d-119">Inicie manualmente o servidor de histórico de Olá do Ambari.</span><span class="sxs-lookup"><span data-stu-id="d727d-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="d727d-120">Problema de permissão no diretório de registo do Spark</span><span class="sxs-lookup"><span data-stu-id="d727d-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="d727d-121">Quando hdiuser submete uma tarefa com spark-submit, há um java.io.FileNotFoundException de erro: /var/log/spark/sparkdriver_hdiuser.log (permissão negada) e Olá registo de controlador não é escrito.</span><span class="sxs-lookup"><span data-stu-id="d727d-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="d727d-122">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="d727d-122">**Mitigation:**</span></span>

1. <span data-ttu-id="d727d-123">Adicione um grupo do hdiuser toohello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d727d-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="d727d-124">Forneça 777 permissões no /var/log/spark após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="d727d-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="d727d-125">Atualize a localização do registo Olá spark utilizando Ambari toobe um diretório com 777 permissões.</span><span class="sxs-lookup"><span data-stu-id="d727d-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="d727d-126">O spark de execução-submeter como sudo.</span><span class="sxs-lookup"><span data-stu-id="d727d-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="d727d-127">O Spark Phoenix conector não é suportado</span><span class="sxs-lookup"><span data-stu-id="d727d-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="d727d-128">Atualmente, o conector do Spark Phoenix Olá não é suportada com um cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d727d-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="d727d-129">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="d727d-129">**Mitigation:**</span></span>

<span data-ttu-id="d727d-130">Conector do Spark HBase Olá tem de utilizar em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d727d-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="d727d-131">Para obter instruções, consulte [como conector toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="d727d-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="d727d-132">Problemas relacionados com tooJupyter blocos de notas</span><span class="sxs-lookup"><span data-stu-id="d727d-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="d727d-133">Seguem-se algumas notas de tooJupyter relacionados problemas conhecidos.</span><span class="sxs-lookup"><span data-stu-id="d727d-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="d727d-134">Blocos de notas com carateres não ASCII em nomes de ficheiros</span><span class="sxs-lookup"><span data-stu-id="d727d-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="d727d-135">Blocos de notas Jupyter que podem ser utilizados em clusters do Spark HDInsight não devem ter carateres não ASCII em nomes de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="d727d-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="d727d-136">Se tentar tooupload um ficheiro através de Olá IU Jupyter que tem um nome de ficheiro não ASCII, ocorrerá uma falha silenciosamente (ou seja, não permite Jupyter carregar ficheiro Olá, mas não irá gerar um erro de visível ou).</span><span class="sxs-lookup"><span data-stu-id="d727d-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="d727d-137">Erro ao carregar os blocos de notas de tamanhos superiores</span><span class="sxs-lookup"><span data-stu-id="d727d-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="d727d-138">Poderá ver um erro  **`Error loading notebook`**  quando carrega blocos de notas que são maiores de tamanho.</span><span class="sxs-lookup"><span data-stu-id="d727d-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="d727d-139">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="d727d-139">**Mitigation:**</span></span>

<span data-ttu-id="d727d-140">Se obtiver este erro, não significa que os dados estão danificados ou perdidos.</span><span class="sxs-lookup"><span data-stu-id="d727d-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="d727d-141">Os blocos de notas são ainda num disco em `/var/lib/jupyter`, e pode SSH para Olá cluster tooaccess-los.</span><span class="sxs-lookup"><span data-stu-id="d727d-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="d727d-142">Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d727d-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="d727d-143">Assim que tiver estabelecido ligação toohello cluster com o SSH, pode copiar os blocos de notas do seu computador local de cluster tooyour (através de SCP ou WinSCP) como a perda de Olá tooprevent cópia de segurança de quaisquer dados importantes no bloco de notas do Olá.</span><span class="sxs-lookup"><span data-stu-id="d727d-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="d727d-144">Pode, em seguida, túnel SSH no seu headnode na porta 8001 tooaccess Jupyter sem passar gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="d727d-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="d727d-145">A partir daí, pode limpar resultado Olá o bloco de notas e guarde-o novamente tamanho do toominimize Olá bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="d727d-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="d727d-146">tooprevent este erro aconteça no Olá futura, tem de seguir algumas melhores práticas:</span><span class="sxs-lookup"><span data-stu-id="d727d-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="d727d-147">É importante tookeep Olá bloco de notas o tamanho pequeno.</span><span class="sxs-lookup"><span data-stu-id="d727d-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="d727d-148">Qualquer saída das tarefas do Spark que é enviada novamente tooJupyter é continuada no bloco de notas do Olá.</span><span class="sxs-lookup"><span data-stu-id="d727d-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="d727d-149">É melhor prática, com o Jupyter no geral tooavoid executar `.collect()` em grande RDD ou dataframes; em vez disso, se quiser toopeek no conteúdo de um RDD, considere executar `.take()` ou `.sample()` para que o resultado não demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="d727d-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="d727d-150">Além disso, quando guardar um bloco de notas, desmarque todos os de saída do tamanho de Olá tooreduce de células.</span><span class="sxs-lookup"><span data-stu-id="d727d-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="d727d-151">Arranque inicial do bloco de notas demora mais tempo do que o previsto</span><span class="sxs-lookup"><span data-stu-id="d727d-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="d727d-152">Primeira instrução de código no bloco de notas do Jupyter utilizando a magia do Spark pode demorar mais do que um minuto.</span><span class="sxs-lookup"><span data-stu-id="d727d-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="d727d-153">**Explicação:**</span><span class="sxs-lookup"><span data-stu-id="d727d-153">**Explanation:**</span></span>

<span data-ttu-id="d727d-154">Isto acontece porque quando a primeira célula do código Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="d727d-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="d727d-155">Em segundo plano de Olá este inicia a configuração de sessão e Spark, SQL e contextos de ramo de registo estão definidos.</span><span class="sxs-lookup"><span data-stu-id="d727d-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="d727d-156">Depois destas contextos estiver definidos, é executada a primeira instrução de Olá e isto dá-impressão Olá que instrução Olá demorou um toocomplete muito tempo.</span><span class="sxs-lookup"><span data-stu-id="d727d-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="d727d-157">Tempo limite de bloco de notas do Jupyter em criar sessão Olá</span><span class="sxs-lookup"><span data-stu-id="d727d-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="d727d-158">Quando o cluster do Spark tem recursos insuficientes, Olá Spark e Pyspark kernels no bloco de notas do Jupyter Olá serão tempo limite excedido da sessão de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="d727d-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="d727d-159">**Mitigações:**</span><span class="sxs-lookup"><span data-stu-id="d727d-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="d727d-160">Liberte alguns recursos do cluster do Spark por:</span><span class="sxs-lookup"><span data-stu-id="d727d-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="d727d-161">A parar os outros blocos de notas do Spark por toohello vai fechar e Halt menu ou clicar encerramento no Explorador do bloco de notas Olá.</span><span class="sxs-lookup"><span data-stu-id="d727d-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="d727d-162">A parar a outras aplicações do Spark do YARN.</span><span class="sxs-lookup"><span data-stu-id="d727d-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="d727d-163">Reinicie o bloco de notas Olá que tentavam toostart cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="d727d-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="d727d-164">Recursos suficientes devem estar disponíveis para toocreate agora uma sessão.</span><span class="sxs-lookup"><span data-stu-id="d727d-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="d727d-165">Consultar também</span><span class="sxs-lookup"><span data-stu-id="d727d-165">See also</span></span>
* [<span data-ttu-id="d727d-166">Descrição geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d727d-167">Cenários</span><span class="sxs-lookup"><span data-stu-id="d727d-167">Scenarios</span></span>
* [<span data-ttu-id="d727d-168">Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI</span><span class="sxs-lookup"><span data-stu-id="d727d-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="d727d-169">Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC</span><span class="sxs-lookup"><span data-stu-id="d727d-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d727d-170">Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares</span><span class="sxs-lookup"><span data-stu-id="d727d-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="d727d-171">Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real</span><span class="sxs-lookup"><span data-stu-id="d727d-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="d727d-172">Análise de registos de sites com o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="d727d-173">Criar e executar aplicações</span><span class="sxs-lookup"><span data-stu-id="d727d-173">Create and run applications</span></span>
* [<span data-ttu-id="d727d-174">Criar uma aplicação autónoma com o Scala</span><span class="sxs-lookup"><span data-stu-id="d727d-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="d727d-175">Executar tarefas remotamente num cluster do Spark com o Livy</span><span class="sxs-lookup"><span data-stu-id="d727d-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="d727d-176">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="d727d-176">Tools and extensions</span></span>
* [<span data-ttu-id="d727d-177">Utilizar o plug-in ferramentas do HDInsight para o IntelliJ IDEA toocreate e submeter aplicações do Spark scala</span><span class="sxs-lookup"><span data-stu-id="d727d-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="d727d-178">Utilizar o plug-in ferramentas do HDInsight para aplicações do Spark IntelliJ IDEA toodebug remotamente</span><span class="sxs-lookup"><span data-stu-id="d727d-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="d727d-179">Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="d727d-180">Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="d727d-181">Utilizar pacotes externos com blocos de notas do Jupyter</span><span class="sxs-lookup"><span data-stu-id="d727d-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="d727d-182">Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="d727d-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="d727d-183">Gerir recursos</span><span class="sxs-lookup"><span data-stu-id="d727d-183">Manage resources</span></span>
* [<span data-ttu-id="d727d-184">Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="d727d-185">Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="d727d-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

