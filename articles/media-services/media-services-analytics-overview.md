---
title: "aaaMedia análise na plataforma de Media Services Olá | Microsoft Docs"
description: "Descrição geral da pré-visualização pública da análise de multimédia, uma coleção de serviços de visão de reconhecimento de voz e o computador em escala empresarial que, de conformidade, de segurança e de alcance global"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Análise de multimédia na plataforma de Media Services Olá
## <a name="overview"></a>Descrição geral
Mais organizações estão a utilizar vídeo como Olá preferencial tootrain médio aos funcionários, interagir com os seus clientes e funções de negócio do documento. Fornece uma forma toostore, de informática em nuvem transmitir e aceder a estes ficheiros de suporte de dados grandes. Mas à medida que aumenta a biblioteca de uma empresa de conteúdos de vídeo, necessita de um meio igualmente eficaz de extrair informações do conteúdo de Olá. 

tooaddress esta necessidade crescente, os Media Services do Azure oferece a análise de multimédia do Azure. Análise de multimédia é uma coleção de componentes de voz e visão que torna mais fácil para organizações e empresas tooderive acionáveis dos respetivos ficheiros de vídeo. Compilado por utilizar componentes de plataforma do Olá principais dos Media Services, análise de multimédia pode processar processamento à escala no primeiro dia do suporte de dados.

Análise do suporte de dados, os programadores podem trazer rapidamente funcionalidades avançadas de vídeo em aplicações. Fornece ambientes empresariais com escala completa Olá, de conformidade, de segurança e de alcance global necessária para grandes organizações.

Olá diagrama seguinte mostra análise de multimédia e outras partes principais da plataforma de Media Services Olá. 

