---
title: aaaCreate tabelas de ramo de registo e carregar dados do Blob Storage do Azure | Microsoft Docs
description: Criar as tabelas do Hive e carregar os dados nas tabelas de toohive de blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="6d7f6-103">Criar as tabelas do Hive e carregar dados do Blob Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="6d7f6-104">Este tópico apresenta genéricas consultas do Hive que criar tabelas do Hive e carregar dados do blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="6d7f6-105">Algumas orientações também são fornecidas na criação de partições de tabelas do Hive e sobre como utilizar Olá otimizada linha Columnar (ORC) formatação tooimprove desempenho das consultas.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="6d7f6-106">Isto **menu** liga tootopics que descrevem como dados tooingest em ambientes de destino onde os dados de Olá podem ser armazenados e processados durante Olá o processo de ciência de dados de equipa (TDSP).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="6d7f6-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d7f6-107">Prerequisites</span></span>
<span data-ttu-id="6d7f6-108">Este artigo pressupõe que tem:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-108">This article assumes that you have:</span></span>

* <span data-ttu-id="6d7f6-109">Criar uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-109">Created an Azure storage account.</span></span> <span data-ttu-id="6d7f6-110">Se precisar de instruções, consulte [contas do storage do Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="6d7f6-111">Aprovisionar um cluster de Hadoop personalizado com Olá serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="6d7f6-112">Se precisar de instruções, consulte [personalizar o Azure HDInsight Hadoop clusters para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="6d7f6-113">Cluster de toohello ativados de acesso remoto, tem sessão iniciada e abrir a consola da linha de comandos do Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="6d7f6-114">Se precisar de instruções, consulte [Olá acesso Head nó de Cluster do Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="6d7f6-115">Carregar o armazenamento de BLOBs de tooAzure de dados</span><span class="sxs-lookup"><span data-stu-id="6d7f6-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="6d7f6-116">Se tiver criado uma máquina virtual do Azure ao seguir as instruções de Olá fornecidas [configurar uma máquina virtual do Azure para análise avançada](machine-learning-data-science-setup-virtual-machine.md), este ficheiro de script deve ter sido transferido toohello *c:\\ Os utilizadores\\\<nome de utilizador\>\\documentos\\Scripts de ciência de dados* diretório na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="6d7f6-117">Estas consultas do Hive apenas requerem que ligue no seu próprio esquema de dados e a configuração de armazenamento de Blobs do Azure no Olá campos apropriados toobe pronto para submissão.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="6d7f6-118">Partimos do princípio que Olá dados para as tabelas do Hive são num **descomprimidos** formato tabular, e que dados Olá foi carregadas toohello predefinida (ou tooan adicional) contentor Olá da conta de armazenamento utilizada pelo cluster de Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="6d7f6-119">Se quiser toopractice no Olá **NYC Taxi viagem dados**, tem de:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="6d7f6-120">**Transferir** Olá 24 [NYC Taxi viagem dados](http://www.andresmh.com/nyctaxitrips) ficheiros (12 viagem e 12 Fare ficheiros),</span><span class="sxs-lookup"><span data-stu-id="6d7f6-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="6d7f6-121">**deszipe** todos os ficheiros para os ficheiros. csv e, em seguida,</span><span class="sxs-lookup"><span data-stu-id="6d7f6-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="6d7f6-122">**carregar** -los toohello predefinida (ou contentor adequado) de Olá conta do storage do Azure que foi criada pelo procedimento de Olá descrito em Olá [personalizar o Azure HDInsight Hadoop clusters para o processo de análise avançada e tecnologia ](machine-learning-data-science-customize-hadoop-cluster.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="6d7f6-123">Olá processo tooupload Olá. csv ficheiros toohello contentor predefinido da conta do storage Olá pode ser encontrado no [página](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="6d7f6-124"><a name="submit"></a>Como consultas do Hive de toosubmit</span><span class="sxs-lookup"><span data-stu-id="6d7f6-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="6d7f6-125">Consultas do Hive podem ser submetidas utilizando:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="6d7f6-126">Submeter consultas do Hive através da linha de comandos do Hadoop no headnode do cluster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="6d7f6-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="6d7f6-127">Submeter consultas do Hive com Olá Editor do Hive</span><span class="sxs-lookup"><span data-stu-id="6d7f6-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="6d7f6-128">Submeter consultas do Hive com comandos do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="6d7f6-129">Consultas do Hive são como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="6d7f6-130">Se estiver familiarizado com o SQL Server, pode encontrar Olá [ramo de registo para a folha de Cheat utilizadores do SQL Server](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="6d7f6-131">Ao submeter uma consulta do Hive, também pode controlar o destino de Olá de saída de Olá de consultas do Hive, se este estar num Olá ecrã ou tooa ficheiro local no nó principal Olá ou tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="6d7f6-132"><a name="headnode"></a> 1. Submeter consultas do Hive através da linha de comandos do Hadoop no headnode do cluster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="6d7f6-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="6d7f6-133">Se Olá Hive consulta é complexa, submetê-lo diretamente no nó principal do Olá do cluster de Hadoop Olá normalmente leva toofaster por sua vez em torno de submetê-lo com um Editor do Hive ou scripts do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="6d7f6-134">Inicie sessão no nó principal do toohello do cluster de Hadoop Olá, abra Olá linha de comandos do Hadoop no ambiente de trabalho de Olá do nó principal Olá e introduza o comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="6d7f6-135">Tem três as consultas do Hive de toosubmit formas no Olá linha de comandos do Hadoop:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="6d7f6-136">diretamente</span><span class="sxs-lookup"><span data-stu-id="6d7f6-136">directly</span></span>
* <span data-ttu-id="6d7f6-137">utilizar .hql ficheiros</span><span class="sxs-lookup"><span data-stu-id="6d7f6-137">using .hql files</span></span>
* <span data-ttu-id="6d7f6-138">com Olá consola comandos de ramo de registo</span><span class="sxs-lookup"><span data-stu-id="6d7f6-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="6d7f6-139">Submeta consultas do Hive diretamente no Hadoop linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="6d7f6-140">Pode executar o comando como `hive -e "<your hive query>;` toosubmit de consultas do Hive simples diretamente no Hadoop linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="6d7f6-141">Eis um exemplo, onde Olá comando que envia a consulta do Hive de Olá destaca de caixa de Olá vermelho e Olá caixa verde destaca Olá resultado da consulta de Hive Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="6d7f6-143">Submeter consultas do Hive nos ficheiros de .hql</span><span class="sxs-lookup"><span data-stu-id="6d7f6-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="6d7f6-144">Quando a consulta do Hive de Olá é mais complicada e tem várias linhas, a edição de consultas na linha de comandos ou consola de comandos do ramo de registo não é prática.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="6d7f6-145">Uma alternativa é toouse um editor de texto no nó principal do Olá de Olá Hadoop cluster toosave Olá consultas do Hive num ficheiro .hql num diretório local do nó principal Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="6d7f6-146">Em seguida, pode ser submetida a consulta do Hive de Olá no ficheiro de .hql Olá utilizando Olá `-f` argumento da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="6d7f6-148">**Suprimir a impressão de ecrã de estado de progresso de consultas do Hive**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="6d7f6-149">Por predefinição, depois de consulta do Hive é submetida numa linha de comandos do Hadoop, progresso de Olá da tarefa de mapa/reduza Olá está impresso no ecrã.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="6d7f6-150">toosuppress Olá impressão de ecrã de progresso da tarefa mapa/reduza Olá, pode utilizar um argumento `-S` ("S" em maiúsculas) no Olá comando linha da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="6d7f6-151">.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-151">.</span></span>    <span data-ttu-id="6d7f6-152">ramo de registo -S -i "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="6d7f6-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="6d7f6-153">Submeta consultas do Hive na consola de comandos do ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="6d7f6-154">Primeiro também pode introduzir a consola de comandos do ramo de registo Olá executando o comando `hive` na linha de comandos do Hadoop e, em seguida, submeter consultas do Hive na consola de comandos do ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="6d7f6-155">Eis um exemplo.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-155">Here is an example.</span></span> <span data-ttu-id="6d7f6-156">Neste exemplo, Olá duas caixas vermelho realce Olá comandos utilizados tooenter Olá consola de comandos do Hive e Olá consulta do Hive submeteu na consola de comandos do ramo de registo, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="6d7f6-157">caixa de Olá verde realça um resultado Olá de consulta do Hive de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-157">hello green box highlights hello output from hello Hive query.</span></span>

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="6d7f6-159">exemplos anteriores Olá diretamente os resultados da consulta do Hive Olá no ecrã de saída.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="6d7f6-160">Também pode escrever Olá tooa local Ficheirodesaída no nó principal Olá ou tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="6d7f6-161">Em seguida, pode utilizar outras ferramentas toofurther analisar a saída de Olá de consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="6d7f6-162">**Saída do ficheiro local de tooa resultados de consulta do Hive.**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="6d7f6-163">toooutput Hive consulta resultados tooa diretório local no nó principal Olá, que tem consulta de Hive toosubmit Olá Olá Hadoop linha de comandos da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="6d7f6-164">No seguinte exemplo de Olá, saída Olá de consulta do Hive é escrita num ficheiro `hivequeryoutput.txt` no diretório `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="6d7f6-166">**Saída tooan de resultados de consulta do Hive BLOBs do Azure**</span><span class="sxs-lookup"><span data-stu-id="6d7f6-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="6d7f6-167">Também pode apresentar Olá Hive consulta resultados tooan BLOBs do Azure, dentro do contentor predefinido de Olá do cluster de Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="6d7f6-168">consulta do Hive de Olá para este é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="6d7f6-169">No seguinte exemplo de Olá, saída Olá de consulta do Hive é escrita diretório de blob tooa `queryoutputdir` dentro do contentor predefinido de Olá do cluster de Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="6d7f6-170">Aqui, basta nome do diretório Olá tooprovide, sem o nome do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="6d7f6-171">Emitido um erro se fornecer nomes de diretório e BLOBs, tais como `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="6d7f6-173">Se abrir o contentor predefinido de Olá do cluster de Hadoop Olá através do Explorador de armazenamento do Azure, pode ver a saída de Olá da consulta do Hive de Olá conforme mostrado no Olá figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="6d7f6-174">Pode aplicar Olá filtro (realçado por caixa vermelha) tooonly obter Olá blob com especificado letras nos nomes.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="6d7f6-176"><a name="hive-editor"></a> 2. Submeter consultas do Hive com Olá Editor do Hive</span><span class="sxs-lookup"><span data-stu-id="6d7f6-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="6d7f6-177">Também pode utilizar Olá consulta consola (Editor do Hive) ao introduzir um URL de formulário Olá *https://&#60; Nome do cluster de Hadoop >.azurehdinsight.net/Home/HiveEditor* num browser.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="6d7f6-178">Tem de ser registadas no Olá consulte esta consola e, por isso, terá das credenciais de cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="6d7f6-179"><a name="ps"></a> 3. Submeter consultas do Hive com comandos do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7f6-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="6d7f6-180">Também pode utilizar consultas do PowerShell toosubmit do Hive.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="6d7f6-181">Para obter instruções, consulte [tarefas submeter o Hive com o PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6d7f6-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="6d7f6-182"><a name="create-tables"></a>Criar tabelas e a base de dados do Hive</span><span class="sxs-lookup"><span data-stu-id="6d7f6-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="6d7f6-183">Olá consultas do Hive são partilhadas no Olá [repositório do GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) , podendo ser transferido a partir daí.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="6d7f6-184">Segue-se a consulta do Hive Olá que cria uma tabela do Hive.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="6d7f6-185">Seguem-se Olá as descrições dos campos de Olá que precisa de tooplug no e outras configurações:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="6d7f6-186">**&#60; nome de base de dados >**: nome de Olá da base de dados de Olá que pretende que o toocreate.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="6d7f6-187">Se pretender apenas toouse Olá predefinido da base de dados, Olá consulta *criar base de dados...*  pode ser omitido.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="6d7f6-188">**&#60; nome da tabela >**: nome de Olá da tabela de Olá que pretende que o toocreate na base de dados especificada Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="6d7f6-189">Se pretender que a base de dados predefinida de Olá toouse, tabela Olá pode ser diretamente referida pela *&#60; nome da tabela >* sem &#60; nome de base de dados >.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="6d7f6-190">**&#60; o separador de campo >**: separador de Olá delimits campos no toobe de ficheiro de dados de Olá carregado toohello tabela de Hive.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="6d7f6-191">**&#60; o separador de linha >**: separador de Olá delimits linhas no ficheiro de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="6d7f6-192">**&#60; localização de armazenamento >**: Olá dados Olá de toosave de localização do armazenamento do Azure de tabelas do Hive.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="6d7f6-193">Se não especificar *localização &#60; localização de armazenamento >*, Olá da base de dados e hello tabelas são armazenadas no *hive/Armazém/* diretório no contentor predefinido de Olá do cluster de ramo de registo de Olá por predefinição.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="6d7f6-194">Se pretender que a localização de armazenamento toospecify Olá, a localização de armazenamento Olá tem toobe dentro do contentor predefinido de Olá para a base de dados de Olá e tabelas.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="6d7f6-195">Esta localização tem toobe que referida como contentor predefinido de toohello relativo de localização do cluster de Olá Olá no formato *' wasb: / / / &#60; diretório 1 > /'* ou *' wasb: / / / &#60; diretório 1 > / &#60; diretório 2 > /'*, etc. Após Olá consulta for executada, diretórios relativo Olá são criados dentro do contentor do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="6d7f6-196">**TBLPROPERTIES("Skip.Header.line.Count"="1")**: se o ficheiro de dados de Olá tem uma linha de cabeçalho, terá de tooadd esta propriedade **no fim de Olá** de Olá *criar tabela* consulta.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="6d7f6-197">Caso contrário, a linha de cabeçalho de Olá está carregada como uma tabela de registos toohello.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="6d7f6-198">Se o ficheiro de dados de Olá não tiver uma linha de cabeçalho, esta configuração pode ser omitida na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="6d7f6-199"><a name="load-data"></a>Carregar dados tooHive tabelas</span><span class="sxs-lookup"><span data-stu-id="6d7f6-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="6d7f6-200">Segue-se a consulta do Hive Olá que carrega dados para uma tabela do Hive.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="6d7f6-201">**&#60; dados de tooblob caminho >**: esteja tabela do Hive de toohello toobe carregado Olá blob ficheiros no contentor predefinido Olá Olá cluster do HDInsight Hadoop, Olá *&#60; dados de tooblob caminho >* deve estar no formato de Olá *' wasb: / / / &#60; diretório neste contentor > / &#60; nome de ficheiro do blob >'*.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="6d7f6-202">ficheiro de blob Olá também pode ter um contentor adicional de Olá cluster do HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="6d7f6-203">Neste caso, *&#60; dados de tooblob caminho >* deve estar no formato de Olá *' wasb: / / &#60; nome do contentor > @&#60; nome da conta de armazenamento >.blob.core.windows.net/ &#60; nome de ficheiro do blob >'*.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6d7f6-204">Olá blob dados toobe carregado tooHive tabela tem toobe predefinido Olá ou contentor adicional Olá da conta de armazenamento para o cluster de Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="6d7f6-205">Caso contrário, Olá *carga dados* consulta falha complaining que não pode aceder a dados Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="6d7f6-206"><a name="partition-orc"></a>Tópicos de avançadas: particionar a tabela e o arquivo de dados do Hive no formato ORC</span><span class="sxs-lookup"><span data-stu-id="6d7f6-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="6d7f6-207">Se os dados de Olá ficarem grandes, a criação de partições de tabela Olá é vantajoso para consultas que apenas necessitam tooscan alguns partições da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="6d7f6-208">Por exemplo, é toopartition razoável Olá registar dados de um web site por datas.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="6d7f6-209">Na adição toopartitioning tabelas de ramo de registo, também é vantajoso toostore dados de ramo de registo de Olá no formato de otimizada linha Columnar (ORC) de Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="6d7f6-210">Para obter mais informações sobre ORC formatação, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">ficheiros ORC utilizando melhora o desempenho ao ramo de registo é ler, escrever e processar dados</a>.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="6d7f6-211">Tabela particionada</span><span class="sxs-lookup"><span data-stu-id="6d7f6-211">Partitioned table</span></span>
<span data-ttu-id="6d7f6-212">Segue-se a consulta do Hive do Olá que cria uma tabela particionada e carrega dados para a mesma.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="6d7f6-213">Ao consultar tabelas particionadas, recomenda-se condição de partição de Olá tooadd no Olá **início** de Olá `where` cláusula deste melhora efficacy Olá de procura significativamente.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="6d7f6-214"><a name="orc"></a>Armazenar dados do Hive no formato ORC</span><span class="sxs-lookup"><span data-stu-id="6d7f6-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="6d7f6-215">Diretamente não é possível carregar os dados a partir do blob storage para as tabelas do Hive, que é armazenado num formato ORC Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="6d7f6-216">Seguem-se passos de Olá esse Olá que necessita para tootake tooload dados a partir do Azure blobs tabelas tooHive armazenadas num formato ORC.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="6d7f6-217">Criar uma tabela externa **ARMAZENADOS TEXTFILE de AS** e carregar dados a partir da tabela de toohello de armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="6d7f6-218">Criar uma tabela interna com Olá mesmo esquema como tabela externa de Olá no passo 1, com Olá mesmo o delimitador de campos e armazenar Olá ramo de registo de dados no formato ORC Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="6d7f6-219">Selecione os dados da tabela externa de Olá no passo 1 e inserir na tabela ORC Olá</span><span class="sxs-lookup"><span data-stu-id="6d7f6-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="6d7f6-220">Se tabela TEXTFILE Olá *&#60; nome de base de dados >. &#60; nome da tabela externa textfile >* tem partições, no passo 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando seleciona Olá variável partição como um campo no Olá devolveu um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="6d7f6-221">Inserir-Olá *&#60; nome de base de dados >. &#60; nome da tabela ORC >* falhar desde *&#60; nome de base de dados >. &#60; nome da tabela ORC >* não tem a variável de partição Olá como um campo no esquema de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="6d7f6-222">Neste caso, terá de toospecifically Olá selecione campos toobe inserido demasiado*&#60; nome de base de dados >. &#60; nome da tabela ORC >* da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="6d7f6-223">É seguro toodrop Olá *&#60; nome da tabela externa textfile >* quando utilizando a seguinte consulta depois de todos os dados de Olá foi inserida na *&#60; nome de base de dados >. &#60; nome da tabela ORC >*:</span><span class="sxs-lookup"><span data-stu-id="6d7f6-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="6d7f6-224">Depois de seguir este procedimento, deve ter uma tabela com dados no Olá ORC formato pronto toouse.</span><span class="sxs-lookup"><span data-stu-id="6d7f6-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
