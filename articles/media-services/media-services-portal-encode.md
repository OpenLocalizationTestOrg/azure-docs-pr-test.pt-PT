---
title: "aaaEncode um elemento com o codificador de multimédia Standard com Olá portal do Azure | Microsoft Docs"
description: "Este tutorial explica Olá passos da codificação de um elemento com o codificador de multimédia Standard com Olá portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="faddd-103">Codificar um elemento com o codificador de multimédia Standard com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="faddd-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="faddd-104">toocomplete neste tutorial, precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="faddd-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="faddd-105">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="faddd-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="faddd-106">Ao trabalhar com uma das situações mais comuns Olá é a distribuição de clientes de tooyour transmissão em fluxo de velocidade de transmissão adaptável de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="faddd-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="faddd-107">Os Media Services suportam Olá seguintes tecnologias de transmissão em fluxo velocidade de transmissão adaptável: HTTP Live Streaming (HLS), transmissão em fluxo uniforme, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="faddd-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="faddd-108">tooprepare seus vídeos para transmissão em fluxo de velocidade de transmissão adaptável, terá de tooencode a origem de vídeo em ficheiros de transmissão múltipla.</span><span class="sxs-lookup"><span data-stu-id="faddd-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="faddd-109">Deve utilizar Olá **codificador de multimédia Standard** codificador tooencode seus vídeos.</span><span class="sxs-lookup"><span data-stu-id="faddd-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="faddd-110">Os Media Services também fornecem um empacotamento dinâmico, permitindo toodeliver dos seus MP4s de transmissão múltipla no Olá seguintes formatos de transmissão em fluxo: MPEG DASH, HLS, transmissão em fluxo uniforme, sem ter toore-pacote para estes formatos de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="faddd-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="faddd-111">Com o empacotamento dinâmico só tem toostore e pagamento para ficheiros de Olá num único formato de armazenamento e dos Media Services irão compilar e disponibilizar a resposta adequada Olá com base nos pedidos de um cliente.</span><span class="sxs-lookup"><span data-stu-id="faddd-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="faddd-112">tootake partido do empacotamento dinâmico, precisa de tooencode o ficheiro de origem para um conjunto de ficheiros MP4 de velocidade de transmissão múltipla (passos Olá da codificação são demonstrados mais à frente nesta secção).</span><span class="sxs-lookup"><span data-stu-id="faddd-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="faddd-113">suporte de dados de tooscale processar, consulte [isto](media-services-portal-scale-media-processing.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="faddd-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="faddd-114">Codificar com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="faddd-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="faddd-115">Esta secção descreve os passos de Olá que pode tomar tooencode o conteúdo com o codificador de multimédia Standard.</span><span class="sxs-lookup"><span data-stu-id="faddd-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="faddd-116">No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="faddd-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="faddd-117">No Olá **definições** janela, selecione **ativos**.</span><span class="sxs-lookup"><span data-stu-id="faddd-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="faddd-118">No Olá **ativos** janela, asset Olá selecione que gostaria de tooencode.</span><span class="sxs-lookup"><span data-stu-id="faddd-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="faddd-119">Olá prima **codificar** botão.</span><span class="sxs-lookup"><span data-stu-id="faddd-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="faddd-120">No Olá **codificar um elemento** janela, o processador "Codificador de multimédia Standard" Olá selecione e uma predefinição.</span><span class="sxs-lookup"><span data-stu-id="faddd-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="faddd-121">Para obter informações sobre predefinições, veja [Gerar automaticamente uma escala de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de Tarefas para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="faddd-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="faddd-122">Se planear toocontrol que predefinição de codificação é utilizada, evitar que isto em mente: é importante tooselect Olá predefinido que é mais adequada para o seu vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="faddd-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="faddd-123">Por exemplo, se souber o seu vídeo de entrada tem uma resolução de 1920 x 1080 pixels, em seguida, pode utilizar Olá "H264 múltipla 1080p" predefinidas.</span><span class="sxs-lookup"><span data-stu-id="faddd-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="faddd-124">Se tiver um vídeo de baixa resolução (640 x 360), não deve estar a utilizar a predefinição "H264 Taxas de Bits Múltiplas 1080p".</span><span class="sxs-lookup"><span data-stu-id="faddd-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="faddd-125">Para facilitar a gestão, tem uma opção de edição Olá nome do elemento de saída Olá e nome de Olá da tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="faddd-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificar elementos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="faddd-127">Prima **Criar**.</span><span class="sxs-lookup"><span data-stu-id="faddd-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="faddd-128">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="faddd-128">Next step</span></span>
<span data-ttu-id="faddd-129">Pode monitorizar o progresso da tarefa codificação com Olá portal do Azure, conforme descrito em [isto](media-services-portal-check-job-progress.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="faddd-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="faddd-130">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="faddd-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="faddd-131">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="faddd-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

