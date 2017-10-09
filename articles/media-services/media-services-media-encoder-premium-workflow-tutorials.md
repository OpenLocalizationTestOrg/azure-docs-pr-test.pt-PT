---
title: Tutoriais de fluxo de trabalho do suporte de dados codificador Premium aaaAvanced
description: "Este documento contém instruções que mostram como tooperform avançadas tarefas com o fluxo de trabalho do suporte de dados codificador Premium e também como toocreate complexas os fluxos de trabalho com o estruturador de fluxo de trabalho."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="21241-103">Tutoriais de fluxo de trabalho do suporte de dados codificador Premium avançadas</span><span class="sxs-lookup"><span data-stu-id="21241-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="21241-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="21241-104">Overview</span></span>
<span data-ttu-id="21241-105">Este documento contém instruções que mostram como toocustomize fluxos de trabalho com **estruturador de fluxo de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="21241-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="21241-106">Pode encontrar os ficheiros de fluxo de trabalho real Olá [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="21241-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="21241-107">TOC</span><span class="sxs-lookup"><span data-stu-id="21241-107">TOC</span></span>
<span data-ttu-id="21241-108">é abrangido Olá os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="21241-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="21241-109">Codificação MXF para uma MP4 de velocidade de transmissão única</span><span class="sxs-lookup"><span data-stu-id="21241-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="21241-110">Iniciar um novo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="21241-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="21241-111">Utilizar Olá entrada de ficheiro do suporte de dados</span><span class="sxs-lookup"><span data-stu-id="21241-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="21241-112">A inspecionar os fluxos de suporte de dados</span><span class="sxs-lookup"><span data-stu-id="21241-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="21241-113">Um codificador vídeo para a adicionar. Geração de ficheiros MP4</span><span class="sxs-lookup"><span data-stu-id="21241-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="21241-114">Sequência de áudio Olá codificação</span><span class="sxs-lookup"><span data-stu-id="21241-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="21241-115">Multiplexação fluxos de áudio e vídeo para um contentor de MP4</span><span class="sxs-lookup"><span data-stu-id="21241-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="21241-116">Escrever Olá MP4 o ficheiro</span><span class="sxs-lookup"><span data-stu-id="21241-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="21241-117">Criar um recurso de serviços de suporte de dados a partir do ficheiro de saída de Olá</span><span class="sxs-lookup"><span data-stu-id="21241-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="21241-118">Olá do teste concluído o fluxo de trabalho localmente</span><span class="sxs-lookup"><span data-stu-id="21241-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="21241-119">Codificação MXF para multibitrate MP4s - empacotamento dinâmico ativado</span><span class="sxs-lookup"><span data-stu-id="21241-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="21241-120">Adicionar um ou mais saídas MP4 adicionais</span><span class="sxs-lookup"><span data-stu-id="21241-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="21241-121">Configurar nomes de saída do ficheiro de Olá</span><span class="sxs-lookup"><span data-stu-id="21241-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="21241-122">Adicionar um registo de áudio separada</span><span class="sxs-lookup"><span data-stu-id="21241-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="21241-123">Adicionar Olá. ISM SMIL ficheiro</span><span class="sxs-lookup"><span data-stu-id="21241-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="21241-124">Codificação MXF para multibitrate MP4 - blueprint avançada</span><span class="sxs-lookup"><span data-stu-id="21241-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="21241-125">Tooenhance de descrição geral do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="21241-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="21241-126">As convenções de nomenclatura de ficheiros</span><span class="sxs-lookup"><span data-stu-id="21241-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="21241-127">Publicação de propriedades do componente na raiz do fluxo de trabalho de Olá</span><span class="sxs-lookup"><span data-stu-id="21241-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="21241-128">Ter gerado o ficheiro de saída nomes baseiam-se nos valores de propriedade publicada</span><span class="sxs-lookup"><span data-stu-id="21241-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="21241-129">Adicionar a saída de MP4 toomultibitrate de miniaturas</span><span class="sxs-lookup"><span data-stu-id="21241-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="21241-130">Miniaturas de tooadd de descrição geral de fluxo de trabalho para</span><span class="sxs-lookup"><span data-stu-id="21241-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="21241-131">Adicionar JPG codificação</span><span class="sxs-lookup"><span data-stu-id="21241-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="21241-132">Lidar com a conversão de espaço de cor</span><span class="sxs-lookup"><span data-stu-id="21241-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="21241-133">Miniaturas de Olá de escrita</span><span class="sxs-lookup"><span data-stu-id="21241-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="21241-134">Detetar erros num fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="21241-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="21241-135">Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="21241-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="21241-136">Corte de baseados no tempo de mensagens em fila de saída multibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="21241-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="21241-137">Fluxo de trabalho descrição geral toostart corte para a adicionar</span><span class="sxs-lookup"><span data-stu-id="21241-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="21241-138">Utilizar Olá Trimmer de fluxo</span><span class="sxs-lookup"><span data-stu-id="21241-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="21241-139">Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="21241-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="21241-140">Introdução ao hello componente convertidos em script</span><span class="sxs-lookup"><span data-stu-id="21241-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="21241-141">Script num fluxo de trabalho: Olá, mundo</span><span class="sxs-lookup"><span data-stu-id="21241-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="21241-142">Com base no período de corte de saída multibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="21241-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="21241-143">Blueprint corte para a adição de toostart de descrição geral</span><span class="sxs-lookup"><span data-stu-id="21241-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="21241-144">Olá Clip lista XML a utilizar</span><span class="sxs-lookup"><span data-stu-id="21241-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="21241-145">Lista de clip Olá modificação de um componente convertidos em script</span><span class="sxs-lookup"><span data-stu-id="21241-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="21241-146">Adicionar uma propriedade de conveniência ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="21241-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="21241-147"><a id="MXF_to_MP4"></a>Codificação MXF para uma MP4 de velocidade de transmissão única</span><span class="sxs-lookup"><span data-stu-id="21241-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="21241-148">Esta explicação passo a passo, vamos criar uma velocidade de transmissão única. Ficheiro MP4 com AAC Putador codificado áudio de um. Ficheiro de entrada MXF.</span><span class="sxs-lookup"><span data-stu-id="21241-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="21241-149"><a id="MXF_to_MP4_start_new"></a>Iniciar um novo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="21241-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="21241-150">Abra o estruturador de fluxo de trabalho e selecione "Blueprint de transcodificar o ficheiro"-"nova área de trabalho"-""</span><span class="sxs-lookup"><span data-stu-id="21241-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="21241-151">novo fluxo de trabalho Olá mostrará 3 elementos:</span><span class="sxs-lookup"><span data-stu-id="21241-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="21241-152">Ficheiro de origem principal</span><span class="sxs-lookup"><span data-stu-id="21241-152">Primary Source File</span></span>
* <span data-ttu-id="21241-153">Lista de clip XML</span><span class="sxs-lookup"><span data-stu-id="21241-153">Clip List XML</span></span>
* <span data-ttu-id="21241-154">Ficheiro/elemento de saída</span><span class="sxs-lookup"><span data-stu-id="21241-154">Output File/Asset</span></span>  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="21241-156">*Novo fluxo de trabalho de codificação*</span><span class="sxs-lookup"><span data-stu-id="21241-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="21241-157"><a id="MXF_to_MP4_with_file_input"></a>Utilizar Olá entrada de ficheiro do suporte de dados</span><span class="sxs-lookup"><span data-stu-id="21241-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="21241-158">Na ordem tooaccept nossa ficheiros de suporte de dados de entrada, um começa com a adição de um componente de entrada de ficheiro do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="21241-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="21241-159">tooadd um fluxo de trabalho de toohello do componente, procure na caixa de pesquisa do repositório de Olá e arraste a entrada de Olá pretendido para Painel estruturador Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="21241-160">Fazê-lo para Olá entrada de ficheiro do suporte de dados e ligue Olá ficheiro de origem principal componente toohello Filename entrada pin do Olá entrada de ficheiro do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="21241-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Entrada de ficheiros de multimédia ligados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="21241-162">*Entrada de ficheiros de multimédia ligados*</span><span class="sxs-lookup"><span data-stu-id="21241-162">*Connected Media File Input*</span></span>

<span data-ttu-id="21241-163">Antes de podermos fazer muito mais, primeiro precisamos estruturador de fluxo de trabalho de toohello tooindicate o ficheiro de exemplo Gostaríamos toouse toodesign nosso fluxo de trabalho com.</span><span class="sxs-lookup"><span data-stu-id="21241-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="21241-164">toodo por isso, clique em segundo plano do estruturador do painel de Olá e procure a propriedade de ficheiro de origem principal Olá no painel da direita de propriedade de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="21241-165">Clique em ícone da pasta Olá e selecione Olá pretendido ficheiro tootest Olá fluxo de trabalho com.</span><span class="sxs-lookup"><span data-stu-id="21241-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="21241-166">Assim que isto é feito, o componente de entrada de ficheiro do suporte de dados de Olá inspecionar o ficheiro de Olá e preencher os respetivos pins tooreflect Olá Ficheirodesaída-inspecioná-los.</span><span class="sxs-lookup"><span data-stu-id="21241-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Entrada do ficheiro de multimédia preenchidas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="21241-168">*Entrada do ficheiro de multimédia preenchidas*</span><span class="sxs-lookup"><span data-stu-id="21241-168">*Populated Media File Input*</span></span>

