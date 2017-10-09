---
title: aaaRun Sqoop tarefas utilizando o .NET e o HDInsight - Azure | Microsoft Docs
description: Saiba como toouse SDK .NET do HDInsight toorun Sqoop importar e exportar entre um cluster do Hadoop e uma base de dados SQL do Azure.
keywords: tarefa de sqoop
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="b0e1a-104">Executar tarefas de Sqoop utilizando o .NET SDK para o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0e1a-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="b0e1a-105">Saiba como toouse SDK .NET do HDInsight toorun Sqoop tarefas no HDInsight tooimport e exportar entre o cluster do HDInsight e a SQL database do Azure ou a base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="b0e1a-106">passos de Olá neste artigo podem ser utilizados com qualquer um baseado em Windows ou Linux cluster HDInsight; No entanto, estes passos apenas trabalham a partir de um cliente Windows.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="b0e1a-107">Utilize o Seletor de separador Olá no Olá parte superior do toochoose artigo outros métodos.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="b0e1a-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0e1a-108">Prerequisites</span></span>
<span data-ttu-id="b0e1a-109">Antes de começar este tutorial, tem de ter Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b0e1a-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="b0e1a-110">**Um cluster do Hadoop no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="b0e1a-111">Consulte [criar o cluster e a SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="b0e1a-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="b0e1a-112">Utilizar o Sqoop nos clusters do HDInsight com o .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b0e1a-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="b0e1a-113">Olá SDK .NET do HDInsight fornece bibliotecas de cliente .NET, que torna mais fácil toowork com clusters do HDInsight a partir do .NET.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="b0e1a-114">Nesta secção, pode cria uma c# consola aplicação tooexport Olá hivesampletable toohello base de dados SQL tabela que criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="b0e1a-115">Submeter uma tarefa de Sqoop</span><span class="sxs-lookup"><span data-stu-id="b0e1a-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="b0e1a-116">Crie uma aplicação de consola c# no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="b0e1a-117">A partir da consola do Gestor de pacotes do Visual Studio Olá, execute Olá seguir o pacote do Nuget comando tooimport Olá.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="b0e1a-118">Utilize o seguinte código no ficheiro Program.cs de Olá de Olá:</span><span class="sxs-lookup"><span data-stu-id="b0e1a-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="b0e1a-119">Prima **F5** programa de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="b0e1a-120">Limitações</span><span class="sxs-lookup"><span data-stu-id="b0e1a-120">Limitations</span></span>
* <span data-ttu-id="b0e1a-121">Exportação em massa - baseado em Linux com o HDInsight, Olá Sqoop conetor utilizado tooexport dados tooMicrosoft do SQL Server ou SQL Database do Azure não suporta atualmente inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="b0e1a-122">Criação de batches - com o HDInsight baseado em Linux, ao utilizar Olá `-batch` mudar quando efetuar inserções, Sqoop efetua várias inserções em vez de criação de batches de operações de inserção de Olá.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0e1a-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b0e1a-123">Next steps</span></span>
<span data-ttu-id="b0e1a-124">Agora que aprendeu como toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="b0e1a-125">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="b0e1a-125">toolearn more, see:</span></span>

* <span data-ttu-id="b0e1a-126">[Utilizar o Oozie com o HDInsight](hdinsight-use-oozie.md): Utilize Sqoop ação um fluxo de trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="b0e1a-127">[Analisar dados de atraso de voo utilizando HDInsight](hdinsight-analyze-flight-delay-data.md): utilizar o Hive voo de tooanalyze atrasar dados e, em seguida, utilizar o Sqoop tooexport dados tooan SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="b0e1a-128">[Carregar dados tooHDInsight](hdinsight-upload-data.md): localizar outros métodos para carregar o armazenamento de Blobs do tooHDInsight/Azure de dados.</span><span class="sxs-lookup"><span data-stu-id="b0e1a-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

