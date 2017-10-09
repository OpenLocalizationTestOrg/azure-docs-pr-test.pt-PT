---
title: Guia de aaaTroubleshooting para o Azure Stream Analytics | Microsoft Docs
description: Como tootroubleshoot a tarefa de Stream Analytics
keywords: "Guia de resolução de problemas"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Guia de resolução de problemas para o Azure Stream Analytics

Resolução de problemas de Stream Analytics do Azure o pode aparecer à primeira vista toobe um esforço complexo. Depois de trabalharem com muitos utilizadores, criou este processo de Olá do guia toohelp otimizar e remover guesswork Olá sobre as entradas, saídas, consultas e funções.

## <a name="troubleshoot-your-stream-analytics-job"></a>Resolver problemas relacionados com a tarefa de Stream Analytics

Para obter os melhores resultados na sua tarefa do Stream Analytics de resolução de problemas, utilize Olá seguintes diretrizes:

1.  Teste a conectividade:
    - Verifique a conectividade tooinputs e saídas utilizando Olá **Testar ligação** botão para cada entrada e saída.

2.  Examine os dados de entrada:
    - tooverify dados de entrada é que fluem para Hub de eventos, utilize [Explorador do Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure Hub de eventos (se for utilizada a entrada do Hub de eventos).  
    - Olá utilize [ **dados de exemplo** ](stream-analytics-sample-data-input.md) botão para cada entrada e transferir os dados de entrada de exemplo de Olá.
    - Inspecione forma Olá toounderstand de dados de exemplo de Olá dos dados de Olá: Olá esquema e Olá [tipos de dados](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  A consulta de teste:
    - No Olá **consulta** separador, utilize Olá **testar** botão consulta de Olá tootest e utilizar dados de exemplo de Olá transferido demasiado[teste Olá consulta](stream-analytics-test-query.md). Examine os erros e tente toocorrect-los.
    - Se utilizar [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verifique se os eventos de Olá têm carimbos maiores Olá [hora de início da tarefa](stream-analytics-out-of-order-and-late-events.md).

4.  A consulta de depuração:
    - Reconstrua a consulta de Olá progressivamente de agregados de complexas de toomore de instrução select simples, utilizando os passos. utilizar toobuild segurança lógica de consulta Olá passo a passo, [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) cláusulas.
    - Utilize [SELECT INTO](stream-analytics-select-into.md) toodebug passos da consulta.

5.  Eliminar pitfalls comuns, tais como:
    - A [ **onde** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) cláusula FROM na consulta de Olá filtrados por todos os eventos, impedir que quaisquer dados que está a ser gerado.
    - Quando utiliza as funções de janela, aguarde toosee de duração de janela todo Olá um resultado de consulta Olá.
    - Olá timestamp eventos precede a hora de início de tarefa Olá e, por conseguinte, os eventos estão a ser ignorados.

6.  Utilize a ordenação de evento:
    - Se hello todos os passos anteriores trabalhados ajustar, aceda toohello **definições** painel e selecione [ **eventos ordenação**](stream-analytics-out-of-order-and-late-events.md). Certifique-se de que esta política está configurada para o que faz sentido no seu cenário. política de Olá *não* aplicada ao utilizar Olá **teste** consulta do botão tootest Olá. Este resultado é uma diferença entre no browser versus executar tarefa de Olá na produção de teste.

7.  Depurar utilizando métricas:
    - Se nenhuma saída é obter depois Olá esperado duração (com base na consulta de Olá), experimente o seguinte Olá:
        - Observe [ **monitorização métricas** ](stream-analytics-monitoring.md) no Olá **Monitor** separador. Porque os valores de Olá são agregados, métricas Olá atrasadas por alguns minutos.
            - Se os eventos de entrada > 0, a tarefa de Olá é tooread capaz de dados de entrada. Se os eventos de entrada não é > 0, em seguida:
                - toosee se a origem de dados de Olá tem dados válidos, registá-lo utilizando [Explorador do Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Esta verificação aplica-se de tarefa Olá está a utilizar o Hub de eventos como entrada.
                - Verifique toosee se o formato de serialização de dados de Olá e codificação de dados estão como esperado.
                - Se a tarefa de Olá utilizar um Hub de eventos, verifique toosee se Olá corpo de mensagem de saudação é *nulo*.
            - Se os erros de conversão de dados > 0 e climbing, seguinte Olá poderá ser verdadeira:
                - tarefa de Olá poderá não ser capaz de toode-serializar eventos Olá.
                - Olá esquema de eventos poderá não corresponder Olá definido ou era esperado o esquema de eventos de Olá na consulta de Olá.
                - Olá tipos de dados de alguns dos campos de Olá no evento Olá poderão não corresponder às expectativas do.
            - Se os erros de Runtime > 0, significa que essa tarefa Olá pode receber dados Olá, mas está a gerar erros ao processar a consulta de Olá.
                - erros de Olá toofind, aceda toohello [registos de auditoria](../azure-resource-manager/resource-group-audit.md) e filtre *falha* estado.
            - Se InputEvents > 0 e OutputEvents = 0, significa que uma das seguintes Olá for verdadeira:
                - O processamento da consulta resultou em zero eventos de saída.
                - Os campos ou eventos poderão estar incorreto, resultando na saída do zero após o processamento de consulta.
                - tarefa de Olá foi toohello de dados não é possível toopush [sink de saída](stream-analytics-select-into.md) por motivos de autenticação ou de conectividade.
        - Em todos os Olá mencionado anteriormente casos de erro, operações de mensagens de registo explicam detalhes adicionais (incluindo o que acontece), exceto nos casos em que a lógica de consulta Olá filtrada a todos os eventos. Se o processamento de Olá de vários eventos gera erros, o Stream Analytics registos Olá três primeiros mensagens de erro do mesmo tipo dentro de 10 minutos tooOperations de Olá regista. -Lo, em seguida, suprime erros idênticos adicionais com uma mensagem que lê "Erros estão a ocorrer demasiado rapidamente, que estes estão a ser suprimidos."

8. Depurar através da utilização de auditoria e registos de diagnóstico:
    - Utilize [registos de auditoria](../azure-resource-manager/resource-group-audit.md)e erros de filtro tooidentify e de depuração.
    - Utilize [os registos de diagnóstico da tarefa](stream-analytics-job-diagnostic-logs.md) erros tooidentify e depuração.

9. Examine Olá saídas:
    - Quando o estado da tarefa de Olá é *executar*, consoante a duração de Olá que stipulated consulta Olá, pode ver o resultado Olá na origem de dados do Olá sink.
    - Se não forem apresentadas saídas que vão tooa tipo de saída específico, redirecioná-los tooan tipo de saída que é menos complexo, tais como um Blob do Azure. Ao utilizar o Explorador de armazenamento, verifique toosee se saída Olá pode ser vista. Além disso, verifique se os limites de limitação na saída de Olá estão a impedir dados a ser recebidos.

10. Utilize a análise de fluxo de dados com a métrica de diagrama de tarefa:
    - dados tooanalyze fluxo e identificar problemas, utilize Olá [diagrama de tarefa com a métrica](stream-analytics-job-diagram-with-metrics.md).

11. Abra um incidente de suporte:
    - Por fim, se todos os resultarem, abra um incidente de suporte da Microsoft utilizando Olá SubscriptionID que contém a tarefa.

## <a name="get-help"></a>Obter ajuda

Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
