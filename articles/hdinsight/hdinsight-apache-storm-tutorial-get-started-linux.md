---
title: Exemplos de aaaStorm-starter no Apache Storm no HDInsight - Azure | Microsoft Docs
description: "Saiba como análise de macrodados toodo e processamento de dados em tempo real com Apache Storm e Olá exemplos de storm-starter no HDInsight."
keywords: storm-starter, exemplo do apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="9970f-104">Introdução ao Apache Storm no HDInsight com exemplos de storm-starter Olá</span><span class="sxs-lookup"><span data-stu-id="9970f-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="9970f-105">Saiba como toouse Apache Storm no HDInsight com Olá exemplos de storm-starter.</span><span class="sxs-lookup"><span data-stu-id="9970f-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="9970f-106">O Apache Storm é um sistema de cálculo dimensionável, tolerante a falhas, distribuído e em tempo real para o processamento de fluxos de dados.</span><span class="sxs-lookup"><span data-stu-id="9970f-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="9970f-107">Com o Storm no Azure HDInsight, pode criar um cluster do Storm baseado na nuvem que executa a análise de macrodados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="9970f-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9970f-108">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9970f-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9970f-109">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="9970f-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9970f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9970f-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="9970f-111">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9970f-111">**An Azure subscription**.</span></span> <span data-ttu-id="9970f-112">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9970f-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="9970f-113">**Estar familiarizado com o SSH e o SCP**.</span><span class="sxs-lookup"><span data-stu-id="9970f-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="9970f-114">Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9970f-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="9970f-115">Criar um cluster do Storm</span><span class="sxs-lookup"><span data-stu-id="9970f-115">Create a Storm cluster</span></span>

