---
title: aaaUse Hadoop o Pig com o SSH num cluster do HDInsight - Azure | Microsoft Docs
description: "Saiba como ligar o cluster de Hadoop baseado em Linux tooa com SSH e, em seguida, utilize Olá Pig comando toorun Pig Latin instruções interativamente, ou como um lote da tarefa."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="2f4b0-103">Executar tarefas do Pig num cluster baseado em Linux com Olá comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="2f4b0-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="2f4b0-104">Saiba como o toointeractively executar tarefas do Pig a partir de um cluster do HDInsight ligação SSH tooyour.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="2f4b0-105">Olá linguagem de programação do Pig Latin permite transformações de toodescribe que são aplicados toohello entrada dados tooproduce Olá pretendido saída.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f4b0-106">Olá passos neste documento exigem um cluster do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2f4b0-107">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2f4b0-108">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="2f4b0-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="2f4b0-109"><a id="ssh"></a>Ligar com SSH</span><span class="sxs-lookup"><span data-stu-id="2f4b0-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="2f4b0-110">Utilize o SSH tooconnect tooyour HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="2f4b0-111">Olá exemplo seguinte estabelece ligação com o nome de cluster de tooa **myhdinsight** como com o nome de conta de Olá **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="2f4b0-112">**Se forneceu uma chave de certificado para autenticação SSH** quando criou o cluster do HDInsight Olá, poderá ser necessário localização de Olá toospecify da chave privada Olá no seu sistema de cliente.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="2f4b0-113">**Se forneceu uma palavra-passe para autenticação SSH** quando criou o cluster do HDInsight Olá, forneça a palavra-passe Olá quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="2f4b0-114">Para obter mais informações sobre como utilizar o SSH com o HDInsight, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2f4b0-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="2f4b0-115"><a id="pig"></a>Utilize o comando de Pig Olá</span><span class="sxs-lookup"><span data-stu-id="2f4b0-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="2f4b0-116">Assim que estiver ligado, inicie o interface de linha de comandos de Pig Olá (CLI) utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="2f4b0-117">Depois de um momento, deve ver um `grunt>` linha.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="2f4b0-118">Introduza Olá a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="2f4b0-119">Este comando carrega Olá conteúdo de Olá sample.log ficheiro para os registos.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="2f4b0-120">Pode ver o conteúdo de Olá do ficheiro de Olá utilizando Olá a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="2f4b0-121">Em seguida, transformar dados de Olá aplicando um nível de registo de Olá apenas tooextract de expressão regular de cada registo utilizando Olá a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="2f4b0-122">Pode utilizar **informação do estado** dados de Olá tooview depois da transformação Olá.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="2f4b0-123">Neste caso, utilize `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="2f4b0-124">Continue a aplicar as transformações utilizando as instruções de Olá Olá a tabela seguinte:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="2f4b0-125">Declaração de PIg Latin</span><span class="sxs-lookup"><span data-stu-id="2f4b0-125">Pig Latin statement</span></span> | <span data-ttu-id="2f4b0-126">Instrução que Olá</span><span class="sxs-lookup"><span data-stu-id="2f4b0-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="2f4b0-127">Remove linhas que contêm um valor nulo para o nível de registo Olá e armazena os resultados de Olá para `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="2f4b0-128">Olá de grupos de linhas por nível de registo e armazena os resultados de Olá para `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="2f4b0-129">Cria um conjunto de dados que contém cada registo exclusivo ocorre valor nível e quantas vezes-lo.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="2f4b0-130">conjunto de dados de Olá é armazenado no `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="2f4b0-131">Ordena os níveis de registo de Olá por contagem (descendente) e armazena para `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="2f4b0-132">Utilize `DUMP` resultado de Olá tooview da transformação Olá depois de cada passo.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="2f4b0-133">Também pode guardar resultados de Olá de uma transformação utilizando Olá `STORE` instrução.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="2f4b0-134">Por exemplo, Olá seguinte declaração guarda Olá `RESULT` toohello `/example/data/pigout` diretório no armazenamento de predefinido Olá para o cluster:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="2f4b0-135">dados de Olá são armazenados no diretório especificado de Olá em ficheiros com o nome `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="2f4b0-136">Se já existe um diretório de Olá, receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="2f4b0-137">Olá tooexit grunt linha, introduza Olá a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="2f4b0-138">Ficheiros de batch de PIg Latin</span><span class="sxs-lookup"><span data-stu-id="2f4b0-138">Pig Latin batch files</span></span>

<span data-ttu-id="2f4b0-139">Também pode utilizar Olá Pig comando toorun Pig Latin contidos num ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="2f4b0-140">Depois de sair linha de grunt Olá, utilize seguinte de Olá comando toopipe STDIN num ficheiro denominado `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="2f4b0-141">Este ficheiro é criado no diretório raiz do Olá para Olá conta de utilizador SSH.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="2f4b0-142">Escreva ou cole Olá seguintes linhas e, em seguida, utilize Ctrl + D quando terminar.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="2f4b0-143">Seguinte de Olá utilize comando toorun Olá `pigbatch.pig` ficheiro utilizando o comando de Pig Olá.</span><span class="sxs-lookup"><span data-stu-id="2f4b0-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="2f4b0-144">Depois de concluída a tarefa de lote Olá, consulte Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="2f4b0-145"><a id="nextsteps"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2f4b0-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2f4b0-146">Para obter informações gerais sobre o Pig no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="2f4b0-147">Utilizar o Pig com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f4b0-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="2f4b0-148">Para obter mais informações sobre outra formas toowork com o Hadoop no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="2f4b0-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="2f4b0-149">Utilizar o Hive com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f4b0-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2f4b0-150">Utilizar o MapReduce com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f4b0-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
