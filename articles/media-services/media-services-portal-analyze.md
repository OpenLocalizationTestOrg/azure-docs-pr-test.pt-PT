---
title: "aaaAnalyze suportes de dados utilizando Olá portal do Azure | Microsoft Docs"
description: "Este tópico descreve como tooprocess Olá de suporte de dados com processadores de suporte de dados de análise de multimédia (MP) utilizando o portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analisar o suporte de dados através de Olá portal do Azure
> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Descrição geral
Análise de serviços de multimédia do Azure é uma coleção de voz e visão componentes (escala empresarial, a conformidade, a segurança e alcance global) que torna mais fácil para organizações e empresas tooderive acionáveis dos respetivos ficheiros de vídeo. Para obter mais descrição geral da análise de serviços de multimédia do Azure consulte [isto](media-services-analytics-overview.md) tópico. 

Este tópico descreve como tooprocess Olá de suporte de dados com processadores de suporte de dados de análise de multimédia (MP) utilizando o portal do Azure. Pacotes de gestão de análise de multimédia produzem ficheiros MP4 ou ficheiros JSON. Se um processador de multimédia produzir um ficheiro MP4, pode transferir progressivamente ficheiros Olá. Se um processador de multimédia produzir um ficheiro JSON, pode transferir o ficheiro de Olá de Olá blob storage do Azure. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Escolha um recurso que pretende que o tooanalyze
1. No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.
2. No Olá **definições** janela, selecione **ativos**.  
   .
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Elemento de Olá selecione que gostaria de Olá tooanalyze e prima **analisar** botão.
   
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. No Olá **recurso de multimédia de processo com a análise de multimédia** janela, o processador de Olá selecione. 
   
    Olá resto artigo Olá explica por que razão e como toouse cada processador. 
5. Prima **criar** toohello iniciar uma tarefa.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Olá **indexador de suporte de dados do Azure** processador de multimédia permite-lhe toomake ficheiros de suporte de dados e conteúdo pesquisável, bem como gerar controla captioning fechada. Estas secções fornece alguns detalhes sobre as opções que pode especificar para este pacote de gestão.

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Idioma
Olá toobe de linguagem natural reconhecido no ficheiro multimedia Olá. Por exemplo, inglês ou espanhol. 

### <a name="captions"></a>Legendas
Pode escolher um formato de legenda que será gerado a partir do seu conteúdo. Uma tarefa de indexação pode gerar ficheiros de legendas no Olá seguintes formatos:  

* **SAMI**
* **TTML**
* **WebVTT**

Fechado ficheiros de legenda (CC) nestes formatos podem ser utilizados toomake áudio e vídeo ficheiros toopeople acessível com hearing disability.

### <a name="aib-file"></a>Ficheiro AIB
Selecione esta opção se que seria, como ficheiro de áudio índice Blob Olá toogenerate para utilização com Olá IFilter de servidor de SQL personalizados. Para obter mais informações, consulte [isto](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogue.

### <a name="keywords"></a>Palavras-chave
Selecione esta opção se pretender que o toogenerate um ficheiro XML de palavras-chave. Este ficheiro contém palavras-chave extraídas do conteúdo de reconhecimento de voz de Olá, com frequência e informações de deslocamento.

### <a name="job-name"></a>Nome da tarefa
Um nome amigável que lhe permite identificar Olá tarefa. [Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa. 

### <a name="output-file"></a>Ficheiro de saída
Um nome amigável que lhe permite identificar Olá conteúdo de saída. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Hyperlapse de multimédia do Azure é um pacote de gestão que cria uniforme vídeos passado o tempo do conteúdo primeira pessoa ou ação câmara.  Para obter mais informações, veja [este](media-services-hyperlapse-content.md) tópico. Estas secções fornece alguns detalhes sobre as opções que pode especificar para este pacote de gestão.

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Velocidade
Especifique a velocidade de Olá com que toospeed segurança as vídeo de entrada de Olá. o resultado de Olá é um rendition stabilized e passado o tempo de vídeo de entrada Olá.

### <a name="job-name"></a>Nome da tarefa
Um nome amigável que lhe permite identificar Olá tarefa. [Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa. 

### <a name="output-file"></a>Ficheiro de saída
Um nome amigável que lhe permite identificar Olá conteúdo de saída. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
Olá **Azure suporte de dados enfrentam Detector** processador de multimédia (MP) permite-lhe toocount, controlar movimentos e mesmo participação do medidor público-alvo e reação através de expressões facial. Este serviço contém duas funcionalidades: 

* **Deteção de rostos em**
  
    Deteção de rostos em localiza e controla faces humanos dentro de um vídeo. Vários faces podem ser detetados e, subsequentemente, ser monitorizados como estes mover-se, com metadados de hora e a localização do Olá devolvidos num ficheiro JSON. Durante o controlo, tentará toogive um toohello ID consistente, mesmo enfrentam enquanto pessoa Olá está a mover à volta no ecrã, mesmo que estes são obstructed ou deixam brevemente moldura Olá.
  
  > [!NOTE]
  > Este serviços não efetua o reconhecimento facial. Uma pessoa que mantém moldura Olá ou fica obstructed para demasiado tempo terá um novo ID quando devolvem.
  > 
  > 
* **Deteção de emoções**
  
    Deteção de emoções é um componente opcional do Olá processador de multimédia de deteção de rostos em devolve Analysis Services em vários atributos emotional de Olá faces detetados, incluindo happiness, sadness, fear, anger e muito mais. 

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Modo de deteção
Um dos seguintes modos de Olá pode ser utilizado pelo processador de Olá:

* Deteção de rostos em
* por deteção de emoções de rostos em
* Deteção de emoções agregado

### <a name="job-name"></a>Nome da tarefa
Um nome amigável que lhe permite identificar Olá tarefa. [Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa. 

### <a name="output-file"></a>Ficheiro de saída
Um nome amigável que lhe permite identificar Olá conteúdo de saída. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
Olá **Detector de movimento de suporte de dados do Azure** ativa de processador (MP do) suporte de dados tooefficiently identificar secções de interesse num vídeo longo e uneventful caso contrário. Deteção de movimento pode ser utilizada em câmara estático filmagens tooidentify secções de vídeo olá onde ocorre o movimento. Gera um ficheiro JSON que contém um metadados com carimbos e Olá delimitadora região onde ocorreu o evento de Olá.

Direcionado para os feeds de vídeo de segurança, esta tecnologia é toocategorize capaz de movimento em eventos relevantes e falsos positivos, tais como sombras e alterações de lighting. Isto permite-lhe alertas de segurança toogenerate da câmara feeds sem ser spammed com eventos irrelevantes endless, enquanto que está a ser instantes tooextract capaz de interesse de vídeos de vigilância extremamente longos.

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Este processador pode ajudar a criar resumos dos vídeos longos selecionando automaticamente interessantes fragmentos do vídeo de origem Olá. Isto é útil quando pretende tooprovide uma descrição geral rápida do que tooexpect um vídeo longo. Para obter informações detalhadas e exemplos, consulte [utilize as miniaturas de vídeo do Azure multimédia tooCreate um resumo de vídeo](media-services-video-summarization.md)

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Nome da tarefa
Um nome amigável que lhe permite identificar Olá tarefa. [Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa. 

### <a name="output-file"></a>Ficheiro de saída
Um nome amigável que lhe permite identificar Olá conteúdo de saída. 

## <a name="next-steps"></a>Passos seguintes
Vista dos Media Services percursos de aprendizagem.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

