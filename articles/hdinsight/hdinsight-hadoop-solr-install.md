---
title: "aaaUse ação de Script tooinstall Solr no cluster de Hadoop - Azure | Microsoft Docs"
description: "Saiba como toocustomize HDInsight cluster com Solr através da ação de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Instalar e utilizar Solr nos clusters do HDInsight baseados em Windows

Saiba como toocustomize HDInsight baseado em Windows cluster com Solr através da ação de Script e como toouse Solr toosearch dados.

> [!IMPORTANT]
> passos seguintes Olá em projetos de apenas este documento com clusters do HDInsight baseados em Windows. HDInsight só está disponível no Windows para as versões inferiores ao HDInsight 3.4. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows). Para obter informações sobre a utilização Solr com um cluster baseado em Linux, consulte [instalar e utilizar Solr nos clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).


Pode instalar Solr em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight utilizando *ação de Script*. Um tooinstall de script de exemplo Solr num cluster do HDInsight está disponível a partir de um blob de armazenamento do Azure só de leitura em [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

script de exemplo de Olá funciona apenas com clusters do HDInsight versão 3.1. Para obter mais informações sobre as versões de cluster do HDInsight, consulte [as versões de cluster do HDInsight](hdinsight-component-versioning.md).

script de exemplo de Olá utilizado neste tópico cria um cluster de Solr baseado no Windows com uma configuração específica. Se pretender que o cluster de Solr Olá tooconfigure com diferentes coleções, shards, esquemas, as réplicas, etc., tem de modificar o script de Olá e binários Solr em conformidade.

**Artigos relacionados**

* [Instalar e utilizar Solr em clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Criar clusters do Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre a criação de clusters do HDInsight.
* [Personalizar clusters do HDInsight através da ação de Script][hdinsight-cluster-customize]: informações gerais sobre a personalização clusters do HDInsight através da ação de Script.
* [Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>O que é Solr?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> é uma plataforma de pesquisa de empresa que lhe permite poderosa pesquisa em texto completo em dados. Enquanto Hadoop permite armazenar e gerir grandes quantidades de dados, Apache Solr fornece capacidades de pesquisa de Olá dados de Olá tooquickly obter.

## <a name="install-solr-using-portal"></a>Instalar Solr através do portal
1. Iniciar criação de um cluster utilizando Olá **criação personalizada** opção, conforme descrito em [clusters do Hadoop criar no HDInsight](hdinsight-provision-clusters.md).
2. No Olá **ações de Script** página do Assistente de Olá, clique em **adicionar ação de script** tooprovide detalhes sobre a ação de script de Olá, conforme mostrado abaixo:

    ![Utilize a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize de ação de Script de utilizar um cluster")

    <table border='1'>
        <tr><th>Propriedade</th><th>Valor</th></tr>
        <tr><td>Nome</td>
            <td>Especifique um nome para a ação de script de Olá. Por exemplo, <b>instalar Solr</b>.</td></tr>
        <tr><td>URI de script</td>
            <td>Especifique Olá Uniform Resource Identifier (URI) toohello script que é invocada toocustomize Olá cluster. Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Tipo de Nó</td>
            <td>Especifique nós de Olá no qual o script de personalização de Olá é executado. Pode escolher <b>todos os nós</b>, <b>apenas nós principais</b>, ou <b>apenas nós de trabalho</b>.
        <tr><td>Parâmetros</td>
            <td>Especifique parâmetros de Olá, se necessário pelo script de Olá. Olá script tooinstall Solr não requer quaisquer parâmetros, pelo que pode deixar isto em branco.</td></tr>
    </table>

    Pode adicionar mais do que um tooinstall de ação de script vários componentes no cluster de Olá. Depois de ter adicionado scripts Olá, clique em Olá marca de verificação toostart Criar cluster Olá.

## <a name="use-solr"></a>Utilizar Solr
Tem de começar com indexação Solr com alguns ficheiros de dados. Em seguida, pode utilizar consultas de pesquisa de toorun Solr nos dados de Olá indexada. Execute Olá os seguintes passos toouse Solr de um cluster do HDInsight:

1. **Utilizar tooremote do protocolo RDP (Remote Desktop Protocol) no cluster do HDInsight Olá com Solr instalado**. Do portal do Azure Olá, ative o ambiente de trabalho remoto para o cluster de Olá que criou com o cluster de Olá instalado e, em seguida, remotamente Solr. Para obter instruções, consulte [ligar a clusters tooHDInsight através de RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Solr índice através do carregamento de ficheiros de dados**. Quando o índice Solr, coloque documentos no mesmo que poderá ser necessário toosearch no. tooindex Solr, utilize RDP tooremote num cluster de Olá, navegue até toohello ambiente de trabalho, abra a linha de comandos do Hadoop Olá e navegue demasiado**C:\apps\dist\solr-4.7.2\example\exampledocs**. Execute Olá os seguintes comandos:

        java -jar post.jar solr.xml monitor.xml

    Verá Olá seguinte resultado na consola de Olá:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    utilitário de post.jar Olá indexa Solr com dois documentos de exemplo, **solr.xml** e **monitor.xml**. utilitário de post.jar Olá e os documentos de exemplo de Olá estão disponíveis com a instalação de Solr.
3. **Utilize Olá Solr dashboard toosearch dentro Olá indexar documentos**. No Olá RDP sessão toohello HDInsight cluster, abra o Internet Explorer e iniciar o dashboard de Solr Olá em **http://headnodehost:8983/solr / #/**. No painel esquerdo Olá, de Olá **Core Seletor** pendente, selecione **collection1**e em que, clique em **consulta**. Como exemplo, tooselect e devolver todos os documentos de Olá no Solr, fornecer Olá os seguintes valores:

   * No Olá **q** texto, introduza  **\*:**\*. Esta ação irá devolver todos os documentos de Olá que são indexados no Solr. Se pretender toosearch para uma cadeia específica dentro de documentos Olá, pode introduzir essa cadeia aqui.
   * No Olá **wt** caixa de texto, selecione Olá formato de saída. Predefinição é **json**. Clique em **executar a consulta**.

     ![Utilize a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "executar uma consulta num Solr dashboard")

     saída de Olá devolve Olá dois documentos que utilizámos para Solr indexação. saída de Olá é semelhante a seguinte Olá:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Recomendado: Cópia de segurança Olá indexada dados a partir de Solr tooAzure armazenamento de BLOBs associado ao cluster de HDInsight Olá**. Como uma boa prática, deve copiar em segurança dados Olá indexada de nós de cluster Solr Olá no Blob storage do Azure. Execute Olá, por isso, os seguintes passos toodo:

   1. A partir de sessão do RDP Olá, abra o Internet Explorer e toohello ponto seguinte URL:

           http://localhost:8983/solr/replication?command=backup

       Deverá ver uma resposta como esta:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. Na sessão remota Olá, navegue demasiado {SOLR_HOME}\{coleção} \data. Para o cluster de Olá criado através do script de exemplo de Olá, este deve ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. Nesta localização, deverá ver uma pasta de instantâneos criada com um nome semelhante demasiado**instantâneo.* Timestamp** *.
   3. Zip pasta de instantâneos de Olá e carregue-o armazenamento de BLOBs de tooAzure. Olá Hadoop linha de comandos, navegue toohello localização da pasta de instantâneos de Olá utilizando Olá os seguintes comandos:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Este comando cópias instantâneo demasiado / / dados de exemplo de Olá/no contentor de Olá dentro da predefinição de Olá armazenamento conta associada Olá cluster.

## <a name="install-solr-using-aure-powershell"></a>Instalar Solr com o Azure PowerShell
Consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemplo de Olá demonstra como tooinstall Spark com o Azure PowerShell. Terá de toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Instalar Solr com o .NET SDK
Consulte [clusters do HDInsight de personalizar através da ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemplo de Olá demonstra como tooinstall Spark utilizando Olá .NET SDK. Terá de toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Consultar também
* [Instalar e utilizar Solr em clusters do HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Criar clusters do Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre a criação de clusters do HDInsight.
* [Personalizar clusters do HDInsight através da ação de Script][hdinsight-cluster-customize]: informações gerais sobre a personalização clusters do HDInsight através da ação de Script.
* [Desenvolver scripts de ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md).
* [Instalar e utilizar o Spark nos clusters do HDInsight][hdinsight-install-spark]: exemplo de ação de Script sobre a instalação do Spark.
* [Instalar o R nos clusters do HDInsight][hdinsight-install-r]: exemplo de ação de Script sobre a instalação do R.
* [Instalar Giraph nos clusters do HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de ação de Script sobre como instalar Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
