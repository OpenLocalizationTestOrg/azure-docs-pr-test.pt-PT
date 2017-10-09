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
# <a name="frequently-asked-questions"></a><span data-ttu-id="d7a0f-103">Perguntas mais frequentes</span><span class="sxs-lookup"><span data-stu-id="d7a0f-103">Frequently asked questions</span></span>

<span data-ttu-id="d7a0f-104">Este artigo aborda perguntas mais frequentes geradas pela Comunidade de utilizadores do Olá serviços de suporte de dados do Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="d7a0f-105">Perguntas frequentes do AMS geral</span><span class="sxs-lookup"><span data-stu-id="d7a0f-105">General AMS FAQs</span></span>
<span data-ttu-id="d7a0f-106">P: como pode dimensionar a indexação</span><span class="sxs-lookup"><span data-stu-id="d7a0f-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="d7a0f-107">R: unidades de Olá reservado são hello mesmo para codificação e tarefas de indexação.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="d7a0f-108">Siga as instruções [como tooScale unidades de codificação reservadas](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="d7a0f-109">**Tenha em atenção** que o desempenho de indexador não é afetado por tipo de unidade reservado.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="d7a0f-110">P: Posso carregou, codificou e publicado um vídeo.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="d7a0f-111">O que seria vídeo de Olá Olá razão não desempenha a quando tento toostream-lo?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="d7a0f-112">R: um dos Olá entre as razões mais comuns é não dispõe de Olá a partir do qual está a tentar tooplayback no Olá de ponto final de transmissão em fluxo **executar** estado.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="d7a0f-113">P: posso fazer compositing num fluxo em direto?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="d7a0f-114">R: compositing em fluxos em direto atualmente não é oferecido na Media Services do Azure, pelo que é necessário toopre-compose no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="d7a0f-115">P: Posso utilizar a CDN do Azure com transmissão em fluxo em direto?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="d7a0f-116">R: Media Services suporta a integração com a CDN do Azure (para obter mais informações, consulte [como tooManage de transmissão em fluxo pontos finais numa conta de Media Services](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="d7a0f-117">Pode utilizar em direto de transmissão em fluxo com CDN.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="d7a0f-118">Media Services do Azure fornece saídas de transmissão em fluxo, HLS e MPEG-DASH uniforme.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="d7a0f-119">Todos os estes formatos de utilizam HTTP para transferir dados e obter benefícios da colocação em cache de HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="d7a0f-120">Em direto de transmissão em fluxo de dados de áudio/vídeo real é dividido toofragments e este fragmentos individuais obterem em cache na CDN.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="d7a0f-121">Apenas dados necessidades toobe atualizar é os dados de manifesto Olá.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="d7a0f-122">CDN, atualiza periodicamente dados manifesto.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="d7a0f-123">P: serviços de multimédia do Azure Does suportam imagens armazenar?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="d7a0f-124">R: Se pretender apenas tirar toostore JPEG ou imagens PNG, deve manter existentes no Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="d7a0f-125">Não há nenhum tooputting benefício-los nos serviços de suporte de dados de conta, a menos que queira tookeep-los associados as vídeo ou áudio ativos.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="d7a0f-126">Ou se pode ter um toouse necessidade Olá imagens como as Sobreposições no codificador vídeo Olá. Codificador de multimédia Standard suporta imagens sobrepor por cima de vídeos e que é o que lista JPEG e PNG como suportados formatos de entrada.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="d7a0f-127">Para obter mais informações, consulte [criar sobrepõe](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="d7a0f-128">P: como copiar recursos de um tooanother de conta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="d7a0f-129">R: toocopy ativos de uma tooanother de conta de Media Services utilizando o .NET, utilize [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) método de extensão disponível na Olá [extensões do SDK .NET do Azure suporte de dados de serviços](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repositório.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="d7a0f-130">Para obter mais informações, consulte [isto](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) thread de Fórum.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="d7a0f-131">P: quais são Olá carateres suportados para atribuir nomes a ficheiros ao trabalhar com AMS?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="d7a0f-132">R: Media Services utiliza o valor de Olá de Olá IAssetFile.Name propriedade quando criar os URLs do Olá transmissão em fluxo conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por este motivo, por cento de codificação não é permitida.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="d7a0f-133">Olá, valor de Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [por cento codificação-reservados carateres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="d7a0f-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="d7a0f-134">Além disso, só pode existir um '.'</span><span class="sxs-lookup"><span data-stu-id="d7a0f-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="d7a0f-135">para a extensão de nome de ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-135">for hello file name extension.</span></span>

<span data-ttu-id="d7a0f-136">P: como utilizar tooconnect REST?</span><span class="sxs-lookup"><span data-stu-id="d7a0f-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="d7a0f-137">R: para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d7a0f-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="d7a0f-138">Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d7a0f-139">É necessário efetuar chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="d7a0f-140">P: como rodar um vídeo durante Olá codificação processo.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="d7a0f-141">R: Olá [codificador de multimédia Standard](media-services-dotnet-encode-with-media-encoder-standard.md) suporta rotação pelos ângulos de 180/90/270.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="d7a0f-142">comportamento predefinido de Olá é "Auto", onde tenta toodetect Olá rotação metadados no ficheiro MP4/MOV recebido do Olá e compensá-lo.</span><span class="sxs-lookup"><span data-stu-id="d7a0f-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="d7a0f-143">Incluem Olá seguinte **origens** tooone de elemento de predefinições de json Olá definido [aqui](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="d7a0f-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="d7a0f-144">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="d7a0f-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7a0f-145">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="d7a0f-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
