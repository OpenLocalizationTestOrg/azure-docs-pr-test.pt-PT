---
title: aaaUse Tez IU com o HDInsight baseado em Windows - Azure | Microsoft Docs
description: "Saiba como toouse Olá Tez IU toodebug Tez tarefas no HDInsight do HDInsight baseados em Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Utilizar Olá Tez IU toodebug Tez tarefas no HDInsight baseado em Windows
Olá Tez IU é uma página web que podem ser utilizadas toounderstand e depurar tarefas que utilizam o Tez como motor de execução de Olá nos clusters do HDInsight baseados em Windows. Olá Tez IU permite-lhe tarefa de Olá toovisualize como um gráfico de itens ligados, explorar cada item e obter as estatísticas e as informações de registo.

> [!IMPORTANT]
> passos de Olá neste documento exigem um cluster do HDInsight que utiliza o Windows. Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

## <a name="prerequisites"></a>Pré-requisitos
* Um cluster do HDInsight baseados em Windows. Para obter os passos sobre como criar um novo cluster, consulte [começar a utilizar o HDInsight baseado em Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Olá Tez IU só está disponível nos clusters do HDInsight baseado em Windows criados após 8th de Fevereiro de 2016.
  >
  >
* Um cliente de ambiente de trabalho remoto baseado em Windows.

## <a name="understanding-tez"></a>Noções sobre Tez
Tez é uma arquitetura extensível para processamento de dados no Hadoop que fornece maiores velocidades de processamento de MapReduce tradicional. Para os clusters do HDInsight baseado em Windows, é um motor de opcional que pode ativar para o ramo de registo utilizando Olá os seguintes comandos como parte da sua consulta do Hive:

    set hive.execution.engine=tez;

Quando o trabalho é submetido tooTez, cria um direcionado Acíclico gráfico (DAG) que descreve a ordem de Olá da execução de ações de Olá necessárias por tarefa Olá. Ações individuais são denominadas vértices e executar um conjunto de Olá tarefa geral. Olá execução real do trabalho Olá descrita através de um vértice denomina-se uma tarefa e pode ser distribuída por vários nós no cluster de Olá.

### <a name="understanding-hello-tez-ui"></a>Olá compreender Tez IU
Olá Tez IU é que uma página web fornece informações sobre os processos que estão em execução ou ter sido executaram utilizando Tez. Permite-lhe tooview Olá DAG gerado pelo Tez, como é distribuído entre clusters, contadores, tais como a memória utilizada por tarefas e vértices e as informações de erro. -Pode oferecer informações úteis no Olá os seguintes cenários:

* Monitorização de processos de execução longa, visualizar Olá progresso de mapa e reduzir as tarefas.
* Analisar dados históricos para processos com êxito ou falha toolearn como processamento pode ser melhorado ou por que falhou.

## <a name="generate-a-dag"></a>Gerar um DAG
Olá Tez IU irá conter apenas dados se uma tarefa que utiliza Olá Tez motor está atualmente em execução ou tem foi executado no Olá passado. Simples consultas do Hive, normalmente, podem ser resolvidas sem utilizar Tez, no entanto mais complexas consultas que fazer filtragem, agrupamento, ordenação, associações, etc. normalmente, irá necessitar Tez.

Utilize Olá os seguintes passos toorun uma consulta de Hive que irão executar utilizando Tez.

1. Num browser, navegue até toohttps://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é Olá nome do cluster do HDInsight.
2. No menu de Olá em Olá parte superior da página Olá, selecione Olá **Editor do Hive**. Isto irá apresentar uma página com Olá consulta de exemplo a seguir.

        Select * from hivesampletable

    Apagar a consulta de exemplo de Olá e substitua-o com o seguinte Olá.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Selecione Olá **submeter** botão. Olá **tarefa sessão** secção Olá parte inferior da página Olá apresentará o estado de Olá da consulta de Olá. Uma vez Olá alterações de estado demasiado**concluído**, selecione Olá **ver detalhes** resultados de Olá tooview de ligação. Olá **resultado da tarefa** deve ser semelhante toohello seguinte:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Utilizar Olá Tez IU
> [!NOTE]
> Olá Tez IU só está disponível a partir do ambiente de trabalho Olá Olá head de nós de cluster, pelo que deverá utilizar nós principais do ambiente de trabalho remoto tooconnect toohello.
>
>

1. De Olá [portal do Azure](https://portal.azure.com), selecione o cluster do HDInsight. A partir da Olá parte superior do painel de HDInsight Olá, selecione Olá **ambiente de trabalho remoto** ícone. Este será apresentado o painel de ambiente de trabalho remoto Olá

    ![Ícone de ambiente de trabalho remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. No painel de ambiente de trabalho remoto Olá, selecione **Connect** nó principal do cluster de toohello tooconnect. Quando lhe for pedido, utilize Olá ambiente de trabalho remoto utilizador nome e palavra-passe tooauthenticate Olá ligação de cluster.

    ![Ícone de ligação de ambiente de trabalho remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Se não tiver ativado a conectividade de ambiente de trabalho remoto, forneça um nome de utilizador, a palavra-passe e a data de expiração, em seguida, selecione **ativar** tooenable ambiente de trabalho remoto. Assim que tiver sido ativada, utilize Olá tooconnect de passos anterior.
   >
   >
3. Assim que estiver ligado, abra o Internet Explorer no Olá ambiente de trabalho remoto, ícone engrenagem Olá selecione Olá canto superior direito do browser Olá e, em seguida, selecione **ver definições de compatibilidade**.
4. Na parte inferior de Olá da **ver definições de compatibilidade**, desmarque caixa de verificação Olá **apresentar sites da intranet na vista de compatibilidade** e **apresenta uma lista de compatibilidade de utilização Microsoft**, e, em seguida, selecione **fechar**.
5. No Internet Explorer, procurar toohttp://headnodehost:8188/tezui / #/. Isto irá apresentar Olá Tez IU

    ![Tez IU](./media/hdinsight-debug-tez-ui/tezui.png)

    Quando carrega Olá IU Tez, verá uma lista de DAGs que estão atualmente em execução ou ter sido executado no cluster de Olá. Vista de predefinida Olá inclui Olá nome Dag, Id, submissor, estado, hora de início, hora de fim, duração, ID da aplicação e fila. É possível adicionar mais colunas utilizando o ícone de engrenagem Olá na Olá direito da página Olá.

    Se tiver apenas uma entrada, será para consulta Olá que tenha sido executada na secção anterior Olá. Se tiver várias entradas, pode pesquisar introduzindo critérios de pesquisa em campos de Olá acima Olá DAGs e acessos **Enter**.
6. Selecione Olá **Dag nome** para a entrada de DAG mais recente Olá. Esta ação apresenta informações sobre Olá DAG, bem como toodownload de opção Olá um zip dos ficheiros JSON que contêm informações sobre Olá DAG.

    ![Detalhes do DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Acima Olá **DAG detalhes** são várias ligações que podem ser utilizados toodisplay informações sobre Olá DAG.

   * **Contadores do DAG** apresenta informações sobre os contadores para este DAG.
   * **Vista gráfica** apresenta uma representação gráfica deste DAG.
   * **Todos os vértices** apresenta uma lista de vértices Olá neste DAG.
   * **Todas as tarefas** apresenta uma lista de tarefas de Olá para todos os vértices neste DAG.
   * **Todos os TaskAttempts** apresenta informações sobre Olá tenta toorun tarefas para esta DAG.

     > [!NOTE]
     > Se se deslocar para a apresentação de coluna Olá para vértices, tarefas e TaskAttempts, tenha em atenção que existem ligações tooview **contadores** e **ver ou transferir registos** para cada linha.
     >
     >

     Se Ocorreu uma falha com a tarefa de Olá, Olá DAG detalhes apresentará um Estado de FALHADO, juntamente com hiperligações tooinformation sobre a tarefa falhada Olá. Informações de diagnóstico serão apresentadas abaixo os detalhes de Olá DAG.
8. Selecione **visualização gráfica**. Esta ação apresenta uma representação gráfica de Olá DAG. É possível colocar o rato Olá através de cada vértice nas informações de toodisplay vista Olá acerca do mesmo.

    ![Vista gráfica](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Clicar num vértice carregará Olá **vértice detalhes** para esse item. Clique em Olá **mapa 1** detalhes de toodisplay vértice para este item. Selecione **confirmar** navegação de Olá tooconfirm.

    ![Detalhes de vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Tenha em atenção que tem agora ligações na Olá parte superior da página Olá toovertices relacionados e tarefas.

    > [!NOTE]
    > Também pode chegam esta página por Retroceder demasiado**DAG detalhes**, selecionando **vértice detalhes**e, em seguida, selecionar Olá **mapa 1** vértice.
    >
    >

    * **Contadores de vértice** apresenta informações do contador para este vértice.
    * **Tarefas** apresenta tarefas para esta vértice.
    * **Tentativas de tarefas** apresenta informações sobre as tarefas de toorun de tentativas para este vértice.
    * **Origens & Sinks** mostra origens de dados e sinks para este vértice.

      > [!NOTE]
      > Como com o menu de anterior Olá, pode se deslocar para a apresentação de coluna Olá para tarefas, as tentativas de tarefas e origens & Sinks__ toodisplay liga toomore informações para cada item.
      >
      >
11. Selecione **tarefas**, e, em seguida, o nome do item de Olá selecione **00_000000**. Isto irá apresentar **detalhes da tarefa** para esta tarefa. Neste ecrã, pode ver **tarefas contadores** e **tarefas tentativas**.

    ![Detalhes da tarefa](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Passos Seguintes
Agora que aprendeu como ver toouse Olá Tez, saiba mais sobre [utilizando o Hive no HDInsight](hdinsight-use-hive.md).

Para obter mais informações técnicas no Tez, consulte Olá [Tez página em Hortonworks](http://hortonworks.com/hadoop/tez/).
