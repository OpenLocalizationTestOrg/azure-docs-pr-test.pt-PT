---
title: "aaaDebug e analisar os serviços de Hadoop com capturas de área dinâmica para dados - Azure | Microsoft Docs"
description: "Recolher informações de área dinâmica para dados de serviços do Hadoop e coloque dentro Olá conta de armazenamento de Blobs do Azure para depuração e de análise automaticamente."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="fcfb5-103">Recolher informações de área dinâmica para dados no Blob storage toodebug e analisar os serviços do Hadoop</span><span class="sxs-lookup"><span data-stu-id="fcfb5-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="fcfb5-104">Área dinâmica para dados capturas contém um instantâneo de memória da aplicação Olá, incluindo valores de Olá das variáveis momento Olá informação Olá foi criada.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="fcfb5-105">Por isso, são úteis para diagnosticar problemas que ocorram em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="fcfb5-106">Capturas de área dinâmica para dados podem ser automaticamente recolhidas para serviços do Hadoop e colocadas dentro de Olá conta de armazenamento de Blobs do Azure de um utilizador em HDInsightHeapDumps /.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="fcfb5-107">coleção de Olá de capturas de área dinâmica para dados de vários serviços tem de estar ativada para os serviços em clusters individuais.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="fcfb5-108">predefinição de Olá para esta funcionalidade está toobe desativada para um cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="fcfb5-109">Estas capturas de área dinâmica para dados podem ser grandes, pelo que é conta de armazenamento de BLOBs de Olá toomonitor recomendado onde estas são guardadas depois de coleção de Olá foi ativada.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcfb5-110">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fcfb5-111">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="fcfb5-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="fcfb5-112">informações de Olá neste artigo aplica-se apenas HDInsight baseado em tooWindows.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="fcfb5-113">Para obter informações sobre o HDInsight baseado em Linux, consulte [informações de estado da área dinâmica para dados de ativação para os serviços do Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb5-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="fcfb5-114">Serviços elegíveis para capturas de área dinâmica para dados</span><span class="sxs-lookup"><span data-stu-id="fcfb5-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="fcfb5-115">Pode ativar a área dinâmica para dados capturas de Olá os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="fcfb5-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="fcfb5-116">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="fcfb5-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="fcfb5-117">**ramo de registo** -hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="fcfb5-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="fcfb5-118">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="fcfb5-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="fcfb5-119">**yarn** -resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="fcfb5-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="fcfb5-120">**hdfs** -datanode secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="fcfb5-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="fcfb5-121">Elementos de configuração que permitem capturas de área dinâmica para dados</span><span class="sxs-lookup"><span data-stu-id="fcfb5-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="fcfb5-122">tooturn em capturas de área dinâmica para dados para um serviço, terá de elementos de configuração adequada Olá tooset na secção de Olá para esse serviço, o que é especificado por **service_name**.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="fcfb5-123">Olá valor **service_name** pode ser qualquer um dos serviços de Olá listados aqui: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, ou namenode.</span><span class="sxs-lookup"><span data-stu-id="fcfb5-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="fcfb5-124">Ativar a utilizar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcfb5-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="fcfb5-125">Por exemplo, tooturn em capturas de área dinâmica para dados utilizando o Azure PowerShell para jobhistoryserver, pode utilizar Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="fcfb5-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="fcfb5-126">Ativar a utilizar o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="fcfb5-126">Enable using .NET SDK</span></span>
<span data-ttu-id="fcfb5-127">Por exemplo, tooturn em capturas de área dinâmica para dados utilizando Olá SDK .NET da Azure HDInsight para jobhistoryserver, pode utilizar Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="fcfb5-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
