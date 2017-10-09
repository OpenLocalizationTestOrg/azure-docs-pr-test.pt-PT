---
title: tarefas de aaaRun Apache Pig com o .NET SDK de Hadoop - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá .NET SDK para tooHadoop tarefas de Pig de toosubmit do Hadoop no HDInsight."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Executar tarefas do Pig utilizando Olá .NET SDK para o Hadoop no HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Saiba como toouse Olá .NET SDK para toosubmit Hadoop Apache Pig tarefas tooHadoop no Azure HDInsight.

Olá SDK .NET do HDInsight fornece bibliotecas de cliente do .NET que torna mais fácil toowork com clusters do HDInsight a partir do .NET. PIg permite operações de MapReduce toocreate por uma série de transformações de dados de modelação. Neste documento, saiba como toouse um básico c# aplicação toosubmit um Pig tarefa tooan cluster do HDInsight.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete Olá passos descritos neste artigo, terá de seguinte Olá.

* Um cluster do Azure HDInsight (Hadoop no HDInsight) (ou Windows ou baseado em Linux).

  > [!IMPORTANT]
  > Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

* Visual Studio 2012 2013, 2015 ou de 2017.

## <a name="create-hello-application"></a>Criar aplicação Olá

Olá SDK .NET do HDInsight fornece bibliotecas de cliente .NET, que torna mais fácil toowork com clusters do HDInsight a partir do .NET.

1. De Olá **ficheiro** menu no Visual Studio, selecione **novo** e, em seguida, selecione **projeto**.

2. Para o novo projeto Olá, tipo ou selecione Olá os seguintes valores:

   | Propriedade | Valor |
   | ------ | ------ |
   | Categoria | Templates/Visual C#/Windows |
   | Modelo | Aplicação de Consola |
   | Nome | SubmitPigJob |

3. Clique em **OK** projeto de Olá toocreate.

4. De Olá **ferramentas** menu, selecione **Gestor de pacotes de biblioteca** ou **Gestor de pacotes Nuget**e, em seguida, selecione **consola do Gestor de pacotes**.

5. pacotes de .NET SDK do tooinstall Olá, utilize Olá os seguintes comandos:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. A partir do Explorador de soluções, faça duplo clique em **Program.cs** tooopen-lo. Substitua o código existente Olá pelo seguinte Olá.

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. aplicação de Olá toostart, prima **F5**.

8. aplicação de Olá tooexit, prima **ENTER**.

## <a name="summary"></a>Resumo

Como pode ver, Olá SDK .NET para o Hadoop permite-lhe toocreate aplicações de .NET que submetem cluster do HDInsight Pig tarefas tooan e monitorizar o estado da tarefa Olá.

## <a name="next-steps"></a>Passos seguintes

Para obter informações sobre o Pig no HDInsight, consulte [utilizar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md).

Para obter mais informações sobre como utilizar o Hadoop no HDInsight, consulte Olá seguintes documentos:

* [Utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md)
* [Utilizar o MapReduce com o Hadoop no HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
