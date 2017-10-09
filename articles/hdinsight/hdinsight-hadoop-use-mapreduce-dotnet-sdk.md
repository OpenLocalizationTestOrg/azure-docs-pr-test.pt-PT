---
title: as tarefas do MapReduce aaaSubmit utilizando o SDK .NET do HDInsight - Azure | Microsoft Docs
description: Saiba como toosubmit MapReduce tarefas tooAzure Hadoop do HDInsight utilizando o SDK .NET do HDInsight.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="e0e40-103">Executar tarefas de MapReduce com o SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e40-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="e0e40-104">Saiba como toosubmit MapReduce tarefas utilizando o SDK .NET do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0e40-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="e0e40-105">HDInsight clusters vêm com um ficheiro jar com alguns exemplos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e0e40-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="e0e40-106">é o ficheiro jar de Olá */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="e0e40-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="e0e40-107">Um dos exemplos de Olá é *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="e0e40-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="e0e40-108">Desenvolver uma c# consola aplicação toosubmit uma tarefa de wordcount.</span><span class="sxs-lookup"><span data-stu-id="e0e40-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="e0e40-109">tarefa de Olá lê Olá */example/data/gutenberg/davinci.txt* ficheiro e saídas Olá resultados demasiado*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="e0e40-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="e0e40-110">Se pretender que a aplicação de Olá toorerun, tem de limpar Olá pasta de saída.</span><span class="sxs-lookup"><span data-stu-id="e0e40-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e40-111">passos de Olá neste artigo devem ser executados a partir de um cliente Windows.</span><span class="sxs-lookup"><span data-stu-id="e0e40-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="e0e40-112">Para informações sobre como utilizar um Linux, OS X ou Unix cliente toowork com o Hive, utilize o Seletor de separador Olá apresentada na parte superior de Olá artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="e0e40-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e0e40-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0e40-113">Prerequisites</span></span>
<span data-ttu-id="e0e40-114">Antes de começar este artigo, tem de ter Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e0e40-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="e0e40-115">**Um cluster do Hadoop no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e0e40-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="e0e40-116">Consulte [começar a utilizar o Hadoop baseado em Linux no HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0e40-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="e0e40-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="e0e40-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="e0e40-118">Submeter tarefas de MapReduce com o SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e40-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="e0e40-119">Olá SDK .NET do HDInsight fornece bibliotecas de cliente .NET, que torna mais fácil toowork com clusters do HDInsight a partir do .NET.</span><span class="sxs-lookup"><span data-stu-id="e0e40-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="e0e40-120">**tarefas de tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="e0e40-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="e0e40-121">Crie uma aplicação de consola c# no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0e40-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="e0e40-122">A partir da consola do Gestor de pacotes Nuget Olá, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="e0e40-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="e0e40-123">Utilize Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="e0e40-123">Use hello following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="e0e40-124">Prima **F5** aplicação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="e0e40-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="e0e40-125">tarefa de Olá toorun novamente, tem de alterar Olá tarefa saída nome de pasta, no exemplo de Olá, é "/ dados/exemplo/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="e0e40-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="e0e40-126">Quando a tarefa de Olá for concluída com êxito, a aplicação Olá imprime conteúdo Olá Olá ficheiro de saída "parte-r-00000".</span><span class="sxs-lookup"><span data-stu-id="e0e40-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0e40-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e0e40-127">Next steps</span></span>
<span data-ttu-id="e0e40-128">Neste artigo, aprendeu a várias formas toocreate um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0e40-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="e0e40-129">toolearn mais, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="e0e40-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="e0e40-130">Para submeter uma tarefa do Hive, consulte [executar consultas do Hive com o SDK .NET do HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e0e40-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="e0e40-131">Para criar clusters do HDInsight, consulte [clusters do Hadoop baseados em criar Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e0e40-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="e0e40-132">Para gerir clusters do HDInsight, consulte [clusters do Hadoop gerir no HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e0e40-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="e0e40-133">Para aprender Olá SDK .NET do HDInsight, consulte [referência do SDK .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0e40-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="e0e40-134">Para não interativo autenticar tooAzure, consulte [criar aplicações do HDInsight de .NET de autenticação não interativa](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e0e40-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

