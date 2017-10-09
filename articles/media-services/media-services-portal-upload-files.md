---
title: "AAA\"ficheiros de carregamento para uma conta de Media Services utilizando Olá portal do Azure | Microsoft Docs\""
description: "Este tutorial explica Olá passos de carregamento de ficheiros para uma conta de Media Services utilizando Olá portal do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Carregar ficheiros para uma conta de Media Services utilizando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


Nos Serviços de Multimédia, os ficheiros digitais são carregados para um elemento. Olá recurso pode conter vídeo, áudio, imagens, coleções de miniaturas, texto controla e legendas ficheiros (e Olá metadados sobre estes ficheiros.) Depois de Olá ficheiros são carregados, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.


## <a name="upload-files"></a>Carregar ficheiros

>[!NOTE]
>Não há um limite toohello tamanho máximo suportado para processamento nos Media Services. Consulte [isto](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre limitação de tamanho de ficheiro Olá.
>

1. No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.
2. No Olá **definições** painel, clique em **ativos**.
   
    ![Carregar ficheiros](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Clique em Olá **carregar** botão.
   
    Olá **carregar um elemento de vídeo** surge a janela.
   
   > [!NOTE]
   > Não existe qualquer limite de tamanho de ficheiro.
   > 
   > 
4. Procurar as vídeo toohello pretendido no seu computador, selecione-o e clique em OK.  
   
    Olá carregamento inicia e pode ver o progresso de Olá em nome de ficheiro Olá.  

Após a conclusão do carregamento de Olá, verá Olá novo elemento listado na Olá **ativos** janela. 

## <a name="next-steps"></a>Passos seguintes
Agora, pode codificar os elementos que carregar. Para obter mais informações, veja [Codificar elementos](media-services-portal-encode.md)

Também pode utilizar as funções do Azure tootrigger uma tarefa de codificação baseada num ficheiro chegar no contentor de Olá configurado. Para obter mais informações, veja [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

