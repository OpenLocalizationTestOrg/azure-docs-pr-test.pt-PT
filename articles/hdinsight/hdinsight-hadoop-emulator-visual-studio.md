---
title: ferramentas de aaaData Lake para Visual Studio com a Hortonworks Sandbox - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá ferramentas do Azure Data Lake para Visual Studio com sandbox de Hortonworks Olá em execução numa local VM. Com estas ferramentas, pode criar e executar tarefas do Hive e do Pig em sandbox Olá e o resultado da tarefa de vista e o histórico."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="54056-104">Utilize Olá do Azure Data Lake tools para Visual Studio com Olá Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="54056-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="54056-105">Azure Data Lake inclui ferramentas para trabalhar com clusters do Hadoop genéricos.</span><span class="sxs-lookup"><span data-stu-id="54056-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="54056-106">Este documento fornece passos Olá necessitam as ferramentas do Data Lake de Olá toouse com Olá Hortonworks Sandbox em execução numa máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="54056-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="54056-107">Utilizar Olá Hortonworks Sandbox permite-lhe toowork com o Hadoop localmente no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="54056-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="54056-108">Depois de ter programado uma solução e pretender toodeploy-lo em escala, em seguida, pode mover o cluster do HDInsight tooan.</span><span class="sxs-lookup"><span data-stu-id="54056-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54056-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54056-109">Prerequisites</span></span>

