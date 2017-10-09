---
title: velocidade de gerir AAA e simultaneidade da sua encoding com Media Services do Azure | Microsoft Docs
description: "Este artigo fornece uma breve descrição geral de como pode gerir velocidade e simultaneidade das suas tarefas/tarefas codificação com Media Services do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Gerir velocidade e simultaneidade da codificação

Este artigo fornece uma breve descrição geral de como pode gerir velocidade e simultaneidade de tarefas as codificação/tarefas.

## <a name="overview"></a>Descrição geral

Nos Media Services, um **um tipo de unidade reservado** determina a velocidade de Olá com que o suporte de dados de processamento de tarefas é processados. Pode escolher entre seguinte Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**. Por exemplo, Olá mesma tarefa de codificação é executada mais rapidamente quando utilizar Olá **S2** tipo de unidade reservada comparar toohello **S1** tipo. Olá [dimensionamento unidades de codificação](media-services-scale-media-processing-overview.md) tópico mostra uma tabela que o ajuda a tomar a decisão ao escolher entre diferentes velocidades de codificação.

Além disso toospecifying Olá reservados de um tipo de unidade, pode especificar a conta com tooprovision **unidades reservadas**. número de Olá de unidades reservadas aprovisionados determina o número de Olá das tarefas de suporte de dados que podem ser processados em simultâneo numa conta especificada. Por exemplo, se a sua conta tem cinco unidades reservadas, em seguida, as tarefas de suporte de dados de cinco estarão em execução em simultâneo desde como existem toobe tarefas processado. tarefas restantes Olá irão aguardar na fila de Olá e irão obter captadas para processar sequencialmente quando terminar, uma tarefa em execução. Se uma conta não tem quaisquer unidades reservadas aprovisionadas, em seguida, tarefas irão estar captadas sequencialmente. Neste caso, Olá Aguarde algum tempo entre uma tarefa a concluir a e hello iniciar junto de um dependerá da disponibilidade de Olá dos recursos no sistema de Olá.

Para obter informações detalhadas e exemplos que mostram como unidades de codificação tooscale, consulte [isto](media-services-scale-media-processing-overview.md) tópico.

## <a name="next-step"></a>Passo seguinte

[Unidades de codificação de escala](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

