---
title: aaaDeploy e gerir topologias Apache Storm no HDInsight | Microsoft Docs
description: "Saiba como toodeploy, monitorizar e gerir topologias do Apache Storm utilizando Olá Storm Dashboard no HDInsight. Utilize as ferramentas Hadoop para o Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="fbb39-104">Implementar e gerir topologias Apache Storm no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="fbb39-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="fbb39-105">Olá Storm Dashboard permite-lhe tooeasily implementar e executar o cluster do Apache Storm topologias tooyour HDInsight ao utilizar o seu browser.</span><span class="sxs-lookup"><span data-stu-id="fbb39-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="fbb39-106">Também pode utilizar Olá dashboard toomonitor e gerir topologias em execução.</span><span class="sxs-lookup"><span data-stu-id="fbb39-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="fbb39-107">Se utilizar o Visual Studio, Olá ferramentas do HDInsight para Visual Studio fornecem semelhantes funcionalidades no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbb39-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="fbb39-108">Olá Storm Dashboard e funcionalidades de Storm Olá no Olá as ferramentas do HDInsight dependem Olá API de REST de Storm, que podem ser utilizado toocreate as suas próprias soluções de monitorização e gestão.</span><span class="sxs-lookup"><span data-stu-id="fbb39-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbb39-109">passos de Olá neste documento exigem um Storm no cluster do HDInsight que utiliza o Windows como sistema de operativo Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="fbb39-110">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="fbb39-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fbb39-111">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="fbb39-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="fbb39-112">Para obter informações sobre como implementar e gerir topologias do Storm com um cluster do HDInsight que utiliza o Linux, consulte [implementar e gerir topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="fbb39-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbb39-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fbb39-113">Prerequisites</span></span>

