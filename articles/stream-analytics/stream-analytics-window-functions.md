---
title: "as funções de janela de análise do aaaIntroduction tooStream | Microsoft Docs"
description: "Saiba mais sobre Olá três as funções de janela no Stream Analytics (em cascata, hopping, a deslizante)."
keywords: em cascata janela, numa janela, hopping janela deslizante
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Funções de janela de análise de tooStream de introdução
Em tempo real muitos cenários de transmissão em fluxo, é necessário tooperform operações apenas nos dados de Olá contidos no windows temporais. Suporte nativo para funções de modos de janela é uma funcionalidade chave do Azure Stream Analytics que são transmitidos agulha Olá na produtividade do programador na criação as tarefas de processamento de fluxo complexas. Do Stream Analytics permite aos programadores toouse [ **em cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) e [ **deslizantes** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operações dados de transmissão em fluxo. É importante salientar que, todos os [janela](https://msdn.microsoft.com/library/dn835019.aspx) operações saída resultados em Olá **final** da janela de Olá. saída de Olá da janela de Olá será evento único com base na função de agregação Olá utilizada. evento de Olá terão carimbo de hora Olá da extremidade Olá da janela de Olá e todas as funções de janela estão definidas com um comprimento fixo. Por último é importante toonote que todas as funções de janela devem ser utilizadas num [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) cláusula.

![Conceitos de funções de janela de análise de fluxo](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Janela em cascata
As funções de janela em cascata são utilizado toosegment um fluxo de dados em segmentos de hora diferente e uma função contra eles, como exemplo de Olá abaixo. differentiators de chave Olá de uma janela em cascata são que eles repetir, não se sobreponha e um evento não pode pertencer toomore que uma janela em cascata.

![Funções de janela de análise de fluxo em cascata introdução](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Janela de salto
Salto salto de funções de janela reencaminhar na hora por um período fixo. Poderá ser toothink fácil deles como janelas em cascata podem sobrepor-se, pelo que os eventos podem pertencer toomore que um conjunto de resultados de janela Hopping. toomake uma janela de Hopping Olá mesmo como uma janela em cascata um especificaria simplesmente toobe de tamanho de salto Olá Olá mesmo como o tamanho da janela Olá. 

![Janela do Stream Analytics funciona salto de introdução](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Numa janela deslizante
Funções de janela deslizante, ao contrário do salto windows, ou em cascata produzem uma saída **apenas** quando ocorre um evento. Cada janela vai ter, pelo menos, um evento e janela Olá continuamente move reencaminhar por um € (epsilon). Como salto Windows, os eventos podem pertencer toomore que uma janela a deslizante.

![Funções de Stream Analytics janela deslizante de introdução](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Obter ajuda com as funções de janela
Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

