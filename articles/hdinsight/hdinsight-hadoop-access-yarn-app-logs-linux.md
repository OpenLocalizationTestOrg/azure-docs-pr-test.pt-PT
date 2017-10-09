---
title: "os registos de aaaAccess aplicação YARN de Hadoop no HDInsight baseado em Linux - Azure | Microsoft Docs"
description: "Saiba como aplicações de YARN tooaccess os registos de um cluster de HDInsight (Hadoop) baseado em Linux utilizando Olá da linha de comandos e um browser."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Os registos de aplicação de YARN de acesso no HDInsight baseado em Linux

Saiba como tooaccess Olá registos para aplicações de YARN (ainda outro recurso Negotiator) num cluster de Hadoop no Azure HDInsight.

> [!IMPORTANT]
> passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Linux. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, consulte [controlo de versões do HDInsight componente](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>Servidor de linha cronológica YARN

Olá [YARN linha cronológica servidor](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) fornece informações genéricas nas aplicações concluídas e informações de aplicação específica do framework através de duas interfaces de rede diferentes. Especificamente:

* Armazenamento e a obtenção de informações de aplicação genérica nos clusters do HDInsight foi ativado com a versão 3.1.1.374 ou superior.
* Olá específicas do framework informações do componente da aplicação de Olá linha cronológica de servidor não está atualmente disponível nos clusters do HDInsight.

Genéricas informações sobre as aplicações incluem Olá seguinte tipo de dados:

* ID da aplicação Olá, um identificador exclusivo de uma aplicação
* utilizador Olá quem iniciou a aplicação Olá
* Informações sobre as tentativas efetuadas a aplicação de Olá toocomplete
* contentores de Olá utilizados por qualquer tentativa de aplicação

## <a name="YARNAppsAndLogs"></a>Registos de aplicações de YARN e

YARN suporta vários modelos de programação (MapReduce que está a ser um dos atributos) ao desassociar a gestão de recursos de agendamento/monitorização de aplicações. YARN utiliza um global *ResourceManager* (RM), por--nó de trabalho *NodeManagers* (NMs) e por aplicação *ApplicationMasters* (AMs). Olá por aplicação AM negoceia recursos (CPU, memória, disco, rede) para executar a aplicação com Olá RM. Olá RM funciona com NMs toogrant destes recursos, são concedidos como *contentores*. Olá AM é responsável por controlar o progresso Olá Olá contentores atribuídos tooit por Olá RM. Uma aplicação pode necessitar de vários contentores, dependendo da natureza Olá da aplicação Olá.

Cada aplicação pode consistir em várias *tentativas da aplicação*. Se uma aplicação falhar, pode ser repetida como uma nova tentativa. Cada tentativa é executado num contentor. Num sentido, um contentor fornece um contexto Olá para a unidade básica de trabalho realizado por uma aplicação YARN. Todo o trabalho que é efetuado no contexto de Olá de um contentor é executado no nó de trabalho única de Olá no qual Olá contentor foi alocado. Consulte [YARN conceitos] [ YARN-concepts] para obter mais referência.

Registos de aplicação (e os registos do contentor de Olá associado) são fatores essenciais de depuração problemáticas aplicações do Hadoop. O YARN fornece uma arquitetura nice para recolher, Agregar e armazenar os registos de aplicação com Olá [registo agregação] [ log-aggregation] funcionalidade. funcionalidade de registo agregação Olá torna mais determinista ao aceder aos registos de aplicação. Isto agrega registos através de todos os contentores num nó de trabalho e armazena-os como um ficheiro de registo agregados por nó de trabalho. registo de Olá é armazenado no sistema de ficheiros predefinido Olá após a conclusão de uma aplicação. A aplicação pode utilizar centenas ou milhares de contentores, mas os registos para todos os contentores executados num nó único do worker são sempre tooa agregado ficheiros única. Por isso apenas é 1 registo por nó de trabalho utilizada pela sua aplicação. Agregação de registo está ativada por predefinição em clusters do HDInsight versão 3.0 e posteriores. Agregados registos estão localizados no armazenamento de predefinido para o cluster de Olá. Olá seguinte caminho é Olá HDFS caminho toohello registos:

    /app-logs/<user>/logs/<applicationId>

No caminho de Olá, `user` é Olá nome de utilizador de Olá que iniciou a aplicação Olá. Olá `applicationId` é Olá Identificador exclusivo atribuído tooan aplicação por RM. YARN de Olá

Olá registos de agregados não são diretamente legíveis, como são escritos [TFile][T-file], [formato binário] [ binary-format] indexado por contentor. Utilize Olá que registos YARN ResourceManager ou tooview de ferramentas da CLI estes registos como texto simples para aplicações ou contentores de interesse.

## <a name="yarn-cli-tools"></a>Ferramentas da CLI do YARN

ferramentas do toouse Olá YARN CLI, tem de ligar primeiro toohello cluster do HDInsight através de SSH. Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

Pode ver estes registos como texto não encriptado, executando um dos seguintes comandos de Olá:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Especifique Olá &lt;applicationId >, &lt;-quem-iniciado-a-aplicação do utilizador >, &lt;ID do contentor >, e &lt;endereço do nó do trabalho > informações quando executar estes comandos.

## <a name="yarn-resourcemanager-ui"></a>IU do YARN ResourceManager

Olá IU do YARN ResourceManager é executada em Olá headnode de cluster. É acedido através da web do Ambari Olá IU. Olá utilize os seguintes passos tooview Olá YARN registos:

1. No seu browser, navegue até toohttps://CLUSTERNAME.azurehdinsight.net. Substitua CLUSTERNAME pelo nome de Olá do cluster do HDInsight.
2. Na lista de Olá dos serviços Olá esquerda, selecione **YARN**.

    ![Serviço de yarn selecionado](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. De Olá **ligações rápidas** lista pendente, selecione um de nós principais do cluster Olá e, em seguida, selecione **ResourceManager registo**.

    ![Ligações rápidas yarn](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    É-lhe apresentada uma lista de ligações tooYARN registos.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
