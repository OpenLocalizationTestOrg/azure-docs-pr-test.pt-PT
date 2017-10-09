---
title: aaaUse Hive do Hadoop com o PowerShell no HDInsight - Azure | Microsoft Docs
description: Utilize consultas do PowerShell toorun do Hive no Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="1910c-103">Executar consultas do Hive com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1910c-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="1910c-104">Este documento fornece um exemplo de utilização do Azure PowerShell em consultas do Hive toorun de modo de grupo de recursos do Azure de Olá num Hadoop num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1910c-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1910c-105">Este documento não fornece uma descrição detalhada do que declarações HiveQL Olá que são utilizadas nos exemplos de Olá fazem.</span><span class="sxs-lookup"><span data-stu-id="1910c-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="1910c-106">Para obter informações sobre Olá HiveQL que é utilizada neste exemplo, consulte [utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="1910c-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="1910c-107">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="1910c-107">**Prerequisites**</span></span>

* <span data-ttu-id="1910c-108">**Um cluster do Azure HDInsight**: é irrelevante se o cluster de Olá é Windows ou baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="1910c-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1910c-109">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1910c-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1910c-110">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="1910c-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1910c-111">**Uma estação de trabalho com o Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1910c-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="1910c-112">Executar consultas do Hive com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1910c-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="1910c-113">O Azure PowerShell fornece *cmdlets* que permitem-lhe tooremotely executar as consultas do Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1910c-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="1910c-114">Internamente, cmdlets Olá efetuar chamadas REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) num cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="1910c-115">Olá cmdlets seguintes são utilizados quando executar consultas do Hive num cluster de HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="1910c-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="1910c-116">**Add-AzureRmAccount**: autentica o Azure PowerShell tooyour subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="1910c-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="1910c-117">**Novo AzureRmHDInsightHiveJobDefinition**: cria um *definição de tarefa* utilizando Olá especificado declarações HiveQL</span><span class="sxs-lookup"><span data-stu-id="1910c-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="1910c-118">**Início AzureRmHDInsightJob**: envia tooHDInsight de definição de tarefa Olá, inicia a tarefa de Olá e devolve um *tarefa* objetos que podem ser utilizados toocheck Olá estado da tarefa de Olá</span><span class="sxs-lookup"><span data-stu-id="1910c-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="1910c-119">**Espera-AzureRmHDInsightJob**: utiliza Olá tarefa toocheck Olá o estado do objeto de tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="1910c-120">Deve aguardar até concluir a tarefa de Olá ou excedido o tempo de espera de Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="1910c-121">**Get-AzureRmHDInsightJobOutput**: utilizada tooretrieve resultado Olá tarefa Olá</span><span class="sxs-lookup"><span data-stu-id="1910c-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="1910c-122">**AzureRmHDInsightHiveJob invocar**: utilizada toorun HiveQL instruções.</span><span class="sxs-lookup"><span data-stu-id="1910c-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="1910c-123">Esta consulta do cmdlet blocos Olá estiver concluída, em seguida, devolve resultados Olá</span><span class="sxs-lookup"><span data-stu-id="1910c-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="1910c-124">**Utilize AzureRmHDInsightCluster**: conjuntos Olá toouse de cluster atual para Olá **Invoke-AzureRmHDInsightHiveJob** comando</span><span class="sxs-lookup"><span data-stu-id="1910c-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="1910c-125">Olá passos seguintes demonstram como toouse toorun estes cmdlets uma tarefa no cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1910c-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="1910c-126">Com um editor, guardar Olá seguinte código como **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="1910c-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="1910c-127">Abra uma nova **Azure PowerShell** linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="1910c-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="1910c-128">Alterar a localização de toohello de diretórios de Olá **hivejob.ps1** de ficheiros, em seguida, utilize o seguinte script do comando toorun Olá de Olá:</span><span class="sxs-lookup"><span data-stu-id="1910c-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="1910c-129">Quando executa o script de Olá, é pedido tooenter Olá cluster nome e Olá HTTPS/Admin as credenciais da conta para o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="1910c-130">Também pode ser pedido toolog no tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1910c-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="1910c-131">Quando tiver concluído a tarefa de Olá, devolve toohello semelhante informações thext os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1910c-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="1910c-132">Conforme mencionado anteriormente, **Invoke-Hive** podem ser utilizado toorun uma consulta e aguardar resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="1910c-133">Utilize Olá toosee de script como funciona o Invoke-Hive os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1910c-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="1910c-134">saída de Olá aspeto Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="1910c-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="1910c-135">Para consultas de HiveQL maiores, pode utilizar Olá Azure PowerShell **aqui cadeias** cmdlet ou HiveQL ficheiros de script.</span><span class="sxs-lookup"><span data-stu-id="1910c-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="1910c-136">Olá seguinte fragmento mostra como toouse Olá **Invoke-Hive** cmdlet toorun um ficheiro de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="1910c-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="1910c-137">Olá HiveQL ficheiro de script tem de ser carregados toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="1910c-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="1910c-138">Para obter mais informações sobre **aqui cadeias**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">utilizando o Windows PowerShell aqui-cadeias</a>.</span><span class="sxs-lookup"><span data-stu-id="1910c-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1910c-139">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="1910c-139">Troubleshooting</span></span>

<span data-ttu-id="1910c-140">Se nenhuma informação é devolvida quando Olá tarefa é concluída, pode ter Ocorreu um erro durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="1910c-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="1910c-141">informações de erro tooview para esta tarefa de adicionar Olá seguir final toohello Olá **hivejob.ps1** ficheiro, guarde-o e, em seguida, execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="1910c-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="1910c-142">Este cmdlet devolve informações de Olá escrito tooSTDERR no servidor de Olá quando executou a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="1910c-143">Resumo</span><span class="sxs-lookup"><span data-stu-id="1910c-143">Summary</span></span>

<span data-ttu-id="1910c-144">Como pode ver, Azure PowerShell, fornece uma forma fácil toorun consultas do Hive num cluster do HDInsight, Olá monitor estado da tarefa e obter o resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="1910c-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1910c-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1910c-145">Next steps</span></span>

<span data-ttu-id="1910c-146">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1910c-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="1910c-147">Utilizar o Hive com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1910c-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="1910c-148">Para obter informações sobre outras formas pode trabalhar com o Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1910c-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1910c-149">Utilizar o Pig com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1910c-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1910c-150">Utilizar o MapReduce com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1910c-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
