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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Executar tarefas de Sqoop utilizando o .NET SDK para o Hadoop no HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Saiba como toouse SDK .NET do HDInsight toorun Sqoop tarefas no HDInsight tooimport e exportar entre o cluster do HDInsight e a SQL database do Azure ou a base de dados do SQL Server.

> [!NOTE]
> passos de Olá neste artigo podem ser utilizados com qualquer um baseado em Windows ou Linux cluster HDInsight; No entanto, estes passos apenas trabalham a partir de um cliente Windows. Utilize o Seletor de separador Olá no Olá parte superior do toochoose artigo outros métodos.
> 
> 

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, tem de ter Olá seguintes itens:

* **Um cluster do Hadoop no HDInsight**. Consulte [criar o cluster e a SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Utilizar o Sqoop nos clusters do HDInsight com o .NET SDK
Olá SDK .NET do HDInsight fornece bibliotecas de cliente .NET, que torna mais fácil toowork com clusters do HDInsight a partir do .NET. Nesta secção, pode cria uma c# consola aplicação tooexport Olá hivesampletable toohello base de dados SQL tabela que criou anteriormente neste tutorial.

## <a name="submit-a-sqoop-job"></a>Submeter uma tarefa de Sqoop

1. Crie uma aplicação de consola c# no Visual Studio.
2. A partir da consola do Gestor de pacotes do Visual Studio Olá, execute Olá seguir o pacote do Nuget comando tooimport Olá.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Utilize o seguinte código no ficheiro Program.cs de Olá de Olá:
   
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
4. Prima **F5** programa de Olá toorun. 

## <a name="limitations"></a>Limitações
* Exportação em massa - baseado em Linux com o HDInsight, Olá Sqoop conetor utilizado tooexport dados tooMicrosoft do SQL Server ou SQL Database do Azure não suporta atualmente inserções em massa.
* Criação de batches - com o HDInsight baseado em Linux, ao utilizar Olá `-batch` mudar quando efetuar inserções, Sqoop efetua várias inserções em vez de criação de batches de operações de inserção de Olá.

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu como toouse Sqoop. toolearn mais, consulte:

* [Utilizar o Oozie com o HDInsight](hdinsight-use-oozie.md): Utilize Sqoop ação um fluxo de trabalho do Oozie.
* [Analisar dados de atraso de voo utilizando HDInsight](hdinsight-analyze-flight-delay-data.md): utilizar o Hive voo de tooanalyze atrasar dados e, em seguida, utilizar o Sqoop tooexport dados tooan SQL database do Azure.
* [Carregar dados tooHDInsight](hdinsight-upload-data.md): localizar outros métodos para carregar o armazenamento de Blobs do tooHDInsight/Azure de dados.

