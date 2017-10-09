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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Recolher informações de área dinâmica para dados no Blob storage toodebug e analisar os serviços do Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Área dinâmica para dados capturas contém um instantâneo de memória da aplicação Olá, incluindo valores de Olá das variáveis momento Olá informação Olá foi criada. Por isso, são úteis para diagnosticar problemas que ocorram em tempo de execução. Capturas de área dinâmica para dados podem ser automaticamente recolhidas para serviços do Hadoop e colocadas dentro de Olá conta de armazenamento de Blobs do Azure de um utilizador em HDInsightHeapDumps /.

coleção de Olá de capturas de área dinâmica para dados de vários serviços tem de estar ativada para os serviços em clusters individuais. predefinição de Olá para esta funcionalidade está toobe desativada para um cluster. Estas capturas de área dinâmica para dados podem ser grandes, pelo que é conta de armazenamento de BLOBs de Olá toomonitor recomendado onde estas são guardadas depois de coleção de Olá foi ativada.

> [!IMPORTANT]
> Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows). informações de Olá neste artigo aplica-se apenas HDInsight baseado em tooWindows. Para obter informações sobre o HDInsight baseado em Linux, consulte [informações de estado da área dinâmica para dados de ativação para os serviços do Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Serviços elegíveis para capturas de área dinâmica para dados
Pode ativar a área dinâmica para dados capturas de Olá os seguintes serviços:

* **hcatalog** -tempelton
* **ramo de registo** -hiveserver2, metastore, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager, nodemanager, timelineserver
* **hdfs** -datanode secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Elementos de configuração que permitem capturas de área dinâmica para dados
tooturn em capturas de área dinâmica para dados para um serviço, terá de elementos de configuração adequada Olá tooset na secção de Olá para esse serviço, o que é especificado por **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Olá valor **service_name** pode ser qualquer um dos serviços de Olá listados aqui: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, ou namenode.

## <a name="enable-using-azure-powershell"></a>Ativar a utilizar o Azure PowerShell
Por exemplo, tooturn em capturas de área dinâmica para dados utilizando o Azure PowerShell para jobhistoryserver, pode utilizar Olá seguintes script:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Ativar a utilizar o SDK do .NET
Por exemplo, tooturn em capturas de área dinâmica para dados utilizando Olá SDK .NET da Azure HDInsight para jobhistoryserver, pode utilizar Olá seguinte código:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
