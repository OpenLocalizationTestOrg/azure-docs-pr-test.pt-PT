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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="5845c-103">Executar tarefas do Pig utilizando Olá .NET SDK para o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5845c-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="5845c-104">Saiba como toouse Olá .NET SDK para toosubmit Hadoop Apache Pig tarefas tooHadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5845c-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="5845c-105">Olá SDK .NET do HDInsight fornece bibliotecas de cliente do .NET que torna mais fácil toowork com clusters do HDInsight a partir do .NET.</span><span class="sxs-lookup"><span data-stu-id="5845c-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="5845c-106">PIg permite operações de MapReduce toocreate por uma série de transformações de dados de modelação.</span><span class="sxs-lookup"><span data-stu-id="5845c-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="5845c-107">Neste documento, saiba como toouse um básico c# aplicação toosubmit um Pig tarefa tooan cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5845c-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5845c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5845c-108">Prerequisites</span></span>

<span data-ttu-id="5845c-109">toocomplete Olá passos descritos neste artigo, terá de seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="5845c-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="5845c-110">Um cluster do Azure HDInsight (Hadoop no HDInsight) (ou Windows ou baseado em Linux).</span><span class="sxs-lookup"><span data-stu-id="5845c-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5845c-111">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="5845c-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5845c-112">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="5845c-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5845c-113">Visual Studio 2012 2013, 2015 ou de 2017.</span><span class="sxs-lookup"><span data-stu-id="5845c-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="5845c-114">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="5845c-114">Create hello application</span></span>

<span data-ttu-id="5845c-115">Olá SDK .NET do HDInsight fornece bibliotecas de cliente .NET, que torna mais fácil toowork com clusters do HDInsight a partir do .NET.</span><span class="sxs-lookup"><span data-stu-id="5845c-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="5845c-116">De Olá **ficheiro** menu no Visual Studio, selecione **novo** e, em seguida, selecione **projeto**.</span><span class="sxs-lookup"><span data-stu-id="5845c-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="5845c-117">Para o novo projeto Olá, tipo ou selecione Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="5845c-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="5845c-118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5845c-118">Property</span></span> | <span data-ttu-id="5845c-119">Valor</span><span class="sxs-lookup"><span data-stu-id="5845c-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="5845c-120">Categoria</span><span class="sxs-lookup"><span data-stu-id="5845c-120">Category</span></span> | <span data-ttu-id="5845c-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="5845c-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="5845c-122">Modelo</span><span class="sxs-lookup"><span data-stu-id="5845c-122">Template</span></span> | <span data-ttu-id="5845c-123">Aplicação de Consola</span><span class="sxs-lookup"><span data-stu-id="5845c-123">Console Application</span></span> |
   | <span data-ttu-id="5845c-124">Nome</span><span class="sxs-lookup"><span data-stu-id="5845c-124">Name</span></span> | <span data-ttu-id="5845c-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="5845c-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="5845c-126">Clique em **OK** projeto de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="5845c-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="5845c-127">De Olá **ferramentas** menu, selecione **Gestor de pacotes de biblioteca** ou **Gestor de pacotes Nuget**e, em seguida, selecione **consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="5845c-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="5845c-128">pacotes de .NET SDK do tooinstall Olá, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5845c-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="5845c-129">A partir do Explorador de soluções, faça duplo clique em **Program.cs** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="5845c-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="5845c-130">Substitua o código existente Olá pelo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="5845c-130">Replace hello existing code with hello following.</span></span>

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

7. <span data-ttu-id="5845c-131">aplicação de Olá toostart, prima **F5**.</span><span class="sxs-lookup"><span data-stu-id="5845c-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="5845c-132">aplicação de Olá tooexit, prima **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="5845c-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="5845c-133">Resumo</span><span class="sxs-lookup"><span data-stu-id="5845c-133">Summary</span></span>

<span data-ttu-id="5845c-134">Como pode ver, Olá SDK .NET para o Hadoop permite-lhe toocreate aplicações de .NET que submetem cluster do HDInsight Pig tarefas tooan e monitorizar o estado da tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="5845c-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5845c-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5845c-135">Next steps</span></span>

<span data-ttu-id="5845c-136">Para obter informações sobre o Pig no HDInsight, consulte [utilizar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="5845c-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="5845c-137">Para obter mais informações sobre como utilizar o Hadoop no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="5845c-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="5845c-138">Utilizar o Hive com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5845c-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5845c-139">Utilizar o MapReduce com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5845c-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
