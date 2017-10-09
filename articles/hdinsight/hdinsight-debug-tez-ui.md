---
title: aaaUse Tez IU com o HDInsight baseado em Windows - Azure | Microsoft Docs
description: "Saiba como toouse Olá Tez IU toodebug Tez tarefas no HDInsight do HDInsight baseados em Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="c3f16-103">Utilizar Olá Tez IU toodebug Tez tarefas no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="c3f16-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="c3f16-104">Olá Tez IU é uma página web que podem ser utilizadas toounderstand e depurar tarefas que utilizam o Tez como motor de execução de Olá nos clusters do HDInsight baseados em Windows.</span><span class="sxs-lookup"><span data-stu-id="c3f16-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c3f16-105">Olá Tez IU permite-lhe tarefa de Olá toovisualize como um gráfico de itens ligados, explorar cada item e obter as estatísticas e as informações de registo.</span><span class="sxs-lookup"><span data-stu-id="c3f16-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3f16-106">passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Windows.</span><span class="sxs-lookup"><span data-stu-id="c3f16-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="c3f16-107">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="c3f16-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3f16-108">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="c3f16-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3f16-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c3f16-109">Prerequisites</span></span>
* <span data-ttu-id="c3f16-110">Um cluster do HDInsight baseados em Windows.</span><span class="sxs-lookup"><span data-stu-id="c3f16-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="c3f16-111">Para obter os passos sobre como criar um novo cluster, consulte [começar a utilizar o HDInsight baseado em Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c3f16-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c3f16-112">Olá Tez IU só está disponível nos clusters do HDInsight baseado em Windows criados após 8th de Fevereiro de 2016.</span><span class="sxs-lookup"><span data-stu-id="c3f16-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="c3f16-113">Um cliente de ambiente de trabalho remoto baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="c3f16-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="c3f16-114">Noções sobre Tez</span><span class="sxs-lookup"><span data-stu-id="c3f16-114">Understanding Tez</span></span>
<span data-ttu-id="c3f16-115">Tez é uma arquitetura extensível para processamento de dados no Hadoop que fornece maiores velocidades de processamento de MapReduce tradicional.</span><span class="sxs-lookup"><span data-stu-id="c3f16-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="c3f16-116">Para os clusters do HDInsight baseado em Windows, é um motor de opcional que pode ativar para o ramo de registo utilizando Olá os seguintes comandos como parte da sua consulta do Hive:</span><span class="sxs-lookup"><span data-stu-id="c3f16-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="c3f16-117">Quando o trabalho é submetido tooTez, cria um direcionado Acíclico gráfico (DAG) que descreve a ordem de Olá da execução de ações de Olá necessárias por tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="c3f16-118">Ações individuais são denominadas vértices e executar um conjunto de Olá tarefa geral.</span><span class="sxs-lookup"><span data-stu-id="c3f16-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="c3f16-119">Olá execução real do trabalho Olá descrita através de um vértice denomina-se uma tarefa e pode ser distribuída por vários nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="c3f16-120">Olá compreender Tez IU</span><span class="sxs-lookup"><span data-stu-id="c3f16-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="c3f16-121">Olá Tez IU é que uma página web fornece informações sobre os processos que estão em execução ou ter sido executaram utilizando Tez.</span><span class="sxs-lookup"><span data-stu-id="c3f16-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="c3f16-122">Permite-lhe tooview Olá DAG gerado pelo Tez, como é distribuído entre clusters, contadores, tais como a memória utilizada por tarefas e vértices e as informações de erro.</span><span class="sxs-lookup"><span data-stu-id="c3f16-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="c3f16-123">-Pode oferecer informações úteis no Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="c3f16-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="c3f16-124">Monitorização de processos de execução longa, visualizar Olá progresso de mapa e reduzir as tarefas.</span><span class="sxs-lookup"><span data-stu-id="c3f16-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="c3f16-125">Analisar dados históricos para processos com êxito ou falha toolearn como processamento pode ser melhorado ou por que falhou.</span><span class="sxs-lookup"><span data-stu-id="c3f16-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="c3f16-126">Gerar um DAG</span><span class="sxs-lookup"><span data-stu-id="c3f16-126">Generate a DAG</span></span>
<span data-ttu-id="c3f16-127">Olá Tez IU irá conter apenas dados se uma tarefa que utiliza Olá Tez motor está atualmente em execução ou tem foi executado no Olá passado.</span><span class="sxs-lookup"><span data-stu-id="c3f16-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="c3f16-128">Simples consultas do Hive, normalmente, podem ser resolvidas sem utilizar Tez, no entanto mais complexas consultas que fazer filtragem, agrupamento, ordenação, associações, etc. normalmente, irá necessitar Tez.</span><span class="sxs-lookup"><span data-stu-id="c3f16-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="c3f16-129">Utilize Olá os seguintes passos toorun uma consulta de Hive que irão executar utilizando Tez.</span><span class="sxs-lookup"><span data-stu-id="c3f16-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="c3f16-130">Num browser, navegue até toohttps://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é Olá nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3f16-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="c3f16-131">No menu de Olá em Olá parte superior da página Olá, selecione Olá **Editor do Hive**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="c3f16-132">Isto irá apresentar uma página com Olá consulta de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c3f16-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="c3f16-133">Apagar a consulta de exemplo de Olá e substitua-o com o seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="c3f16-134">Selecione Olá **submeter** botão.</span><span class="sxs-lookup"><span data-stu-id="c3f16-134">Select hello **Submit** button.</span></span> <span data-ttu-id="c3f16-135">Olá **tarefa sessão** secção Olá parte inferior da página Olá apresentará o estado de Olá da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="c3f16-136">Uma vez Olá alterações de estado demasiado**concluído**, selecione Olá **ver detalhes** resultados de Olá tooview de ligação.</span><span class="sxs-lookup"><span data-stu-id="c3f16-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="c3f16-137">Olá **resultado da tarefa** deve ser semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="c3f16-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="c3f16-138">Utilizar Olá Tez IU</span><span class="sxs-lookup"><span data-stu-id="c3f16-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="c3f16-139">Olá Tez IU só está disponível a partir do ambiente de trabalho Olá Olá head de nós de cluster, pelo que deverá utilizar nós principais do ambiente de trabalho remoto tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="c3f16-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="c3f16-140">De Olá [portal do Azure](https://portal.azure.com), selecione o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3f16-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="c3f16-141">A partir da Olá parte superior do painel de HDInsight Olá, selecione Olá **ambiente de trabalho remoto** ícone.</span><span class="sxs-lookup"><span data-stu-id="c3f16-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="c3f16-142">Este será apresentado o painel de ambiente de trabalho remoto Olá</span><span class="sxs-lookup"><span data-stu-id="c3f16-142">This will display hello remote desktop blade</span></span>

    ![Ícone de ambiente de trabalho remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="c3f16-144">No painel de ambiente de trabalho remoto Olá, selecione **Connect** nó principal do cluster de toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c3f16-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="c3f16-145">Quando lhe for pedido, utilize Olá ambiente de trabalho remoto utilizador nome e palavra-passe tooauthenticate Olá ligação de cluster.</span><span class="sxs-lookup"><span data-stu-id="c3f16-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Ícone de ligação de ambiente de trabalho remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="c3f16-147">Se não tiver ativado a conectividade de ambiente de trabalho remoto, forneça um nome de utilizador, a palavra-passe e a data de expiração, em seguida, selecione **ativar** tooenable ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="c3f16-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="c3f16-148">Assim que tiver sido ativada, utilize Olá tooconnect de passos anterior.</span><span class="sxs-lookup"><span data-stu-id="c3f16-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="c3f16-149">Assim que estiver ligado, abra o Internet Explorer no Olá ambiente de trabalho remoto, ícone engrenagem Olá selecione Olá canto superior direito do browser Olá e, em seguida, selecione **ver definições de compatibilidade**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="c3f16-150">Na parte inferior de Olá da **ver definições de compatibilidade**, desmarque caixa de verificação Olá **apresentar sites da intranet na vista de compatibilidade** e **apresenta uma lista de compatibilidade de utilização Microsoft**, e, em seguida, selecione **fechar**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="c3f16-151">No Internet Explorer, procurar toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="c3f16-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="c3f16-152">Isto irá apresentar Olá Tez IU</span><span class="sxs-lookup"><span data-stu-id="c3f16-152">This will display hello Tez UI</span></span>

    ![Tez IU](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="c3f16-154">Quando carrega Olá IU Tez, verá uma lista de DAGs que estão atualmente em execução ou ter sido executado no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="c3f16-155">Vista de predefinida Olá inclui Olá nome Dag, Id, submissor, estado, hora de início, hora de fim, duração, ID da aplicação e fila.</span><span class="sxs-lookup"><span data-stu-id="c3f16-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="c3f16-156">É possível adicionar mais colunas utilizando o ícone de engrenagem Olá na Olá direito da página Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="c3f16-157">Se tiver apenas uma entrada, será para consulta Olá que tenha sido executada na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="c3f16-158">Se tiver várias entradas, pode pesquisar introduzindo critérios de pesquisa em campos de Olá acima Olá DAGs e acessos **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="c3f16-159">Selecione Olá **Dag nome** para a entrada de DAG mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="c3f16-160">Esta ação apresenta informações sobre Olá DAG, bem como toodownload de opção Olá um zip dos ficheiros JSON que contêm informações sobre Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Detalhes do DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="c3f16-162">Acima Olá **DAG detalhes** são várias ligações que podem ser utilizados toodisplay informações sobre Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="c3f16-163">**Contadores do DAG** apresenta informações sobre os contadores para este DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="c3f16-164">**Vista gráfica** apresenta uma representação gráfica deste DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="c3f16-165">**Todos os vértices** apresenta uma lista de vértices Olá neste DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="c3f16-166">**Todas as tarefas** apresenta uma lista de tarefas de Olá para todos os vértices neste DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="c3f16-167">**Todos os TaskAttempts** apresenta informações sobre Olá tenta toorun tarefas para esta DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c3f16-168">Se se deslocar para a apresentação de coluna Olá para vértices, tarefas e TaskAttempts, tenha em atenção que existem ligações tooview **contadores** e **ver ou transferir registos** para cada linha.</span><span class="sxs-lookup"><span data-stu-id="c3f16-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="c3f16-169">Se Ocorreu uma falha com a tarefa de Olá, Olá DAG detalhes apresentará um Estado de FALHADO, juntamente com hiperligações tooinformation sobre a tarefa falhada Olá.</span><span class="sxs-lookup"><span data-stu-id="c3f16-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="c3f16-170">Informações de diagnóstico serão apresentadas abaixo os detalhes de Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="c3f16-171">Selecione **visualização gráfica**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-171">Select **Graphical View**.</span></span> <span data-ttu-id="c3f16-172">Esta ação apresenta uma representação gráfica de Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="c3f16-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="c3f16-173">É possível colocar o rato Olá através de cada vértice nas informações de toodisplay vista Olá acerca do mesmo.</span><span class="sxs-lookup"><span data-stu-id="c3f16-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Vista gráfica](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="c3f16-175">Clicar num vértice carregará Olá **vértice detalhes** para esse item.</span><span class="sxs-lookup"><span data-stu-id="c3f16-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="c3f16-176">Clique em Olá **mapa 1** detalhes de toodisplay vértice para este item.</span><span class="sxs-lookup"><span data-stu-id="c3f16-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="c3f16-177">Selecione **confirmar** navegação de Olá tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="c3f16-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Detalhes de vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="c3f16-179">Tenha em atenção que tem agora ligações na Olá parte superior da página Olá toovertices relacionados e tarefas.</span><span class="sxs-lookup"><span data-stu-id="c3f16-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3f16-180">Também pode chegam esta página por Retroceder demasiado**DAG detalhes**, selecionando **vértice detalhes**e, em seguida, selecionar Olá **mapa 1** vértice.</span><span class="sxs-lookup"><span data-stu-id="c3f16-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="c3f16-181">**Contadores de vértice** apresenta informações do contador para este vértice.</span><span class="sxs-lookup"><span data-stu-id="c3f16-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="c3f16-182">**Tarefas** apresenta tarefas para esta vértice.</span><span class="sxs-lookup"><span data-stu-id="c3f16-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="c3f16-183">**Tentativas de tarefas** apresenta informações sobre as tarefas de toorun de tentativas para este vértice.</span><span class="sxs-lookup"><span data-stu-id="c3f16-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="c3f16-184">**Origens & Sinks** mostra origens de dados e sinks para este vértice.</span><span class="sxs-lookup"><span data-stu-id="c3f16-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c3f16-185">Como com o menu de anterior Olá, pode se deslocar para a apresentação de coluna Olá para tarefas, as tentativas de tarefas e origens & Sinks__ toodisplay liga toomore informações para cada item.</span><span class="sxs-lookup"><span data-stu-id="c3f16-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="c3f16-186">Selecione **tarefas**, e, em seguida, o nome do item de Olá selecione **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="c3f16-187">Isto irá apresentar **detalhes da tarefa** para esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="c3f16-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="c3f16-188">Neste ecrã, pode ver **tarefas contadores** e **tarefas tentativas**.</span><span class="sxs-lookup"><span data-stu-id="c3f16-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Detalhes da tarefa](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="c3f16-190">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="c3f16-190">Next Steps</span></span>
<span data-ttu-id="c3f16-191">Agora que aprendeu como ver toouse Olá Tez, saiba mais sobre [utilizando o Hive no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="c3f16-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="c3f16-192">Para obter mais informações técnicas no Tez, consulte Olá [Tez página em Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="c3f16-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
