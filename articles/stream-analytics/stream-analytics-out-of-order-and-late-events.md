---
title: aaaHandling ordem de eventos e lateness Azure Stream Analytics | Microsoft Docs
description: Saiba mais sobre como funciona o Stream Analytics com eventos fora de ordem ou enlace tardio em fluxos de dados.
keywords: fora de ordem, eventos
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Processamento de ordem de eventos do Azure Stream Analytics

Numa transmissão em fluxo temporal dados de eventos, cada evento é registado com a hora de Olá esse evento Olá é recebido. Algumas condições poderão fazer com que os fluxos de eventos toooccasionally receber alguns eventos por uma ordem diferente, a qual foram enviadas. Retransmitir uma TCP simple ou até mesmo um desfasamento de relógio entre Olá enviar hello a receber de hub de eventos e de dispositivos pode causar este toooccur. Eventos de "Pontuação" também são adicionados tooreceived fluxos de eventos, tempo de Olá tooadvance na ausência Olá arrivals de eventos. Estas são necessárias em cenários como "Notificar-me quando não existem inícios de sessão ocorrer para 3 minutos."

Fluxos de entrada que não estão na ordem são:
* Ordenada (e, por isso **atrasada**).
* Tendo em conta pelo sistema Olá, de acordo com a política de utilizador especificado tooa.


## <a name="lateness-tolerance"></a>Tolerância lateness
Do Stream Analytics tolerates estes tipos de cenários. Análise de fluxo tem o processamento de eventos "fora de ordem" e "dinâmico". Processa a estes eventos no Olá seguintes formas:

* Os eventos que chegam desordenados mas dentro Olá definir tolerância são **reordenados por timestamp**.
* Os eventos que chegam posterior tolerância são **removido ou ajustado**.
    * **Tendo em conta**: tooappear ajustada toohave chegou momento Olá mais recente aceitável.
    * **Removido**: rejeitados.

![Processamento de eventos do Stream Analytics](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Reduza o número de Olá de eventos de fora de ordem

Porque o Stream Analytics aplica uma transformação temporal quando processa eventos de entrada (por exemplo, para as agregações ou associações temporais), o Stream Analytics ordena os eventos recebidos por ordem de timestamp.

Quando estiver a palavra-chave de Olá "timestamp por" **não** utilizado, tempo de colocar em fila de eventos do Olá Event Hubs do Azure é utilizado por predefinição. Os Event Hubs garante monotonicity de Olá timestamp em cada partição Olá do hub de eventos. Esta ação garante também que os eventos a partir de todas as partições serão Unidos timestamp por ordem. Estes dois garantias de Event Hubs Certifique-se não há eventos fora de ordem.

Por vezes, é importante para timestamp toouse Olá do remetente. Nesse caso, um carimbo do payload do evento Olá é escolhido utilizando "timestamp por". Nestes cenários, poderão ser introduzidas um ou mais origens de misorder de evento:

* Os produtores de eventos tem skews relógio. Isto é comum quando produtores de computadores diferentes, pelo que têm relógios diferentes.
* Não há um atraso de rede a partir da origem de Olá Olá eventos toohello destino do hub de eventos.
* O relógio skews existem entre as partições do hub de eventos. Do Stream Analytics pela primeira vez ordena eventos a partir de todas as partições do hub de eventos por hora de colocar em fila de eventos. Em seguida, examina a sequência de dados de Olá misordered eventos.

No separador de configuração de Olá, consulte Olá seguintes predefinições:

![Processamento do Stream Analytics fora de ordem](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Se utilizar 0 segundos como período de tolerância de fora de ordem de Olá, afirma que todos os eventos são, por ordem, tempo Olá. Tendo em conta Olá três as origens de eventos misordered, é provável que este é verdadeiro. 

tooallow Stream Analytics toocorrect misorder um evento, pode especificar um período de tolerância fora de ordem de diferente de zero. Stream Analytics coloca os eventos de cópia de segurança toothat janela e, em seguida, reordena-los utilizando Olá timestamp que escolheu. Em seguida, aplica-se transformação temporal Olá. Pode começar com uma janela de 3-segundo e otimizar Olá valor tooreduce Olá diversas eventos que são hora ajustada. 

Um efeito de colocação em memória intermédia Olá está saída Olá **atrasada pelo Olá mesmo período de tempo**. Pode otimizar Olá valor tooreduce Olá número fora de ordem eventos e manter a latência de tarefa Olá baixa.

## <a name="get-help"></a>Obter ajuda
Para obter assistência adicional, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar tarefas do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da REST API de gestão de análise de fluxo](https://msdn.microsoft.com/library/azure/dn835031.aspx)