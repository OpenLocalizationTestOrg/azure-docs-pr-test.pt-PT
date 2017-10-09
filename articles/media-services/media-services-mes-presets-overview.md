---
title: "Predefinições de aaaTask para MES (codificador de multimédia Standard) | Microsoft Docs"
description: "Olá tópico fornecem e descrição geral das predefinições de tarefas para MES (codificador de multimédia Standard)."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Predefinições de tarefas para MES (Standard de codificador de multimédia)

**Codificador de multimédia Standard** define um conjunto de predefinições, pode utilizar quando criar tarefas de codificação de codificação. É recomendado Olá toouse "Transmissão em fluxo adaptável" se quiser tooencode um vídeo para transmissão em fluxo com os serviços de suporte de dados da configuração predefinida. Se especificar esta será codificador de multimédia Standard predefinida, [gerar automaticamente um ladder de velocidade de transmissão](media-services-autogen-bitrate-ladder-with-mes.md). 

No entanto, se precisar de toocustomize uma predefinição de codificação, deve efetuar uma das Olá codificação predefinições definidas nesta secção como um modelo para a sua configuração personalizada. Para explicações de que cada elemento estas predefinições significa e os valores válidos de Olá para cada elemento, consulte Olá [esquema codificador de multimédia Standard](media-services-mes-schema.md) tópico.  
  
> [!NOTE]
>  Quando utilizar uma predefinição de 4K codifica, deve obter Olá `S3` reservados de um tipo de unidade. Para obter mais informações, consulte [como tooScale codificação](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Ao trabalhar com o codificador de multimédia Standard, rotação está ativada por predefinição. Se as vídeo tenha sido registado num smartphone ou outro dispositivo móvel no modo de vertical, em seguida, estas predefinições serão, por predefinição, rodá-los tooLandscape modo tooencoding anterior (ao contrário, quando trabalha com o codificador de multimédia do Azure, onde o vídeo rotação é uma operação manual, conforme documentado no [isto](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blogue, em "Rotação de vídeo").  
  
Predefinições disponíveis:  
  
 [H264 de múltipla 1080p áudio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produz um conjunto de 8 ficheiros MP4 alinhada GOP, vão de 6000 kbps too400 kbps e AAC 5.1 áudio.  
  
 [H264 múltipla 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produz um conjunto de 8 ficheiros MP4 alinhada GOP, vão de 6000 kbps too400 kbps e stereo áudio AAC.  
  
 [H264 múltipla 16 x 9 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produz um conjunto de 8 ficheiros MP4 alinhada GOP, vão de 8500 kbps too200 kbps e stereo áudio AAC.  
  
 [H264 múltipla 16 x 9 SD áudio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produz um conjunto de 5 ficheiros MP4 alinhada GOP, vão de 1900 kbps too400 kbps e AAC 5.1 áudio.  
  
 [H264 múltipla 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produz um conjunto de 5 ficheiros MP4 alinhada GOP, vão de 1900 kbps too400 kbps e stereo áudio AAC.  
  
 [Áudio H264 múltipla 4K 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produz um conjunto de 12 ficheiros MP4 alinhada GOP, vão de 20000 kbps de too1000 kbps e AAC 5.1 áudio.  
  
 [H264 múltipla 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produz um conjunto de 12 ficheiros MP4 alinhada GOP, vão de 20000 kbps de too1000 kbps e stereo áudio AAC.  
  
 [H264 múltipla 4, 3 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produz um conjunto de 8 ficheiros MP4 alinhada GOP, vão de 8500 kbps too200 kbps e stereo áudio AAC.  
  
 [H264 múltipla 4 x 3 SD áudio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produz um conjunto de 5 ficheiros MP4 alinhada GOP, vão de 1600 kbps too400 kbps e AAC 5.1 áudio.  
  
 [H264 múltipla 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produz um conjunto de 5 ficheiros MP4 alinhada GOP, vão de 1600 kbps too400 kbps e stereo áudio AAC.  
  
 [H264 de múltipla 720p áudio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produz um conjunto de 6 ficheiros MP4 alinhada GOP, vão de 3400 kbps too400 kbps e AAC 5.1 áudio.  
  
 [H264 múltipla 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produz um conjunto de 6 ficheiros MP4 alinhada GOP, vão de 3400 kbps too400 kbps e stereo áudio AAC.  
  
 [Velocidade de transmissão única H264 1080p áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produz um único ficheiro MP4 com velocidade de transmissão de 6750 kbps e AAC 5.1 áudio.  
  
 [Velocidade de transmissão única do H264 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produz um único ficheiro MP4 com velocidade de transmissão de 6750 kbps e stereo áudio AAC.  
  
 [Velocidade de transmissão única do H264 4K áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produz um único ficheiro MP4 com velocidade de transmissão de 18000 kbps e AAC 5.1 áudio.  
  
 [Velocidade de transmissão única do H264 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produz um único ficheiro MP4 com velocidade de transmissão de 18000 kbps e stereo áudio AAC.  
  
 [Velocidade de transmissão única do H264 4 x 3 SD áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produz um único ficheiro MP4 com velocidade de transmissão de 1800 kbps e AAC 5.1 áudio.  
  
 [Velocidade de transmissão única do H264 4 x 3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produz um único ficheiro MP4 com velocidade de transmissão de 1800 kbps e stereo áudio AAC.  
  
 [Velocidade de transmissão única do H264 16 x 9 SD áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produz um único ficheiro MP4 com velocidade de transmissão de 2200 kbps e AAC 5.1 áudio.  
  
 [Velocidade de transmissão única do H264 16 x 9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produz um único ficheiro MP4 com velocidade de transmissão de 2200 kbps e stereo áudio AAC.  
  
 [Velocidade de transmissão única H264 720p áudio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produz um único ficheiro MP4 com velocidade de transmissão de 4500 kbps e AAC 5.1 áudio.  
  
 [Velocidade de transmissão única do H264 720p para Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) predefinição produz um único ficheiro MP4 com velocidade de transmissão de 2000 kbps e stereo AAC.  
  
 [Velocidade de transmissão única do H264 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produz um único ficheiro MP4 com velocidade de transmissão de 4500 kbps e stereo áudio AAC.  
  
 [H264 única de velocidade de transmissão elevada qualidade SD para Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produz um único ficheiro MP4 com velocidade de transmissão de 500 kbps e stereo áudio AAC...  
  
 [H264 única de velocidade de transmissão baixa qualidade SD para Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produz um único ficheiro MP4 com velocidade de transmissão de 56 kbps e stereo áudio AAC.  
  
 Para obter mais informações consulte tooMedia relacionados serviços codificadores, [codificação a pedido com Media Services do Azure](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
