---
title: "Carregar ficheiros para uma conta dos Serviços de Multimédia no portal do Azure | Microsoft Docs"
description: "Este tutorial orienta-o ao longo dos passos para carregar ficheiros para uma conta dos Serviços de Multimédia no portal do Azure."
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
ms.openlocfilehash: 7ddfe44918b358a1749640d1c93dba490855cc5a
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/18/2017
---
# <a name="upload-files-to-a-media-services-account-in-the-azure-portal"></a>Carregar ficheiros para uma conta dos Serviços de Multimédia no portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> Para concluir este tutorial, precisa de uma conta do Azure. Para obter mais detalhes, veja [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 

Nos Serviços de Multimédia do Azure, os ficheiros digitais são carregados para um elemento. O elemento pode conter ficheiros de vídeo, áudio, imagens, coleções de miniaturas, pistas de texto e legendas (e os metadados relativos a esses ficheiros). Assim que os ficheiros forem carregados, o seu conteúdo é armazenado em segurança na cloud, para processamento adicional e transmissão em fluxo.

> [!NOTE]
> Os Serviços de Multimédia têm um tamanho de ficheiro máximo para o processamento de ficheiros. Para obter mais informações sobre limites de tamanho de ficheiros, veja [Media Services quotas and limitations](media-services-quotas-and-limitations.md) (Quotas e limitações dos Serviços de Multimédia).
>

## <a name="upload-files"></a>Carregar ficheiros
1. No [portal do Azure](https://portal.azure.com/) selecione a sua conta de Serviços de Multimédia do Azure.
2. Selecione **Definições** > **Elementos**. Em seguida, selecione o botão **Carregar**.
   
    ![Carregar ficheiros](./media/media-services-portal-vod-get-started/media-services-upload.png)
   
    A janela **Carregar um elemento de vídeo** é apresentada.
   
   > [!NOTE]
   > Os Serviços de Multimédia não limitam o tamanho de ficheiro para o carregamento de vídeos.
 
3. No seu computador, aceda ao vídeo que quer carregar. Selecione o vídeo e, em seguida, selecione **OK**.  
   
    O carregamento começa. Pode ver o progresso abaixo do nome do ficheiro.  

Quando o carregamento estiver concluído, o elemento novo é apresentado no painel **Elementos**. 

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passos seguintes
* Veja [Encode your uploaded assets](media-services-portal-encode.md) (Codificar os seus elementos carregados).

* Também pode utilizar as Funções do Azure para acionar um trabalho de codificação num ficheiro que esteja a chegar ao contentor configurado. Para obter mais informações, veja o exemplo em [Media Services: Integrating Azure Media Services with Azure Functions and Logic Apps](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/) (Serviços de Multimédia: Integrar os Serviços de Multimédia nas Funções do Azure e no Logic Apps).


