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
# <a name="run-hive-queries-using-powershell"></a>Executar consultas do Hive com o PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Este documento fornece um exemplo de utilização do Azure PowerShell em consultas do Hive toorun de modo de grupo de recursos do Azure de Olá num Hadoop num cluster do HDInsight.

> [!NOTE]
> Este documento não fornece uma descrição detalhada do que declarações HiveQL Olá que são utilizadas nos exemplos de Olá fazem. Para obter informações sobre Olá HiveQL que é utilizada neste exemplo, consulte [utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md).

**Pré-requisitos**

* **Um cluster do Azure HDInsight**: é irrelevante se o cluster de Olá é Windows ou baseado em Linux.

  > [!IMPORTANT]
  > Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

* **Uma estação de trabalho com o Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Executar consultas do Hive com o Azure PowerShell

O Azure PowerShell fornece *cmdlets* que permitem-lhe tooremotely executar as consultas do Hive no HDInsight. Internamente, cmdlets Olá efetuar chamadas REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) num cluster do HDInsight Olá.

Olá cmdlets seguintes são utilizados quando executar consultas do Hive num cluster de HDInsight remoto:

* **Add-AzureRmAccount**: autentica o Azure PowerShell tooyour subscrição do Azure
* **Novo AzureRmHDInsightHiveJobDefinition**: cria um *definição de tarefa* utilizando Olá especificado declarações HiveQL
* **Início AzureRmHDInsightJob**: envia tooHDInsight de definição de tarefa Olá, inicia a tarefa de Olá e devolve um *tarefa* objetos que podem ser utilizados toocheck Olá estado da tarefa de Olá
* **Espera-AzureRmHDInsightJob**: utiliza Olá tarefa toocheck Olá o estado do objeto de tarefa Olá. Deve aguardar até concluir a tarefa de Olá ou excedido o tempo de espera de Olá.
* **Get-AzureRmHDInsightJobOutput**: utilizada tooretrieve resultado Olá tarefa Olá
* **AzureRmHDInsightHiveJob invocar**: utilizada toorun HiveQL instruções. Esta consulta do cmdlet blocos Olá estiver concluída, em seguida, devolve resultados Olá
* **Utilize AzureRmHDInsightCluster**: conjuntos Olá toouse de cluster atual para Olá **Invoke-AzureRmHDInsightHiveJob** comando

Olá passos seguintes demonstram como toouse toorun estes cmdlets uma tarefa no cluster do HDInsight:

1. Com um editor, guardar Olá seguinte código como **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Abra uma nova **Azure PowerShell** linha de comandos. Alterar a localização de toohello de diretórios de Olá **hivejob.ps1** de ficheiros, em seguida, utilize o seguinte script do comando toorun Olá de Olá:

        .\hivejob.ps1

    Quando executa o script de Olá, é pedido tooenter Olá cluster nome e Olá HTTPS/Admin as credenciais da conta para o cluster de Olá. Também pode ser pedido toolog no tooyour subscrição do Azure.

3. Quando tiver concluído a tarefa de Olá, devolve toohello semelhante informações thext os seguintes:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Conforme mencionado anteriormente, **Invoke-Hive** podem ser utilizado toorun uma consulta e aguardar resposta Olá. Utilize Olá toosee de script como funciona o Invoke-Hive os seguintes:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    saída de Olá aspeto Olá seguinte texto:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Para consultas de HiveQL maiores, pode utilizar Olá Azure PowerShell **aqui cadeias** cmdlet ou HiveQL ficheiros de script. Olá seguinte fragmento mostra como toouse Olá **Invoke-Hive** cmdlet toorun um ficheiro de script de HiveQL. Olá HiveQL ficheiro de script tem de ser carregados toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Para obter mais informações sobre **aqui cadeias**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">utilizando o Windows PowerShell aqui-cadeias</a>.

## <a name="troubleshooting"></a>Resolução de problemas

Se nenhuma informação é devolvida quando Olá tarefa é concluída, pode ter Ocorreu um erro durante o processamento. informações de erro tooview para esta tarefa de adicionar Olá seguir final toohello Olá **hivejob.ps1** ficheiro, guarde-o e, em seguida, execute-o novamente.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Este cmdlet devolve informações de Olá escrito tooSTDERR no servidor de Olá quando executou a tarefa de Olá.

## <a name="summary"></a>Resumo

Como pode ver, Azure PowerShell, fornece uma forma fácil toorun consultas do Hive num cluster do HDInsight, Olá monitor estado da tarefa e obter o resultado de Olá.

## <a name="next-steps"></a>Passos seguintes

Para obter informações gerais sobre o Hive no HDInsight:

* [Utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter informações sobre outras formas pode trabalhar com o Hadoop no HDInsight:

* [Utilizar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md)
* [Utilizar o MapReduce com o Hadoop no HDInsight](hdinsight-use-mapreduce.md)