<span data-ttu-id="9970f-116">Utilize Olá os seguintes passos toocreate um Storm num cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9970f-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="9970f-117">De Olá [portal do Azure](https://portal.azure.com), selecione **+ novo**, **Intelligence + análise**e, em seguida, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9970f-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Criar um cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="9970f-119">De Olá **Noções básicas** painel, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="9970f-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="9970f-120">**Nome do cluster**: nome de Olá do cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="9970f-121">**Subscrição**: selecione Olá toouse de subscrição.</span><span class="sxs-lookup"><span data-stu-id="9970f-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="9970f-122">**Nome de utilizador de início de sessão do cluster** e **palavra-passe de início de sessão do Cluster**: início de sessão de Olá ao aceder ao cluster Olá através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9970f-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="9970f-123">Utiliza estas credenciais tooaccess os serviços, tais como Olá IU da Web do Ambari ou a REST API.</span><span class="sxs-lookup"><span data-stu-id="9970f-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="9970f-124">**Secure Shell (SSH) username**: início de sessão de Olá utilizado ao aceder ao cluster Olá através de SSH.</span><span class="sxs-lookup"><span data-stu-id="9970f-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="9970f-125">Por predefinição, palavra-passe de Olá é Olá igual a palavra-passe de início de sessão do Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="9970f-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="9970f-126">**Grupo de recursos**: Olá recursos grupo toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="9970f-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="9970f-127">**Localização**: Olá região do Azure toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="9970f-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Selecionar subscrição](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="9970f-129">Selecione **tipo de Cluster**, e, em seguida, o conjunto Olá seguindo os valores do Olá **configuração de Cluster** painel:</span><span class="sxs-lookup"><span data-stu-id="9970f-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="9970f-130">**Tipo de Cluster**: Storm</span><span class="sxs-lookup"><span data-stu-id="9970f-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="9970f-131">**Sistema operativo**: Linux</span><span class="sxs-lookup"><span data-stu-id="9970f-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="9970f-132">**Versão**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="9970f-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="9970f-133">**Escalão do Cluster**: Standard</span><span class="sxs-lookup"><span data-stu-id="9970f-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="9970f-134">Por último, utilize Olá **selecione** botão toosave definições.</span><span class="sxs-lookup"><span data-stu-id="9970f-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Selecionar tipo de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="9970f-136">Depois de selecionar o tipo de cluster Olá, utilize Olá __selecione__ botão de tipo de cluster de Olá tooset.</span><span class="sxs-lookup"><span data-stu-id="9970f-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="9970f-137">Em seguida, utilize Olá __seguinte__ configuração básica do botão toofinish.</span><span class="sxs-lookup"><span data-stu-id="9970f-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="9970f-138">De Olá **armazenamento** painel, selecione ou crie uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9970f-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="9970f-139">Para obter os passos de Olá neste documento, deixe Olá outros campos neste painel, os valores predefinidos de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="9970f-140">Olá utilize __seguinte__ configuração de armazenamento de toosave do botão.</span><span class="sxs-lookup"><span data-stu-id="9970f-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Configurar as definições de conta de armazenamento Olá para o HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="9970f-142">De Olá **resumo** painel, reveja Olá configuração para o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="9970f-143">Olá utilize __editar__ liga toochange quaisquer definições que estão incorretas.</span><span class="sxs-lookup"><span data-stu-id="9970f-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="9970f-144">Por fim, utilize o cluster do the__Create__ botão toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Resumo da configuração do cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="9970f-146">Pode demorar até o cluster de Olá too20 minutos toocreate.</span><span class="sxs-lookup"><span data-stu-id="9970f-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="9970f-147">Executar um exemplo do storm-starter no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9970f-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="9970f-148">Ligar o cluster do HDInsight toohello utilizando SSH:</span><span class="sxs-lookup"><span data-stu-id="9970f-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="9970f-149">Se utilizou uma palavra-passe toosecure a conta de utilizador do SSH, é pedido tooentê-lo.</span><span class="sxs-lookup"><span data-stu-id="9970f-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="9970f-150">Se tiver utilizado uma chave pública, poderá precisar de utilizar Olá `-i` parâmetro toospecify Olá chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="9970f-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="9970f-151">Por exemplo, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9970f-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="9970f-152">Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9970f-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9970f-153">Utilize o seguinte comando toostart uma topologia de exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="9970f-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="9970f-154">Em versões anteriores do HDInsight, o nome de classe de Olá da topologia de Olá é `storm.starter.WordCountTopology` em vez de `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="9970f-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="9970f-155">Este comando inicia a topologia do WordCount de exemplo de Olá no cluster de Olá, com um nome amigável "WordCount".</span><span class="sxs-lookup"><span data-stu-id="9970f-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="9970f-156">Gerar aleatoriamente frases e a ocorrência de Olá de contagem de cada palavra nas frases Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9970f-157">Ao submeter o seu próprio cluster do toohello topologias, terá primeiro de copiar ficheiros de jar Olá que contém o cluster de Olá antes de utilizar Olá `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="9970f-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="9970f-158">Olá utilize `scp` o ficheiro de Olá toocopy de comandos.</span><span class="sxs-lookup"><span data-stu-id="9970f-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="9970f-159">Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="9970f-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="9970f-160">Olá exemplo de WordCount e outros exemplos de storm-starter já estão incluídos no seu cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="9970f-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="9970f-161">Se estiver interessado em Ver origem Olá para obter exemplos de storm-starter Olá, pode encontrar o código de Olá no [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="9970f-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="9970f-162">Esta ligação é para o Storm 1.1.x, que é fornecido com o HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="9970f-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="9970f-163">Para outras versões do Storm, utilize Olá __ramo__ botão, Olá parte superior do Olá página tooselect uma versão diferente do Storm.</span><span class="sxs-lookup"><span data-stu-id="9970f-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="9970f-164">Topologia de Olá do monitor</span><span class="sxs-lookup"><span data-stu-id="9970f-164">Monitor hello topology</span></span>

<span data-ttu-id="9970f-165">Olá IU do Storm fornece uma interface web para trabalhar com topologias em execução e está incluído no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9970f-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="9970f-166">Utilize Olá topologia de Olá passos toomonitor Olá IU do Storm a utilizar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9970f-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="9970f-167">Olá toodisplay IU do Storm, abra um web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="9970f-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="9970f-168">Substitua **CLUSTERNAME** com o nome de Olá do cluster.</span><span class="sxs-lookup"><span data-stu-id="9970f-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9970f-169">Se lhe for perguntado tooprovide um nome de utilizador e palavra-passe, introduza o administrador de clusters de Olá (administrador) e a palavra-passe que utilizou quando criar cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="9970f-170">Em **resumo da topologia**, selecione Olá **wordcount** entrada no Olá **nome** coluna.</span><span class="sxs-lookup"><span data-stu-id="9970f-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="9970f-171">Informações sobre a topologia de Olá são apresentadas.</span><span class="sxs-lookup"><span data-stu-id="9970f-171">Information about hello topology is displayed.</span></span>

    ![Dashboard do Storm com informações de topologia do WordCount do storm-starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="9970f-173">Esta página fornece Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="9970f-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="9970f-174">**Estatísticas de topologia** -informações básicas sobre desempenho Olá da topologia, organizadas em intervalos de tempo.</span><span class="sxs-lookup"><span data-stu-id="9970f-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="9970f-175">Selecionar um intervalo de tempo de Olá de alterações de janela do tempo específico das informações apresentadas noutras secções da página Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="9970f-176">**Spouts** -informações básicas sobre spouts, incluindo Olá último erro devolvido por cada spout.</span><span class="sxs-lookup"><span data-stu-id="9970f-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="9970f-177">**Bolts** – informações básicas sobre bolts.</span><span class="sxs-lookup"><span data-stu-id="9970f-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="9970f-178">**Configuração da topologia** -informações detalhadas sobre a configuração da topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="9970f-179">Esta página também fornece ações que podem ser executadas na topologia de Olá:</span><span class="sxs-lookup"><span data-stu-id="9970f-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="9970f-180">**Ativar** – retoma o processamento de uma topologia desativada.</span><span class="sxs-lookup"><span data-stu-id="9970f-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="9970f-181">**Desativar** – coloca em pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="9970f-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="9970f-182">**Rebalancear** -ajusta o paralelismo Olá da topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="9970f-183">Deve rebalancear as topologias em execução depois de ter alterado o número de Olá de nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="9970f-184">Reequilíbrio ajusta o paralelismo toocompensate para o número de Olá maior/menor de nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="9970f-185">Para obter mais informações, consulte [compreender o paralelismo Olá de uma topologia do Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="9970f-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="9970f-186">**Kill** -termina uma topologia do Storm após Olá especificado tempo limite.</span><span class="sxs-lookup"><span data-stu-id="9970f-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="9970f-187">Nesta página, selecione uma entrada de Olá **Spouts** ou **Bolts** secção.</span><span class="sxs-lookup"><span data-stu-id="9970f-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="9970f-188">Informações sobre o componente selecionado Olá são apresentadas.</span><span class="sxs-lookup"><span data-stu-id="9970f-188">Information about hello selected component is displayed.</span></span>

    ![Dashboard do Storm com informações sobre os componentes selecionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="9970f-190">Esta página apresenta Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="9970f-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="9970f-191">**Estatísticas de spout/Bolt** -informações básicas sobre o desempenho do componente de Olá, organizadas em intervalos de tempo.</span><span class="sxs-lookup"><span data-stu-id="9970f-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="9970f-192">Selecionar um intervalo de tempo de Olá de alterações de janela do tempo específico das informações apresentadas noutras secções da página Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="9970f-193">**Estatísticas de entrada** (apenas bolt) – informações sobre componentes que produzem os dados consumidos pelo bolt Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="9970f-194">**Estatísticas de saída** – Informações sobre dados emitidos por este bolt.</span><span class="sxs-lookup"><span data-stu-id="9970f-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="9970f-195">**Executores** – Informações sobre as instâncias deste componente.</span><span class="sxs-lookup"><span data-stu-id="9970f-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="9970f-196">**Erros** – Erros produzidos por este componente.</span><span class="sxs-lookup"><span data-stu-id="9970f-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="9970f-197">Quando visualiza detalhes de Olá de um spout ou bolt, selecione uma entrada de Olá **porta** coluna na Olá **executores** secção tooview detalhes de uma instância específica do componente de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="9970f-198">Neste exemplo, Olá word **sete** Ocorreu 1493957 vezes.</span><span class="sxs-lookup"><span data-stu-id="9970f-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="9970f-199">Esta contagem é o número de vezes word Olá foi detetado desde que esta topologia foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="9970f-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="9970f-200">Parar a topologia de Olá</span><span class="sxs-lookup"><span data-stu-id="9970f-200">Stop hello topology</span></span>

<span data-ttu-id="9970f-201">Devolver toohello **resumo da topologia** página topologia da contagem word Olá e, em seguida, selecione Olá **Kill** botão de Olá **ações de topologia** secção.</span><span class="sxs-lookup"><span data-stu-id="9970f-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="9970f-202">Quando lhe for pedido, introduza 10 Olá segundos toowait antes de parar a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="9970f-203">Após o período de tempo limite de Olá, topologia Olá já não é apresentada quando visitar Olá **IU do Storm** secção do dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="9970f-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="9970f-204">Eliminar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="9970f-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="9970f-205">Caso se depare com um problema com a criação de um cluster do HDInsight, veja [aceder aos requisitos de controlo](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="9970f-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="9970f-206"><a id="next"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9970f-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="9970f-207">Neste tutorial do Apache Storm, aprendeu as noções básicas de Olá do trabalho com o Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9970f-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="9970f-208">Seguidamente, saiba como demasiado[topologias baseadas em Java desenvolver com o Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9970f-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="9970f-209">Se já estiver familiarizado com o desenvolvimento de topologias baseadas em Java e pretender toodeploy um tooHDInsight de topologia existentes, consulte [implementar e gerir topologias Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9970f-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="9970f-210">Se for um programador do .NET, pode criar topologias C# ou C#/Java híbridas com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9970f-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="9970f-211">Para obter mais informações, veja [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio (Desenvolver topologias C# para Apache Storm no HDInsight com ferramentas do Hadoop para o Visual Studio)](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9970f-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="9970f-212">Para topologias de exemplo que podem ser utilizadas com o Storm no HDInsight, consulte Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9970f-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="9970f-213">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9970f-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
