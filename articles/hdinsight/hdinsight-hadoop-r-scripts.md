---
title: aaaUse R nos clusters do HDInsight toocustomize - Azure | Microsoft Docs
description: "Saiba como utilizar tooinstall R Script ação e utilize R nos clusters do HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Instalar e utilizar R em clusters do HDInsight Hadoop

Saiba como toocustomize Windows com base em cluster do HDInsight com R através da ação de Script e como clusters toouse R no HDInsight. Olá [HDInsight oferta](https://azure.microsoft.com/pricing/details/hdinsight/) inclui o R Server como parte do cluster do HDInsight. Isto permite que os scripts de R toouse MapReduce e Spark computações toorun distribuído. Para obter mais informações, consulte [Começar a utilizar o Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md). Para obter informações sobre como utilizar o R com um cluster baseado em Linux, consulte [instalar e utilizar R na clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md).

Pode instalar o R qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight utilizando *ação de Script*. Um exemplo tooinstall script R num cluster do HDInsight está disponível a partir de um blob de armazenamento do Azure só de leitura em [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Artigos relacionados**

* [Instalar e utilizar o R em clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Criar clusters do Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre a criação de clusters do HDInsight
* [Personalizar clusters do HDInsight através da ação de Script][hdinsight-cluster-customize]: informações gerais sobre a personalização clusters do HDInsight através da ação de Script
* [Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>O que é R?
Olá <a href="http://www.r-project.org/" target="_blank">R projeto para o cálculo estatístico</a> é um ambiente para o cálculo estatístico e abra idioma da origem. R fornece centenas de compilação no funções estatísticas e a suas próprias linguagem de programação que combina aspetos funciona e orientado para objetos de programação. Também fornece extensas capacidades de gráficas. R é Olá preferencial programação ambiente quanto mais profissionais statisticians e cientistas numa grande variedade de campos.

R é compatível com o armazenamento de Blobs do Azure (WASB), para que os dados armazenados existe podem ser processados utilizando R no HDInsight.  

## <a name="install-r"></a>Instalar o R
A [script de exemplo](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R num cluster do HDInsight está disponível a partir de um blob só de leitura no armazenamento do Azure. Esta secção fornece instruções sobre como toouse Olá script de exemplo ao criar o cluster de Olá utilizando Olá Portal do Azure.

> [!NOTE]
> script de exemplo de Olá foi introduzido com clusters do HDInsight versão 3.1. Para mais informações sobre as versões de cluster do HDInsight, consulte [as versões de cluster do HDInsight](hdinsight-component-versioning.md).
>
>

1. Quando criar um cluster do HDInsight a partir Olá Portal, clique em **configuração opcional**e, em seguida, clique em **ações de Script**.
2. No Olá **ações de Script** página, introduza Olá os seguintes valores:

    ![Utilize a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize de ação de Script de utilizar um cluster")

    <table border='1'>
        <tr><th>Propriedade</th><th>Valor</th></tr>
        <tr><td>Nome</td>
            <td>Especifique um nome para a ação de script de Olá, por exemplo, <b>instalar R</b>.</td></tr>
        <tr><td>URI de script</td>
            <td>Especifique Olá URI toohello script que é o cluster de Olá toocustomize invocado, por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Tipo de Nó</td>
            <td>Especifique nós de Olá no qual o script de personalização de Olá é executado. Pode escolher <b>todos os nós</b>, <b>apenas nós principais</b>, ou <b>nós de trabalho</b> apenas.
        <tr><td>Parâmetros</td>
            <td>Especifique parâmetros de Olá, se necessário pelo script de Olá. No entanto, Olá tooinstall de script R não requer quaisquer parâmetros, pelo que pode deixar isto em branco.</td></tr>
    </table>

    Pode adicionar mais do que um tooinstall de ação de script vários componentes no cluster de Olá. Depois de ter adicionado scripts Olá, clique em Olá marca de verificação toostart crating cluster Olá.

Também pode utilizar Olá script tooinstall R no HDInsight ao utilizar o Azure PowerShell ou Olá SDK .NET do HDInsight. Neste artigo, são fornecidas instruções para estes procedimentos.

## <a name="run-r-scripts"></a>Executar scripts de R
Esta secção descreve como toorun um R script no Olá Hadoop cluster com o HDInsight.

1. **Estabelecer um cluster de toohello de ligação de ambiente de trabalho remoto**: Olá Portal, ativar o ambiente de trabalho remoto para o cluster de Olá que criou com o R instalado e, em seguida, ligue o cluster de toohello. Para obter instruções, consulte [ligar a clusters tooHDInsight através de RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Consola aberta Olá R**: instalação Olá R coloca uma consola de toohello R de ligação no ambiente de trabalho de Olá do nó principal Olá. Clique na mesma consola de Olá R tooopen.
3. **Executar script de Olá R**: script Olá R pode ser executado diretamente a partir da consola de Olá R colando-lo, selecionando-e premindo ENTER. Eis um script de exemplo simples que gera Olá too100 de números entre 1 e, em seguida, multiplica-los por 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Olá as primeiras duas linhas chamada Olá RHadoop bibliotecas que estão instaladas com o R. Olá linha final impressões Olá resultados toohello consola. saída de Olá deve ter o seguinte aspeto:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Instalar o R com o Azure PowerShell
Consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemplo de Olá demonstra como tooinstall Spark com o Azure PowerShell. Terá de toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Instalar o R com o .NET SDK
Consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemplo de Olá demonstra como tooinstall Spark utilizando Olá .NET SDK. Terá de toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Consultar também
* [Instalar e utilizar o R em clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Criar clusters do Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre a criação de clusters do HDInsight
* [Personalizar clusters do HDInsight através da ação de Script][hdinsight-cluster-customize]: informações gerais sobre a personalização clusters do HDInsight através da ação de Script
* [Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)
* [Instalar e utilizar o Spark nos clusters do HDInsight][hdinsight-install-spark]: exemplo de ação de Script sobre a instalação do Spark
* [Instalar Giraph nos clusters do HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de ação de Script sobre como instalar Giraph
* [Instalar Solr nos clusters do HDInsight](hdinsight-hadoop-solr-install-linux.md): exemplo de ação de Script sobre como instalar Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