* <span data-ttu-id="54056-110">Olá Hortonworks Sandbox, em execução numa máquina virtual no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="54056-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="54056-111">Este documento foi escrito e testado com sandbox Olá em execução no Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="54056-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="54056-112">Para informações sobre como configurar sandbox Olá, consulte Olá [introdução ao sandbox de Hortonworks Olá.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="54056-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="54056-113">documento.</span><span class="sxs-lookup"><span data-stu-id="54056-113">document.</span></span>

* <span data-ttu-id="54056-114">Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (qualquer edição).</span><span class="sxs-lookup"><span data-stu-id="54056-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="54056-115">Olá [Azure SDK para .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="54056-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="54056-116">Olá [do Azure Data Lake tools para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="54056-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="54056-117">Configurar palavras-passe para a sandbox Olá</span><span class="sxs-lookup"><span data-stu-id="54056-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="54056-118">Certifique-se de que Olá que hortonworks Sandbox está em execução.</span><span class="sxs-lookup"><span data-stu-id="54056-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="54056-119">Em seguida, siga os passos de Olá Olá [começar Olá Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento.</span><span class="sxs-lookup"><span data-stu-id="54056-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="54056-120">Estes passos configurar Olá palavra-passe para Olá SSH `root` conta e Olá Ambari `admin` conta.</span><span class="sxs-lookup"><span data-stu-id="54056-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="54056-121">Estas palavras-passe é utilizados quando se liga toohello sandbox a partir do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54056-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="54056-122">Ligar sandbox de toohello Olá ferramentas</span><span class="sxs-lookup"><span data-stu-id="54056-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="54056-123">Abra o Visual Studio, selecione **vista**e, em seguida, selecione **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="54056-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="54056-124">De **Explorador de servidores**, contexto Olá **HDInsight** entrada e, em seguida, selecione **ligar tooHDInsight emulador**.</span><span class="sxs-lookup"><span data-stu-id="54056-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Captura de ecrã do Explorador de servidores, com Connect tooHDInsight emulador realçado](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="54056-126">De Olá **ligar tooHDInsight emulador** caixa de diálogo, introduza a palavra-passe de Olá que configurou para Ambari.</span><span class="sxs-lookup"><span data-stu-id="54056-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Captura de ecrã da caixa de diálogo, com a caixa de texto de palavra-passe realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="54056-128">Selecione **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="54056-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="54056-129">Olá utilize **palavra-passe** palavra-passe campo tooenter Olá configurado para Olá `root` conta.</span><span class="sxs-lookup"><span data-stu-id="54056-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="54056-130">Deixe Olá outros campos no valor predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-130">Leave hello other fields at hello default value.</span></span>

    ![Captura de ecrã da caixa de diálogo, com a caixa de texto de palavra-passe realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="54056-132">Selecione **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="54056-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="54056-133">Aguarde que a validação de Olá toofinish de serviços.</span><span class="sxs-lookup"><span data-stu-id="54056-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="54056-134">Em alguns casos, validação pode falhar e solicitar a configuração de Olá tooupdate.</span><span class="sxs-lookup"><span data-stu-id="54056-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="54056-135">Se a validação falhar, selecione **atualização**e aguarde que a configuração de Olá e verificação para Olá serviço toofinish.</span><span class="sxs-lookup"><span data-stu-id="54056-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Captura de ecrã da caixa de diálogo, com o botão de atualização realçado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="54056-137">processo de atualização de Olá utiliza Ambari toomodify Olá Hortonworks Sandbox configuração toowhat é esperado pelas ferramentas de Data Lake Olá para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54056-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="54056-138">Depois de concluir a validação, selecione **concluir** toocomplete configuração.</span><span class="sxs-lookup"><span data-stu-id="54056-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="54056-139">![Captura de ecrã da caixa de diálogo, com o botão Concluir realçado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="54056-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="54056-140">Consoante a velocidade de Olá do ambiente de desenvolvimento e da quantidade de Olá de memória alocada a máquina virtual de toohello, pode demorar vários minutos tooconfigure e confirme Olá serviços.</span><span class="sxs-lookup"><span data-stu-id="54056-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="54056-141">Depois de seguir estes passos, tem agora um **HDInsight local cluster** entrada existente no Explorador de servidores, sob Olá **HDInsight** secção.</span><span class="sxs-lookup"><span data-stu-id="54056-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="54056-142">Escrever uma consulta do Hive</span><span class="sxs-lookup"><span data-stu-id="54056-142">Write a Hive query</span></span>

<span data-ttu-id="54056-143">Ramo de registo fornece um idioma de consulta como o SQL Server (HiveQL) para trabalhar com dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="54056-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="54056-144">Utilize Olá toolearn passos como toorun a pedido consulta contra o cluster local Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="54056-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="54056-145">No **Explorador de servidores**, faça duplo clique entrada Olá para o cluster local Olá que adicionou anteriormente e, em seguida, selecione **escrever uma consulta do Hive**.</span><span class="sxs-lookup"><span data-stu-id="54056-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Captura de ecrã do Explorador de servidores, com uma consulta do Hive realçado de escrita](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="54056-147">É apresentada uma nova janela de consulta.</span><span class="sxs-lookup"><span data-stu-id="54056-147">A new query window appears.</span></span> <span data-ttu-id="54056-148">Aqui, pode rapidamente escrever e submeter um cluster local de toohello de consulta.</span><span class="sxs-lookup"><span data-stu-id="54056-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="54056-149">Na nova janela de consulta Olá, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="54056-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="54056-150">consulta do toorun Olá, selecione **submeter** em Olá parte superior da janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="54056-151">Deixe Olá outros valores (**Batch** e nome do servidor), os valores predefinidos de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Captura de ecrã da janela de consulta, com o botão para submeter Olá realçado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="54056-153">Também pode utilizar o menu pendente de Olá junto demasiado**submeter** tooselect **avançadas**.</span><span class="sxs-lookup"><span data-stu-id="54056-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="54056-154">Opções avançadas permitem-lhe opções adicionais tooprovide ao submeter a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Caixa de diálogo de captura de ecrã de submeter Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="54056-156">Depois de submeter a consulta de Olá, é apresentado o estado da tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="54056-157">Estado da tarefa Olá apresenta informações sobre a tarefa de Olá como processado por Hadoop.</span><span class="sxs-lookup"><span data-stu-id="54056-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="54056-158">**Estado da tarefa** fornece Olá estado da tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="54056-159">Estado de Olá é atualizado periodicamente, ou pode utilizar Olá atualizar ícone toorefresh Olá estado manualmente.</span><span class="sxs-lookup"><span data-stu-id="54056-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Caixa de diálogo de captura de ecrã da vista de tarefas, com o estado da tarefa realçado](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="54056-161">Depois de Olá **estado da tarefa** alterações demasiado**concluído**, é apresentado um direcionado Acíclico gráfico (DAG).</span><span class="sxs-lookup"><span data-stu-id="54056-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="54056-162">Este diagrama descreve o caminho de execução de Olá foi determinado pelo Tez ao processar a consulta do Hive de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="54056-163">Tez é o motor de execução de predefinição do Olá para o ramo de registo no cluster local Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54056-164">Tez também é predefinido Olá quando estiver a utilizar clusters do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="54056-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="54056-165">Não é predefinido Olá no HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="54056-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="54056-166">toouse-lo, tem de adicionar a linha de Olá `set hive.execution.engine = tez;` toohello início da sua consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="54056-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="54056-167">Olá utilize **resultado da tarefa** saída de Olá tooview de ligação.</span><span class="sxs-lookup"><span data-stu-id="54056-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="54056-168">Neste caso, é 823, número de Olá de linhas na tabela de sample_08 Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="54056-169">Pode ver informações de diagnóstico sobre a tarefa de Olá utilizando Olá **registo da tarefa** e **transferir o registo de YARN** ligações.</span><span class="sxs-lookup"><span data-stu-id="54056-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="54056-170">Também pode executar tarefas do Hive interativamente alterando Olá **Batch** campo demasiado**interativo**.</span><span class="sxs-lookup"><span data-stu-id="54056-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="54056-171">Em seguida, selecione **executar**.</span><span class="sxs-lookup"><span data-stu-id="54056-171">Then select **Execute**.</span></span>

    ![Captura de ecrã de interativa e executar botões realçados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="54056-173">Uma consulta interativa fluxos Olá registo de saídas gerado durante o processamento toohello **HiveServer2 saída** janela.</span><span class="sxs-lookup"><span data-stu-id="54056-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54056-174">Olá informações é Olá, mesmo que esteja disponível a partir do Olá **registo da tarefa** ligação depois de terminar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="54056-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Captura de ecrã do registo de saída](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="54056-176">Criar um projeto do Hive</span><span class="sxs-lookup"><span data-stu-id="54056-176">Create a Hive project</span></span>

<span data-ttu-id="54056-177">Também pode criar um projeto que contém vários scripts Hive.</span><span class="sxs-lookup"><span data-stu-id="54056-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="54056-178">Utilize um projeto quando ter relacionados scripts ou pretender toostore scripts num sistema de controlo de versão.</span><span class="sxs-lookup"><span data-stu-id="54056-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="54056-179">No Visual Studio, selecione **ficheiro**, **novo**e, em seguida, **projeto**.</span><span class="sxs-lookup"><span data-stu-id="54056-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="54056-180">Na lista de Olá de projetos, expanda **modelos**, expanda **do Azure Data Lake**e, em seguida, selecione **ramo de registo (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="54056-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="54056-181">Na lista de Olá dos modelos, selecione **do Hive de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="54056-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="54056-182">Introduza um nome e localização e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="54056-182">Enter a name and location, and then select **OK**.</span></span>

    ![Janela de captura de ecrã do novo projeto, com o Azure Data Lake, HIVE, do Hive de exemplo e OK realçado](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="54056-184">Olá **do Hive de exemplo** projeto contém dois scripts, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="54056-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="54056-185">Pode submeter estes scripts utilizando Olá mesmo **submeter** botão na Olá parte superior da janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="54056-186">Criar um projeto do Pig</span><span class="sxs-lookup"><span data-stu-id="54056-186">Create a Pig project</span></span>

<span data-ttu-id="54056-187">Enquanto o ramo de registo fornece uma linguagem semelhante a SQL para trabalhar com dados estruturados, Pig funciona efetuando transformações de dados.</span><span class="sxs-lookup"><span data-stu-id="54056-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="54056-188">PIg fornece um idioma (Pig Latin) que permite-lhe toodevelop um pipeline de transformações.</span><span class="sxs-lookup"><span data-stu-id="54056-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="54056-189">toouse Pig com o cluster local Olá, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="54056-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="54056-190">Abra o Visual Studio e selecione **ficheiro**, **novo**e, em seguida, **projeto**.</span><span class="sxs-lookup"><span data-stu-id="54056-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="54056-191">Na lista de Olá de projetos, expanda **modelos**, expanda **do Azure Data Lake**e, em seguida, selecione **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="54056-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="54056-192">Na lista de Olá dos modelos, selecione **Pig aplicação**.</span><span class="sxs-lookup"><span data-stu-id="54056-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="54056-193">Introduza um nome, localização e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="54056-193">Enter a name, location, and then select **OK**.</span></span>

    ![Janela de captura de ecrã do novo projeto, com o Azure Data Lake, Pig, Pig aplicação e OK realçado](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="54056-195">Introduza Olá seguir texto como conteúdo Olá Olá **script.pig** ficheiro que foi criado com este projeto.</span><span class="sxs-lookup"><span data-stu-id="54056-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="54056-196">Enquanto o Pig utiliza um idioma diferente de ramo de registo, como executar tarefas de Olá é consistente entre ambos os idiomas, através de Olá **submeter** botão.</span><span class="sxs-lookup"><span data-stu-id="54056-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="54056-197">Selecionar Olá pendente junto a **submeter** apresenta uma caixa de diálogo de submissão avançada para o Pig.</span><span class="sxs-lookup"><span data-stu-id="54056-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Caixa de diálogo de captura de ecrã de submeter Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="54056-199">Também é apresentado o estado da tarefa Olá e de saída, Olá mesmo como uma consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="54056-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Captura de ecrã de uma tarefa Pig concluída](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="54056-201">Ver tarefas</span><span class="sxs-lookup"><span data-stu-id="54056-201">View jobs</span></span>

<span data-ttu-id="54056-202">Ferramentas do Data Lake também permitem-lhe tooeasily ver informações sobre as tarefas que foram executadas no Hadoop.</span><span class="sxs-lookup"><span data-stu-id="54056-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="54056-203">Os seguintes passos toosee Olá as tarefas que foram executadas no cluster local Olá Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="54056-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="54056-204">De **Explorador de servidores**, clique no cluster local Olá e, em seguida, selecione **ver tarefas**.</span><span class="sxs-lookup"><span data-stu-id="54056-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="54056-205">É apresentada uma lista de tarefas que foram submetidos toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="54056-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Captura de ecrã do Explorador de servidores, com as tarefas da vista realçados](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="54056-207">Na lista de Olá de tarefas, selecione um detalhes da tarefa tooview Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Captura de ecrã da tarefa de Browser, uma das tarefas de Olá realçadas](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="54056-209">informação de Olá apresentada é semelhante toowhat que consulte depois de executar uma consulta do Hive ou Pig, incluindo ligações tooview Olá saída e o registo de informações.</span><span class="sxs-lookup"><span data-stu-id="54056-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="54056-210">Também pode modificar e submeta novamente a tarefa de Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="54056-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="54056-211">Ver as bases de dados do Hive</span><span class="sxs-lookup"><span data-stu-id="54056-211">View Hive databases</span></span>

1. <span data-ttu-id="54056-212">No **Explorador de servidores**, expanda Olá **HDInsight local cluster** entrada e, em seguida, expanda **bases de dados do Hive**.</span><span class="sxs-lookup"><span data-stu-id="54056-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="54056-213">Olá **predefinido** e **xademo** bases de dados no cluster local Olá são apresentados.</span><span class="sxs-lookup"><span data-stu-id="54056-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="54056-214">Uma base de dados de expansão mostra tabelas de Olá na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Captura de ecrã do Explorador de servidores, com bases de dados expandidos](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="54056-216">Expandir uma tabela mostra colunas Olá para essa tabela.</span><span class="sxs-lookup"><span data-stu-id="54056-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="54056-217">tooquickly ver dados de Olá, uma tabela com o botão direito e selecione **vista primeiras 100 linhas**.</span><span class="sxs-lookup"><span data-stu-id="54056-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Captura de ecrã do Explorador de servidores, com a tabela expandido e vista primeiras 100 linhas selecionadas](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="54056-219">Propriedades de base de dados e tabela</span><span class="sxs-lookup"><span data-stu-id="54056-219">Database and table properties</span></span>

<span data-ttu-id="54056-220">Pode ver as propriedades de Olá de uma base de dados ou tabela.</span><span class="sxs-lookup"><span data-stu-id="54056-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="54056-221">Selecionar **propriedades** apresenta os detalhes do item de Olá selecionado na janela de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="54056-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="54056-222">Por exemplo, consulte as informações de Olá mostradas na seguinte captura de ecrã de Olá:</span><span class="sxs-lookup"><span data-stu-id="54056-222">For example, see hello information shown in hello following screenshot:</span></span>

![Janela de captura de ecrã de propriedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="54056-224">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="54056-224">Create a table</span></span>

<span data-ttu-id="54056-225">toocreate uma tabela, faça duplo clique uma base de dados e, em seguida, selecione **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="54056-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Captura de ecrã do Explorador de servidores, com Create Table realçado](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="54056-227">Em seguida, pode criar tabela Olá utilizando um formulário.</span><span class="sxs-lookup"><span data-stu-id="54056-227">You can then create hello table using a form.</span></span> <span data-ttu-id="54056-228">Na parte inferior de Olá de Olá seguinte captura de ecrã, pode ver Olá HiveQL não processado que é utilizado toocreate Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="54056-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Captura de ecrã do formulário Olá utilizado toocreate uma tabela](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="54056-230">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="54056-230">Next steps</span></span>

* [<span data-ttu-id="54056-231">Learning ropes Olá de Olá Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="54056-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="54056-232">Tutorial do Hadoop - introdução HDP</span><span class="sxs-lookup"><span data-stu-id="54056-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
