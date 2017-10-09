---
title: "fluxo de aaaLive com codificadores no local utilizando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial explica Olá passos da criação de um canal que está configurado para uma entrega pass-through."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="0b984-103">Como tooperform em direto de transmissão em fluxo no local codificadores utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0b984-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b984-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0b984-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="0b984-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0b984-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="0b984-106">REST</span><span class="sxs-lookup"><span data-stu-id="0b984-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="0b984-107">Este tutorial explica passos para Olá Olá toocreate portal do Azure a utilizar um **canal** que está configurado para uma entrega pass-through.</span><span class="sxs-lookup"><span data-stu-id="0b984-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0b984-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0b984-108">Prerequisites</span></span>
<span data-ttu-id="0b984-109">Olá, são tutorial de Olá toocomplete necessário:</span><span class="sxs-lookup"><span data-stu-id="0b984-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="0b984-110">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b984-110">An Azure account.</span></span> <span data-ttu-id="0b984-111">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b984-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="0b984-112">Uma conta dos Media Services.</span><span class="sxs-lookup"><span data-stu-id="0b984-112">A Media Services account.</span></span> <span data-ttu-id="0b984-113">toocreate uma conta de Media Services, consulte [como tooCreate uma conta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0b984-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="0b984-114">Uma câmara Web.</span><span class="sxs-lookup"><span data-stu-id="0b984-114">A webcam.</span></span> <span data-ttu-id="0b984-115">Por exemplo, [codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="0b984-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="0b984-116">É altamente recomendável Olá tooreview seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0b984-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="0b984-117">Azure Media Services RTMP Support and Live Encoders (Suporte RTMP dos Serviços de Multimédia do Azure e Codificadores em Direto)</span><span class="sxs-lookup"><span data-stu-id="0b984-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="0b984-118">Overview of Live Streaming using Azure Media Services (Descrição Geral da Transmissão em Fluxo em Direto com os Serviços de Multimédia do Azure)</span><span class="sxs-lookup"><span data-stu-id="0b984-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="0b984-119">Transmissão em fluxo em direto com codificadores no local que criam transmissões com velocidade de transmissão múltipla</span><span class="sxs-lookup"><span data-stu-id="0b984-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="0b984-120"><a id="scenario"></a>Cenário comum de transmissão em fluxo em direto</span><span class="sxs-lookup"><span data-stu-id="0b984-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="0b984-121">Olá passos seguintes descrevem as tarefas envolvidas na criação de aplicações de transmissão em fluxo em direto comuns que utilizam canais que estão configurados para entrega pass-through.</span><span class="sxs-lookup"><span data-stu-id="0b984-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="0b984-122">Este tutorial mostra como toocreate e gerir um canal pass-through e eventos em direto.</span><span class="sxs-lookup"><span data-stu-id="0b984-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="0b984-123">Certifique-se Olá a partir das quais pretende toostream conteúdo de ponto final de transmissão em fluxo no Olá **executar** estado.</span><span class="sxs-lookup"><span data-stu-id="0b984-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="0b984-124">Ligue um computador de tooa câmara de vídeo.</span><span class="sxs-lookup"><span data-stu-id="0b984-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="0b984-125">Iniciar e configurar um codificador em direto no local que produza um RTMP com velocidade de transmissão múltipla ou uma transmissão em fluxo MP4 fragmentada.</span><span class="sxs-lookup"><span data-stu-id="0b984-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="0b984-126">Para obter mais informações, consulte [Suporte RTMP dos Media Services do Azure e Codificadores em Direto](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="0b984-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="0b984-127">Este passo também pode ser realizado depois de criar o Canal.</span><span class="sxs-lookup"><span data-stu-id="0b984-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="0b984-128">Criar e iniciar um Canal pass-through.</span><span class="sxs-lookup"><span data-stu-id="0b984-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="0b984-129">URL de inserção de obter Olá canal.</span><span class="sxs-lookup"><span data-stu-id="0b984-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="0b984-130">URL de inserção de Olá é utilizado pelo Olá codificador em direto toosend Olá fluxo toohello canal.</span><span class="sxs-lookup"><span data-stu-id="0b984-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="0b984-131">Obter o URL de pré-visualização do canal de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="0b984-132">Utilize este tooverify de URL que o canal está a receber corretamente em fluxo em direto Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="0b984-133">Crie um evento/programa em direto.</span><span class="sxs-lookup"><span data-stu-id="0b984-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="0b984-134">Quando utilizar hello portal do Azure, criar um evento em direto também cria um recurso.</span><span class="sxs-lookup"><span data-stu-id="0b984-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="0b984-135">Inicie Olá. o evento/programa quando estiver pronto toostart de transmissão em fluxo e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="0b984-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="0b984-136">Opcionalmente, o codificador em direto Olá pode ser assinalado toostart um anúncio.</span><span class="sxs-lookup"><span data-stu-id="0b984-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="0b984-137">anúncio de Olá é inserido no fluxo de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="0b984-138">Pare Olá. o evento/programa sempre que pretender toostop de transmissão em fluxo e arquivar o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="0b984-139">Eliminar Olá. o evento/programa (e, opcionalmente, elimine o elemento de Olá).</span><span class="sxs-lookup"><span data-stu-id="0b984-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="0b984-140">Reveja [transmissão em fluxo em direto com codificadores no local que criar fluxos de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md) toolearn sobre conceitos e considerações relacionadas com a transmissão em fluxo toolive com codificadores no local e canais pass-through.</span><span class="sxs-lookup"><span data-stu-id="0b984-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="0b984-141">tooview notificações e erros</span><span class="sxs-lookup"><span data-stu-id="0b984-141">tooview notifications and errors</span></span>
<span data-ttu-id="0b984-142">Se pretender tooview notificações e erros produzidos por Olá portal do Azure, clique no ícone de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Notificações](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="0b984-144">Criar e iniciar eventos e canais pass-through</span><span class="sxs-lookup"><span data-stu-id="0b984-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="0b984-145">Um canal está associado a eventos/programas que permitem a publicação de Olá toocontrol e armazenamento de segmentos numa transmissão em fluxo em direto.</span><span class="sxs-lookup"><span data-stu-id="0b984-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="0b984-146">Os canais gerem eventos.</span><span class="sxs-lookup"><span data-stu-id="0b984-146">Channels manage events.</span></span> 

<span data-ttu-id="0b984-147">Pode especificar Olá número de horas que pretende tooretain Olá registada conteúdo para o programa de Olá por definição Olá **janela de arquivo** comprimento.</span><span class="sxs-lookup"><span data-stu-id="0b984-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="0b984-148">Este valor pode ser definido a partir de um mínimo de máximo de tooa de 5 minutos de 25 horas.</span><span class="sxs-lookup"><span data-stu-id="0b984-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="0b984-149">Duração da janela de arquivo dita também Olá período de tempo máximo os clientes podem recuar a partir da posição atual em direto Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="0b984-150">Eventos podem ser executados durante período de tempo especificado Olá, mas o conteúdo que se situe atrás da duração da janela Olá é continuamente descartado.</span><span class="sxs-lookup"><span data-stu-id="0b984-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="0b984-151">Este valor desta propriedade também determina o cliente de Olá quanto possam crescer manifestos.</span><span class="sxs-lookup"><span data-stu-id="0b984-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="0b984-152">Cada evento está associado a um elemento.</span><span class="sxs-lookup"><span data-stu-id="0b984-152">Each event is associated with an asset.</span></span> <span data-ttu-id="0b984-153">evento de Olá toopublish, tem de criar um localizador OnDemand para o recurso de Olá associado.</span><span class="sxs-lookup"><span data-stu-id="0b984-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="0b984-154">Ter este localizador permite toobuild um URL de transmissão em fluxo que pode fornecer tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="0b984-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="0b984-155">Um canal suporta até toothree eventos a executar em simultâneo para que possa criar vários arquivos do Olá mesmo fluxo de entrada.</span><span class="sxs-lookup"><span data-stu-id="0b984-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="0b984-156">Isto permite-lhe toopublish e arquivar diferentes partes de um evento conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0b984-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="0b984-157">Por exemplo, o requisito comercial será tooarchive 6 horas de um programa mas toobroadcast apenas últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="0b984-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="0b984-158">tooaccomplish isto, terá de programas em execução em simultâneo de dois toocreate.</span><span class="sxs-lookup"><span data-stu-id="0b984-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="0b984-159">Um programa está definido tooarchive 6 horas do evento de Olá mas Olá programa não está publicado.</span><span class="sxs-lookup"><span data-stu-id="0b984-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="0b984-160">Olá outro programa está definido tooarchive durante 10 minutos e este programa está publicado.</span><span class="sxs-lookup"><span data-stu-id="0b984-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="0b984-161">Não deve reutilizar os eventos em direto existentes.</span><span class="sxs-lookup"><span data-stu-id="0b984-161">You should not reuse existing live events.</span></span> <span data-ttu-id="0b984-162">Em vez disso, crie e inicie um novo evento para cada evento.</span><span class="sxs-lookup"><span data-stu-id="0b984-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="0b984-163">Inicie o evento de Olá quando estiver pronto toostart de transmissão em fluxo e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="0b984-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="0b984-164">Pare o programa de Olá sempre que pretender toostop de transmissão em fluxo e arquivar o evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="0b984-165">conteúdo toodelete arquivado, pare e eliminar o evento de Olá e, em seguida, elimine o elemento associado Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="0b984-166">Não é possível eliminar um recurso que é utilizado por um evento; evento de Olá deve ser eliminado primeiro.</span><span class="sxs-lookup"><span data-stu-id="0b984-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="0b984-167">Mesmo depois de parar e eliminar o evento de Olá, Olá utilizadores seria capaz de toostream seu conteúdo arquivado como um vídeo a pedido, desde que não a eliminar o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="0b984-168">Se pretender Olá tooretain arquivado conteúdo, mas não o tiver disponível para transmissão em fluxo, elimine Olá localizador de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="0b984-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="0b984-169">toouse Olá portal toocreate um canal</span><span class="sxs-lookup"><span data-stu-id="0b984-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="0b984-170">Esta secção mostra como toouse Olá **criação rápida** opção toocreate um canal pass-through.</span><span class="sxs-lookup"><span data-stu-id="0b984-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="0b984-171">Para obter mais detalhes sobre canais pass-through, veja [Transmissão em fluxo em direto com codificadores no local que criam transmissões em fluxo com velocidade de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="0b984-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="0b984-172">No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b984-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="0b984-173">No Olá **definições** janela, clique em **transmissão em direto**.</span><span class="sxs-lookup"><span data-stu-id="0b984-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Introdução](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="0b984-175">Olá **a transmissão em fluxo em direto** surge a janela.</span><span class="sxs-lookup"><span data-stu-id="0b984-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="0b984-176">Clique em **criação rápida** toocreate um canal pass-through com Olá RTMP protocolo de inserção.</span><span class="sxs-lookup"><span data-stu-id="0b984-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="0b984-177">Olá **criar um novo canal** surge a janela.</span><span class="sxs-lookup"><span data-stu-id="0b984-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="0b984-178">Dê um nome de canal novo Olá e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="0b984-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="0b984-179">Esta ação cria um canal pass-through com Olá protocolo de inserção RTMP.</span><span class="sxs-lookup"><span data-stu-id="0b984-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="0b984-180">Criar eventos</span><span class="sxs-lookup"><span data-stu-id="0b984-180">Create events</span></span>
1. <span data-ttu-id="0b984-181">Selecione um toowhich de canal que pretende tooadd um evento.</span><span class="sxs-lookup"><span data-stu-id="0b984-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="0b984-182">Prima o botão **Evento em Direto**.</span><span class="sxs-lookup"><span data-stu-id="0b984-182">Press **Live Event** button.</span></span>

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="0b984-184">Obter URLs de inserção</span><span class="sxs-lookup"><span data-stu-id="0b984-184">Get ingest URLs</span></span>
<span data-ttu-id="0b984-185">Depois de Olá canal seja criado, pode obter os URLs que irá fornecer o codificador em direto toohello de inserção.</span><span class="sxs-lookup"><span data-stu-id="0b984-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="0b984-186">codificador Olá utiliza estes URLs tooinput uma transmissão em fluxo em direto.</span><span class="sxs-lookup"><span data-stu-id="0b984-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Criado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="0b984-188">Evento de Olá veja</span><span class="sxs-lookup"><span data-stu-id="0b984-188">Watch hello event</span></span>
<span data-ttu-id="0b984-189">evento de Olá toowatch, clique em **veja** no Olá Olá Azure portal ou a cópia do URL de transmissão em fluxo e utilizar um leitor da sua preferência.</span><span class="sxs-lookup"><span data-stu-id="0b984-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Criado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="0b984-191">Evento em direto automaticamente obter conteúdo de convertida tooon a pedido quando parado.</span><span class="sxs-lookup"><span data-stu-id="0b984-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="0b984-192">Limpeza</span><span class="sxs-lookup"><span data-stu-id="0b984-192">Clean up</span></span>
<span data-ttu-id="0b984-193">Para obter mais detalhes sobre canais pass-through, veja [Transmissão em fluxo em direto com codificadores no local que criam transmissões em fluxo com velocidade de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="0b984-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="0b984-194">Um canal pode ser parado apenas quando todos os eventos/programas no canal Olá foram parados.</span><span class="sxs-lookup"><span data-stu-id="0b984-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="0b984-195">Depois de Olá canal esteja parado, não é cobrado qualquer custo.</span><span class="sxs-lookup"><span data-stu-id="0b984-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="0b984-196">Quando tiver toostart-la novamente, pode ter hello mesmo URL de inserção por isso não terá de tooreconfigure o codificador.</span><span class="sxs-lookup"><span data-stu-id="0b984-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="0b984-197">Um canal pode ser eliminado apenas quando todos os eventos em direto no canal Olá tem sido eliminados.</span><span class="sxs-lookup"><span data-stu-id="0b984-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="0b984-198">Ver conteúdo arquivado</span><span class="sxs-lookup"><span data-stu-id="0b984-198">View archived content</span></span>
<span data-ttu-id="0b984-199">Mesmo depois de parar e eliminar o evento de Olá, Olá utilizadores seria capaz de toostream seu conteúdo arquivado como um vídeo a pedido, desde que não a eliminar o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="0b984-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="0b984-200">Não é possível eliminar um recurso que é utilizado por um evento; evento de Olá deve ser eliminado primeiro.</span><span class="sxs-lookup"><span data-stu-id="0b984-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="0b984-201">Selecione os recursos de toomanage **definição** e clique em **ativos**.</span><span class="sxs-lookup"><span data-stu-id="0b984-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Elementos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="0b984-203">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="0b984-203">Next step</span></span>
<span data-ttu-id="0b984-204">Rever os percursos de aprendizagem dos Serviços de Multimédia</span><span class="sxs-lookup"><span data-stu-id="0b984-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0b984-205">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="0b984-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