![Fluxo de trabalho do VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

Os processadores de multimédia de Análise de Multimédia produzem ficheiros MP4 ou ficheiros JSON. Se um processador de multimédia produz um ficheiro MP4, pode transferir progressivamente ficheiros Olá. Se um processador de multimédia produz um ficheiro JSON, pode transferir o ficheiro de Olá do Blob storage do Azure. 

## <a name="media-analytics-services"></a>Serviços de análise de multimédia

### <a name="indexer"></a>Indexador
Com o indexador de suporte de dados do Azure, pode efetuar conteúdo pesquisáveis e gerar controla captioning fechado. A versão anterior em comparação com toohello, pré-visualização de 2 de indexador de suporte de dados do Azure tem mais rápida indexação e mais amplo idioma suporta. Idiomas suportados incluem o inglês, espanhol, francês, alemão, italiano, chinês, português e árabe. Para obter informações detalhadas e exemplos, consulte [processa vídeos com o Azure Media Indexer 2](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse combina estabilização de vídeo e capacidade time-lapse toocreate rápido, consumíveis vídeos do seu conteúdo de formulário longa. Para além de criar as vídeo time-lapse, pode utilizar Hyperlapse toocreate estáveis vídeos de vídeos shaky capturados através de telemóveis e camcorders. Para obter informações detalhadas e exemplos, consulte [Hyperlapse de ficheiros de multimédia com Hyperlapse de multimédia do Azure](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Detetor de Movimento
Pode utilizar o movimento do movimento Detector toodetect um vídeo com estacionário dos jogadores. Isto torna possível toocheck para falsos positivos detetada pelo câmaras de vigilância de eventos de movimento. Para obter informações detalhadas e exemplos, consulte [deteção para análise de multimédia do Azure de movimento](media-services-motion-detection.md).
### <a name="face-detector"></a>Detetor de Rosto
Ao utilizar enfrentam Detector, pode detetar faces das pessoas e os respetivos emotions, incluindo happiness, sadness e surprise. Isto tem vários da indústria útil aplicações, descritas mais tarde, incluindo agregar e analisar reactions das pessoas attending um evento. Para obter informações detalhadas e exemplos, consulte [deteção de rostos em e emoções para análise de multimédia do Azure](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Resumo do vídeo
Resumo do vídeo pode ajudar a criar resumos dos vídeos longos selecionando automaticamente interessantes fragmentos do vídeo de origem Olá. Esta capacidade é útil quando pretende tooprovide uma descrição geral rápida do que tooexpect um vídeo longo. Para obter informações detalhadas e exemplos, consulte [resumo do vídeo as vídeo miniaturas de utilização do Azure multimédia toocreate](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Reconhecimento ótico de carateres
Com OCR de suporte de dados do Azure (reconhecimento de caráter optical), pode converter os conteúdos de texto nos ficheiros de vídeos num editável, pesquisável texto digital. Em seguida, pode automatizar extração Olá dos metadados significativo do sinal de vídeo Olá do suporte de dados.
### <a name="scalable-face-redaction"></a>Redaction enfrentam dimensionável
Redactor de suporte de dados do Azure é um processador de multimédia de análise de multimédia que oferece redaction enfrentam dimensionável na nuvem de Olá. Através da utilização de rostos em redaction, pode modificar os faces tooblur vídeo de indivíduos selecionados. Pode querer serviço de redaction de letra do toouse Olá no suporte de notícias, ou quando está envolvida segurança pública. Alguns minutos de imagens que contém vários faces podem demorar horas tooredact manualmente, mas com este serviço, enfrentam redaction demora apenas alguns passos simples. Para obter mais informações, consulte Olá [Redact faces análise de multimédia do Azure](media-services-face-redaction.md) artigo.

## <a name="common-scenarios"></a>Cenários comuns
Análise de multimédia pode ajudar as organizações e empresas glean conhecimentos aprofundados sobre novo vídeo e mais grandes volumes de conteúdo de vídeo gerir de forma eficaz. Seguem-se vários cenários:

* **Chamar centros**. Mesmo com a introdução de Olá de redes sociais, o cliente chamada centros facilitam ainda uma grande percentagem de transações do serviço de cliente. Estes dados de áudio com codificação é uma grande quantidade de informações de cliente que podem ser analisados tooachieve superior satisfação do cliente. Utilizando o indexador de suporte de dados, as organizações podem extraia o texto e crie índices de pesquisa e dashboards. Em seguida, eles possam extrair intelligence em torno queixas comuns, fontes de queixas e outros dados relevantes.
* **Gerados pelo utilizador conteúda moderação de interrupção**. Dos departamentos de toopolice saídas de suporte de dados de notícias, muitas organizações têm portais destinado ao público que aceitam o suporte de dados gerados pelo utilizador, tais como vídeos e imagens. volume de Olá de conteúdo pode aumentam devido toounexpected eventos. Nestes cenários, é difícil tooconduct Efetivo revisões manual de conteúdo para appropriateness. Os clientes podem dependem Olá moderação de interrupção conteúdo serviço toofocus no conteúdo que é adequado.
* **Vigilância**. Com Olá crescimento na utilização de câmaras IP é fornecido um inventário crescente de vídeo de vigilância. Rever manualmente as vídeo de vigilância-se tempo toohuman intensiva e propensas ao erro. Análise de multimédia fornece serviços como o processo de Olá toomake Hyperlapse de rever, gerir e criar derivados mais fácil, de deteção de rostos em e de deteção de movimento.

## <a name="media-analytics-media-processors"></a>Processadores de multimédia de análise de multimédia
Esta secção apresenta uma lista de Olá processadores de multimédia de análise de multimédia e mostra como toouse .NET ou REST tooget um objeto de processador (MP do) suporte de dados.

### <a name="mp-names"></a>Nomes de MP
* Pré-visualização de indexador 2 de Media Services do Azure
* Azure Media Indexer
* Azure Media Hyperlapse
* Azure Media Face Detector
* Azure Media Motion Detector
* Azure Media Video Thumbnails
* Azure Media OCR

### <a name="net"></a>.NET
Olá seguinte função demora um de Olá especificado MP os nomes e devolve um objeto de pacote de gestão.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
Pedido:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Resposta:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Demonstrações
Consulte [demonstrações de análise de multimédia do Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Passos seguintes
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artigos relacionados
Consulte [anúncio de análise de serviços de multimédia](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
