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
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="c8c15-103">Análise de multimédia na plataforma de Media Services Olá</span><span class="sxs-lookup"><span data-stu-id="c8c15-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="c8c15-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="c8c15-104">Overview</span></span>
<span data-ttu-id="c8c15-105">Mais organizações estão a utilizar vídeo como Olá preferencial tootrain médio aos funcionários, interagir com os seus clientes e funções de negócio do documento.</span><span class="sxs-lookup"><span data-stu-id="c8c15-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="c8c15-106">Fornece uma forma toostore, de informática em nuvem transmitir e aceder a estes ficheiros de suporte de dados grandes.</span><span class="sxs-lookup"><span data-stu-id="c8c15-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="c8c15-107">Mas à medida que aumenta a biblioteca de uma empresa de conteúdos de vídeo, necessita de um meio igualmente eficaz de extrair informações do conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c8c15-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="c8c15-108">tooaddress esta necessidade crescente, os Media Services do Azure oferece a análise de multimédia do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c15-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="c8c15-109">Análise de multimédia é uma coleção de componentes de voz e visão que torna mais fácil para organizações e empresas tooderive acionáveis dos respetivos ficheiros de vídeo.</span><span class="sxs-lookup"><span data-stu-id="c8c15-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="c8c15-110">Compilado por utilizar componentes de plataforma do Olá principais dos Media Services, análise de multimédia pode processar processamento à escala no primeiro dia do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="c8c15-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="c8c15-111">Análise do suporte de dados, os programadores podem trazer rapidamente funcionalidades avançadas de vídeo em aplicações.</span><span class="sxs-lookup"><span data-stu-id="c8c15-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="c8c15-112">Fornece ambientes empresariais com escala completa Olá, de conformidade, de segurança e de alcance global necessária para grandes organizações.</span><span class="sxs-lookup"><span data-stu-id="c8c15-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="c8c15-113">Olá diagrama seguinte mostra análise de multimédia e outras partes principais da plataforma de Media Services Olá.</span><span class="sxs-lookup"><span data-stu-id="c8c15-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![Fluxo de trabalho do VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="c8c15-115">Os processadores de multimédia de Análise de Multimédia produzem ficheiros MP4 ou ficheiros JSON.</span><span class="sxs-lookup"><span data-stu-id="c8c15-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="c8c15-116">Se um processador de multimédia produz um ficheiro MP4, pode transferir progressivamente ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="c8c15-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="c8c15-117">Se um processador de multimédia produz um ficheiro JSON, pode transferir o ficheiro de Olá do Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c15-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="c8c15-118">Serviços de análise de multimédia</span><span class="sxs-lookup"><span data-stu-id="c8c15-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="c8c15-119">Indexador</span><span class="sxs-lookup"><span data-stu-id="c8c15-119">Indexer</span></span>
<span data-ttu-id="c8c15-120">Com o indexador de suporte de dados do Azure, pode efetuar conteúdo pesquisáveis e gerar controla captioning fechado.</span><span class="sxs-lookup"><span data-stu-id="c8c15-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="c8c15-121">A versão anterior em comparação com toohello, pré-visualização de 2 de indexador de suporte de dados do Azure tem mais rápida indexação e mais amplo idioma suporta.</span><span class="sxs-lookup"><span data-stu-id="c8c15-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="c8c15-122">Idiomas suportados incluem o inglês, espanhol, francês, alemão, italiano, chinês, português e árabe.</span><span class="sxs-lookup"><span data-stu-id="c8c15-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="c8c15-123">Para obter informações detalhadas e exemplos, consulte [processa vídeos com o Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="c8c15-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="c8c15-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c8c15-124">Hyperlapse</span></span>
<span data-ttu-id="c8c15-125">Microsoft Hyperlapse combina estabilização de vídeo e capacidade time-lapse toocreate rápido, consumíveis vídeos do seu conteúdo de formulário longa.</span><span class="sxs-lookup"><span data-stu-id="c8c15-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="c8c15-126">Para além de criar as vídeo time-lapse, pode utilizar Hyperlapse toocreate estáveis vídeos de vídeos shaky capturados através de telemóveis e camcorders.</span><span class="sxs-lookup"><span data-stu-id="c8c15-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="c8c15-127">Para obter informações detalhadas e exemplos, consulte [Hyperlapse de ficheiros de multimédia com Hyperlapse de multimédia do Azure](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="c8c15-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="c8c15-128">Detetor de Movimento</span><span class="sxs-lookup"><span data-stu-id="c8c15-128">Motion Detector</span></span>
<span data-ttu-id="c8c15-129">Pode utilizar o movimento do movimento Detector toodetect um vídeo com estacionário dos jogadores.</span><span class="sxs-lookup"><span data-stu-id="c8c15-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="c8c15-130">Isto torna possível toocheck para falsos positivos detetada pelo câmaras de vigilância de eventos de movimento.</span><span class="sxs-lookup"><span data-stu-id="c8c15-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="c8c15-131">Para obter informações detalhadas e exemplos, consulte [deteção para análise de multimédia do Azure de movimento](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="c8c15-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="c8c15-132">Detetor de Rosto</span><span class="sxs-lookup"><span data-stu-id="c8c15-132">Face Detector</span></span>
<span data-ttu-id="c8c15-133">Ao utilizar enfrentam Detector, pode detetar faces das pessoas e os respetivos emotions, incluindo happiness, sadness e surprise.</span><span class="sxs-lookup"><span data-stu-id="c8c15-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="c8c15-134">Isto tem vários da indústria útil aplicações, descritas mais tarde, incluindo agregar e analisar reactions das pessoas attending um evento.</span><span class="sxs-lookup"><span data-stu-id="c8c15-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="c8c15-135">Para obter informações detalhadas e exemplos, consulte [deteção de rostos em e emoções para análise de multimédia do Azure](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="c8c15-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="c8c15-136">Resumo do vídeo</span><span class="sxs-lookup"><span data-stu-id="c8c15-136">Video summarization</span></span>
<span data-ttu-id="c8c15-137">Resumo do vídeo pode ajudar a criar resumos dos vídeos longos selecionando automaticamente interessantes fragmentos do vídeo de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="c8c15-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="c8c15-138">Esta capacidade é útil quando pretende tooprovide uma descrição geral rápida do que tooexpect um vídeo longo.</span><span class="sxs-lookup"><span data-stu-id="c8c15-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="c8c15-139">Para obter informações detalhadas e exemplos, consulte [resumo do vídeo as vídeo miniaturas de utilização do Azure multimédia toocreate](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="c8c15-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="c8c15-140">Reconhecimento ótico de carateres</span><span class="sxs-lookup"><span data-stu-id="c8c15-140">Optical character recognition</span></span>
<span data-ttu-id="c8c15-141">Com OCR de suporte de dados do Azure (reconhecimento de caráter optical), pode converter os conteúdos de texto nos ficheiros de vídeos num editável, pesquisável texto digital.</span><span class="sxs-lookup"><span data-stu-id="c8c15-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="c8c15-142">Em seguida, pode automatizar extração Olá dos metadados significativo do sinal de vídeo Olá do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="c8c15-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="c8c15-143">Redaction enfrentam dimensionável</span><span class="sxs-lookup"><span data-stu-id="c8c15-143">Scalable face redaction</span></span>
<span data-ttu-id="c8c15-144">Redactor de suporte de dados do Azure é um processador de multimédia de análise de multimédia que oferece redaction enfrentam dimensionável na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="c8c15-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="c8c15-145">Através da utilização de rostos em redaction, pode modificar os faces tooblur vídeo de indivíduos selecionados.</span><span class="sxs-lookup"><span data-stu-id="c8c15-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="c8c15-146">Pode querer serviço de redaction de letra do toouse Olá no suporte de notícias, ou quando está envolvida segurança pública.</span><span class="sxs-lookup"><span data-stu-id="c8c15-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="c8c15-147">Alguns minutos de imagens que contém vários faces podem demorar horas tooredact manualmente, mas com este serviço, enfrentam redaction demora apenas alguns passos simples.</span><span class="sxs-lookup"><span data-stu-id="c8c15-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="c8c15-148">Para obter mais informações, consulte Olá [Redact faces análise de multimédia do Azure](media-services-face-redaction.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c8c15-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="c8c15-149">Cenários comuns</span><span class="sxs-lookup"><span data-stu-id="c8c15-149">Common scenarios</span></span>
<span data-ttu-id="c8c15-150">Análise de multimédia pode ajudar as organizações e empresas glean conhecimentos aprofundados sobre novo vídeo e mais grandes volumes de conteúdo de vídeo gerir de forma eficaz.</span><span class="sxs-lookup"><span data-stu-id="c8c15-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="c8c15-151">Seguem-se vários cenários:</span><span class="sxs-lookup"><span data-stu-id="c8c15-151">Here are several scenarios:</span></span>

* <span data-ttu-id="c8c15-152">**Chamar centros**.</span><span class="sxs-lookup"><span data-stu-id="c8c15-152">**Call centers**.</span></span> <span data-ttu-id="c8c15-153">Mesmo com a introdução de Olá de redes sociais, o cliente chamada centros facilitam ainda uma grande percentagem de transações do serviço de cliente.</span><span class="sxs-lookup"><span data-stu-id="c8c15-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="c8c15-154">Estes dados de áudio com codificação é uma grande quantidade de informações de cliente que podem ser analisados tooachieve superior satisfação do cliente.</span><span class="sxs-lookup"><span data-stu-id="c8c15-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="c8c15-155">Utilizando o indexador de suporte de dados, as organizações podem extraia o texto e crie índices de pesquisa e dashboards.</span><span class="sxs-lookup"><span data-stu-id="c8c15-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="c8c15-156">Em seguida, eles possam extrair intelligence em torno queixas comuns, fontes de queixas e outros dados relevantes.</span><span class="sxs-lookup"><span data-stu-id="c8c15-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="c8c15-157">**Gerados pelo utilizador conteúda moderação de interrupção**.</span><span class="sxs-lookup"><span data-stu-id="c8c15-157">**User-generated content moderation**.</span></span> <span data-ttu-id="c8c15-158">Dos departamentos de toopolice saídas de suporte de dados de notícias, muitas organizações têm portais destinado ao público que aceitam o suporte de dados gerados pelo utilizador, tais como vídeos e imagens.</span><span class="sxs-lookup"><span data-stu-id="c8c15-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="c8c15-159">volume de Olá de conteúdo pode aumentam devido toounexpected eventos.</span><span class="sxs-lookup"><span data-stu-id="c8c15-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="c8c15-160">Nestes cenários, é difícil tooconduct Efetivo revisões manual de conteúdo para appropriateness.</span><span class="sxs-lookup"><span data-stu-id="c8c15-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="c8c15-161">Os clientes podem dependem Olá moderação de interrupção conteúdo serviço toofocus no conteúdo que é adequado.</span><span class="sxs-lookup"><span data-stu-id="c8c15-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="c8c15-162">**Vigilância**.</span><span class="sxs-lookup"><span data-stu-id="c8c15-162">**Surveillance**.</span></span> <span data-ttu-id="c8c15-163">Com Olá crescimento na utilização de câmaras IP é fornecido um inventário crescente de vídeo de vigilância.</span><span class="sxs-lookup"><span data-stu-id="c8c15-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="c8c15-164">Rever manualmente as vídeo de vigilância-se tempo toohuman intensiva e propensas ao erro.</span><span class="sxs-lookup"><span data-stu-id="c8c15-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="c8c15-165">Análise de multimédia fornece serviços como o processo de Olá toomake Hyperlapse de rever, gerir e criar derivados mais fácil, de deteção de rostos em e de deteção de movimento.</span><span class="sxs-lookup"><span data-stu-id="c8c15-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="c8c15-166">Processadores de multimédia de análise de multimédia</span><span class="sxs-lookup"><span data-stu-id="c8c15-166">Media Analytics media processors</span></span>
<span data-ttu-id="c8c15-167">Esta secção apresenta uma lista de Olá processadores de multimédia de análise de multimédia e mostra como toouse .NET ou REST tooget um objeto de processador (MP do) suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="c8c15-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="c8c15-168">Nomes de MP</span><span class="sxs-lookup"><span data-stu-id="c8c15-168">MP names</span></span>
* <span data-ttu-id="c8c15-169">Pré-visualização de indexador 2 de Media Services do Azure</span><span class="sxs-lookup"><span data-stu-id="c8c15-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="c8c15-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="c8c15-170">Azure Media Indexer</span></span>
* <span data-ttu-id="c8c15-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c8c15-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="c8c15-172">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="c8c15-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="c8c15-173">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="c8c15-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="c8c15-174">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="c8c15-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="c8c15-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="c8c15-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="c8c15-176">.NET</span><span class="sxs-lookup"><span data-stu-id="c8c15-176">.NET</span></span>
<span data-ttu-id="c8c15-177">Olá seguinte função demora um de Olá especificado MP os nomes e devolve um objeto de pacote de gestão.</span><span class="sxs-lookup"><span data-stu-id="c8c15-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="c8c15-178">REST</span><span class="sxs-lookup"><span data-stu-id="c8c15-178">REST</span></span>
<span data-ttu-id="c8c15-179">Pedido:</span><span class="sxs-lookup"><span data-stu-id="c8c15-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="c8c15-180">Resposta:</span><span class="sxs-lookup"><span data-stu-id="c8c15-180">Response:</span></span>

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

## <a name="demos"></a><span data-ttu-id="c8c15-181">Demonstrações</span><span class="sxs-lookup"><span data-stu-id="c8c15-181">Demos</span></span>
<span data-ttu-id="c8c15-182">Consulte [demonstrações de análise de multimédia do Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="c8c15-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8c15-183">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c8c15-183">Next steps</span></span>
<span data-ttu-id="c8c15-184">Rever os percursos de aprendizagem dos Serviços de Multimédia</span><span class="sxs-lookup"><span data-stu-id="c8c15-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8c15-185">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="c8c15-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="c8c15-186">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="c8c15-186">Related articles</span></span>
<span data-ttu-id="c8c15-187">Consulte [anúncio de análise de serviços de multimédia](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="c8c15-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
