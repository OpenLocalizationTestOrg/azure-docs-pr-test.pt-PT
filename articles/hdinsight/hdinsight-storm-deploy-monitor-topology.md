---
title: aaaDeploy e gerir topologias Apache Storm no HDInsight | Microsoft Docs
description: "Saiba como toodeploy, monitorizar e gerir topologias do Apache Storm utilizando Olá Storm Dashboard no HDInsight. Utilize as ferramentas Hadoop para o Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Implementar e gerir topologias Apache Storm no HDInsight baseado em Windows

Olá Storm Dashboard permite-lhe tooeasily implementar e executar o cluster do Apache Storm topologias tooyour HDInsight ao utilizar o seu browser. Também pode utilizar Olá dashboard toomonitor e gerir topologias em execução. Se utilizar o Visual Studio, Olá ferramentas do HDInsight para Visual Studio fornecem semelhantes funcionalidades no Visual Studio.

Olá Storm Dashboard e funcionalidades de Storm Olá no Olá as ferramentas do HDInsight dependem Olá API de REST de Storm, que podem ser utilizado toocreate as suas próprias soluções de monitorização e gestão.

> [!IMPORTANT]
> passos de Olá neste documento exigem um Storm no cluster do HDInsight que utiliza o Windows como sistema de operativo Olá. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).
>
> Para obter informações sobre como implementar e gerir topologias do Storm com um cluster do HDInsight que utiliza o Linux, consulte [implementar e gerir topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Pré-requisitos

* **Apache Storm no HDInsight** -consulte [introdução ao Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para obter os passos sobre como criar um cluster.

* Para Olá **Storm Dashboard**: um browser moderno que suporte HTML5.

* Para **Visual Studio** -Azure SDK 2.5.1 ou mais recente e hello as ferramentas do HDInsight para Visual Studio. Consulte [começar a utilizar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall e configurar ferramentas do HDInsight Olá para Visual Studio.

    Uma das seguintes versões do Visual Studio de Olá:

  * Visual Studio 2012 com atualização 4

  * Visual Studio 2013 atualização 4 ou Visual Studio 2013 Community

  * Visual Studio 2015 (qualquer edição)

  * Visual Studio 2017 (qualquer edição)

## <a name="storm-dashboard"></a>Storm Dashboard

Olá Storm Dashboard é uma página web disponíveis no seu cluster do Storm. URL de Olá é **https://&lt;clustername >.azurehdinsight.net/**, onde **clustername** é Olá nome do seu cluster Storm no HDInsight.

Na parte superior de Olá de Olá Storm Dashboard, selecione **submeter topologia**. Siga as instruções de Olá no Olá página toorun uma topologia de exemplo ou tooupload e execute uma topologia que criou.

![Olá submeter página topologia][storm-dashboard-submit]

### <a name="storm-ui"></a>IU do Storm

A partir do Storm Dashboard Olá, selecione Olá **IU do Storm** ligação. Esta ação apresenta informações sobre o cluster de Olá, na execução de topologias de tooany de adição.

![IU do storm Olá][storm-dashboard-ui]

> [!NOTE]
> Com algumas versões do Internet Explorer, poderá descobrir que Olá que não atualizar a IU do Storm após o primeiro visitaram-lo. Por exemplo, esta operação poderá não mostrar topologias novo Olá submetidas ou esta operação poderá mostrar uma topologia como o Active Directory quando desativada anteriormente. A Microsoft está ciente de que este problema e está a funcionar numa solução.

#### <a name="main-page"></a>Página principal

página principal do Olá do Olá IU do Storm fornece Olá seguintes informações:

* **Resumo do cluster**: informações básicas sobre o cluster do Storm Olá.

* **Resumo da topologia**: uma lista de execução de topologias. Utilize Olá ligações na tooview secção obter mais informações sobre topologias específicas.

* **Resumo do supervisor**: informações sobre o supervisor de Storm Olá.

* **Configuração de nimbus**: configuração de Nimbus para cluster Olá.

#### <a name="topology-summary"></a>Topologia de resumo

Selecionar uma ligação de Olá **resumo da topologia** secção apresenta Olá informações sobre a topologia de Olá os seguintes:

* **Resumo da topologia**: informações básicas sobre a topologia de Olá.

* **Ações de topologia**: ações de gestão que pode efetuar para topologia de Olá.

  * **Ativar**: retoma o processamento de uma topologia desativada.

  * **Desativar**: pausa uma topologia em execução.

  * **Rebalancear**: ajusta o paralelismo Olá da topologia de Olá. Deve rebalancear as topologias em execução depois de ter alterado o número de Olá de nós no cluster de Olá. Isto permite Olá topologia tooadjust paralelismo toocompensate para Olá aumentado ou diminuído número de nós no cluster de Olá.

      Para obter mais informações, consulte [compreender o paralelismo Olá de uma topologia do Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kill**: termina uma topologia do Storm após Olá especificado tempo limite.

* **Estatísticas de topologia**: estatísticas sobre a topologia de Olá. Utilize as ligações de Olá Olá **janela** período de tempo de coluna tooset Olá para Olá restantes entradas na página Olá.

* **Spouts**: Olá spouts utilizados por topologia Olá. Utilize ligações de Olá na tooview secção obter mais informações sobre spouts específicos.

* **Bolts**: Olá bolts utilizados por topologia Olá. Utilize ligações de Olá na tooview secção obter mais informações sobre bolts específicos.

* **Configuração da topologia**: configuração de Olá da topologia de Olá selecionado.

#### <a name="spout-and-bolt-summary"></a>Spout e resumo Bolt

A seleção de um spout Olá **Spouts** ou **Bolts** secções apresenta Olá seguintes informações sobre o item de Olá selecionado:

* **Resumo de componente**: informações básicas sobre Olá spout ou bolt.

* **Estatísticas de spout/Bolt**: estatísticas sobre Olá spout ou bolt. Utilize as ligações de Olá Olá **janela** período de tempo de coluna tooset Olá para Olá restantes entradas na página Olá.

* **Estatísticas de entrada** (apenas bolt): informações sobre Olá fluxos consumidos pelo bolt Olá de entrada.

* **Estatísticas de saída**: informações sobre fluxos de Olá emitidos por este spout ou bolt.

* **Executores**: informações sobre instâncias Olá Olá spout ou bolt. Selecione Olá **porta** produzidos de um registo de informações de diagnóstico de entrada para um tooview executor específicas para esta instância.

* **Erros**: quaisquer informações de erro para este spout ou bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>Ferramentas do HDInsight para Visual Studio

as ferramentas do HDInsight Olá podem ser utilizados toosubmit c# ou híbrida topologias tooyour cluster do Storm. os seguintes passos de Olá utiliza uma aplicação de exemplo. Para obter informações sobre como criar as seus próprios topologias utilizando as ferramentas do HDInsight Olá, consulte [desenvolver topologias c# utilizando Olá ferramentas do HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Utilizar Olá os seguintes passos toodeploy tooyour um exemplo Storm num cluster do HDInsight, em seguida, ver e gerir a topologia de Olá.

1. Se já não tiver instalado o versão mais recente do Olá do Olá as ferramentas do HDInsight para Visual Studio, consulte o artigo [começar a utilizar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Abra o Visual Studio, selecione **ficheiro** > **novo** > **projeto**.

3. No Olá **novo projeto** diálogo caixa, expanda **instalada** > **modelos**e, em seguida, selecione **HDInsight**. Na lista de Olá dos modelos, selecione **exemplo do Storm**. Olá parte inferior da caixa de diálogo Olá, escreva um nome para a aplicação Olá.

    ![Imagem](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. No **Explorador de soluções**, clique no projeto Olá e selecione **submeter tooStorm no HDInsight**.

   > [!NOTE]
   > Se lhe for solicitado, introduza as credenciais de início de sessão Olá para a sua subscrição do Azure. Se tiver mais do que uma subscrição, inicie sessão toohello que contenha o seu cluster Storm no HDInsight.

5. Selecione o cluster Storm no HDInsight Olá **Cluster do Storm** na lista pendente e, em seguida, selecione **submeter**. Pode monitorizar se submissão Olá é efetuada com êxito utilizando Olá **saída** janela.

6. Quando a topologia de Olá foi submetida com êxito, Olá **topologias Storm** para cluster Olá deve aparecer. Selecione a topologia de Olá Olá lista tooview sobre Olá com topologia.

    ![monitor do Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > Também pode ver **topologias Storm** de **Explorador de servidores** expandindo **Azure** > **HDInsight**e, em seguida, clicar um cluster Storm no HDInsight e selecionando **topologias do Storm vista**.

    Selecione a forma de Olá para Olá spouts ou bolts tooview informações sobre estes componentes. Abre uma nova janela para cada item selecionado.

   > [!NOTE]
   > nome de Olá da topologia de Olá é o nome de classe de Olá da topologia de Olá (neste caso, `HelloWord`,) com um carimbo anexado.

7. De Olá **resumo da topologia** visualizar, selecione **Kill** topologia de Olá toostop.

   > [!NOTE]
   > Topologias do Storm continuam em execução até que estão paradas ou cluster Olá é eliminado.


## <a name="rest-api"></a>API REST

Olá IU do Storm é desenvolvida Olá REST API, pelo que pode realizar semelhante de gestão e monitorização funcionalidade utilizando Olá REST API. Pode utilizar ferramentas personalizadas do Olá REST API toocreate de gestão e monitorização topologias do Storm.

Para obter mais informações, consulte [API de REST de IU do Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Olá informações seguintes são específicos toousing Olá API REST do Apache Storm no HDInsight.

### <a name="base-uri"></a>URI de base

Olá URI base para a REST API de Olá nos clusters do HDInsight é **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, onde **clustername** é o nome de Olá do Storm no Cluster do HDInsight.

### <a name="authentication"></a>Autenticação

Toohello pedidos tem de utilizar a REST API **autenticação básica**, por isso, utilize o nome de administrador de cluster de HDInsight Olá e a palavra-passe.

> [!NOTE]
> Porque a autenticação básica é enviada através da utilização de texto não encriptado, deve **sempre** utilizar comunicações de toosecure HTTPS com cluster Olá.

### <a name="return-values"></a>Valores de retorno

Informações de que são devolvidas de Olá REST API podem apenas ser utilizável num cluster de Olá ou Olá, máquinas virtuais na mesma rede Virtual do Azure como cluster Olá. Por exemplo, nome de domínio completamente qualificado de Olá (FQDN) para servidores de Zookeeper devolvido não são estar acessível a partir do Olá Internet.

## <a name="next-steps"></a>Passos Seguintes

Agora que aprendeu como topologias toodeploy e monitor utilizando Olá Storm Dashboard, saiba como:

* [Desenvolver topologias c# utilizando Olá ferramentas do HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Desenvolver topologias baseadas em Java com o Maven](hdinsight-storm-develop-java-topology.md)

Para obter uma lista das topologias de exemplo mais, consulte [topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
