---
title: "aaaConfigure Olá FMLE codificador toosend uma transmissão em fluxo em direto | Microsoft Docs"
description: "Este tópico mostra como tooconfigure Olá Flash suporte de dados em direto codificador (FMLE) codificador toosend um canais de tooAMS de fluxo de velocidade de transmissão única que estão ativado para live encoding."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="d6f34-103">Utilizar Olá FMLE codificador toosend uma transmissão em fluxo em direto</span><span class="sxs-lookup"><span data-stu-id="d6f34-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6f34-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="d6f34-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="d6f34-105">Elementar em direto</span><span class="sxs-lookup"><span data-stu-id="d6f34-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="d6f34-106">Transcodificadores</span><span class="sxs-lookup"><span data-stu-id="d6f34-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="d6f34-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="d6f34-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="d6f34-108">Este tópico mostra como tooconfigure Olá [codificador em direto de Flash multimédia](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) codificador toosend tooAMS canais ativados para live encoding de fluxo de velocidade de transmissão única.</span><span class="sxs-lookup"><span data-stu-id="d6f34-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="d6f34-109">Para obter mais informações, consulte [trabalhar com canais que é tooPerform ativado em direto Encoding com Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="d6f34-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="d6f34-110">Este tutorial mostra como toomanage dos Media Services do Azure (AMS) com a ferramenta Explorador de serviços de suporte de dados do Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="d6f34-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="d6f34-111">Esta ferramenta é executada apenas em PCs Windows.</span><span class="sxs-lookup"><span data-stu-id="d6f34-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="d6f34-112">Se estiver no Mac ou Linux, utilize Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="d6f34-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="d6f34-113">Tenha em atenção que este tutorial descreve AAC a utilizar.</span><span class="sxs-lookup"><span data-stu-id="d6f34-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="d6f34-114">No entanto, FMLE não suporta AAC por predefinição.</span><span class="sxs-lookup"><span data-stu-id="d6f34-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="d6f34-115">Terá de toopurchase um plug-in para codificação AAC tais como MainConcept: [Plug-in do AAC](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="d6f34-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6f34-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6f34-116">Prerequisites</span></span>
* [<span data-ttu-id="d6f34-117">Criar uma conta de Media Services do Azure</span><span class="sxs-lookup"><span data-stu-id="d6f34-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="d6f34-118">Certifique-se existe um ponto de final de transmissão em fluxo em execução.</span><span class="sxs-lookup"><span data-stu-id="d6f34-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="d6f34-119">Para obter mais informações, consulte [gerir transmissão em fluxo pontos finais numa conta de Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="d6f34-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="d6f34-120">Instale a versão mais recente do Olá do Olá [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="d6f34-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="d6f34-121">Inicie a ferramenta Olá e ligar conta tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="d6f34-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="d6f34-122">Sugestões</span><span class="sxs-lookup"><span data-stu-id="d6f34-122">Tips</span></span>
* <span data-ttu-id="d6f34-123">Sempre que possível, utilize uma ligação de internet hardwired.</span><span class="sxs-lookup"><span data-stu-id="d6f34-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="d6f34-124">Uma boa regra prática ao determinar os requisitos de largura de banda é Olá toodouble de forma de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="d6f34-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="d6f34-125">Embora não seja um requisito obrigatório, irá ajudar a mitigar o impacto de Olá congestionamento de rede.</span><span class="sxs-lookup"><span data-stu-id="d6f34-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="d6f34-126">Quando utilizar o software com base no codificadores, feche enviados quaisquer programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="d6f34-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="d6f34-127">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="d6f34-127">Create a channel</span></span>
1. <span data-ttu-id="d6f34-128">Na ferramenta AMSE de Olá, navegue toohello **em direto** separador e o botão direito do rato clique na área de canal de Olá.</span><span class="sxs-lookup"><span data-stu-id="d6f34-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="d6f34-129">Selecione **canal de criar...**</span><span class="sxs-lookup"><span data-stu-id="d6f34-129">Select **Create channel…**</span></span> <span data-ttu-id="d6f34-130">no menu Olá.</span><span class="sxs-lookup"><span data-stu-id="d6f34-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="d6f34-132">Especifique um nome de canal, Olá campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="d6f34-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="d6f34-133">Em definições de canal, selecione **padrão** para Olá opção Live Encoding, com Olá entrada protocolo definido demasiado**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="d6f34-134">Pode deixar a todas as outras definições conforme está.</span><span class="sxs-lookup"><span data-stu-id="d6f34-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="d6f34-135">Certifique-se de que Olá **início Olá novo canal agora** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="d6f34-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="d6f34-136">Clique em **criar canal**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="d6f34-138">canal de Olá pode demorar até 20 minutos toostart.</span><span class="sxs-lookup"><span data-stu-id="d6f34-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="d6f34-139">Enquanto está a iniciar o canal de Olá pode [configurar codificador Olá](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="d6f34-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6f34-140">Tenha em atenção que a faturação é iniciada assim que o canal entra no estado pronto.</span><span class="sxs-lookup"><span data-stu-id="d6f34-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="d6f34-141">Para obter mais informações, consulte [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="d6f34-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="d6f34-142"><a id=configure_fmle_rtmp></a>Configurar o codificador FMLE Olá</span><span class="sxs-lookup"><span data-stu-id="d6f34-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="d6f34-143">Este tutorial hello são utilizadas seguintes definições de saída.</span><span class="sxs-lookup"><span data-stu-id="d6f34-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="d6f34-144">rest Olá desta secção descreve os passos de configuração mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="d6f34-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="d6f34-145">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="d6f34-145">**Video**:</span></span>

* <span data-ttu-id="d6f34-146">Codec: 264</span><span class="sxs-lookup"><span data-stu-id="d6f34-146">Codec: H.264</span></span>
* <span data-ttu-id="d6f34-147">Perfil: Alta (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="d6f34-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="d6f34-148">Velocidade de transmissão: kbps 5000</span><span class="sxs-lookup"><span data-stu-id="d6f34-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="d6f34-149">Keyframe: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="d6f34-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="d6f34-150">Taxa de moldura: 30</span><span class="sxs-lookup"><span data-stu-id="d6f34-150">Frame Rate: 30</span></span>

<span data-ttu-id="d6f34-151">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="d6f34-151">**Audio**:</span></span>

* <span data-ttu-id="d6f34-152">O codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="d6f34-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="d6f34-153">Velocidade de transmissão: kbps 192</span><span class="sxs-lookup"><span data-stu-id="d6f34-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="d6f34-154">Frequência de amostragem: kHz 44.1</span><span class="sxs-lookup"><span data-stu-id="d6f34-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="d6f34-155">Passos de configuração</span><span class="sxs-lookup"><span data-stu-id="d6f34-155">Configuration steps</span></span>
1. <span data-ttu-id="d6f34-156">Navegue toohello que interface Flash Live codificador de multimédia (FMLE) na máquina de Olá a ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="d6f34-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="d6f34-157">interface de Olá é uma página principal de definições.</span><span class="sxs-lookup"><span data-stu-id="d6f34-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="d6f34-158">Tome nota dos seguintes Olá recomendados definições tooget começar a transmissão em fluxo utilizando FMLE.</span><span class="sxs-lookup"><span data-stu-id="d6f34-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="d6f34-159">Formato: Taxa de moldura 264: 30.00</span><span class="sxs-lookup"><span data-stu-id="d6f34-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="d6f34-160">Tamanho de entrada: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="d6f34-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="d6f34-161">Taxa de bits: Kbps de 5000 (pode ser ajustado com base no limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="d6f34-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="d6f34-163">Quando utilizar entrelaçadas origens, volte a marca de verificação Olá "Deinterlace" opção</span><span class="sxs-lookup"><span data-stu-id="d6f34-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="d6f34-164">Selecione Olá chave inglesa ícone seguinte tooFormat, devem ser estas definições adicionais:</span><span class="sxs-lookup"><span data-stu-id="d6f34-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="d6f34-165">Perfil: principal</span><span class="sxs-lookup"><span data-stu-id="d6f34-165">Profile: Main</span></span>
   * <span data-ttu-id="d6f34-166">Nível: 4.0</span><span class="sxs-lookup"><span data-stu-id="d6f34-166">Level: 4.0</span></span>
   * <span data-ttu-id="d6f34-167">Frequência de Keyframe: segundos de 2</span><span class="sxs-lookup"><span data-stu-id="d6f34-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="d6f34-169">Definir Olá seguinte definição de áudio importante:</span><span class="sxs-lookup"><span data-stu-id="d6f34-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="d6f34-170">Formato: AAC</span><span class="sxs-lookup"><span data-stu-id="d6f34-170">Format: AAC</span></span>
   * <span data-ttu-id="d6f34-171">Frequência de amostragem: Hz 44100</span><span class="sxs-lookup"><span data-stu-id="d6f34-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="d6f34-172">Velocidade de transmissão: Kbps 192</span><span class="sxs-lookup"><span data-stu-id="d6f34-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="d6f34-174">Obter o URL de entrada do canal de Olá na ordem tooassign-do toohello FMLE **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="d6f34-175">Navegue ferramenta AMSE de back-toohello e verificar estado de conclusão de canal de Olá.</span><span class="sxs-lookup"><span data-stu-id="d6f34-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="d6f34-176">Depois do Estado de Olá foi alterado de **inicial** demasiado**executar**, pode obter o URL de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="d6f34-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="d6f34-177">Quando o canal de Olá está em execução, clique com o botão direito do rato em nome do canal Olá, navegue para baixo toohover através de **tooclipboard do URL de entrada de cópia** e, em seguida, selecione **primário URL de entrada**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="d6f34-179">Colar estas informações no Olá **FMS URL** campo da secção de saída Olá e atribuir um nome de fluxo.</span><span class="sxs-lookup"><span data-stu-id="d6f34-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="d6f34-181">Para fins de redundância adicional, repita estes passos com Olá secundário URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="d6f34-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="d6f34-182">Selecione **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6f34-183">Antes de clicar em **Connect**, **tem** Certifique-se de que o canal de Olá está pronto.</span><span class="sxs-lookup"><span data-stu-id="d6f34-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="d6f34-184">Além disso, certifique-se de que não tooleave Olá canal no estado pronto sem uma entrada contribuição feed durante um período superior > 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="d6f34-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="d6f34-185">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="d6f34-185">Test playback</span></span>

<span data-ttu-id="d6f34-186">Navegue ferramenta AMSE de toohello e clique com o botão direito do rato em Olá canal toobe testado.</span><span class="sxs-lookup"><span data-stu-id="d6f34-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="d6f34-187">No menu de Olá, coloque o cursor sobre **Olá reprodução pré-visualização** e selecione **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="d6f34-188">Se o fluxo de Olá aparece no leitor de Olá, o codificador de Olá foi tooAMS tooconnect está corretamente configurada.</span><span class="sxs-lookup"><span data-stu-id="d6f34-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="d6f34-189">Se é recebido um erro, o canal Olá terá toobe reposição codificador as definições e ajustadas.</span><span class="sxs-lookup"><span data-stu-id="d6f34-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="d6f34-190">Consulte Olá [resolução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="d6f34-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="d6f34-191">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="d6f34-191">Create a program</span></span>
1. <span data-ttu-id="d6f34-192">Depois de reprodução de canal é confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="d6f34-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="d6f34-193">Em Olá **em direto** separador ferramenta AMSE de Olá, com o botão direito clique na área de programa Olá e selecione **criar um novo programa**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="d6f34-195">Nome do programa de Olá e, se necessário, ajuste Olá **duração da janela de arquivo** (as horas de too4 predefinições).</span><span class="sxs-lookup"><span data-stu-id="d6f34-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="d6f34-196">Também pode especificar uma localização de armazenamento ou deixe como a predefinição de Olá.</span><span class="sxs-lookup"><span data-stu-id="d6f34-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="d6f34-197">Verifique Olá **agora iniciar Olá programa** caixa.</span><span class="sxs-lookup"><span data-stu-id="d6f34-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="d6f34-198">Clique em **criar programa**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="d6f34-199">Criação de programa demora menos tempo que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="d6f34-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="d6f34-200">Depois de executa o programa de Olá, confirme reprodução clicando com o botão direito do rato em programa Olá e navegar demasiado**reprodução Olá programas** e, em seguida, selecionar **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="d6f34-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="d6f34-201">Depois de confirmar, o botão direito do rato em novamente o programa de Olá e selecione **copiar Olá URL de saída tooClipboard** (ou obter estas informações de Olá **definições e as informações do programa** opção do menu de Olá).</span><span class="sxs-lookup"><span data-stu-id="d6f34-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="d6f34-202">fluxo Olá está agora pronto toobe incorporado num leitor ou tooan distribuída a público-alvo live visualização.</span><span class="sxs-lookup"><span data-stu-id="d6f34-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="d6f34-203">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="d6f34-203">Troubleshooting</span></span>
<span data-ttu-id="d6f34-204">Consulte Olá [resolução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="d6f34-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d6f34-205">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="d6f34-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6f34-206">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="d6f34-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
