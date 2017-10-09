---
title: "Olá aaaUse vista de execução de vértice nas ferramentas do Data Lake para Visual Studio | Microsoft Docs"
description: "Saiba como toouse Olá tarefas de Data Lake Analytics tooexam de vista de execução de vértice."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Utilize Olá vista de execução de vértice ferramentas do Data Lake para Visual Studio
Saiba como toouse Olá tarefas de Data Lake Analytics tooexam de vista de execução de vértice.

## <a name="prerequisites"></a>Pré-requisitos

É necessário um conhecimento básico da utilização de ferramentas do Data Lake em script do Visual Studio toodevelop U-SQL.  Consulte [Tutorial: desenvolver scripts U-SQL com ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Abrir Olá vista de execução de vértice
Abra uma tarefa de U-SQL no Data Lake Tools para Visual Studio. Clique em **vista de execução de vértice** no canto inferior esquerdo Olá. Poderá ser pedido tooload perfis pela primeira vez e pode demorar algum tempo consoante a conectividade de rede.

![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Compreender a vista de execução de vértice
Olá vista de execução de vértice tem três partes:

![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Olá **Seletor de vértice** no permite esquerdo Olá selecionar vértices as funcionalidades (tais como dados de 10 de principais de leitura ou optar por fase). Um dos filtros de mais frequentemente utilizadas Olá é toosee Olá **vértices no caminho crítico**. Olá **caminho crítico** Olá cadeia mais longo de vértices de uma tarefa de U-SQL. Caminho de crítico de Olá compreender é útil para otimizar as suas tarefas, verificando qual vértice demora tempo mais longo Olá.
  
![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

Painel de parte superior ao centro de Olá mostra Olá **com o estado de todos os vértices de Olá**.
  
![Vista de execução de vértice de ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

painel do Olá na parte inferior central mostra informações sobre cada vertex:
* : Processo Olá nome da instância do Olá vértice. -Lo é composto por diferentes partes no StageName | VertexName | VertexRunInstance. Por exemplo, vértice de .v1 [62] Olá SV7_Split representa Olá segunda instância em execução (.v1, índice a partir de 0) número vértice 62 na fase SV7_Split.
* Leitura de dados total/Written: Olá estavam dados leitura/escrita por esta vértice.
* Estado de estado/saída: Olá estado final quando vértice Olá é terminado.
* Tipo de falha do código de saída: Olá Ocorreu um erro ao vértice Olá falhou.
* Razão de criação: Por que motivo vértice Olá foi criado.
* Latência de fila do recurso latência/processe latência/PN: Olá tempo do Olá vértice toowait para recursos, tooprocess dados e toostay na fila de Olá.
* GUID de processo/criador: GUID vértice do Olá atual em execução ou o criador.
* Versão: instância Olá N-ésimo Olá executar vértice (sistema de Olá pode agendar a novas instâncias de um vértice para muitos motivos, por exemplo, ativação pós-falha, computação redundância, etc.)
* Versão criada tempo.
* Processar criar início tempo/processe em fila tempo/processe início tempo/processe concluída tempo: quando o processo de vértice Olá começa a criar; Quando o processo de vértice Olá inicia tooqueue; Quando Olá iniciado o processo determinadas vértice; Quando hello determinadas vértice está concluída.

## <a name="next-steps"></a>Passos seguintes
* informações de diagnóstico toolog, consulte [aceder a registos de diagnóstico para o Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* consulte os detalhes da tarefa tooview, [Browser de tarefa de utilização e a vista de tarefas para tarefas do Azure Data lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)
