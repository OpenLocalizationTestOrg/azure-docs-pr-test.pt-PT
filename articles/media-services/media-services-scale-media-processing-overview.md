---
title: "Descrição geral do suporte de dados de processamento aaaScaling | Microsoft Docs"
description: "Este tópico é uma descrição geral do suporte de dados de dimensionamento processamento com Media Services do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Descrição geral do suporte de dados de processamento de dimensionamento
Esta página fornece uma descrição geral de como e por que motivo tooscale processamento de suporte de dados. 

## <a name="overview"></a>Descrição geral
Uma conta de Media Services está associada um tipo de unidade reservado, que determina a velocidade de Olá com que o suporte de dados de processamento de tarefas é processados. Pode escolher entre seguinte Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**. Por exemplo, Olá mesma tarefa de codificação é executada mais rapidamente quando utilizar Olá **S2** tipo de unidade reservada comparar toohello **S1** tipo. Para obter mais informações, consulte Olá [reservado tipos de unidade](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Além disso toospecifying Olá reservados de um tipo de unidade, tooprovision pode especificar a conta com unidades reservadas. número de Olá de unidades reservadas aprovisionados determina o número de Olá das tarefas de suporte de dados que podem ser processados em simultâneo numa conta especificada. Por exemplo, se a sua conta tem cinco unidades reservadas, em seguida, as tarefas de suporte de dados de cinco estarão em execução em simultâneo desde como existem toobe tarefas processado. tarefas restantes Olá irão aguardar na fila de Olá e irão obter captadas para processar sequencialmente quando terminar, uma tarefa em execução. Se uma conta não tem quaisquer unidades reservadas aprovisionadas, em seguida, tarefas irão estar captadas sequencialmente. Neste caso, Olá Aguarde algum tempo entre uma tarefa a concluir a e hello iniciar junto de um dependerá da disponibilidade de Olá dos recursos no sistema de Olá.

## <a name="choosing-between-different-reserved-unit-types"></a>Escolher entre tipos diferentes de unidade reservada
Olá, a tabela seguinte ajuda-o a tomar a decisão ao escolher entre diferentes velocidades de codificação. Também fornece alguns casos de benchmark e fornece os URLs de SAS que podem utilizar vídeos toodownload em que pode realizar os seus próprios testes:

| Cenários | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Caso de utilização prevista |Velocidade de transmissão única de codificação. <br/>Ficheiros SD ou abaixo resoluções, não um prazo confidenciais, baixo custo. |Velocidade de transmissão única e várias codificação de velocidade de transmissão.<br/>Utilização normal para SD e HD codificação. |Velocidade de transmissão única e várias codificação de velocidade de transmissão.<br/>Vídeos de resolução do HD e de 4K completos. Tempo de resposta mais rápida confidencial, mais rápida de codificação. |
| Benchmark |[Ficheiro de entrada: 5 minutos longos 640x360p em 29.97 fotogramas por segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Ficheiro MP4 de velocidade de transmissão única tooa de codificar em Olá resolução do mesma, demora cerca de 11 minutos. |[Ficheiro de entrada: 5 minutos longos 1280x720p em 29.97 fotogramas por segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>Com "H264 velocidade de transmissão única 720p" predefinição de codificação demora cerca de 5 minutos.<br/><br/>Codificação com "H264 múltipla 720p" predefinição demora cerca de 11.5 minutos. |[Ficheiro de entrada: 5 minutos longos 1920x1080p em 29.97 fotogramas por segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>Com "H264 velocidade de transmissão única 1080p" predefinição de codificação demora cerca de 2.7 minutos.<br/><br/>Codificação com "H264 múltipla 1080p" predefinição demora cerca de 5.7 minutos. |

## <a name="considerations"></a>Considerações
> [!IMPORTANT]
> Reveja as considerações descritas nesta secção.  
> 
> 

* Unidades reservadas de trabalho para parallelizing todo o processamento de suporte de dados, incluindo a indexação tarefas utilizando o indexador de suporte de dados do Azure.  No entanto, ao contrário da codificação, os trabalhos de indexação não são processados mais depressa com unidades reservadas mais rápidas.
* Se utilizar Olá partilhado conjunto, ou seja, sem qualquer unidades reservadas de, em seguida, tem das tarefas de codificar Olá mesmo desempenho tal como acontece com S1 RUs. No entanto, com as suas tarefas podem gastam num Estado em fila sem limite superior toohello tempo e, em qualquer momento, no máximo apenas uma tarefa estarão em execução.
* Olá seguintes centros de dados não oferecem Olá **S2** reservados de um tipo de unidade: sul do Brasil e oeste da Índia.
* Olá seguintes Centro de dados não oferecem Olá **S3** reservados de um tipo de unidade: Índia Ocidental.

## <a name="billing"></a>Faturação

São-lhe cobrados os minutos efetivos de utilização de Unidades Reservadas de Multimédia. Para obter uma explicação detalhada, consulte a secção Olá FAQ Olá [preços dos Media Services](https://azure.microsoft.com/pricing/details/media-services/) página.   

## <a name="quotas-and-limitations"></a>Quotas e limitações
Para obter informações sobre quotas e limitações e como tooopen um pedido de suporte, consulte [Quotas e limitações](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Passo seguinte
Alcançar Olá dimensionamento processar tarefas com uma destas tecnologias de suporte de dados: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

