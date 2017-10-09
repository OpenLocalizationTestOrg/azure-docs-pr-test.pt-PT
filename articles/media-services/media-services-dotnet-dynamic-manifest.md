---
title: Filtros de aaaCreating com SDK .NET do Azure Media Services
description: "Este tópico descreve como toocreate filtros para que o cliente possa utilizar toostream secções específicas de um fluxo. Os Media Services cria manifestos dinâmica tooachieve este seletiva de transmissão em fluxo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="c6433-104">Criar Filtros com o SDK .NET dos Serviços de Multimédia do Azure</span><span class="sxs-lookup"><span data-stu-id="c6433-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6433-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c6433-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="c6433-106">REST</span><span class="sxs-lookup"><span data-stu-id="c6433-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="c6433-107">A partir da versão 2.11, os Media Services permite-lhe toodefine filtros para os elementos.</span><span class="sxs-lookup"><span data-stu-id="c6433-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="c6433-108">Estes filtros são as regras do lado do servidor que irão permitir que os seus clientes toochoose toodo coisas como: reprodução apenas uma secção de um vídeo (em vez de reproduzir Olá todo vídeo), ou especifique apenas um subconjunto de áudio e vídeos renditions que o dispositivo do seu cliente pode processar ( em vez de todos os renditions de Olá que estão associados com recurso de Olá).</span><span class="sxs-lookup"><span data-stu-id="c6433-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="c6433-109">Esta filtragem dos seus ativos é conseguido através de **manifesto dinâmica**s que são criados após toostream de pedido do cliente um vídeo com base em filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="c6433-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="c6433-110">Para obter informações mais detalhadas toofilters relacionados e o manifesto dinâmico, consulte [dinâmico manifestos descrição geral](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6433-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="c6433-111">Este tópico mostra como toouse SDK .NET dos Media Services toocreate, atualizar e eliminar os filtros.</span><span class="sxs-lookup"><span data-stu-id="c6433-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="c6433-112">Tenha em atenção de que o se atualizar um filtro, pode demorar até too2 minutos para regras de Olá toorefresh de ponto final de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="c6433-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="c6433-113">Se Olá conteúdo tiver sido servido com este filtro (e colocados em cache no proxies e CDN caches), ao atualizar este filtro pode resultar em falhas de leitor.</span><span class="sxs-lookup"><span data-stu-id="c6433-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="c6433-114">É recomendável a cache de Olá tooclear depois de atualizar o filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="c6433-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="c6433-115">Se esta opção não for possível, considere utilizar um filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="c6433-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="c6433-116">Os tipos de utilizados toocreate filtros</span><span class="sxs-lookup"><span data-stu-id="c6433-116">Types used toocreate filters</span></span>
<span data-ttu-id="c6433-117">Olá tipos seguintes são utilizados durante a criação de filtros:</span><span class="sxs-lookup"><span data-stu-id="c6433-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="c6433-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="c6433-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="c6433-119">Este tipo baseia-se no Olá seguintes REST API [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="c6433-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="c6433-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="c6433-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="c6433-121">Este tipo baseia-se no Olá seguintes REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="c6433-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="c6433-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="c6433-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="c6433-123">Este tipo baseia-se no Olá seguintes REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="c6433-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="c6433-124">**FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="c6433-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="c6433-125">Estes tipos são baseados no Olá seguir REST APIs [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="c6433-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="c6433-126">Criar/atualizar/leitura/eliminar filtros de global</span><span class="sxs-lookup"><span data-stu-id="c6433-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="c6433-127">Olá código seguinte mostra como toouse .NET toocreate, atualizar, ler e eliminar os filtros de recurso.</span><span class="sxs-lookup"><span data-stu-id="c6433-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="c6433-128">Filtros de recurso criar/atualizar/leitura/eliminar</span><span class="sxs-lookup"><span data-stu-id="c6433-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="c6433-129">Olá código seguinte mostra como toouse .NET toocreate, atualizar, ler e eliminar os filtros de recurso.</span><span class="sxs-lookup"><span data-stu-id="c6433-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="c6433-130">Criar URLs que utilizam filtros de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="c6433-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="c6433-131">Para obter informações sobre como toopublish e fornecer os recursos, consulte o artigo [tooCustomers descrição geral do fornecimento de conteúdo](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6433-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="c6433-132">Olá exemplos seguintes mostram como tooadd filtra tooyour URLs de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="c6433-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="c6433-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="c6433-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="c6433-134">**Apple HTTP Live transmissão em fluxo (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="c6433-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="c6433-135">**Apple HTTP Live transmissão em fluxo (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="c6433-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="c6433-136">**Transmissão em fluxo uniforme**</span><span class="sxs-lookup"><span data-stu-id="c6433-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="c6433-137">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="c6433-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6433-138">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="c6433-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c6433-139">Veja Também</span><span class="sxs-lookup"><span data-stu-id="c6433-139">See Also</span></span>
[<span data-ttu-id="c6433-140">Descrição geral de manifestos dinâmica</span><span class="sxs-lookup"><span data-stu-id="c6433-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

