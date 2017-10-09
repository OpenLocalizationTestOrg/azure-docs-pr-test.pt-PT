---
title: "aaaAnalyze suportes de dados utilizando Olá portal do Azure | Microsoft Docs"
description: "Este tópico descreve como tooprocess Olá de suporte de dados com processadores de suporte de dados de análise de multimédia (MP) utilizando o portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="969a3-103">Analisar o suporte de dados através de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="969a3-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="969a3-104">toocomplete neste tutorial, precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="969a3-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="969a3-105">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="969a3-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="969a3-106">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="969a3-106">Overview</span></span>
<span data-ttu-id="969a3-107">Análise de serviços de multimédia do Azure é uma coleção de voz e visão componentes (escala empresarial, a conformidade, a segurança e alcance global) que torna mais fácil para organizações e empresas tooderive acionáveis dos respetivos ficheiros de vídeo.</span><span class="sxs-lookup"><span data-stu-id="969a3-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="969a3-108">Para obter mais descrição geral da análise de serviços de multimédia do Azure consulte [isto](media-services-analytics-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="969a3-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="969a3-109">Este tópico descreve como tooprocess Olá de suporte de dados com processadores de suporte de dados de análise de multimédia (MP) utilizando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="969a3-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="969a3-110">Pacotes de gestão de análise de multimédia produzem ficheiros MP4 ou ficheiros JSON.</span><span class="sxs-lookup"><span data-stu-id="969a3-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="969a3-111">Se um processador de multimédia produzir um ficheiro MP4, pode transferir progressivamente ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="969a3-112">Se um processador de multimédia produzir um ficheiro JSON, pode transferir o ficheiro de Olá de Olá blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="969a3-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="969a3-113">Escolha um recurso que pretende que o tooanalyze</span><span class="sxs-lookup"><span data-stu-id="969a3-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="969a3-114">No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="969a3-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="969a3-115">No Olá **definições** janela, selecione **ativos**.</span><span class="sxs-lookup"><span data-stu-id="969a3-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="969a3-116">.</span><span class="sxs-lookup"><span data-stu-id="969a3-116">.</span></span>
    <span data-ttu-id="969a3-117">![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="969a3-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="969a3-118">Elemento de Olá selecione que gostaria de Olá tooanalyze e prima **analisar** botão.</span><span class="sxs-lookup"><span data-stu-id="969a3-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="969a3-120">No Olá **recurso de multimédia de processo com a análise de multimédia** janela, o processador de Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="969a3-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="969a3-121">Olá resto artigo Olá explica por que razão e como toouse cada processador.</span><span class="sxs-lookup"><span data-stu-id="969a3-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="969a3-122">Prima **criar** toohello iniciar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="969a3-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="969a3-123">Azure Media Indexer</span></span>
<span data-ttu-id="969a3-124">Olá **indexador de suporte de dados do Azure** processador de multimédia permite-lhe toomake ficheiros de suporte de dados e conteúdo pesquisável, bem como gerar controla captioning fechada.</span><span class="sxs-lookup"><span data-stu-id="969a3-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="969a3-125">Estas secções fornece alguns detalhes sobre as opções que pode especificar para este pacote de gestão.</span><span class="sxs-lookup"><span data-stu-id="969a3-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="969a3-127">Idioma</span><span class="sxs-lookup"><span data-stu-id="969a3-127">Language</span></span>
<span data-ttu-id="969a3-128">Olá toobe de linguagem natural reconhecido no ficheiro multimedia Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="969a3-129">Por exemplo, inglês ou espanhol.</span><span class="sxs-lookup"><span data-stu-id="969a3-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="969a3-130">Legendas</span><span class="sxs-lookup"><span data-stu-id="969a3-130">Captions</span></span>
<span data-ttu-id="969a3-131">Pode escolher um formato de legenda que será gerado a partir do seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="969a3-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="969a3-132">Uma tarefa de indexação pode gerar ficheiros de legendas no Olá seguintes formatos:</span><span class="sxs-lookup"><span data-stu-id="969a3-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="969a3-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="969a3-133">**SAMI**</span></span>
* <span data-ttu-id="969a3-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="969a3-134">**TTML**</span></span>
* <span data-ttu-id="969a3-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="969a3-135">**WebVTT**</span></span>

<span data-ttu-id="969a3-136">Fechado ficheiros de legenda (CC) nestes formatos podem ser utilizados toomake áudio e vídeo ficheiros toopeople acessível com hearing disability.</span><span class="sxs-lookup"><span data-stu-id="969a3-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="969a3-137">Ficheiro AIB</span><span class="sxs-lookup"><span data-stu-id="969a3-137">AIB file</span></span>
<span data-ttu-id="969a3-138">Selecione esta opção se que seria, como ficheiro de áudio índice Blob Olá toogenerate para utilização com Olá IFilter de servidor de SQL personalizados.</span><span class="sxs-lookup"><span data-stu-id="969a3-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="969a3-139">Para obter mais informações, consulte [isto](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogue.</span><span class="sxs-lookup"><span data-stu-id="969a3-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="969a3-140">Palavras-chave</span><span class="sxs-lookup"><span data-stu-id="969a3-140">Keywords</span></span>
<span data-ttu-id="969a3-141">Selecione esta opção se pretender que o toogenerate um ficheiro XML de palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="969a3-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="969a3-142">Este ficheiro contém palavras-chave extraídas do conteúdo de reconhecimento de voz de Olá, com frequência e informações de deslocamento.</span><span class="sxs-lookup"><span data-stu-id="969a3-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="969a3-143">Nome da tarefa</span><span class="sxs-lookup"><span data-stu-id="969a3-143">Job name</span></span>
<span data-ttu-id="969a3-144">Um nome amigável que lhe permite identificar Olá tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="969a3-145">[Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="969a3-146">Ficheiro de saída</span><span class="sxs-lookup"><span data-stu-id="969a3-146">Output file</span></span>
<span data-ttu-id="969a3-147">Um nome amigável que lhe permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="969a3-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="969a3-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="969a3-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="969a3-149">Hyperlapse de multimédia do Azure é um pacote de gestão que cria uniforme vídeos passado o tempo do conteúdo primeira pessoa ou ação câmara.</span><span class="sxs-lookup"><span data-stu-id="969a3-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="969a3-150">Para obter mais informações, veja [este](media-services-hyperlapse-content.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="969a3-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="969a3-151">Estas secções fornece alguns detalhes sobre as opções que pode especificar para este pacote de gestão.</span><span class="sxs-lookup"><span data-stu-id="969a3-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="969a3-153">Velocidade</span><span class="sxs-lookup"><span data-stu-id="969a3-153">Speed</span></span>
<span data-ttu-id="969a3-154">Especifique a velocidade de Olá com que toospeed segurança as vídeo de entrada de Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="969a3-155">o resultado de Olá é um rendition stabilized e passado o tempo de vídeo de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="969a3-156">Nome da tarefa</span><span class="sxs-lookup"><span data-stu-id="969a3-156">Job name</span></span>
<span data-ttu-id="969a3-157">Um nome amigável que lhe permite identificar Olá tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="969a3-158">[Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="969a3-159">Ficheiro de saída</span><span class="sxs-lookup"><span data-stu-id="969a3-159">Output file</span></span>
<span data-ttu-id="969a3-160">Um nome amigável que lhe permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="969a3-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="969a3-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="969a3-161">Azure Media Face Detector</span></span>
<span data-ttu-id="969a3-162">Olá **Azure suporte de dados enfrentam Detector** processador de multimédia (MP) permite-lhe toocount, controlar movimentos e mesmo participação do medidor público-alvo e reação através de expressões facial.</span><span class="sxs-lookup"><span data-stu-id="969a3-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="969a3-163">Este serviço contém duas funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="969a3-163">This service contains two features:</span></span> 

* <span data-ttu-id="969a3-164">**Deteção de rostos em**</span><span class="sxs-lookup"><span data-stu-id="969a3-164">**Face detection**</span></span>
  
    <span data-ttu-id="969a3-165">Deteção de rostos em localiza e controla faces humanos dentro de um vídeo.</span><span class="sxs-lookup"><span data-stu-id="969a3-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="969a3-166">Vários faces podem ser detetados e, subsequentemente, ser monitorizados como estes mover-se, com metadados de hora e a localização do Olá devolvidos num ficheiro JSON.</span><span class="sxs-lookup"><span data-stu-id="969a3-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="969a3-167">Durante o controlo, tentará toogive um toohello ID consistente, mesmo enfrentam enquanto pessoa Olá está a mover à volta no ecrã, mesmo que estes são obstructed ou deixam brevemente moldura Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="969a3-168">Este serviços não efetua o reconhecimento facial.</span><span class="sxs-lookup"><span data-stu-id="969a3-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="969a3-169">Uma pessoa que mantém moldura Olá ou fica obstructed para demasiado tempo terá um novo ID quando devolvem.</span><span class="sxs-lookup"><span data-stu-id="969a3-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="969a3-170">**Deteção de emoções**</span><span class="sxs-lookup"><span data-stu-id="969a3-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="969a3-171">Deteção de emoções é um componente opcional do Olá processador de multimédia de deteção de rostos em devolve Analysis Services em vários atributos emotional de Olá faces detetados, incluindo happiness, sadness, fear, anger e muito mais.</span><span class="sxs-lookup"><span data-stu-id="969a3-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="969a3-173">Modo de deteção</span><span class="sxs-lookup"><span data-stu-id="969a3-173">Detection mode</span></span>
<span data-ttu-id="969a3-174">Um dos seguintes modos de Olá pode ser utilizado pelo processador de Olá:</span><span class="sxs-lookup"><span data-stu-id="969a3-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="969a3-175">Deteção de rostos em</span><span class="sxs-lookup"><span data-stu-id="969a3-175">face detection</span></span>
* <span data-ttu-id="969a3-176">por deteção de emoções de rostos em</span><span class="sxs-lookup"><span data-stu-id="969a3-176">per face emotion detection</span></span>
* <span data-ttu-id="969a3-177">Deteção de emoções agregado</span><span class="sxs-lookup"><span data-stu-id="969a3-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="969a3-178">Nome da tarefa</span><span class="sxs-lookup"><span data-stu-id="969a3-178">Job name</span></span>
<span data-ttu-id="969a3-179">Um nome amigável que lhe permite identificar Olá tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="969a3-180">[Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="969a3-181">Ficheiro de saída</span><span class="sxs-lookup"><span data-stu-id="969a3-181">Output file</span></span>
<span data-ttu-id="969a3-182">Um nome amigável que lhe permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="969a3-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="969a3-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="969a3-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="969a3-184">Olá **Detector de movimento de suporte de dados do Azure** ativa de processador (MP do) suporte de dados tooefficiently identificar secções de interesse num vídeo longo e uneventful caso contrário.</span><span class="sxs-lookup"><span data-stu-id="969a3-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="969a3-185">Deteção de movimento pode ser utilizada em câmara estático filmagens tooidentify secções de vídeo olá onde ocorre o movimento.</span><span class="sxs-lookup"><span data-stu-id="969a3-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="969a3-186">Gera um ficheiro JSON que contém um metadados com carimbos e Olá delimitadora região onde ocorreu o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="969a3-187">Direcionado para os feeds de vídeo de segurança, esta tecnologia é toocategorize capaz de movimento em eventos relevantes e falsos positivos, tais como sombras e alterações de lighting.</span><span class="sxs-lookup"><span data-stu-id="969a3-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="969a3-188">Isto permite-lhe alertas de segurança toogenerate da câmara feeds sem ser spammed com eventos irrelevantes endless, enquanto que está a ser instantes tooextract capaz de interesse de vídeos de vigilância extremamente longos.</span><span class="sxs-lookup"><span data-stu-id="969a3-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="969a3-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="969a3-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="969a3-191">Este processador pode ajudar a criar resumos dos vídeos longos selecionando automaticamente interessantes fragmentos do vídeo de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="969a3-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="969a3-192">Isto é útil quando pretende tooprovide uma descrição geral rápida do que tooexpect um vídeo longo.</span><span class="sxs-lookup"><span data-stu-id="969a3-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="969a3-193">Para obter informações detalhadas e exemplos, consulte [utilize as miniaturas de vídeo do Azure multimédia tooCreate um resumo de vídeo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="969a3-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="969a3-195">Nome da tarefa</span><span class="sxs-lookup"><span data-stu-id="969a3-195">Job name</span></span>
<span data-ttu-id="969a3-196">Um nome amigável que lhe permite identificar Olá tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="969a3-197">[Isto](media-services-portal-check-job-progress.md) artigo descreve como pode monitorizar o progresso de Olá de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="969a3-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="969a3-198">Ficheiro de saída</span><span class="sxs-lookup"><span data-stu-id="969a3-198">Output file</span></span>
<span data-ttu-id="969a3-199">Um nome amigável que lhe permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="969a3-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="969a3-200">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="969a3-200">Next steps</span></span>
<span data-ttu-id="969a3-201">Vista dos Media Services percursos de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="969a3-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="969a3-202">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="969a3-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

