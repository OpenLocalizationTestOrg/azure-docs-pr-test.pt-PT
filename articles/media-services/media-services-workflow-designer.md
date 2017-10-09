---
title: "aaaCreate avançadas codificação fluxos de trabalho com o estruturador de fluxo de trabalho | Microsoft Docs"
description: "Saiba mais sobre como toocreate avançadas codificação fluxos de trabalho com o estruturador de fluxo de trabalho."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>Criar Fluxos de Trabalho de Codificação Avançados com o Estruturador de Fluxos de Trabalho
## <a name="overview"></a>Descrição geral
Olá **estruturador de fluxo de trabalho** é uma ferramenta de ambiente de trabalho do Windows que é utilizados toodesign e compilação fluxos de trabalho personalizados para codificação com **o fluxo de trabalho do suporte de dados codificador Premium**.
Através da utilização de energia Olá da ferramenta de estruturador de fluxo de trabalho de Olá, pode conceber e criar fluxos de trabalho complexos que serão executada no **Premium codificador de multimédia**.  

Fluxos de trabalho podem incluir a lógica de decisão de cliente e a ramificação com base nas propriedades do ficheiro de origem de entrada Olá. Pode criar fluxos de trabalho com substituíveis propriedades e valores dinâmicos toomake Olá mesmo mais complexo codificação tarefas fácil toorepeat e personalizar na nuvem de Olá.

Os fluxos de trabalho de exemplo que pode criar incluem:

* Decisão baseada em fluxos de trabalho que inspecionem conteúdo de origem Olá para a resolução e codificar apenas controla de saída de Olá assim o desejar.  Isto é helfpul eliminando Olá desperdiçado controla que seria gerada pelo upscaling inadvertantly de conteúdo de origem Olá.
* Vários ficheiros de entrada podem ser utilizados toosupport legendas, as Sobreposições e stitching conteúdo em conjunto. 

Esta ferramenta pode também ser utilizada toomodify qualquer uma das nossas [publicados fluxos de trabalho](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> Contacte o seu cópia da ferramenta do estruturador de fluxo de trabalho de Olá, tooget mepd@microsoft.com.
> 
> 

Quando é criado um ficheiro de fluxo de trabalho, pode ser carregado como um recurso e, em seguida, ser utilizada para codificação ficheiros de suporte de dados. Para obter informações sobre como tooencode com **o fluxo de trabalho do suporte de dados codificador Premium** utilizando **.NET**, consulte [avançadas codificação com o fluxo de trabalho do suporte de dados codificador Premium](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Modificar os fluxos de trabalho existentes
Olá predefinido [publicados fluxos de trabalho](media-services-workflow-designer.md#existing_workflows) pode ser modificado utilizando a ferramenta de estruturador Olá. Pode obter ficheiros de fluxo de trabalho predefinido Olá [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). pasta de Olá também contém a descrição de Olá destes ficheiros.

Olá vídeos os seguintes demonstram como toouse Olá designer.

### <a name="day-1--getting-started"></a>Dia 1 – Introdução
Vídeo de 1 dia abrange:

* Descrição geral do estruturador
* Fluxos de trabalho básicos – "Olá mundo"
* Criar vários ficheiros MP4 para utilização com Media Services do Azure de transmissão em fluxo de saída

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Dia 2
Vídeo de 2 dias abrange:

* Vários cenários de ficheiro de origem – processamento de áudio
* Fluxos de trabalho com lógica avançada
* Fases do gráfico

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>3 dias
Vídeo de 3 dias abrange:

* Scripting dentro de fluxos de trabalho/esquemas
* Restrições com Olá codificador atual
* AS PERGUNTAS E RESPOSTAS

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Passo seguinte
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Se precisar de suportar ou tiver dúvidas sobre a criação de fluxos de trabalho personalizados na ferramenta de estruturador de fluxo de trabalho de Olá, envie um e-mail toomepd@microsoft.com.

## <a name="see-also"></a>Veja Também
[Vídeos de formação do estruturador de fluxo de trabalho de codificador Premium do Azure](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

