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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Criar Filtros com o SDK .NET dos Serviços de Multimédia do Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

A partir da versão 2.11, os Media Services permite-lhe toodefine filtros para os elementos. Estes filtros são as regras do lado do servidor que irão permitir que os seus clientes toochoose toodo coisas como: reprodução apenas uma secção de um vídeo (em vez de reproduzir Olá todo vídeo), ou especifique apenas um subconjunto de áudio e vídeos renditions que o dispositivo do seu cliente pode processar ( em vez de todos os renditions de Olá que estão associados com recurso de Olá). Esta filtragem dos seus ativos é conseguido através de **manifesto dinâmica**s que são criados após toostream de pedido do cliente um vídeo com base em filtros especificados.

Para obter informações mais detalhadas toofilters relacionados e o manifesto dinâmico, consulte [dinâmico manifestos descrição geral](media-services-dynamic-manifest-overview.md).

Este tópico mostra como toouse SDK .NET dos Media Services toocreate, atualizar e eliminar os filtros. 

Tenha em atenção de que o se atualizar um filtro, pode demorar até too2 minutos para regras de Olá toorefresh de ponto final de transmissão em fluxo. Se Olá conteúdo tiver sido servido com este filtro (e colocados em cache no proxies e CDN caches), ao atualizar este filtro pode resultar em falhas de leitor. É recomendável a cache de Olá tooclear depois de atualizar o filtro de Olá. Se esta opção não for possível, considere utilizar um filtro diferente. 

## <a name="types-used-toocreate-filters"></a>Os tipos de utilizados toocreate filtros
Olá tipos seguintes são utilizados durante a criação de filtros: 

* **IStreamingFilter**.  Este tipo baseia-se no Olá seguintes REST API [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Este tipo baseia-se no Olá seguintes REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Este tipo baseia-se no Olá seguintes REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**. Estes tipos são baseados no Olá seguir REST APIs [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Criar/atualizar/leitura/eliminar filtros de global
Olá código seguinte mostra como toouse .NET toocreate, atualizar, ler e eliminar os filtros de recurso.

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


## <a name="createupdatereaddelete-asset-filters"></a>Filtros de recurso criar/atualizar/leitura/eliminar
Olá código seguinte mostra como toouse .NET toocreate, atualizar, ler e eliminar os filtros de recurso.

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




## <a name="build-streaming-urls-that-use-filters"></a>Criar URLs que utilizam filtros de transmissão em fluxo
Para obter informações sobre como toopublish e fornecer os recursos, consulte o artigo [tooCustomers descrição geral do fornecimento de conteúdo](media-services-deliver-content-overview.md).

Olá exemplos seguintes mostram como tooadd filtra tooyour URLs de transmissão em fluxo.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live transmissão em fluxo (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live transmissão em fluxo (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Transmissão em fluxo uniforme**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Veja Também
[Descrição geral de manifestos dinâmica](media-services-dynamic-manifest-overview.md)

