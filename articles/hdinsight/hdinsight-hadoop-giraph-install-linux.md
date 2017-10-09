---
title: aaaInstall e utilize Giraph no HDInsight (Hadoop) - Azure | Microsoft Docs
description: "Saiba como tooinstall Giraph no HDInsight baseado em Linux clusters utilizando ações de Script. Ações de script permitem-lhe cluster de Olá toocustomize durante a criação, alteração da configuração de cluster ou instalar os serviços e utilitários."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Instalar Giraph em clusters do HDInsight Hadoop e utilizar Giraph tooprocess em grande escala gráficos

Saiba como tooinstall Apache Giraph num cluster do HDInsight. funcionalidade de ação de script de Olá do HDInsight permite-lhe toocustomize cluster executando um script de bash. Scripts podem ser utilizados toocustomize clusters durante e após a criação do cluster.

> [!IMPORTANT]
> passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Linux. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a name="whatis"></a>O que é Giraph

[Apache Giraph](http://giraph.apache.org/) permite-lhe o gráfico de tooperform processamento ao utilizar o Hadoop e pode ser utilizado com o Azure HDInsight. Relações entre objetos de modelo de gráficos. Por exemplo, Olá ligações entre routers numa rede grande como Olá Internet ou relações entre as pessoas em redes sociais. Processamento de gráfico permite-lhe tooreason sobre Olá as relações entre objetos de um gráfico, tais como:

* Identificar potenciais amigos com base na sua relações atuais.

* Identificação Olá mais curta rota entre dois computadores numa rede.

* Calcular a posição da página Olá das páginas Web.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados - Support Microsoft ajuda-o tooisolate e resolver problemas relacionados toothese componentes.
>
> Componentes personalizados, tais como Giraph, recebem suporte comercialmente razoáveis toohelp toofurther poderá resolver o problema de Olá. Microsoft Support poderá tooresolving capaz de problema de Olá. Caso contrário, tem de consultar Comunidades de open source para onde se encontra profundo conhecimentos para que a tecnologia. Por exemplo, existem vários sites de Comunidade que podem ser utilizadas, como: [fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Também projetos do Apache tem sites de projeto no [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>O script de Olá faz

Este script executa Olá seguintes ações:

* Instala Giraph demasiado`/usr/hdp/current/giraph`

* Olá cópias `giraph-examples.jar` armazenamento de ficheiros toodefault (WASB) para o cluster:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Instalar Giraph utilizando ações de Script

Um tooinstall de script de exemplo Giraph num cluster do HDInsight está disponível em Olá seguinte localização:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Esta secção fornece instruções sobre como toouse Olá script de exemplo ao criar o cluster de Olá utilizando Olá portal do Azure.

> [!NOTE]
> Uma ação de script pode ser aplicada utilizando qualquer um dos seguintes métodos de Olá:
> * Azure PowerShell
> * Olá CLI do Azure
> * Olá SDK .NET do HDInsight
> * Modelos do Azure Resource Manager
> 
> Também pode aplicar tooalready de ações de script clusters em execução. Para obter mais informações, consulte [HDInsight personalizar clusters com ações de Script](hdinsight-hadoop-customize-cluster-linux.md).

1. Iniciar criação de um cluster, utilizando os passos de Olá no [clusters do HDInsight baseado em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md), mas não concluir a criação.

2. No Olá **configuração opcional** painel, selecione **ações de Script**e forneça Olá seguintes informações:

   * **NOME**: introduza um nome amigável para a ação de script de Olá.

   * **URI de SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**: esta entrada de verificação

   * **TRABALHO**: deixe esta entrada desmarcada

   * **ZOOKEEPER**: deixe esta entrada desmarcada

   * **Os parâmetros**: deixe este campo em branco

3. Na parte inferior de Olá de Olá **ações de Script**, utilize Olá **selecione** configuração de Olá toosave do botão. Por último, utilize Olá **selecione** botão na parte inferior de Olá de Olá **configuração opcional** painel toosave Olá opcional as informações de configuração.

4. Continuar a criar cluster Olá, conforme descrito em [clusters do HDInsight baseado em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Como utilizar o Giraph no HDInsight?

Quando o cluster de Olá tiver sido criado, utilize Olá seguinte passos toorun Olá SimpleShortestPathsComputation exemplo incluído com Giraph. Este exemplo utiliza básico Olá [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementação para localizar o caminho mais curto do Olá entre objetos de um gráfico.

1. Ligar o cluster do HDInsight toohello utilizando SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Seguinte de Olá utilize comando toocreate um ficheiro denominado **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Utilize Olá seguir texto como conteúdo Olá deste ficheiro:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Estes dados descreve uma relação entre objetos de um gráfico direcionado, utilizando o formato de Olá `[source_id, source_value,[[dest_id], [edge_value],...]]`. Cada linha representa uma relação entre um `source_id` objeto e um ou mais `dest_id` objetos. Olá `edge_value` pode considerar como força Olá ou distance Olá da ligação de entre `source_id` e `dest\_id`.

    Desenhado horizontalmente, e utilizar o valor de Olá (ou ponderação) como distância Olá entre objetos, dados de Olá aspeto que poderão ter Olá diagrama a seguir:

    ![tiny_graph.txt desenhado como circles com linhas de variando distância entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. ficheiro de Olá toosave, utilize **Ctrl + X**, em seguida, **Y**e, finalmente, **Enter** nome de ficheiro de Olá tooaccept.

4. Utilize Olá os seguintes dados de Olá toostore para o armazenamento primário para o cluster do HDInsight:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Execute Olá SimpleShortestPathsComputation exemplo, utilizando Olá os seguintes comandos:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    os parâmetros de Olá utilizados com este comando descritos Olá a tabela seguinte:

   | Parâmetro | O que faz |
   | --- | --- |
   | `jar` |ficheiro jar Olá que contém exemplos de Olá. |
   | `org.apache.giraph.GiraphRunner` |classe de Olá utilizada exemplos de Olá toostart. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |exemplo de Olá que é utilizado. Neste exemplo, calcula caminho mais curto do Olá entre 1 de ID e todos os outros IDs no gráfico de Olá. |
   | `-ca mapred.job.tracker` |Olá headnode para cluster Olá. |
   | `-vif` |Olá toouse de formato de entrada para dados de entrada Olá. |
   | `-vip` |ficheiro de dados de entrada Olá. |
   | `-vof` |formato de saída Olá. Neste exemplo, a ID e o valor como texto simples. |
   | `-op` |localização de saída Olá. |
   | `-w 2` |Olá número workers toouse. Neste exemplo, 2. |

    Para obter mais informações sobre estes e outros parâmetros utilizados Giraph exemplos, consulte Olá [início rápido de Giraph](http://giraph.apache.org/quick_start.html).

6. Depois de concluir a tarefa de Olá, Olá estão armazenados no Olá **/example/out/shotestpaths** diretório. Olá nomes de ficheiro de saída de começar por **parte-m -** e terminar com um número a indicar Olá em primeiro lugar, segundo, ficheiro etc.. Utilize Olá resultado do comando tooview Olá os seguintes:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    saída de Olá deve aparecer toohello semelhante seguinte texto:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    exemplo de SimpleShortestPathComputation Olá está hard-coded toostart com 1 de ID de objeto e localizar Olá objetos de tooother de caminho mais curto. saída de Olá está num formato de Olá de `destination_id` e `distance`. Olá `distance` é Olá valor (ou ponderação) das margens Olá percorrer entre 1 de ID de objeto e ID de destino Olá.

    Visualizar estes dados, pode verificar os resultados de Olá, viaja caminhos mais curto Olá entre 1 de ID e todos os outros objetos. caminho mais curto do Olá entre ID 1 e ID 4 é 5. Este valor é distância total do Olá entre <span style="color:orange">ID 1 e 3</span>e, em seguida, <span style="color:red">ID 3 e 4</span>.

    ![Desenho de objetos como circles com mais curto caminhos desenhados entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Passos seguintes

* [Instalar e utilizar Hue nos clusters do HDInsight](hdinsight-hadoop-hue-linux.md).

* [Instalar Solr nos clusters do HDInsight](hdinsight-hadoop-solr-install-linux.md).
