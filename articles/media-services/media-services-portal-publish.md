---
title: "AAA\"publicar conteúdo com Olá portal do Azure | Microsoft Docs\""
description: "Este tutorial explica passos para publicar o conteúdo com o portal do Azure de Olá Olá."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Publicar conteúdo com Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Descrição geral
> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

tooprovide ao utilizador com um URL que pode ser utilizado toostream ou transferir o conteúdo, primeiro tem de demasiado "publicar" o elemento criando um localizador. Os localizadores fornecem toofiles acesso contidos no elemento de Olá. Os Media Services suportam dois tipos de localizadores: 

* Transmissão em fluxo () ondemandorigin, utilizados para transmissão em fluxo adaptável (por exemplo, toostream MPEG DASH, HLS ou transmissão em fluxo uniforme). toocreate um localizador de transmissão em fluxo seu elemento tem de conter um ficheiro. ISM. 
* Os localizadores progressivos (SAS), utilizados para a entrega de vídeo através de transferência progressiva.

Um URL de transmissão em fluxo tem Olá seguinte formato e pode utilizá-lo a recursos de transmissão em fluxo uniforme tooplay.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Acrescentar toobuild um URL de transmissão em fluxo HLS (formato = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

toobuild um MPEG DASH, transmissão em fluxo URL, acrescente (formato = mpd-time-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

Um URL SAS tem Olá seguir o formato.

    {blob container name}/{asset name}/{file name}/{SAS signature}

Para obter mais informações, consulte [fornecimento de descrição geral do conteúdo](media-services-deliver-content-overview.md).

> [!NOTE]
> Se utilizou localizadores de portal toocreate Olá antes de Março de 2015, foram criados localizadores com uma data de expiração de dois anos.  
> 
> 

tooupdate uma data de expiração num localizador, utilize [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs. Tenha em atenção que quando atualizar a data de expiração de Olá de um localizador SAS, Olá URL é alterado.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse Olá portal toopublish um recurso
toouse Olá portal toopublish um recurso, Olá seguintes:

1. No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.
2. Selecione **Definições** > **Elementos**.
3. Selecione o elemento de Olá que pretende que o toopublish.
4. Clique em Olá **publicar** botão.
5. Selecione o tipo de localizador Olá.
6. Prima **Adicionar**.
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Olá URL será adicionado toohello lista de **URLs publicados**.

## <a name="play-content-from-hello-portal"></a>Reproduzir conteúdos a partir do portal de Olá
Olá portal do Azure fornece um leitor de conteúdos que é possível utilizar tootest o vídeo.

Clique em vídeo Olá pretendido e, em seguida, clique em Olá **reproduzir** botão.

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

São aplicáveis algumas considerações:

* Certifique-se Olá vídeo foi publicado.
* Isto **Media player** reproduz a partir do ponto final de transmissão em fluxo de predefinido de Olá. Se quiser tooplay de um não predefinido, transmissão em fluxo ponto final, clique toocopy Olá URL e utilize outro leitor. Por exemplo, [Leitor dos Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Olá a partir da qual transmissão em fluxo de ponto final de transmissão em fluxo tem de estar em execução.  

## <a name="next-steps"></a>Passos seguintes
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