<span data-ttu-id="21241-169">Enquanto esta ação Especifica com que a entrada de que Gostaríamos toowork com, não indica ainda onde a saída de Olá codificado deve aceda a.</span><span class="sxs-lookup"><span data-stu-id="21241-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="21241-170">Semelhante toohow Olá, que foi configurado, o ficheiro de origem principal agora configurar Olá propriedade da variável de pasta de saída, imediatamente abaixo do mesmo.</span><span class="sxs-lookup"><span data-stu-id="21241-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Propriedades de entrada e saída configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="21241-172">*Propriedades de entrada e saída configuradas*</span><span class="sxs-lookup"><span data-stu-id="21241-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="21241-173"><a id="MXF_to_MP4_streams"></a>A inspecionar os fluxos de suporte de dados</span><span class="sxs-lookup"><span data-stu-id="21241-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="21241-174">Muitas vezes, se pretendido tooknow aspeto como nesse fluxo Olá flui através do fluxo de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="21241-175">tooinspect uma transmissão em fluxo em qualquer ponto num fluxo de trabalho Olá, basta clicar uma saída ou entrada pin em qualquer um dos componentes de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="21241-176">Neste caso, tente clicar no pin de saída de vídeo descomprimidos Olá do nosso entrada de ficheiro do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="21241-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="21241-177">Uma caixa de diálogo abre-se que permite as vídeo de saída de Olá tooinspect.</span><span class="sxs-lookup"><span data-stu-id="21241-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![A inspecionar o pin de saída de vídeo descomprimidos Olá](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="21241-179">*A inspecionar o pin de saída de vídeo descomprimidos Olá*</span><span class="sxs-lookup"><span data-stu-id="21241-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="21241-180">No nosso caso, indica-nos por exemplo, está a lidar com uma entrada de 1920 x 1080 em 24 fotogramas por segundo em 4: amostragem de 2:2 para um vídeo de quase 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="21241-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="21241-181"><a id="MXF_to_MP4_file_generation"></a>Um codificador vídeo para a adicionar. Geração de ficheiros MP4</span><span class="sxs-lookup"><span data-stu-id="21241-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="21241-182">Tenha em atenção que agora, um vídeo descomprimidos e vários pins de saída de áudio descomprimidos estão disponíveis para utilização no nosso entrada de ficheiro do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="21241-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="21241-183">Na ordem tooencode Olá as vídeo de entrada, precisamos de um componente de codificação - neste caso, para a geração. Ficheiros MP4.</span><span class="sxs-lookup"><span data-stu-id="21241-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="21241-184">tooencode Olá tooH.264 de fluxo de vídeo, adicione a superfície de toohello de componente codificador vídeo AVC do Olá designer.</span><span class="sxs-lookup"><span data-stu-id="21241-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="21241-185">Este componente assume um fluxo de vídeo uncompress como entrada e disponibiliza um AVC de fluxo de vídeo comprimido no respetivo pin de saída.</span><span class="sxs-lookup"><span data-stu-id="21241-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Codificador de AVC desligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="21241-187">*Codificador de AVC desligado*</span><span class="sxs-lookup"><span data-stu-id="21241-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="21241-188">As respetivas propriedades determinam como exatamente Olá codificação ocorre.</span><span class="sxs-lookup"><span data-stu-id="21241-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="21241-189">Vamos tem uma vista de olhos algumas das Olá definições mais importantes:</span><span class="sxs-lookup"><span data-stu-id="21241-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="21241-190">Largura de saída e a altura de saída: determinam estes resolução Olá de vídeo Olá codificado.</span><span class="sxs-lookup"><span data-stu-id="21241-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="21241-191">No nosso caso, vamos com 640 x 360</span><span class="sxs-lookup"><span data-stu-id="21241-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="21241-192">Velocidade de fotogramas: quando toopassthrough conjunto irá apenas adotar velocidade de fotogramas da origem Olá, é possível toooverride neste apesar.</span><span class="sxs-lookup"><span data-stu-id="21241-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="21241-193">Tenha em atenção que essas conversão framerate não é movimento-compensada.</span><span class="sxs-lookup"><span data-stu-id="21241-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="21241-194">Perfil e nível: estes determinam que perfil de Olá AVC e nível.</span><span class="sxs-lookup"><span data-stu-id="21241-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="21241-195">tooconveniently obter mais informações sobre os diferentes níveis de Olá e perfis, clique no ícone de ponto de interrogação Olá no componente de codificador de vídeo AVC Olá e página de ajuda de Olá irá mostrar mais detalhes sobre cada um dos níveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="21241-196">Para o nosso exemplo, vamos com perfil principal ao nível 3.2 (predefinição Olá).</span><span class="sxs-lookup"><span data-stu-id="21241-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="21241-197">Taxa de modo de controlo e velocidade de transmissão (kbps): no nosso cenário, optar por uma constante de velocidade de transmissão (CBR) de saída em 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="21241-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="21241-198">Formato de vídeo: trata sobre Olá VUI (informações de utilização de vídeo) que obtém escrito no fluxo de 264 Olá (informações de lado que podem ser utilizadas por uma apresentação do descodificador tooenhance Olá, mas não essencial toocorrectly descodificar):</span><span class="sxs-lookup"><span data-stu-id="21241-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="21241-199">NTSC (típico para EUA ou Japão, utilizando 30 fps)</span><span class="sxs-lookup"><span data-stu-id="21241-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="21241-200">PAL (típico para a Europa, utilizando 25 fps)</span><span class="sxs-lookup"><span data-stu-id="21241-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="21241-201">Modo de dimensionamento GOP: irá ser configurado de tamanho fixo GOP para a nossa fins com uma chave de intervalo de 2 segundos com GOPs fechado.</span><span class="sxs-lookup"><span data-stu-id="21241-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="21241-202">Isto garante a compatibilidade com Olá que fornece de Media Services do Azure empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="21241-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="21241-203">toofeed codificador nosso AVC, ligar o pin de saída de vídeo descomprimidos Olá de Olá entrada de ficheiro do suporte de dados componente toohello as vídeo descomprimidos entrada pin do codificador Olá AVC.</span><span class="sxs-lookup"><span data-stu-id="21241-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Codificador de AVC ligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="21241-205">*Codificador de AVC principal ligado*</span><span class="sxs-lookup"><span data-stu-id="21241-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="21241-206"><a id="MXF_to_MP4_audio"></a>Sequência de áudio Olá codificação</span><span class="sxs-lookup"><span data-stu-id="21241-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="21241-207">Neste momento, estamos ter codificado vídeo, mas sequência de áudio descomprimidos original Olá ainda tem toobe comprimido.</span><span class="sxs-lookup"><span data-stu-id="21241-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="21241-208">Para este podemos irá aceder com AAC codificação por Olá componente AAC codificador (Dolby).</span><span class="sxs-lookup"><span data-stu-id="21241-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="21241-209">Adicione fluxo de trabalho toohello.</span><span class="sxs-lookup"><span data-stu-id="21241-209">Add it toohello workflow.</span></span>

![Codificador de AVC desligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="21241-211">*Codificador AAC desligado*</span><span class="sxs-lookup"><span data-stu-id="21241-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="21241-212">Agora é não existe uma incompatibilidade: há apenas um único descomprimido áudio entrado pin do Olá AAC codificador enquanto mais do que provavelmente Olá de entrada de ficheiro do suporte de dados terá dois diferentes descomprimidos disponível de sequência de áudio: um para Olá deixado de canal de áudio e outro para Olá direito.</span><span class="sxs-lookup"><span data-stu-id="21241-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="21241-213">(Se estiver a lidar com surround som, que é 6 canais). Por isso não é possível toodirectly ligar áudio Olá a partir da origem de entrada de ficheiro do suporte de dados de Olá no codificador de áudio Olá AAC.</span><span class="sxs-lookup"><span data-stu-id="21241-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="21241-214">Olá componente AAC espera que uma sequência de áudio "intercalada" so-called: um fluxo único que tem ambos Olá à esquerda e Olá canais direita interleaved entre si.</span><span class="sxs-lookup"><span data-stu-id="21241-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="21241-215">Depois de sabemos da nossa ficheiros de suporte de dados de origem que controla áudio em que posição na origem de Olá, iremos pode gerar essa sequência de áudio intercalada com Olá corretamente atribuídos posições de orador para a esquerda e direita.</span><span class="sxs-lookup"><span data-stu-id="21241-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="21241-216">Primeiro uma melhor toogenerated um fluxo de canais de áudio Olá necessário origem intercalado.</span><span class="sxs-lookup"><span data-stu-id="21241-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="21241-217">componente de áudio fluxo Interleaver Olá irá processar esta-nos.</span><span class="sxs-lookup"><span data-stu-id="21241-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="21241-218">Adicionar fluxo de trabalho toohello e ligue saídas de áudio Olá de Olá entrada de ficheiro do suporte de dados para a mesma.</span><span class="sxs-lookup"><span data-stu-id="21241-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Ligado Interleaver de sequência de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="21241-220">*Ligado Interleaver de sequência de áudio*</span><span class="sxs-lookup"><span data-stu-id="21241-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="21241-221">Agora que temos uma sequência de áudio intercalada, mas ainda não especificou um onde orador relativos à esquerda ou direita do Olá tooassign posições a.</span><span class="sxs-lookup"><span data-stu-id="21241-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="21241-222">Ordenar toospecify isto, iremos pode tirar partido das Olá orador posição Assigner.</span><span class="sxs-lookup"><span data-stu-id="21241-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Adicionar um Assigner de posição de orador](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="21241-224">*Adicionar um Assigner de posição de orador*</span><span class="sxs-lookup"><span data-stu-id="21241-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="21241-225">Configurar Olá orador posição Assigner para utilização com um fluxo de entrada stereo através de um filtro de configuração predefinida de codificador de "Personalizada" e Olá canal predefinido denominado "2.0 (L, R)".</span><span class="sxs-lookup"><span data-stu-id="21241-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="21241-226">(Isto irá atribuir Olá orador esquerdo posição toochannel 1 e Olá orador direita posição toochannel 2.)</span><span class="sxs-lookup"><span data-stu-id="21241-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="21241-227">Ligar a saída de Olá da entrada de toohello de orador posição Assigner Olá de Olá AAC codificador.</span><span class="sxs-lookup"><span data-stu-id="21241-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="21241-228">Em seguida, informar Olá AAC codificador toowork com um "2.0 (L, R)" canal da configuração predefinida, para que confie toodeal com stereo áudio como entrada.</span><span class="sxs-lookup"><span data-stu-id="21241-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="21241-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexação fluxos de áudio e vídeo para um contentor de MP4</span><span class="sxs-lookup"><span data-stu-id="21241-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="21241-230">Fornecido nosso AVC codificado de transmissão e a nossa AAC codificado sequência de áudio, iremos pode capturar ambos para uma. Contentor de MP4.</span><span class="sxs-lookup"><span data-stu-id="21241-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="21241-231">processo de Olá de combinar vários fluxos para um único é denominado "multiplexação" (ou "muxing").</span><span class="sxs-lookup"><span data-stu-id="21241-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="21241-232">Neste caso, iremos estiver a interleaving áudio Olá e fluxos de vídeo Olá numa única coherent. Pacote MP4.</span><span class="sxs-lookup"><span data-stu-id="21241-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="21241-233">componente de Olá que coordena isto para um. Contentor de MP4 é designado por Olá Multiplexer ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="21241-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="21241-234">Adicione uma superfície do designer toohello e ligar Olá AVC vídeo codificador e entradas de tooits Olá AAC codificador.</span><span class="sxs-lookup"><span data-stu-id="21241-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Ligado MPEG4 Multiplexer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="21241-236">*Ligado MPEG4 Multiplexer*</span><span class="sxs-lookup"><span data-stu-id="21241-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="21241-237"><a id="MXF_to_MP4_writing_mp4"></a>Escrever Olá MP4 o ficheiro</span><span class="sxs-lookup"><span data-stu-id="21241-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="21241-238">Ao escrever um ficheiro de saída, é utilizado o componente de saída do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="21241-239">Iremos pode ligar este resultado toohello Olá ISO MPEG-4 Multiplexer para que o resultado obtém escrito toodisk.</span><span class="sxs-lookup"><span data-stu-id="21241-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="21241-240">toodo, ligar Olá contentor (MPEG-4) saída pin toohello escrita entrada pin de Olá ficheiro de saída.</span><span class="sxs-lookup"><span data-stu-id="21241-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Ligado a saída do ficheiro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="21241-242">*Ligado a saída do ficheiro*</span><span class="sxs-lookup"><span data-stu-id="21241-242">*Connected File Output*</span></span>

<span data-ttu-id="21241-243">Olá filename que será utilizado é determinado pelo Olá propriedade de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="21241-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="21241-244">Embora essa propriedade pode ser tooa codificado deu um valor, provavelmente um convém tooset-lo através de uma expressão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="21241-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="21241-245">o fluxo de trabalho do toohave Olá determinar automaticamente saída Olá propriedade de nome de uma expressão de ficheiros, clique em Olá buton seguinte toohello nome do ficheiro (ícone da pasta toohello seguinte).</span><span class="sxs-lookup"><span data-stu-id="21241-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="21241-246">De Olá menu pendente, em seguida, selecione "Expressão".</span><span class="sxs-lookup"><span data-stu-id="21241-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="21241-247">Editor de expressão Olá será apresentada.</span><span class="sxs-lookup"><span data-stu-id="21241-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="21241-248">Limpe conteúdo Olá do editor de Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="21241-248">Clear hello contents of hello editor first.</span></span>

![Editor de expressão vazia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="21241-250">*Editor de expressão vazia*</span><span class="sxs-lookup"><span data-stu-id="21241-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="21241-251">editor de expressão Olá permite tooenter qualquer valor literal, misturada com uma ou mais variáveis.</span><span class="sxs-lookup"><span data-stu-id="21241-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="21241-252">As variáveis de começar com uma cifrão.</span><span class="sxs-lookup"><span data-stu-id="21241-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="21241-253">Como acessos chave de $ Olá, o editor de Olá irá mostrar uma caixa de lista pendente com uma opção de variáveis disponíveis.</span><span class="sxs-lookup"><span data-stu-id="21241-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="21241-254">No nosso caso utilizaremos uma combinação de variável de diretório de saída Olá e a variável de nome de ficheiro de entrada base Olá:</span><span class="sxs-lookup"><span data-stu-id="21241-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Preenchido fora do Editor de expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="21241-256">*Preenchido fora do Editor de expressão*</span><span class="sxs-lookup"><span data-stu-id="21241-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="21241-257">Ordem toosee ver um ficheiro de saída da tarefa codificação no Azure, tem de fornecer um valor no editor de expressão Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="21241-258">Quando o utilizador confirma expressão Olá por atingir ok, janela de propriedade Olá será pré-visualize toowhat valor Olá ficheiro propriedade resolve neste ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="21241-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![Expressão de ficheiro resolve dir de saída](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="21241-260">*Expressão de ficheiro resolve dir de saída*</span><span class="sxs-lookup"><span data-stu-id="21241-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="21241-261"><a id="MXF_to_MP4_asset_from_output"></a>Criar um recurso de serviços de suporte de dados a partir do ficheiro de saída de Olá</span><span class="sxs-lookup"><span data-stu-id="21241-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="21241-262">Enquanto é escrever um ficheiro de saída MP4, ainda temos tooindicate que este ficheiro pertence toohello de saída do recurso de que os media services irão gerar como resultado de executar este fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21241-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="21241-263">toothis final, o nó de elemento/ficheiro de saída de Olá na tela de fluxo de trabalho de Olá é utilizado.</span><span class="sxs-lookup"><span data-stu-id="21241-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="21241-264">Todos os ficheiros de entrada para este nó fará parte do recurso de Media Services do Azure resultante Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="21241-265">Ligar Olá ficheiro saída componente toohello ficheiro/elemento de saída componente toofinish Olá fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21241-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="21241-267">*Fluxo de trabalho concluído*</span><span class="sxs-lookup"><span data-stu-id="21241-267">*Finished Workflow*</span></span>

### <span data-ttu-id="21241-268"><a id="MXF_to_MP4_test"></a>Olá do teste concluído o fluxo de trabalho localmente</span><span class="sxs-lookup"><span data-stu-id="21241-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="21241-269">tootest Olá fluxo de trabalho localmente, atingiu o botão de reproduzir Olá na barra de ferramentas de Olá na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="21241-270">Quando o fluxo de trabalho Olá concluído executar, Inspecione saída Olá criada na pasta de saída Olá configurado.</span><span class="sxs-lookup"><span data-stu-id="21241-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="21241-271">Verá Olá terminou o ficheiro de saída MP4 codificado do ficheiro de origem de entrada de MXF Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="21241-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codificação MXF em MP4 - multibitrate empacotamento dinâmico ativado</span><span class="sxs-lookup"><span data-stu-id="21241-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="21241-273">Esta explicação passo a passo vamos criar um conjunto de vários ficheiros MP4 de velocidade de transmissão com AAC codificado áudio de um único. Ficheiro de entrada MXF.</span><span class="sxs-lookup"><span data-stu-id="21241-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="21241-274">Quando uma saída de elemento de transmissão múltipla for pretendida para utilização em combinação com funcionalidades de empacotamento dinâmico Olá oferecidas pelos serviços de suporte de dados do Azure, vários ficheiros MP4 alinhada GOP de cada uma resolução e velocidade de transmissão diferentes terá toobe gerado.</span><span class="sxs-lookup"><span data-stu-id="21241-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="21241-275">por isso, Olá toodo [MXF de codificação de mensagens em fila para uma MP4 de velocidade de transmissão única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) explicação passo a passo fornece-nos com um ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="21241-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Iniciar o fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="21241-277">*Iniciar o fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="21241-277">*Starting Workflow*</span></span>

### <span data-ttu-id="21241-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adicionar um ou mais saídas MP4 adicionais</span><span class="sxs-lookup"><span data-stu-id="21241-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="21241-279">Todos os ficheiros MP4 no nosso resultante recurso de Media Services do Azure irão suportar uma resolução e velocidade de transmissão diferentes.</span><span class="sxs-lookup"><span data-stu-id="21241-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="21241-280">Vamos adicionar um ou mais MP4 saída ficheiros toohello fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21241-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="21241-281">toomake se temos Olá todos os nossos vídeos codificadores criadas com as mesmas definições, tooduplicate mais conveniente Olá codificador vídeo de AVC já existente e configurar outra combinação de resolução e velocidade de transmissão (vamos adicionar um 960 x 540 em 25 fotogramas por segundo em 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="21241-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="21241-282">codificador existente do Olá tooduplicate, cópia colar na superfície do designer Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="21241-283">Ligar o pin de saída de vídeo descomprimidos Olá de Olá entrada de ficheiro do suporte de dados para o nosso novo componente AVC.</span><span class="sxs-lookup"><span data-stu-id="21241-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Segundo codificador de AVC ligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="21241-285">*Segundo codificador de AVC ligado*</span><span class="sxs-lookup"><span data-stu-id="21241-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="21241-286">Agora adapte configuração Olá para o nosso toooutput de codificador AVC de nova 960 x 540 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="21241-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="21241-287">(Utilizar o respetivo propriedades "largura de saída", "Altura de saída" e "Velocidade de transmissão (kbps)" para este.)</span><span class="sxs-lookup"><span data-stu-id="21241-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="21241-288">Dado que queremos toouse asset resultante de Olá, juntamente com o empacotamento dinâmico dos serviços de suporte de dados do Azure, tem de Olá ponto final de transmissão em fluxo toobe capaz de gerar destes fragmentos HLS/fragmentado MP4/DASH que são exatamente alinhado tooeach outro de uma forma de ficheiros MP4 Se os clientes que são alternar entre diferentes de forma obtêm uma único uniforme contínua áudio e vídeo experiência.</span><span class="sxs-lookup"><span data-stu-id="21241-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="21241-289">toomake que ocorrem, precisamos tooensure que, nas propriedades de Olá de ambos os codificadores AVC Olá tamanho GOP ("grupo de imagens") para ambos os ficheiros MP4 está definida too2 segundos, que podem ser efetuados por:</span><span class="sxs-lookup"><span data-stu-id="21241-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="21241-290">Definir Olá GOP tamanho modo tooFixed GOP tamanho e</span><span class="sxs-lookup"><span data-stu-id="21241-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="21241-291">segundos de tootwo de intervalo de moldura de chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="21241-292">também definir Olá GOP IDR controlo tooClosed GOP tooensure colocado é de todos os GOP nos respetivas sem dependências</span><span class="sxs-lookup"><span data-stu-id="21241-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="21241-293">toomake nosso toounderstand conveniente de fluxo de trabalho, mudar o nome de codificador de AVC primeiro Olá demasiado "codificador de vídeo AVC 640 x 360 1200kbps" e Olá segundo codificador de AVC "codificador vídeo AVC 960 x 540 2500 kbps".</span><span class="sxs-lookup"><span data-stu-id="21241-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="21241-294">Agora pode adicione uma segunda ISO MPEG-4 Multiplexer e uma segunda saída de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="21241-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="21241-295">Ligue Olá multiplexer toohello novo AVC codificador e certifique-se de que o resultado é direcionado para Olá ficheiro de saída.</span><span class="sxs-lookup"><span data-stu-id="21241-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="21241-296">Em seguida, ligar também Olá AAC codificador áudio saída toohello novo entrada da multiplexer.</span><span class="sxs-lookup"><span data-stu-id="21241-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="21241-297">Olá ficheiro de saída por sua vez, em seguida, possível tooadd de nó de elemento/ficheiro de saída toohello ligado-toohello Asset de serviços de suporte de dados que será criado.</span><span class="sxs-lookup"><span data-stu-id="21241-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Segundo Muxer e ficheiro de saída ligados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="21241-299">*Segundo Muxer e ficheiro de saída ligados*</span><span class="sxs-lookup"><span data-stu-id="21241-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="21241-300">Para compatibilidade com o empacotamento dinâmico de Media Services do Azure, configure a contagem de tooGOP Olá do multiplexer modo de segmento ou a duração e defina Olá GOPs por segmento too1.</span><span class="sxs-lookup"><span data-stu-id="21241-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="21241-301">(Deve ser predefinido Olá.)</span><span class="sxs-lookup"><span data-stu-id="21241-301">(This should be hello default.)</span></span>

![Modos de segmento de Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="21241-303">*Modos de segmento de Muxer*</span><span class="sxs-lookup"><span data-stu-id="21241-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="21241-304">Nota: poderá toorepeat este processo para quaisquer outros velocidade de transmissão e resolução combinações pretende toohave adicionado toohello saída de recurso.</span><span class="sxs-lookup"><span data-stu-id="21241-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="21241-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configurar nomes de saída do ficheiro de Olá</span><span class="sxs-lookup"><span data-stu-id="21241-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="21241-306">Temos de mais do que um elemento de saída de ficheiro único adicionado toohello.</span><span class="sxs-lookup"><span data-stu-id="21241-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="21241-307">Isto fornece uma necessidade toomake se Olá nomes de ficheiros para cada um dos Olá saída ficheiros são diferentes entre si e talvez mesmo aplicam-se uma convenção de nomenclatura de ficheiros, de modo, torna-se limpar do nome de ficheiro Olá está a lidar com.</span><span class="sxs-lookup"><span data-stu-id="21241-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="21241-308">Atribuição de nome de saída do ficheiro pode ser controlada através da expressões no estruturador de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="21241-309">Abra o painel de propriedade Olá para um dos componentes de saída do ficheiro de Olá e abra o editor de expressão Olá para Olá propriedade de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="21241-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="21241-310">A nossa primeiro ficheiro de saída foi configurado através de Olá seguintes expressão (consulte o tutorial Olá para que vai da [MXF tooa transmissão MP4 saída](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="21241-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="21241-311">Isto significa que o nosso filename é determinado pelo duas variáveis: Olá saída toowrite de diretório no e hello nome de base do ficheiro de origem.</span><span class="sxs-lookup"><span data-stu-id="21241-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="21241-312">anterior Olá está exposta como uma propriedade numa raiz de fluxo de trabalho de Olá e Olá esta última opção é determinado pelo ficheiro de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="21241-313">Tenha em atenção que diretório de saída Olá está a utilizar para fins de teste local; Esta propriedade será substituída pelo motor de fluxo de trabalho de Olá quando o fluxo de trabalho Olá é executado pelo processador de multimédia baseado na nuvem de Olá nos Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="21241-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="21241-314">toogive ambos os nossa saída ficheiros uma saída consistente de nomenclatura, alteração Olá primeiro ficheiro expressão Nomenclatura para:</span><span class="sxs-lookup"><span data-stu-id="21241-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="21241-315">e Olá segundo para:</span><span class="sxs-lookup"><span data-stu-id="21241-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="21241-316">Execute um teste intermédio executar toomake se ambos os ficheiros de saída MP4 corretamente são gerados.</span><span class="sxs-lookup"><span data-stu-id="21241-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="21241-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adicionar um registo de áudio separada</span><span class="sxs-lookup"><span data-stu-id="21241-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="21241-318">Como Iremos ver mais tarde quando geramos uma toogo de ficheiro ISM com ficheiros MP4 de saída, iremos irá requerer também um ficheiro MP4 de só de áudio como controlar áudio Olá para nosso transmissão em fluxo adaptável.</span><span class="sxs-lookup"><span data-stu-id="21241-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="21241-319">toocreate este ficheiro, adicione um muxer adicionais toohello fluxo de trabalho de (ISO-MPEG-4 Multiplexer) e ligar o pin de saída do codificador AAC Olá com o respetivo pin de entrada para controlar 1.</span><span class="sxs-lookup"><span data-stu-id="21241-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Áudio Muxer adicionado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="21241-321">*Áudio Muxer adicionado*</span><span class="sxs-lookup"><span data-stu-id="21241-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="21241-322">Crie uma terceira fluxo saído do ficheiro de saída componente toooutput Olá de Olá muxer e configure a expressão de nomenclatura de ficheiro de Olá como:</span><span class="sxs-lookup"><span data-stu-id="21241-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Áudio Muxer criação da saída de ficheiro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="21241-324">*Áudio Muxer criação da saída de ficheiro*</span><span class="sxs-lookup"><span data-stu-id="21241-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="21241-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adicionar Olá. ISM SMIL ficheiro</span><span class="sxs-lookup"><span data-stu-id="21241-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="21241-326">Para Olá empacotamento dinâmico toowork em combinação com ambos os MP4 ficheiros (e Olá MP4 só de áudio) no nosso recurso dos Media Services, também tem de um ficheiro de manifesto (também designado por um ficheiro de "SMIL": sincronizados idioma de integração de suporte).</span><span class="sxs-lookup"><span data-stu-id="21241-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="21241-327">Este ficheiro indica tooAzure Media Services que ficheiros MP4 estão disponíveis para um empacotamento dinâmico e que esses tooconsider para Olá áudio transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="21241-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="21241-328">Um ficheiro de manifesto típico para um conjunto do MP4 com uma única sequência de áudio tem o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="21241-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="21241-329">ficheiro. ISM Olá contém dentro de uma instrução de comutador, tooeach uma referência de Olá MP4 vídeos ficheiros individuais e além do ficheiro de áudio toothose também um (ou mais) referencia tooan MP4 que contém apenas áudio Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="21241-330">A gerar ficheiro de manifesto Olá para o nosso conjunto do MP4 pode ser feito através de um componente chamado Olá "AMS escritor Manifest".</span><span class="sxs-lookup"><span data-stu-id="21241-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="21241-331">toouse, arraste-o para a superfície de Olá e ligue Olá "Escrever concluída" pins de saída de Olá três ficheiros de saída componentes toohello AMS manifesto do escritor de entrada.</span><span class="sxs-lookup"><span data-stu-id="21241-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="21241-332">Em seguida, certifique-se de que tooconnect Olá resultado Olá AMS manifesto escritor toohello ficheiro/elemento de saída.</span><span class="sxs-lookup"><span data-stu-id="21241-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="21241-333">Tal como acontece com a nossa outros ficheiros saída componentes, configure o nome de saída do Olá ISM ficheiro com uma expressão:</span><span class="sxs-lookup"><span data-stu-id="21241-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="21241-334">Nosso fluxo de trabalho concluído aspeto Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="21241-334">Our finished workflow looks like hello below:</span></span>

![Terminar MXF toomultibitrate MP4 fluxo de trabalho de](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="21241-336">*Terminar MXF toomultibitrate MP4 fluxo de trabalho de*</span><span class="sxs-lookup"><span data-stu-id="21241-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="21241-337"><a id="MXF_to__multibitrate_MP4"></a>Codificação MXF para multibitrate MP4 - blueprint avançada</span><span class="sxs-lookup"><span data-stu-id="21241-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="21241-338">No Olá [instruções anteriores do fluxo de trabalho](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) viu como um único recurso de entrada MXF pode ser convertido para um elemento de saída com ficheiros MP4 de velocidade de transmissão múltipla, um ficheiro MP4 de só de áudio e um ficheiro de manifesto para utilização em conjunto com suporte de dados do Azure Serviços de empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="21241-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="21241-339">Estas instruções irão mostrar como alguns dos aspetos Olá podem ser melhorados e efetuadas mais conveniente.</span><span class="sxs-lookup"><span data-stu-id="21241-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="21241-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance de descrição geral do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="21241-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 tooenhance de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="21241-342">*Multibitrate MP4 tooenhance de fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="21241-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="21241-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>As convenções de nomenclatura de ficheiros</span><span class="sxs-lookup"><span data-stu-id="21241-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="21241-344">Fluxo de trabalho anterior Olá especificamos numa expressão simples como base Olá para gerar nomes de ficheiro de saída.</span><span class="sxs-lookup"><span data-stu-id="21241-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="21241-345">Temos algumas duplicação apesar: todos os componentes de ficheiro de saída individual de Olá Olá especificado essa expressão.</span><span class="sxs-lookup"><span data-stu-id="21241-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="21241-346">Por exemplo, o nosso componente de saída do ficheiro para o ficheiro de vídeo primeiro Olá está configurado com esta expressão:</span><span class="sxs-lookup"><span data-stu-id="21241-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="21241-347">Enquanto para Olá segundo saída gráfica, temos de uma expressão como:</span><span class="sxs-lookup"><span data-stu-id="21241-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="21241-348">Não possível limpeza, menos erro suscetível e mais conveniente se podemos foi remova alguns deste duplicação e certifique-coisas mais configuráveis em vez disso?</span><span class="sxs-lookup"><span data-stu-id="21241-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="21241-349">Luckily podemos: capacidades de expressão do designer de Olá em combinação com Olá capacidade toocreate as propriedades personalizadas no nosso raiz de fluxo de trabalho irão dar-numa camada adicional de conveniência.</span><span class="sxs-lookup"><span data-stu-id="21241-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="21241-350">Vamos assumir que irá unidade nome de ficheiro configuração do Olá de forma de ficheiros MP4 individuais de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="21241-351">Estes forma irá pretendemos tooconfigure no Centro de um colocar (em Olá raiz do nosso gráfico), de onde estejam acedida geração de nome de ficheiro de unidade e tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="21241-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="21241-352">toodo isto, vamos começar por publicar a propriedade de velocidade de transmissão de Olá partir de ambos os AVC codificadores toohello de raiz do nosso fluxo de trabalho, para que este fica acessível a partir de ambos os raiz Olá, bem como codificadores Olá AVC.</span><span class="sxs-lookup"><span data-stu-id="21241-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="21241-353">(Mesmo se apresentados em dois oportunidades diferentes, é apenas um valor subjacente.)</span><span class="sxs-lookup"><span data-stu-id="21241-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="21241-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publicação de propriedades do componente na raiz do fluxo de trabalho de Olá</span><span class="sxs-lookup"><span data-stu-id="21241-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="21241-355">Abra o codificador de AVC primeiro Olá, aceda a propriedade de velocidade de transmissão (kbps) toohello e a partir da lista pendente de Olá escolha publicar.</span><span class="sxs-lookup"><span data-stu-id="21241-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Propriedade de velocidade de transmissão de Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="21241-357">*Propriedade de velocidade de transmissão de Olá publicação*</span><span class="sxs-lookup"><span data-stu-id="21241-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="21241-358">Configurar Olá publicar diálogo toopublish toohello de raiz do nosso gráfico de fluxo de trabalho, com um nome de "video1bitrate" publicado e um nome a apresentar legível "Velocidade de transmissão do vídeo 1".</span><span class="sxs-lookup"><span data-stu-id="21241-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="21241-359">Configurar um personalizado o nome do grupo chamado "Transmissão em fluxo de forma" e prima publicar.</span><span class="sxs-lookup"><span data-stu-id="21241-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Propriedade de velocidade de transmissão de Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="21241-361">*Caixa de diálogo de publicação para a propriedade de velocidade de transmissão*</span><span class="sxs-lookup"><span data-stu-id="21241-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="21241-362">Olá repetida mesmo para a propriedade de velocidade de transmissão de Olá do Olá segunda codificador AVC e dê-lhe nome "video2bitrate" com um nome a apresentar "Velocidade de transmissão do vídeo de 2", no Olá mesmo personalizada "Transmissão em fluxo de forma" de grupo.</span><span class="sxs-lookup"><span data-stu-id="21241-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="21241-363">Se agora, iremos inspecionar as propriedades de raiz do fluxo de trabalho Olá, iremos ver nosso grupo personalizado com hello apareçam duas propriedades publicadas.</span><span class="sxs-lookup"><span data-stu-id="21241-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="21241-364">Ambos são ao refletir o valor de Olá da respetiva velocidade de transmissão de codificador de AVC respetiva.</span><span class="sxs-lookup"><span data-stu-id="21241-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Propriedades de velocidade de transmissão publicada numa raiz de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="21241-366">Sempre que queremos tooaccess estas propriedades a partir do código ou a partir de uma expressão, podemos fazer, como esta:</span><span class="sxs-lookup"><span data-stu-id="21241-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="21241-367">a partir do código inline de um componente imediatamente abaixo da raiz de Olá: node.getPropertyAsString('.. / video1bitrate', nulo)</span><span class="sxs-lookup"><span data-stu-id="21241-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="21241-368">dentro de uma expressão: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="21241-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="21241-369">Vamos completar o grupo de "Transmissão em fluxo de forma" Olá ao nosso transmissão de áudio controlar no mesmo, bem como a publicação.</span><span class="sxs-lookup"><span data-stu-id="21241-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="21241-370">Dentro propriedades Olá Olá AAC codificador, procure a definição de velocidade de transmissão de Olá e selecione publicar Olá pendente seguinte tooit.</span><span class="sxs-lookup"><span data-stu-id="21241-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="21241-371">Publicar toohello raiz do gráfico de Olá com o nome "audio1bitrate" e o nome "Velocidade de transmissão do áudio 1" no nosso grupo personalizado "Transmissão em fluxo de forma" a apresentar.</span><span class="sxs-lookup"><span data-stu-id="21241-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Caixa de diálogo publicação de velocidade de transmissão de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="21241-373">*Caixa de diálogo publicação de velocidade de transmissão de áudio*</span><span class="sxs-lookup"><span data-stu-id="21241-373">*Publishing dialog for audio bitrate*</span></span>

![Propriedades de áudio e vídeos resultantes numa raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="21241-375">*Propriedades de áudio e vídeos resultantes numa raiz*</span><span class="sxs-lookup"><span data-stu-id="21241-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="21241-376">Tenha em atenção que a alteração de qualquer um desses três valores também configura novamente e alterações Olá valores em componentes respetivos Olá estes estão ligados com (e onde publicados a partir da).</span><span class="sxs-lookup"><span data-stu-id="21241-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="21241-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Ter gerado o ficheiro de saída nomes baseiam-se nos valores de propriedade publicada</span><span class="sxs-lookup"><span data-stu-id="21241-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="21241-378">Em vez de codificar nosso nomes de ficheiro gerado, iremos pode agora alterar nosso expressão de nome de ficheiro em cada um dos toorely de componentes de saída do ficheiro de Olá nas propriedades de velocidade de transmissão de Olá que vamos apenas publicados na raiz do gráfico Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="21241-379">Começando com o nosso primeiro saída de ficheiro, localizar a propriedade de ficheiro Olá e Editar expressão Olá como esta:</span><span class="sxs-lookup"><span data-stu-id="21241-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="21241-380">parâmetros diferentes de Olá nesta expressão podem ser acedidos e introduzidos por atingir Olá cifrão no teclado Olá enquanto na janela de expressão de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="21241-381">Um dos parâmetros disponíveis Olá é nossa propriedade video1bitrate que iremos publicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="21241-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Aceder a parâmetros dentro de uma expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="21241-383">*Aceder a parâmetros dentro de uma expressão*</span><span class="sxs-lookup"><span data-stu-id="21241-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="21241-384">Olá, mesmo para o resultado de ficheiro Olá para os nosso vídeo segundo:</span><span class="sxs-lookup"><span data-stu-id="21241-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="21241-385">e de saída de ficheiro só de áudio Olá:</span><span class="sxs-lookup"><span data-stu-id="21241-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="21241-386">Se agora, vamos alterar Olá velocidade de transmissão de qualquer um dos vídeo Olá ou ficheiros de áudio, será reconfigurado de codificador respetivos Olá e Convenção de nome de ficheiro com base na velocidade de transmissão de Olá será cumprida todos os automática.</span><span class="sxs-lookup"><span data-stu-id="21241-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="21241-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adicionar a saída de MP4 toomultibitrate de miniaturas</span><span class="sxs-lookup"><span data-stu-id="21241-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="21241-388">A partir de um fluxo de trabalho que gera [um multibitrate MP4 um resultado de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), iremos irá agora ser à procura para adicionar a saída de toohello miniaturas.</span><span class="sxs-lookup"><span data-stu-id="21241-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="21241-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Miniaturas de tooadd de descrição geral de fluxo de trabalho para</span><span class="sxs-lookup"><span data-stu-id="21241-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Multibitrate MP4 toostart de fluxo de trabalho do](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="21241-391">*Multibitrate MP4 toostart de fluxo de trabalho do*</span><span class="sxs-lookup"><span data-stu-id="21241-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="21241-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adicionar JPG codificação</span><span class="sxs-lookup"><span data-stu-id="21241-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="21241-393">heart Olá da nossa em miniatura geração será o componente de codificador JPG Olá, ficheiros JPG toooutput capaz de.</span><span class="sxs-lookup"><span data-stu-id="21241-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![Codificador JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="21241-395">*Codificador JPG*</span><span class="sxs-lookup"><span data-stu-id="21241-395">*JPG Encoder*</span></span>

<span data-ttu-id="21241-396">Diretamente no entanto, não é possível ligar fluxo nossos vídeo descomprimidos de Olá entrada de ficheiro do suporte de dados para o codificador JPG Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="21241-397">Em vez disso, espera toobe entregar frames individuais.</span><span class="sxs-lookup"><span data-stu-id="21241-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="21241-398">Esta ação, podemos fazer através de componente de porta de moldura de vídeo Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-398">This, we can do through hello Video Frame Gate component.</span></span>

![Ligar um codificador JPG toohello do período da porta](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="21241-400">*Ligar um codificador JPG toohello do período da porta*</span><span class="sxs-lookup"><span data-stu-id="21241-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="21241-401">porta de moldura de Olá depois de cada tantas segundos ou frames permite toopass uma moldura de vídeo.</span><span class="sxs-lookup"><span data-stu-id="21241-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="21241-402">pode ser configurado nas propriedades de Olá Olá intervalo e Olá desvio do tempo com que esta situação acontece.</span><span class="sxs-lookup"><span data-stu-id="21241-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Propriedades de porta de moldura vídeos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="21241-404">*Propriedades de porta de moldura vídeos*</span><span class="sxs-lookup"><span data-stu-id="21241-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="21241-405">Vamos criar uma miniatura a cada minuto definindo Olá modo tooTime (segundos) e Olá too60 do intervalo.</span><span class="sxs-lookup"><span data-stu-id="21241-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="21241-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Lidar com a conversão de espaço de cor</span><span class="sxs-lookup"><span data-stu-id="21241-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="21241-407">Enquanto seria parecer lógica os pins de vídeo descomprimidos de porta de moldura Olá e Olá entrada de ficheiro do suporte de dados agora podem ser ligados, iremos deverá receber um aviso se seria fazemo-lo.</span><span class="sxs-lookup"><span data-stu-id="21241-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Erro de espaço de cor de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="21241-409">*Erro de espaço de cor de entrada*</span><span class="sxs-lookup"><span data-stu-id="21241-409">*Input color space error*</span></span>

<span data-ttu-id="21241-410">Isto acontece porque a forma de Olá em que colour informações são representadas na nossa original em bruto descomprimido vídeo sequência provenientes da nossa MXF é diferente da que Olá JPG codificador espera obter.</span><span class="sxs-lookup"><span data-stu-id="21241-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="21241-411">Mais especificamente, uma so-called "cor espaço" de "RGB" ou "Em tons de cinzento" é esperado tooflow no.</span><span class="sxs-lookup"><span data-stu-id="21241-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="21241-412">Isto significa que entrada de transmissão de que Olá vídeo Frame da porta terá toohave uma conversão aplicada sobre o espaço de cor de primeiro.</span><span class="sxs-lookup"><span data-stu-id="21241-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="21241-413">Arraste para Olá de fluxo de trabalho de Olá conversor de espaço de cor - Intel e ligá-lo a porta de moldura tooour.</span><span class="sxs-lookup"><span data-stu-id="21241-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Ligar um Convertor de espaço de cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="21241-415">*Ligar um Convertor de espaço de cor*</span><span class="sxs-lookup"><span data-stu-id="21241-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="21241-416">Na janela de propriedades de Olá, escolha a entrada de Olá BGR 24 Olá predefinição na lista.</span><span class="sxs-lookup"><span data-stu-id="21241-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="21241-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniaturas de Olá de escrita</span><span class="sxs-lookup"><span data-stu-id="21241-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="21241-418">Diferente do vídeo da nossa MP4, Olá codificador JPG componente irá saída mais do que um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="21241-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="21241-419">Na ordem toodeal com esta opção, pode ser utilizado um componente de cenas pesquisa JPG ficheiro escritor: vai demorar miniaturas JPG entradas Olá e escrevê-las, cada nome de ficheiro que está a ser o sufixo por um número diferente.</span><span class="sxs-lookup"><span data-stu-id="21241-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="21241-420">(número de Olá normalmente indicar o número de Olá de segundos/unidades na sequência de Olá que miniatura Olá foi desenhada a partir de.)</span><span class="sxs-lookup"><span data-stu-id="21241-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Introdução ao hello cena pesquisa JPG ficheiro escritor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="21241-422">*Introdução ao hello cena pesquisa JPG ficheiro escritor*</span><span class="sxs-lookup"><span data-stu-id="21241-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="21241-423">Configurar a propriedade de caminho de pasta de saída de Olá com a expressão de Olá: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="21241-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="21241-424">e Olá propriedade de prefixo de nome de ficheiro com:</span><span class="sxs-lookup"><span data-stu-id="21241-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="21241-425">prefixo de Olá irá determinar como ficheiros em miniatura Olá estão a ser designados.</span><span class="sxs-lookup"><span data-stu-id="21241-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="21241-426">Estes irão ser com o sufixo posição de um número com indicação Olá botão no fluxo de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Propriedades de pesquisa JPG ficheiro escritor cena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="21241-428">*Propriedades de pesquisa JPG ficheiro escritor cena*</span><span class="sxs-lookup"><span data-stu-id="21241-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="21241-429">Ligar o nó de elemento/ficheiro de saída do Olá cena pesquisa JPG ficheiro escritor toohello.</span><span class="sxs-lookup"><span data-stu-id="21241-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="21241-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detetar erros num fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="21241-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="21241-431">Ligar a entrada de Olá Olá cor espaço conversor toohello em bruto descomprimidos vídeo de saída de.</span><span class="sxs-lookup"><span data-stu-id="21241-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="21241-432">Agora a efetuar um teste local a executar o fluxo de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="21241-433">Há um fluxo de trabalho de Olá hipótese boa subitamente irá parar de executar e indicar com um contorno vermelho no componente Olá que encontrou um erro:</span><span class="sxs-lookup"><span data-stu-id="21241-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Erro de conversor de espaço de cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="21241-435">*Erro de conversor de espaço de cor*</span><span class="sxs-lookup"><span data-stu-id="21241-435">*Color Space Converter error*</span></span>

<span data-ttu-id="21241-436">Clique ícone de "I" de Olá ligeiramente vermelho na Olá canto superior direito do Olá conversor de espaço de cor componente toosee que é o motivo de Olá falha na tentativa de codificação Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Caixa de diálogo de erro de conversor de espaço de cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="21241-438">*Caixa de diálogo de erro de conversor de espaço de cor*</span><span class="sxs-lookup"><span data-stu-id="21241-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="21241-439">Transforma, como pode ver, que Olá entrada cor espaço padrão para o conversor de espaço de cor Olá tem toobe rec601 para a nossa conversão pedida de YUV tooRGB.</span><span class="sxs-lookup"><span data-stu-id="21241-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="21241-440">Parecer nosso fluxo não indica de rec601.</span><span class="sxs-lookup"><span data-stu-id="21241-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="21241-441">(Rec 601 é um padrão para codificação entrelaçadas analógica sinais de vídeos em formato digital de vídeo.</span><span class="sxs-lookup"><span data-stu-id="21241-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="21241-442">Especifica uma região de Active Directory que abrangem 720 amostras de luminance e 360 chrominance amostras por linha.</span><span class="sxs-lookup"><span data-stu-id="21241-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="21241-443">cor de Olá codificação sistema é conhecido como YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="21241-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="21241-444">toofix isto, iremos irá indicar nos metadados de Olá do nosso fluxo que estamos a lidar com rec601 conteúdo.</span><span class="sxs-lookup"><span data-stu-id="21241-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="21241-445">toodo, pelo que iremos utilizar um componente do Atualizador de tipo de dados de vídeo, vamos pôr em prática entre nosso em bruto de origem e Olá cor espaço conversão componente.</span><span class="sxs-lookup"><span data-stu-id="21241-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="21241-446">Este atualizador do tipo de dados permite que uma atualização manual Olá de determinados dados de vídeos propriedades de tipo.</span><span class="sxs-lookup"><span data-stu-id="21241-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="21241-447">Configure tooindicate um padrão de espaço de cor de "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="21241-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="21241-448">Isto fará com que fluxo do Olá Atualizador de tipo de dados de vídeo tootag Olá com espaço de cor de "Rec 601" Olá se tiver ocorrido não existe espaço de cor definido ainda.</span><span class="sxs-lookup"><span data-stu-id="21241-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="21241-449">(Esta não substituirão quaisquer metadados existente, a menos que a caixa de verificação de substituição de Olá tiver sido selecionada.)</span><span class="sxs-lookup"><span data-stu-id="21241-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Atualizar o padrão de espaço de cor no Olá Atualizador do tipo de dados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="21241-451">*Atualizar o padrão de espaço de cor no Olá Atualizador do tipo de dados*</span><span class="sxs-lookup"><span data-stu-id="21241-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="21241-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="21241-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="21241-453">Agora que a nossa nosso fluxo de trabalho estiver concluído, efetue outro toosee de execução do teste-passe.</span><span class="sxs-lookup"><span data-stu-id="21241-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Fluxo de trabalho concluído para o resultado de várias mp4 com miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="21241-455">*Fluxo de trabalho concluído para o resultado de várias mp4 com miniaturas*</span><span class="sxs-lookup"><span data-stu-id="21241-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="21241-456"><a id="time_based_trim"></a>Corte de baseados no tempo de mensagens em fila de saída multibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="21241-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="21241-457">A partir de um fluxo de trabalho que gera [um multibitrate MP4 um resultado de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), iremos irá agora ser à procura para corte vídeo de origem Olá com base no carimbos de data / hora.</span><span class="sxs-lookup"><span data-stu-id="21241-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="21241-458"><a id="time_based_trim_start"></a>Fluxo de trabalho descrição geral toostart corte para a adicionar</span><span class="sxs-lookup"><span data-stu-id="21241-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Iniciar o corte de tooadd de fluxo de trabalho para](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="21241-460">*Iniciar o corte de tooadd de fluxo de trabalho para*</span><span class="sxs-lookup"><span data-stu-id="21241-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="21241-461"><a id="time_based_trim_use_stream_trimmer"></a>Utilizar Olá Trimmer de fluxo</span><span class="sxs-lookup"><span data-stu-id="21241-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="21241-462">componente de fluxo Trimmer Olá permite início de Olá tootrim e o fim de um fluxo de entrada base nas informações de temporização (segundos, minutos,...). trimmer Olá não suporta corte baseada no intervalo.</span><span class="sxs-lookup"><span data-stu-id="21241-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Fluxo Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="21241-464">*Fluxo Trimmer*</span><span class="sxs-lookup"><span data-stu-id="21241-464">*Stream Trimmer*</span></span>

<span data-ttu-id="21241-465">Em vez de ligar diretamente codificadores Olá AVC e orador posição assigner toohello entrada de ficheiro do suporte de dados, vamos pôr em prática entre essas trimmer de fluxo de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="21241-466">(Um para o sinal de vídeo Olá e outro para o sinal de áudio intercalado Olá.)</span><span class="sxs-lookup"><span data-stu-id="21241-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Colocar em entre Trimmer de fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="21241-468">*Colocar em entre Trimmer de fluxo*</span><span class="sxs-lookup"><span data-stu-id="21241-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="21241-469">Vamos configurar trimmer Olá, para que iremos só irá processar vídeos e áudio entre 15 segundos e 60 segundos vídeo Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="21241-470">Aceda a propriedades de toohello de Olá Trimmer de fluxo de vídeo e configurar a hora de início (15s) e propriedades de hora de fim (60s).</span><span class="sxs-lookup"><span data-stu-id="21241-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="21241-471">toomake se de que os nosso trimmer de áudio e vídeo é sempre toohello configurado mesmo começar e terminar valores, vamos publicar esses raiz toohello de fluxo de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Publicar a propriedade de hora de início do fluxo Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="21241-473">*Publicar a propriedade de hora de início do fluxo Trimmer*</span><span class="sxs-lookup"><span data-stu-id="21241-473">*Publish start time property from Stream Trimmer*</span></span>

![Publicar a caixa de diálogo de propriedades para a hora de início](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="21241-475">*Publicar a caixa de diálogo de propriedades para a hora de início*</span><span class="sxs-lookup"><span data-stu-id="21241-475">*Publish property dialog for start time*</span></span>

![Publicar a caixa de diálogo de propriedades para a hora de fim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="21241-477">*Publicar a caixa de diálogo de propriedades para a hora de fim*</span><span class="sxs-lookup"><span data-stu-id="21241-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="21241-478">Se agora, iremos inspecionar raiz Olá do nosso fluxo de trabalho, ambas as propriedades serão neatly apresentados e configuráveis a partir daí.</span><span class="sxs-lookup"><span data-stu-id="21241-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Propriedades publicadas disponíveis em raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="21241-480">*Propriedades publicadas disponíveis em raiz*</span><span class="sxs-lookup"><span data-stu-id="21241-480">*Published properties available on root*</span></span>

<span data-ttu-id="21241-481">Agora abra as propriedades de corte Olá trimmer áudio Olá e configurar as horas de início e de fim com uma expressão que referencia toohello publicados propriedades na raiz de Olá da nossa fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21241-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="21241-482">Para a hora de início de áudio corte Olá:</span><span class="sxs-lookup"><span data-stu-id="21241-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="21241-483">e para a respetiva hora de fim:</span><span class="sxs-lookup"><span data-stu-id="21241-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="21241-484"><a id="time_based_trim_finish"></a>Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="21241-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="21241-486">*Fluxo de trabalho concluído*</span><span class="sxs-lookup"><span data-stu-id="21241-486">*Finished Workflow*</span></span>

## <span data-ttu-id="21241-487"><a id="scripting"></a>Introdução ao hello componente convertidos em script</span><span class="sxs-lookup"><span data-stu-id="21241-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="21241-488">Componentes com script podem executar scripts arbitrários durante as fases de execução de Olá do nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21241-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="21241-489">Existem quatro scripts diferentes que podem ser executadas, cada um com características específicas e os seus próprios local no ciclo de vida do fluxo de trabalho Olá:</span><span class="sxs-lookup"><span data-stu-id="21241-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="21241-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="21241-490">**commandScript**</span></span>
* <span data-ttu-id="21241-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="21241-491">**realizeScript**</span></span>
* <span data-ttu-id="21241-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="21241-492">**processInputScript**</span></span>
* <span data-ttu-id="21241-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="21241-493">**lifeCycleScript**</span></span>

<span data-ttu-id="21241-494">documentação de Olá de Olá convertidos em script o componente passa mais detalhadamente para cada um dos Olá acima.</span><span class="sxs-lookup"><span data-stu-id="21241-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="21241-495">No [Olá seguinte secção](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), Olá **realizeScript** script componente é tooconstruct utilizado um xml cliplist no momento de Olá quando o fluxo de trabalho Olá começa.</span><span class="sxs-lookup"><span data-stu-id="21241-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="21241-496">Este script chama-se durante a configuração de componente Olá, o que acontece apenas uma vez no ciclo de vida da mesma.</span><span class="sxs-lookup"><span data-stu-id="21241-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="21241-497"><a id="scripting_hello_world"></a>Script num fluxo de trabalho: Olá, mundo</span><span class="sxs-lookup"><span data-stu-id="21241-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="21241-498">Arraste um componente de criar um script para a superfície do designer Olá e mude o nome (por exemplo, "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="21241-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Adicionar um componente com script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="21241-500">*Adicionar um componente com script*</span><span class="sxs-lookup"><span data-stu-id="21241-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="21241-501">Quando inspecionar propriedades Olá de Olá componente convertidos em script, Olá serão apresentados quatro tipos de script diferentes, cada script diferentes tooa configurável.</span><span class="sxs-lookup"><span data-stu-id="21241-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propriedades do componente de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="21241-503">*Propriedades do componente de script*</span><span class="sxs-lookup"><span data-stu-id="21241-503">*Scripted Component properties*</span></span>

<span data-ttu-id="21241-504">Desmarque Olá processInputScript e abra o editor de Olá para Olá realizeScript.</span><span class="sxs-lookup"><span data-stu-id="21241-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="21241-505">Agora iremos estiver configurados e pronto a toostart scripting.</span><span class="sxs-lookup"><span data-stu-id="21241-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="21241-506">Scripts são escritos no Groovy, uma linguagem de script compilada dinamicamente para a plataforma de Java Olá que mantém a compatibilidade com o Java.</span><span class="sxs-lookup"><span data-stu-id="21241-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="21241-507">Na realidade, o código de Java a maioria das é código Groovy válido.</span><span class="sxs-lookup"><span data-stu-id="21241-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="21241-508">Vamos escrever um script de groovy mundo Olá simples no contexto de Olá da nossa realizeScript.</span><span class="sxs-lookup"><span data-stu-id="21241-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="21241-509">Introduza o seguinte Olá num editor de Olá:</span><span class="sxs-lookup"><span data-stu-id="21241-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="21241-510">Agora a executar uma execução de teste local.</span><span class="sxs-lookup"><span data-stu-id="21241-510">Now execute a local test run.</span></span> <span data-ttu-id="21241-511">Após a execução, Inspecione (através do separador sistema Olá Olá convertidos em script componente) Olá propriedade de registos.</span><span class="sxs-lookup"><span data-stu-id="21241-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Saída de registo do Olá mundo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="21241-513">*Saída de registo do Olá mundo*</span><span class="sxs-lookup"><span data-stu-id="21241-513">*Hello world log output*</span></span>

<span data-ttu-id="21241-514">objeto de nó Olá iremos chamar o método de registo de Olá, refere-se tooour atual "nó" ou Olá componente que está a scripting dentro.</span><span class="sxs-lookup"><span data-stu-id="21241-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="21241-515">Todos os componentes como tal, tem Olá capacidade toooutput dados de registo disponíveis através do separador de sistema Olá. Neste caso, iremos saída Olá literal de cadeia "Olá mundo".</span><span class="sxs-lookup"><span data-stu-id="21241-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="21241-516">Importante toounderstand aqui é que este pode provar toobe uma ferramenta de depuração valiosas, fornecendo-lhe conhecimentos aprofundados sobre os scripts de Olá, na verdade, está a fazer.</span><span class="sxs-lookup"><span data-stu-id="21241-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="21241-517">A partir no nosso ambiente de script, iremos também tem acesso tooproperties nos outros componentes.</span><span class="sxs-lookup"><span data-stu-id="21241-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="21241-518">Experimente este:</span><span class="sxs-lookup"><span data-stu-id="21241-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="21241-519">A nossa janela de registo irá mostrar-nos Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="21241-519">Our log window will show us hello following:</span></span>

![Saída de registo para aceder aos caminhos de nó](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="21241-521">*Saída de registo para aceder aos caminhos de nó*</span><span class="sxs-lookup"><span data-stu-id="21241-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="21241-522"><a id="frame_based_trim"></a>Com base no período de corte de saída multibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="21241-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="21241-523">A partir de um fluxo de trabalho que gera [um multibitrate MP4 um resultado de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), iremos irá agora ser à procura para corte vídeo de origem Olá com base nas contagens de moldura.</span><span class="sxs-lookup"><span data-stu-id="21241-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="21241-524"><a id="frame_based_trim_start"></a>Blueprint corte para a adição de toostart de descrição geral</span><span class="sxs-lookup"><span data-stu-id="21241-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Corte para a adição de toostart de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="21241-526">*Corte para a adição de toostart de fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="21241-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="21241-527"><a id="frame_based_trim_clip_list"></a>Olá Clip lista XML a utilizar</span><span class="sxs-lookup"><span data-stu-id="21241-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="21241-528">Em todos os tutoriais de fluxo de trabalho anterior, utilizámos o componente de entrada de ficheiro do suporte de dados de Olá como nossa vídeo origem de entrada.</span><span class="sxs-lookup"><span data-stu-id="21241-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="21241-529">Para este cenário específico, iremos utilizar componentes de origem da lista de Clip Olá em vez disso.</span><span class="sxs-lookup"><span data-stu-id="21241-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="21241-530">Tenha em atenção que esta não deve ser Olá preferencial forma de trabalho; Utilize apenas Olá Clip lista origem quando existe um toodo razão real, por isso, (tal como no Olá abaixo caso, onde que estamos a efetuar a utilização das capacidades de corte Olá clip lista).</span><span class="sxs-lookup"><span data-stu-id="21241-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="21241-531">tooswitch do nosso toohello entrada de ficheiro do suporte de dados de origem da lista de Clip, arraste o componente de origem da lista de Clip Olá para a superfície de desenho de Olá e ligue Olá Clip lista XML pin toohello Clip lista XML o nó do estruturador de fluxo de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="21241-532">Isto deve preencher Olá Clip lista de origem com pins de saída, de acordo com as vídeo de entrada de tooour.</span><span class="sxs-lookup"><span data-stu-id="21241-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="21241-533">Ligar agora pins de vídeo não comprimidos e descomprimidos áudio Olá de Olá Olá Clip lista origem toohello respetivos AVC codificadores e Interleaver de sequência de áudio.</span><span class="sxs-lookup"><span data-stu-id="21241-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="21241-534">Remova agora Olá entrada de ficheiro do suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="21241-534">Now remove hello Media File Input.</span></span>

![Substituído Olá entrada de ficheiro do suporte de dados com Olá Clip lista de origem](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="21241-536">*Substituído Olá entrada de ficheiro do suporte de dados com Olá Clip lista de origem*</span><span class="sxs-lookup"><span data-stu-id="21241-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="21241-537">componente de origem da lista de Clip Olá aceita como entrada um "XML de lista de Clip".</span><span class="sxs-lookup"><span data-stu-id="21241-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="21241-538">Quando selecionar Olá tootest de ficheiro de origem com localmente, este xml de lista clip é preenchido automaticamente para si.</span><span class="sxs-lookup"><span data-stu-id="21241-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Propriedade de Clip lista XML auto-preenchida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="21241-540">*Propriedade de Clip lista XML auto-preenchida*</span><span class="sxs-lookup"><span data-stu-id="21241-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="21241-541">Procura um pouco mais próximo dos toohello xml, este é o aspeto que tem:</span><span class="sxs-lookup"><span data-stu-id="21241-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Caixa de diálogo de lista de clip editar](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="21241-543">*Caixa de diálogo de lista de clip editar*</span><span class="sxs-lookup"><span data-stu-id="21241-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="21241-544">Isto no entanto não reflete as capacidades de Olá de Olá clip lista xml.</span><span class="sxs-lookup"><span data-stu-id="21241-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="21241-545">Uma opção que temos é tooadd um elemento "Compactar" em vídeo Olá e origem de áudio, como esta:</span><span class="sxs-lookup"><span data-stu-id="21241-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Adicionar uma lista do elemento compactação toohello clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="21241-547">*Adicionar uma lista do elemento compactação toohello clip*</span><span class="sxs-lookup"><span data-stu-id="21241-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="21241-548">Se modificar o xml de lista de clip Olá como esta acima e efetuar um teste local executar, verá as vídeo de Olá foi corretamente cortada entre 10 e 20 segundos vídeo Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="21241-549">Contrary toowhat ocorre quando o fizer uma execução local, embora, este xml cliplist muito mesmo não teriam Olá, mesmo que tenha efeito quando aplicada num fluxo de trabalho que é executado em Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="21241-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="21241-550">Quando é iniciado o codificador de Premium do Azure, Olá cliplist xml é gerado sempre novamente, com base na codificação de Olá de ficheiro de entrada do Olá tarefa foi indicada.</span><span class="sxs-lookup"><span data-stu-id="21241-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="21241-551">Isto significa que quaisquer alterações que fazemos no xml de Olá Infelizmente deverá ser substituídas.</span><span class="sxs-lookup"><span data-stu-id="21241-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="21241-552">toocounter Olá cliplist xml que está a ser eliminado quando é iniciada uma tarefa de codificação, iremos pode voltar gerá-la no momento de Olá imediatamente após o início de Olá do nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="21241-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="21241-553">Essas ações personalizadas podem ser criadas através do qual é denominado um "Component convertidos em script".</span><span class="sxs-lookup"><span data-stu-id="21241-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="21241-554">Para obter mais informações, consulte [Introducing Olá convertidos em script componente](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="21241-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="21241-555">Arraste um componente de criar um script para a superfície do designer Olá e renomeie-demasiado "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="21241-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Adicionar um componente com script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="21241-557">*Adicionar um componente com script*</span><span class="sxs-lookup"><span data-stu-id="21241-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="21241-558">Quando inspecionar propriedades Olá de Olá componente convertidos em script, Olá serão apresentados quatro tipos de script diferentes, cada script diferentes tooa configurável.</span><span class="sxs-lookup"><span data-stu-id="21241-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propriedades do componente de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="21241-560">*Propriedades do componente de script*</span><span class="sxs-lookup"><span data-stu-id="21241-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="21241-561"><a id="frame_based_trim_modify_clip_list"></a>Lista de clip Olá modificação de um componente convertidos em script</span><span class="sxs-lookup"><span data-stu-id="21241-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="21241-562">Antes de voltar iremos poder escrever Olá cliplist xml que é gerado durante o arranque do fluxo de trabalho, precisamos da propriedade do toohave acesso toohello cliplist xml e o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="21241-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="21241-563">Pode fazemo-lo como esta:</span><span class="sxs-lookup"><span data-stu-id="21241-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clip entrada que está a ser registada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="21241-565">*Lista de clip entrada que está a ser registada*</span><span class="sxs-lookup"><span data-stu-id="21241-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="21241-566">Primeiro é preciso toodetermine uma forma do ponto de até que ponto queremos tootrim Olá vídeo.</span><span class="sxs-lookup"><span data-stu-id="21241-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="21241-567">publicar este utilizador de menor technical toohello conveniente de fluxo de trabalho Olá, de toomake raiz de toohello duas propriedades do gráfico Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="21241-568">toodo, clique com o botão direito do rato em superfície do designer Olá e selecione "Adicionar propriedade de":</span><span class="sxs-lookup"><span data-stu-id="21241-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="21241-569">Primeira propriedade: "ClippingTimeStart" do tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="21241-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="21241-570">Segunda propriedade: "ClippingTimeEnd" do tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="21241-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Adicionar caixa de diálogo de propriedades para a hora de início de recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="21241-572">*Adicionar caixa de diálogo de propriedades para a hora de início de recorte*</span><span class="sxs-lookup"><span data-stu-id="21241-572">*Add Property dialog for clipping start time*</span></span>

![Publicado recorte propriedades de tempo na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="21241-574">*Publicado recorte propriedades de tempo na raiz do fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="21241-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="21241-575">Configure o valor adequado de tooa de propriedades:</span><span class="sxs-lookup"><span data-stu-id="21241-575">Configure both properties tooa suitable value:</span></span>

![Configurar Olá recorte propriedades de início e de fim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="21241-577">*Configurar Olá recorte propriedades de início e de fim*</span><span class="sxs-lookup"><span data-stu-id="21241-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="21241-578">Agora, de dentro do nosso script, iremos podem aceder a ambas as propriedades, como esta:</span><span class="sxs-lookup"><span data-stu-id="21241-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Janela de registo que mostra início e fim de recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="21241-580">*Janela de registo que mostra início e fim de recorte*</span><span class="sxs-lookup"><span data-stu-id="21241-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="21241-581">Vamos analisar as cadeias de timecode Olá num formulário toouse mais prático, utilizando uma expressão regular simple:</span><span class="sxs-lookup"><span data-stu-id="21241-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Janela de registo com o resultado do timecode analisado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="21241-583">*Janela de registo com o resultado do timecode analisado*</span><span class="sxs-lookup"><span data-stu-id="21241-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="21241-584">Com estas informações em execução, iremos agora pode modificar o início de Olá do Olá cliplist xml tooreflect e hora de fim para Olá pretendido recorte exata de moldura de filmes Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Elementos de compactação do tooadd de código do script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="21241-586">*Elementos de compactação do tooadd de código do script*</span><span class="sxs-lookup"><span data-stu-id="21241-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="21241-587">Isto foi feito através de operações de manipulação de cadeia normal.</span><span class="sxs-lookup"><span data-stu-id="21241-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="21241-588">Olá resultante clip modificado lista xml não é gravado toohello clipListXML propriedade na raiz do fluxo de trabalho Olá através do método de "setProperty" Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="21241-589">janela de registo Olá após a execução de outro teste seria Mostrar nos Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="21241-589">hello log window after another test run would show us hello following:</span></span>

![Lista de clip resultante Olá de registo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="21241-591">*Lista de clip resultante Olá de registo*</span><span class="sxs-lookup"><span data-stu-id="21241-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="21241-592">Efetue um toosee de execução do teste como fluxos de áudio e vídeo Olá tem sido anexados.</span><span class="sxs-lookup"><span data-stu-id="21241-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="21241-593">Como vai fazer mais do que um teste-execução com diferentes valores para os pontos de corte Olá, irá notar que às serão não ser levados em consideração no entanto!</span><span class="sxs-lookup"><span data-stu-id="21241-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="21241-594">motivo Olá para isto é que designer Olá, ao contrário Olá tempo de execução do Azure, não substituição Olá cliplist xml cada execução.</span><span class="sxs-lookup"><span data-stu-id="21241-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="21241-595">Isto significa que apenas hello muito primeira definiu Olá e terminar pontos, fará com que Olá xml tootransform, todos os outros Olá vezes, nosso cláusula de proteção (se (clipListXML.indexOf ("<trim>") = = -1)) irá impedir que o fluxo de trabalho Olá adicionar outra compactação elemento quando já existe um presente.</span><span class="sxs-lookup"><span data-stu-id="21241-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="21241-596">toomake nosso fluxo de trabalho conveniente tootest localmente, é melhor adicionar algum código de manutenção próxima inspeciona se um elemento de compactação já estava presente.</span><span class="sxs-lookup"><span data-stu-id="21241-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="21241-597">Se assim for, iremos removê-lo antes de continuar, modificando Olá xml com novos valores de Olá.</span><span class="sxs-lookup"><span data-stu-id="21241-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="21241-598">Em vez de utilizar manipulações de cadeia simples, é provavelmente mais segura toodo isto através do objeto de real xml de modelo de análise.</span><span class="sxs-lookup"><span data-stu-id="21241-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="21241-599">Antes de pode adicionamos desse código, embora, precisamos tooadd que um número de declarações de importação no Olá início do nosso script primeiro:</span><span class="sxs-lookup"><span data-stu-id="21241-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="21241-600">Depois da primeira, adicionamos Olá necessário o código de limpeza:</span><span class="sxs-lookup"><span data-stu-id="21241-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="21241-601">Este código passa apenas acima ponto Olá que adicionamos Olá elementos compactação toohello cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="21241-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="21241-602">Neste momento, estamos poderá executar e modificar nosso fluxo de trabalho como sucederia com queremos enquanto tem alterações de Olá aplicadas alguma vez.</span><span class="sxs-lookup"><span data-stu-id="21241-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="21241-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adicionar uma propriedade de conveniência ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="21241-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="21241-604">Como não poderá sempre toohappen de corte, vamos concluir desativar nosso fluxo de trabalho, adicionando um conveniente sinalizador booleano que indica se pretende ou não queremos tooenable corte / recorte.</span><span class="sxs-lookup"><span data-stu-id="21241-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="21241-605">Tal como anteriormente, publicar uma nova propriedade toohello de raiz do nosso fluxo de trabalho chamado "ClippingEnabled" do tipo "BOOLEANO".</span><span class="sxs-lookup"><span data-stu-id="21241-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Publicar uma propriedade para ativar recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="21241-607">*Publicar uma propriedade para ativar recorte*</span><span class="sxs-lookup"><span data-stu-id="21241-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="21241-608">Com Olá abaixo cláusula guard simples, iremos pode verificar se é necessário o corte e decidir se nossa lista de clip como tal, precisa de toobe modificado ou não.</span><span class="sxs-lookup"><span data-stu-id="21241-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="21241-609"><a id="code"></a>Código de conclusão</span><span class="sxs-lookup"><span data-stu-id="21241-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="21241-610">Consulte também</span><span class="sxs-lookup"><span data-stu-id="21241-610">Also see</span></span>
[<span data-ttu-id="21241-611">Introdução às Premium codificação, no suporte de dados do Azure, os serviços</span><span class="sxs-lookup"><span data-stu-id="21241-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="21241-612">Como tooUse Premium codificação na Media Services do Azure</span><span class="sxs-lookup"><span data-stu-id="21241-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="21241-613">A codificação de conteúdo a pedido com o serviço de multimédia do Azure</span><span class="sxs-lookup"><span data-stu-id="21241-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="21241-614">Formatos e Codecs de Fluxo de Trabalho Premium do Codificador de Multimédia</span><span class="sxs-lookup"><span data-stu-id="21241-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="21241-615">Ficheiros de fluxo de trabalho de exemplo</span><span class="sxs-lookup"><span data-stu-id="21241-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="21241-616">Ferramenta de Explorador de serviços de suporte de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="21241-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="21241-617">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="21241-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21241-618">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="21241-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
