---
title: Utilize Zeppelin para executar consultas do Hive no Azure HDInsight | Microsoft Docs
description: Saiba como utilizar Zeppelin para executar consultas do Hive.
keywords: hive do hadoop do hdinsight, consulta interativa, LLAP
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2017
ms.author: jgao
ms.openlocfilehash: 39f99bef252e93db55e0493ee284ef78b7d087a1
ms.sourcegitcommit: 4bd369fc472dced985239aef736fece42fecfb3b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="use-zeppelin-to-run-hive-queries-in-azure-hdinsight"></a>Utilize Zeppelin para executar consultas do Hive no Azure HDInsight 

Clusters do HDInsight de consulta interativa incluem blocos de notas do Zeppelin que pode utilizar para executar consultas interativas do ramo de registo. Neste artigo, irá aprender a utilizar Zeppelin para executar consultas do Hive no Azure HDInsight. 

## <a name="prerequisites"></a>Pré-requisitos
Antes de passar neste artigo, tem de ter os seguintes itens:

* **Cluster de HDInsight de consulta interativa**. Consulte [Criar cluster](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster) para criar um cluster do HDInsight.  Certifique-se escolher o tipo de consulta interativo. 

## <a name="create-a-zeppelin-note"></a>Crie uma nota do Zeppelin

1. Navegue para o seguinte URL:

        https://CLUSTERNAME.azurehdinsight.net/zeppelin
    Substitua **CLUSTERNAME** pelo nome do cluster.

2. Introduza o nome de utilizador do Hadoop e a palavra-passe. Página Zeppelin, pode criar uma nova nota ou abrir notas existentes. HiveSample contém alguns exemplos de consultas do Hive.  

    ![Zeppelin consulta interativa do HDInsight](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin.png)
3. Clique em **criar nova nota**.
4. Escreva ou selecione os seguintes valores:

    - Nome de Nota: introduza um nome para a nota.
    - Predefinição interpretador: selecione **JDBC**.

5. Clique em **criar nota**.
6. Execute a seguinte consulta do Hive:

        %jdbc(hive)
        show tables

    ![HDInsight interativa zeppelin execuções de consulta](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin-query.png)

    O **%jdbc(hive)** instrução na primeira linha indica o bloco de notas para utilizar o interpretador de JDBC ramo de registo.

    A consulta deverá devolver uma tabela de Hive chamada *hivesampletable*.

    Seguem-se duas consultas do Hive mais que podem ser executadas contra o hivesampletable. 

        %jdbc(hive)
        select * from hivesampletable limit 10

        %jdbc(hive)
        select ${group_name}, count(*) as total_count
        from hivesampletable
        group by ${group_name=market,market|deviceplatform|devicemake}
        limit ${total_count=10}

    A comparação com o ramo de registo tradicional, os resultados da consulta voltar atrás tem mais rapidamente.


## <a name="next-steps"></a>Passos Seguintes
Neste artigo, aprendeu a visualizar dados do HDInsight através do Power BI.  Para obter mais informações, consulte os artigos seguintes:

* [Visualizar dados do Hive com o Microsoft Power BI no Azure HDInsight](hadoop/apache-hadoop-connect-hive-power-bi.md).
* [Visualizar dados de ramo de registo de consultas interativas com o Power BI no Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).
* [Ligar o Excel para o HDInsight com o controlador ODBC do Microsoft Hive](hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).
* [Ligar o Excel ao Hadoop com o Power Query](hadoop/apache-hadoop-connect-excel-power-query.md).
* [Ligar ao Azure HDInsight e executar consultas do Hive, utilizando ferramentas do Data Lake para Visual Studio](hadoop/apache-hadoop-visual-studio-tools-get-started.md).
* [Utilizar a ferramenta do Azure HDInsight para Visual Studio Code](hdinsight-for-vscode.md).
* [Carregar dados para o HDInsight](./hdinsight-upload-data.md).
