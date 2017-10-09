---
title: aaaAzure Media Services perguntas mais frequentes | Microsoft Docs
description: Perguntas mais frequentes (FAQ)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Perguntas mais frequentes

Este artigo aborda perguntas mais frequentes geradas pela Comunidade de utilizadores do Olá serviços de suporte de dados do Azure (AMS).

## <a name="general-ams-faqs"></a>Perguntas frequentes do AMS geral
P: como pode dimensionar a indexação

R: unidades de Olá reservado são hello mesmo para codificação e tarefas de indexação. Siga as instruções [como tooScale unidades de codificação reservadas](media-services-scale-media-processing-overview.md). **Tenha em atenção** que o desempenho de indexador não é afetado por tipo de unidade reservado.

P: Posso carregou, codificou e publicado um vídeo. O que seria vídeo de Olá Olá razão não desempenha a quando tento toostream-lo?

R: um dos Olá entre as razões mais comuns é não dispõe de Olá a partir do qual está a tentar tooplayback no Olá de ponto final de transmissão em fluxo **executar** estado.  

P: posso fazer compositing num fluxo em direto?

R: compositing em fluxos em direto atualmente não é oferecido na Media Services do Azure, pelo que é necessário toopre-compose no seu computador.

P: Posso utilizar a CDN do Azure com transmissão em fluxo em direto?

R: Media Services suporta a integração com a CDN do Azure (para obter mais informações, consulte [como tooManage de transmissão em fluxo pontos finais numa conta de Media Services](media-services-portal-manage-streaming-endpoints.md)).  Pode utilizar em direto de transmissão em fluxo com CDN. Media Services do Azure fornece saídas de transmissão em fluxo, HLS e MPEG-DASH uniforme. Todos os estes formatos de utilizam HTTP para transferir dados e obter benefícios da colocação em cache de HTTP. Em direto de transmissão em fluxo de dados de áudio/vídeo real é dividido toofragments e este fragmentos individuais obterem em cache na CDN. Apenas dados necessidades toobe atualizar é os dados de manifesto Olá. CDN, atualiza periodicamente dados manifesto.

P: serviços de multimédia do Azure Does suportam imagens armazenar?

R: Se pretender apenas tirar toostore JPEG ou imagens PNG, deve manter existentes no Blob Storage do Azure. Não há nenhum tooputting benefício-los nos serviços de suporte de dados de conta, a menos que queira tookeep-los associados as vídeo ou áudio ativos. Ou se pode ter um toouse necessidade Olá imagens como as Sobreposições no codificador vídeo Olá. Codificador de multimédia Standard suporta imagens sobrepor por cima de vídeos e que é o que lista JPEG e PNG como suportados formatos de entrada. Para obter mais informações, consulte [criar sobrepõe](media-services-advanced-encoding-with-mes.md#overlay).

P: como copiar recursos de um tooanother de conta de Media Services.

R: toocopy ativos de uma tooanother de conta de Media Services utilizando o .NET, utilize [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) método de extensão disponível na Olá [extensões do SDK .NET do Azure suporte de dados de serviços](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repositório. Para obter mais informações, consulte [isto](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) thread de Fórum.

P: quais são Olá carateres suportados para atribuir nomes a ficheiros ao trabalhar com AMS?

R: Media Services utiliza o valor de Olá de Olá IAssetFile.Name propriedade quando criar os URLs do Olá transmissão em fluxo conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por este motivo, por cento de codificação não é permitida. Olá, valor de Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [por cento codificação-reservados carateres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Além disso, só pode existir um '.' para a extensão de nome de ficheiro Olá.

P: como utilizar tooconnect REST?

R: para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados. É necessário efetuar chamadas subsequentes toohello novo URI. 

P: como rodar um vídeo durante Olá codificação processo.

R: Olá [codificador de multimédia Standard](media-services-dotnet-encode-with-media-encoder-standard.md) suporta rotação pelos ângulos de 180/90/270. comportamento predefinido de Olá é "Auto", onde tenta toodetect Olá rotação metadados no ficheiro MP4/MOV recebido do Olá e compensá-lo. Incluem Olá seguinte **origens** tooone de elemento de predefinições de json Olá definido [aqui](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
