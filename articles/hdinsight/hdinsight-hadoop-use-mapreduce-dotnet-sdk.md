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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Executar tarefas de MapReduce com o SDK .NET do HDInsight
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Saiba como toosubmit MapReduce tarefas utilizando o SDK .NET do HDInsight. HDInsight clusters vêm com um ficheiro jar com alguns exemplos de MapReduce. é o ficheiro jar de Olá */example/jars/hadoop-mapreduce-examples.jar*.  Um dos exemplos de Olá é *wordcount*. Desenvolver uma c# consola aplicação toosubmit uma tarefa de wordcount.  tarefa de Olá lê Olá */example/data/gutenberg/davinci.txt* ficheiro e saídas Olá resultados demasiado*/example/data/davinciwordcount*.  Se pretender que a aplicação de Olá toorerun, tem de limpar Olá pasta de saída.

> [!NOTE]
> passos de Olá neste artigo devem ser executados a partir de um cliente Windows. Para informações sobre como utilizar um Linux, OS X ou Unix cliente toowork com o Hive, utilize o Seletor de separador Olá apresentada na parte superior de Olá artigo Olá.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, tem de ter Olá seguintes itens:

* **Um cluster do Hadoop no HDInsight**. Consulte [começar a utilizar o Hadoop baseado em Linux no HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Submeter tarefas de MapReduce com o SDK .NET do HDInsight
Olá SDK .NET do HDInsight fornece bibliotecas de cliente .NET, que torna mais fácil toowork com clusters do HDInsight a partir do .NET. 

**tarefas de tooSubmit**

1. Crie uma aplicação de consola c# no Visual Studio.
2. A partir da consola do Gestor de pacotes Nuget Olá, execute Olá os seguintes comandos:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Utilize Olá seguinte código:
   
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
4. Prima **F5** aplicação de Olá toorun.

tarefa de Olá toorun novamente, tem de alterar Olá tarefa saída nome de pasta, no exemplo de Olá, é "/ dados/exemplo/davinciwordcount".

Quando a tarefa de Olá for concluída com êxito, a aplicação Olá imprime conteúdo Olá Olá ficheiro de saída "parte-r-00000".

## <a name="next-steps"></a>Passos seguintes
Neste artigo, aprendeu a várias formas toocreate um cluster do HDInsight. toolearn mais, consulte Olá seguintes artigos:

* Para submeter uma tarefa do Hive, consulte [executar consultas do Hive com o SDK .NET do HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Para criar clusters do HDInsight, consulte [clusters do Hadoop baseados em criar Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Para gerir clusters do HDInsight, consulte [clusters do Hadoop gerir no HDInsight](hdinsight-administer-use-portal-linux.md).
* Para aprender Olá SDK .NET do HDInsight, consulte [referência do SDK .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).
* Para não interativo autenticar tooAzure, consulte [criar aplicações do HDInsight de .NET de autenticação não interativa](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

