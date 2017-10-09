---
title: cluster aaaTroubleshoot problemas com o Apache Spark no Azure HDInsight | Microsoft Docs
description: Saiba mais sobre problemas relacionados tooApache clusters do Spark no Azure HDInsight e como toowork em torno dos.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Problemas conhecidos para o cluster do Apache Spark no HDInsight

Este documento mantém um registo dos Olá todos os problemas conhecidos para Olá pré-visualização pública do HDInsight Spark.  

## <a name="livy-leaks-interactive-session"></a>O Livy fugas de sessão interativa
Quando o Livy é reiniciado (do Ambari ou devido a reinício da máquina virtual de tooheadnode 0), com uma sessão interativa ainda ativo, uma sessão interativa de tarefa será transmitida. Por este motivo, novas tarefas podem bloqueada no Olá aceites estado e não pode ser iniciado.

**Atenuação:**

Utilize Olá problema do procedimento tooworkaround Olá os seguintes:

1. SSH para headnode. Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Olá executar aplicações do comando toofind Olá os seguintes IDs de tarefas interativa Olá trabalhar com o Livy. 
   
        yarn application –list
   
    Olá nomes de tarefa de predefinição será o Livy se tarefas de Olá foram começar com uma sessão interativa de Livy sem nomes explícitos especificados para Olá Livy iniciado pelo bloco de notas do Jupyter, o nome da tarefa Olá será início de sessão com remotesparkmagics_ *. 
3. Execute Olá os seguintes comandos tookill essas tarefas. 
   
        yarn application –kill <Application ID>

Novas tarefas iniciará a executar. 

## <a name="spark-history-server-not-started"></a>Servidor de histórico de Spark não foi iniciado
Servidor do histórico de Spark não está iniciado automaticamente depois de um cluster é criado.  

**Atenuação:** 

Inicie manualmente o servidor de histórico de Olá do Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problema de permissão no diretório de registo do Spark
Quando hdiuser submete uma tarefa com spark-submit, há um java.io.FileNotFoundException de erro: /var/log/spark/sparkdriver_hdiuser.log (permissão negada) e Olá registo de controlador não é escrito. 

**Atenuação:**

1. Adicione um grupo do hdiuser toohello Hadoop. 
2. Forneça 777 permissões no /var/log/spark após a criação do cluster. 
3. Atualize a localização do registo Olá spark utilizando Ambari toobe um diretório com 777 permissões.  
4. O spark de execução-submeter como sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>O Spark Phoenix conector não é suportado

Atualmente, o conector do Spark Phoenix Olá não é suportada com um cluster do HDInsight Spark.

**Atenuação:**

Conector do Spark HBase Olá tem de utilizar em vez disso. Para obter instruções, consulte [como conector toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Problemas relacionados com tooJupyter blocos de notas
Seguem-se algumas notas de tooJupyter relacionados problemas conhecidos.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Blocos de notas com carateres não ASCII em nomes de ficheiros
Blocos de notas Jupyter que podem ser utilizados em clusters do Spark HDInsight não devem ter carateres não ASCII em nomes de ficheiros. Se tentar tooupload um ficheiro através de Olá IU Jupyter que tem um nome de ficheiro não ASCII, ocorrerá uma falha silenciosamente (ou seja, não permite Jupyter carregar ficheiro Olá, mas não irá gerar um erro de visível ou). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Erro ao carregar os blocos de notas de tamanhos superiores
Poderá ver um erro  **`Error loading notebook`**  quando carrega blocos de notas que são maiores de tamanho.  

**Atenuação:**

Se obtiver este erro, não significa que os dados estão danificados ou perdidos.  Os blocos de notas são ainda num disco em `/var/lib/jupyter`, e pode SSH para Olá cluster tooaccess-los. Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

Assim que tiver estabelecido ligação toohello cluster com o SSH, pode copiar os blocos de notas do seu computador local de cluster tooyour (através de SCP ou WinSCP) como a perda de Olá tooprevent cópia de segurança de quaisquer dados importantes no bloco de notas do Olá. Pode, em seguida, túnel SSH no seu headnode na porta 8001 tooaccess Jupyter sem passar gateway Olá.  A partir daí, pode limpar resultado Olá o bloco de notas e guarde-o novamente tamanho do toominimize Olá bloco de notas.

tooprevent este erro aconteça no Olá futura, tem de seguir algumas melhores práticas:

* É importante tookeep Olá bloco de notas o tamanho pequeno. Qualquer saída das tarefas do Spark que é enviada novamente tooJupyter é continuada no bloco de notas do Olá.  É melhor prática, com o Jupyter no geral tooavoid executar `.collect()` em grande RDD ou dataframes; em vez disso, se quiser toopeek no conteúdo de um RDD, considere executar `.take()` ou `.sample()` para que o resultado não demasiado grande.
* Além disso, quando guardar um bloco de notas, desmarque todos os de saída do tamanho de Olá tooreduce de células.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Arranque inicial do bloco de notas demora mais tempo do que o previsto
Primeira instrução de código no bloco de notas do Jupyter utilizando a magia do Spark pode demorar mais do que um minuto.  

**Explicação:**

Isto acontece porque quando a primeira célula do código Olá é executada. Em segundo plano de Olá este inicia a configuração de sessão e Spark, SQL e contextos de ramo de registo estão definidos. Depois destas contextos estiver definidos, é executada a primeira instrução de Olá e isto dá-impressão Olá que instrução Olá demorou um toocomplete muito tempo.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Tempo limite de bloco de notas do Jupyter em criar sessão Olá
Quando o cluster do Spark tem recursos insuficientes, Olá Spark e Pyspark kernels no bloco de notas do Jupyter Olá serão tempo limite excedido da sessão de Olá toocreate. 

**Mitigações:** 

1. Liberte alguns recursos do cluster do Spark por:
   
   * A parar os outros blocos de notas do Spark por toohello vai fechar e Halt menu ou clicar encerramento no Explorador do bloco de notas Olá.
   * A parar a outras aplicações do Spark do YARN.
2. Reinicie o bloco de notas Olá que tentavam toostart cópias de segurança. Recursos suficientes devem estar disponíveis para toocreate agora uma sessão.

## <a name="see-also"></a>Consultar também
* [Descrição geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: Efetuar uma análise de dados interativa com o Spark no HDInsight com ferramentas do BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Machine Learning: Utilizar o Spark no HDInsight para analisar a temperatura do edifício com dados de AVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com Machine Learning: utilizar o Spark no HDInsight toopredict inspeções alimentares](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Transmissão em Fluxo do Spark: Utilizar o Spark no HDInsight para criar aplicações de transmissão em fluxo em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de registos de sites com o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicações
* [Criar uma aplicação autónoma com o Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar tarefas remotamente num cluster do Spark com o Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Utilizar o plug-in ferramentas do HDInsight para o IntelliJ IDEA toocreate e submeter aplicações do Spark scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizar o plug-in ferramentas do HDInsight para aplicações do Spark IntelliJ IDEA toodebug remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utilizar blocos de notas do Zeppelin com um cluster do Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de notas do Jupyter no cluster do Spark para o HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utilizar pacotes externos com blocos de notas do Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar o Jupyter no seu computador e ligue tooan cluster do HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerir recursos
* [Gerir os recursos de cluster do Apache Spark Olá no Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Controlar e depurar tarefas em execução num cluster do Apache Spark do HDInsight](hdinsight-apache-spark-job-debugging.md)

