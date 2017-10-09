---
title: "aaaEncode um elemento com o codificador de multimédia Standard com Olá portal do Azure | Microsoft Docs"
description: "Este tutorial explica Olá passos da codificação de um elemento com o codificador de multimédia Standard com Olá portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Codificar um elemento com o codificador de multimédia Standard com Olá portal do Azure
> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Ao trabalhar com uma das situações mais comuns Olá é a distribuição de clientes de tooyour transmissão em fluxo de velocidade de transmissão adaptável de Media Services do Azure. Os Media Services suportam Olá seguintes tecnologias de transmissão em fluxo velocidade de transmissão adaptável: HTTP Live Streaming (HLS), transmissão em fluxo uniforme, MPEG DASH. tooprepare seus vídeos para transmissão em fluxo de velocidade de transmissão adaptável, terá de tooencode a origem de vídeo em ficheiros de transmissão múltipla. Deve utilizar Olá **codificador de multimédia Standard** codificador tooencode seus vídeos.  

Os Media Services também fornecem um empacotamento dinâmico, permitindo toodeliver dos seus MP4s de transmissão múltipla no Olá seguintes formatos de transmissão em fluxo: MPEG DASH, HLS, transmissão em fluxo uniforme, sem ter toore-pacote para estes formatos de transmissão em fluxo. Com o empacotamento dinâmico só tem toostore e pagamento para ficheiros de Olá num único formato de armazenamento e dos Media Services irão compilar e disponibilizar a resposta adequada Olá com base nos pedidos de um cliente.

tootake partido do empacotamento dinâmico, precisa de tooencode o ficheiro de origem para um conjunto de ficheiros MP4 de velocidade de transmissão múltipla (passos Olá da codificação são demonstrados mais à frente nesta secção).

suporte de dados de tooscale processar, consulte [isto](media-services-portal-scale-media-processing.md) tópico.

## <a name="encode-with-hello-azure-portal"></a>Codificar com Olá portal do Azure
Esta secção descreve os passos de Olá que pode tomar tooencode o conteúdo com o codificador de multimédia Standard.

1. No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.
2. No Olá **definições** janela, selecione **ativos**.  
3. No Olá **ativos** janela, asset Olá selecione que gostaria de tooencode.
4. Olá prima **codificar** botão.
5. No Olá **codificar um elemento** janela, o processador "Codificador de multimédia Standard" Olá selecione e uma predefinição. Para obter informações sobre predefinições, veja [Gerar automaticamente uma escala de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de Tarefas para MES](media-services-mes-presets-overview.md). Se planear toocontrol que predefinição de codificação é utilizada, evitar que isto em mente: é importante tooselect Olá predefinido que é mais adequada para o seu vídeo de entrada. Por exemplo, se souber o seu vídeo de entrada tem uma resolução de 1920 x 1080 pixels, em seguida, pode utilizar Olá "H264 múltipla 1080p" predefinidas. Se tiver um vídeo de baixa resolução (640 x 360), não deve estar a utilizar a predefinição "H264 Taxas de Bits Múltiplas 1080p".
   
   Para facilitar a gestão, tem uma opção de edição Olá nome do elemento de saída Olá e nome de Olá da tarefa de Olá.
   
   ![Codificar elementos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Prima **Criar**.

## <a name="next-step"></a>Passo seguinte
Pode monitorizar o progresso da tarefa codificação com Olá portal do Azure, conforme descrito em [isto](media-services-portal-check-job-progress.md) artigo.  

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