* <span data-ttu-id="fbb39-114">**Apache Storm no HDInsight** -consulte [introdução ao Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para obter os passos sobre como criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="fbb39-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="fbb39-115">Para Olá **Storm Dashboard**: um browser moderno que suporte HTML5.</span><span class="sxs-lookup"><span data-stu-id="fbb39-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="fbb39-116">Para **Visual Studio** -Azure SDK 2.5.1 ou mais recente e hello as ferramentas do HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbb39-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="fbb39-117">Consulte [começar a utilizar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall e configurar ferramentas do HDInsight Olá para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbb39-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="fbb39-118">Uma das seguintes versões do Visual Studio de Olá:</span><span class="sxs-lookup"><span data-stu-id="fbb39-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="fbb39-119">Visual Studio 2012 com atualização 4</span><span class="sxs-lookup"><span data-stu-id="fbb39-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="fbb39-120">Visual Studio 2013 atualização 4 ou Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="fbb39-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="fbb39-121">Visual Studio 2015 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="fbb39-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="fbb39-122">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="fbb39-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="fbb39-123">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="fbb39-123">Storm Dashboard</span></span>

<span data-ttu-id="fbb39-124">Olá Storm Dashboard é uma página web disponíveis no seu cluster do Storm.</span><span class="sxs-lookup"><span data-stu-id="fbb39-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="fbb39-125">URL de Olá é **https://&lt;clustername >.azurehdinsight.net/**, onde **clustername** é Olá nome do seu cluster Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbb39-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="fbb39-126">Na parte superior de Olá de Olá Storm Dashboard, selecione **submeter topologia**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="fbb39-127">Siga as instruções de Olá no Olá página toorun uma topologia de exemplo ou tooupload e execute uma topologia que criou.</span><span class="sxs-lookup"><span data-stu-id="fbb39-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Olá submeter página topologia][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="fbb39-129">IU do Storm</span><span class="sxs-lookup"><span data-stu-id="fbb39-129">Storm UI</span></span>

<span data-ttu-id="fbb39-130">A partir do Storm Dashboard Olá, selecione Olá **IU do Storm** ligação.</span><span class="sxs-lookup"><span data-stu-id="fbb39-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="fbb39-131">Esta ação apresenta informações sobre o cluster de Olá, na execução de topologias de tooany de adição.</span><span class="sxs-lookup"><span data-stu-id="fbb39-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![IU do storm Olá][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="fbb39-133">Com algumas versões do Internet Explorer, poderá descobrir que Olá que não atualizar a IU do Storm após o primeiro visitaram-lo.</span><span class="sxs-lookup"><span data-stu-id="fbb39-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="fbb39-134">Por exemplo, esta operação poderá não mostrar topologias novo Olá submetidas ou esta operação poderá mostrar uma topologia como o Active Directory quando desativada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fbb39-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="fbb39-135">A Microsoft está ciente de que este problema e está a funcionar numa solução.</span><span class="sxs-lookup"><span data-stu-id="fbb39-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="fbb39-136">Página principal</span><span class="sxs-lookup"><span data-stu-id="fbb39-136">Main page</span></span>

<span data-ttu-id="fbb39-137">página principal do Olá do Olá IU do Storm fornece Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="fbb39-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="fbb39-138">**Resumo do cluster**: informações básicas sobre o cluster do Storm Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="fbb39-139">**Resumo da topologia**: uma lista de execução de topologias.</span><span class="sxs-lookup"><span data-stu-id="fbb39-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="fbb39-140">Utilize Olá ligações na tooview secção obter mais informações sobre topologias específicas.</span><span class="sxs-lookup"><span data-stu-id="fbb39-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="fbb39-141">**Resumo do supervisor**: informações sobre o supervisor de Storm Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="fbb39-142">**Configuração de nimbus**: configuração de Nimbus para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="fbb39-143">Topologia de resumo</span><span class="sxs-lookup"><span data-stu-id="fbb39-143">Topology summary</span></span>

<span data-ttu-id="fbb39-144">Selecionar uma ligação de Olá **resumo da topologia** secção apresenta Olá informações sobre a topologia de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fbb39-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="fbb39-145">**Resumo da topologia**: informações básicas sobre a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="fbb39-146">**Ações de topologia**: ações de gestão que pode efetuar para topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="fbb39-147">**Ativar**: retoma o processamento de uma topologia desativada.</span><span class="sxs-lookup"><span data-stu-id="fbb39-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="fbb39-148">**Desativar**: pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="fbb39-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="fbb39-149">**Rebalancear**: ajusta o paralelismo Olá da topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="fbb39-150">Deve rebalancear as topologias em execução depois de ter alterado o número de Olá de nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="fbb39-151">Isto permite Olá topologia tooadjust paralelismo toocompensate para Olá aumentado ou diminuído número de nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="fbb39-152">Para obter mais informações, consulte [compreender o paralelismo Olá de uma topologia do Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="fbb39-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="fbb39-153">**Kill**: termina uma topologia do Storm após Olá especificado tempo limite.</span><span class="sxs-lookup"><span data-stu-id="fbb39-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="fbb39-154">**Estatísticas de topologia**: estatísticas sobre a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="fbb39-155">Utilize as ligações de Olá Olá **janela** período de tempo de coluna tooset Olá para Olá restantes entradas na página Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="fbb39-156">**Spouts**: Olá spouts utilizados por topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="fbb39-157">Utilize ligações de Olá na tooview secção obter mais informações sobre spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="fbb39-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="fbb39-158">**Bolts**: Olá bolts utilizados por topologia Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="fbb39-159">Utilize ligações de Olá na tooview secção obter mais informações sobre bolts específicos.</span><span class="sxs-lookup"><span data-stu-id="fbb39-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="fbb39-160">**Configuração da topologia**: configuração de Olá da topologia de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="fbb39-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="fbb39-161">Spout e resumo Bolt</span><span class="sxs-lookup"><span data-stu-id="fbb39-161">Spout and Bolt summary</span></span>

<span data-ttu-id="fbb39-162">A seleção de um spout Olá **Spouts** ou **Bolts** secções apresenta Olá seguintes informações sobre o item de Olá selecionado:</span><span class="sxs-lookup"><span data-stu-id="fbb39-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="fbb39-163">**Resumo de componente**: informações básicas sobre Olá spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="fbb39-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="fbb39-164">**Estatísticas de spout/Bolt**: estatísticas sobre Olá spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="fbb39-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="fbb39-165">Utilize as ligações de Olá Olá **janela** período de tempo de coluna tooset Olá para Olá restantes entradas na página Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="fbb39-166">**Estatísticas de entrada** (apenas bolt): informações sobre Olá fluxos consumidos pelo bolt Olá de entrada.</span><span class="sxs-lookup"><span data-stu-id="fbb39-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="fbb39-167">**Estatísticas de saída**: informações sobre fluxos de Olá emitidos por este spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="fbb39-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="fbb39-168">**Executores**: informações sobre instâncias Olá Olá spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="fbb39-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="fbb39-169">Selecione Olá **porta** produzidos de um registo de informações de diagnóstico de entrada para um tooview executor específicas para esta instância.</span><span class="sxs-lookup"><span data-stu-id="fbb39-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="fbb39-170">**Erros**: quaisquer informações de erro para este spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="fbb39-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="fbb39-171">Ferramentas do HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbb39-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="fbb39-172">as ferramentas do HDInsight Olá podem ser utilizados toosubmit c# ou híbrida topologias tooyour cluster do Storm.</span><span class="sxs-lookup"><span data-stu-id="fbb39-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="fbb39-173">os seguintes passos de Olá utiliza uma aplicação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fbb39-173">hello following steps use a sample application.</span></span> <span data-ttu-id="fbb39-174">Para obter informações sobre como criar as seus próprios topologias utilizando as ferramentas do HDInsight Olá, consulte [desenvolver topologias c# utilizando Olá ferramentas do HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fbb39-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="fbb39-175">Utilizar Olá os seguintes passos toodeploy tooyour um exemplo Storm num cluster do HDInsight, em seguida, ver e gerir a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="fbb39-176">Se já não tiver instalado o versão mais recente do Olá do Olá as ferramentas do HDInsight para Visual Studio, consulte o artigo [começar a utilizar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fbb39-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="fbb39-177">Abra o Visual Studio, selecione **ficheiro** > **novo** > **projeto**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="fbb39-178">No Olá **novo projeto** diálogo caixa, expanda **instalada** > **modelos**e, em seguida, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="fbb39-179">Na lista de Olá dos modelos, selecione **exemplo do Storm**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="fbb39-180">Olá parte inferior da caixa de diálogo Olá, escreva um nome para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Imagem](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="fbb39-182">No **Explorador de soluções**, clique no projeto Olá e selecione **submeter tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbb39-183">Se lhe for solicitado, introduza as credenciais de início de sessão Olá para a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb39-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="fbb39-184">Se tiver mais do que uma subscrição, inicie sessão toohello que contenha o seu cluster Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbb39-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="fbb39-185">Selecione o cluster Storm no HDInsight Olá **Cluster do Storm** na lista pendente e, em seguida, selecione **submeter**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="fbb39-186">Pode monitorizar se submissão Olá é efetuada com êxito utilizando Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="fbb39-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="fbb39-187">Quando a topologia de Olá foi submetida com êxito, Olá **topologias Storm** para cluster Olá deve aparecer.</span><span class="sxs-lookup"><span data-stu-id="fbb39-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="fbb39-188">Selecione a topologia de Olá Olá lista tooview sobre Olá com topologia.</span><span class="sxs-lookup"><span data-stu-id="fbb39-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![monitor do Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="fbb39-190">Também pode ver **topologias Storm** de **Explorador de servidores** expandindo **Azure** > **HDInsight**e, em seguida, clicar um cluster Storm no HDInsight e selecionando **topologias do Storm vista**.</span><span class="sxs-lookup"><span data-stu-id="fbb39-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="fbb39-191">Selecione a forma de Olá para Olá spouts ou bolts tooview informações sobre estes componentes.</span><span class="sxs-lookup"><span data-stu-id="fbb39-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="fbb39-192">Abre uma nova janela para cada item selecionado.</span><span class="sxs-lookup"><span data-stu-id="fbb39-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbb39-193">nome de Olá da topologia de Olá é o nome de classe de Olá da topologia de Olá (neste caso, `HelloWord`,) com um carimbo anexado.</span><span class="sxs-lookup"><span data-stu-id="fbb39-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="fbb39-194">De Olá **resumo da topologia** visualizar, selecione **Kill** topologia de Olá toostop.</span><span class="sxs-lookup"><span data-stu-id="fbb39-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbb39-195">Topologias do Storm continuam em execução até que estão paradas ou cluster Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="fbb39-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="fbb39-196">API REST</span><span class="sxs-lookup"><span data-stu-id="fbb39-196">REST API</span></span>

<span data-ttu-id="fbb39-197">Olá IU do Storm é desenvolvida Olá REST API, pelo que pode realizar semelhante de gestão e monitorização funcionalidade utilizando Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="fbb39-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="fbb39-198">Pode utilizar ferramentas personalizadas do Olá REST API toocreate de gestão e monitorização topologias do Storm.</span><span class="sxs-lookup"><span data-stu-id="fbb39-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="fbb39-199">Para obter mais informações, consulte [API de REST de IU do Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="fbb39-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="fbb39-200">Olá informações seguintes são específicos toousing Olá API REST do Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbb39-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="fbb39-201">URI de base</span><span class="sxs-lookup"><span data-stu-id="fbb39-201">Base URI</span></span>

<span data-ttu-id="fbb39-202">Olá URI base para a REST API de Olá nos clusters do HDInsight é **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, onde **clustername** é o nome de Olá do Storm no Cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbb39-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="fbb39-203">Autenticação</span><span class="sxs-lookup"><span data-stu-id="fbb39-203">Authentication</span></span>

<span data-ttu-id="fbb39-204">Toohello pedidos tem de utilizar a REST API **autenticação básica**, por isso, utilize o nome de administrador de cluster de HDInsight Olá e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="fbb39-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="fbb39-205">Porque a autenticação básica é enviada através da utilização de texto não encriptado, deve **sempre** utilizar comunicações de toosecure HTTPS com cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="fbb39-206">Valores de retorno</span><span class="sxs-lookup"><span data-stu-id="fbb39-206">Return values</span></span>

<span data-ttu-id="fbb39-207">Informações de que são devolvidas de Olá REST API podem apenas ser utilizável num cluster de Olá ou Olá, máquinas virtuais na mesma rede Virtual do Azure como cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="fbb39-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="fbb39-208">Por exemplo, nome de domínio completamente qualificado de Olá (FQDN) para servidores de Zookeeper devolvido não são estar acessível a partir do Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="fbb39-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbb39-209">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="fbb39-209">Next Steps</span></span>

<span data-ttu-id="fbb39-210">Agora que aprendeu como topologias toodeploy e monitor utilizando Olá Storm Dashboard, saiba como:</span><span class="sxs-lookup"><span data-stu-id="fbb39-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="fbb39-211">Desenvolver topologias c# utilizando Olá ferramentas do HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbb39-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="fbb39-212">Desenvolver topologias baseadas em Java com o Maven</span><span class="sxs-lookup"><span data-stu-id="fbb39-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="fbb39-213">Para obter uma lista das topologias de exemplo mais, consulte [topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fbb39-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
