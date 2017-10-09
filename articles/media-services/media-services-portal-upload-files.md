---
title: "AAA\"ficheiros de carregamento para uma conta de Media Services utilizando Olá portal do Azure | Microsoft Docs\""
description: "Este tutorial explica Olá passos de carregamento de ficheiros para uma conta de Media Services utilizando Olá portal do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="40efd-103">Carregar ficheiros para uma conta de Media Services utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="40efd-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40efd-104">Portal</span><span class="sxs-lookup"><span data-stu-id="40efd-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="40efd-105">.NET</span><span class="sxs-lookup"><span data-stu-id="40efd-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="40efd-106">REST</span><span class="sxs-lookup"><span data-stu-id="40efd-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="40efd-107">toocomplete neste tutorial, precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="40efd-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="40efd-108">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40efd-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="40efd-109">Nos Serviços de Multimédia, os ficheiros digitais são carregados para um elemento.</span><span class="sxs-lookup"><span data-stu-id="40efd-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="40efd-110">Olá recurso pode conter vídeo, áudio, imagens, coleções de miniaturas, texto controla e legendas ficheiros (e Olá metadados sobre estes ficheiros.) Depois de Olá ficheiros são carregados, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="40efd-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="40efd-111">Carregar ficheiros</span><span class="sxs-lookup"><span data-stu-id="40efd-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="40efd-112">Não há um limite toohello tamanho máximo suportado para processamento nos Media Services.</span><span class="sxs-lookup"><span data-stu-id="40efd-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="40efd-113">Consulte [isto](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre limitação de tamanho de ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="40efd-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="40efd-114">No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="40efd-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="40efd-115">No Olá **definições** painel, clique em **ativos**.</span><span class="sxs-lookup"><span data-stu-id="40efd-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Carregar ficheiros](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="40efd-117">Clique em Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="40efd-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="40efd-118">Olá **carregar um elemento de vídeo** surge a janela.</span><span class="sxs-lookup"><span data-stu-id="40efd-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40efd-119">Não existe qualquer limite de tamanho de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="40efd-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="40efd-120">Procurar as vídeo toohello pretendido no seu computador, selecione-o e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="40efd-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="40efd-121">Olá carregamento inicia e pode ver o progresso de Olá em nome de ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="40efd-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="40efd-122">Após a conclusão do carregamento de Olá, verá Olá novo elemento listado na Olá **ativos** janela.</span><span class="sxs-lookup"><span data-stu-id="40efd-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40efd-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="40efd-123">Next steps</span></span>
<span data-ttu-id="40efd-124">Agora, pode codificar os elementos que carregar.</span><span class="sxs-lookup"><span data-stu-id="40efd-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="40efd-125">Para obter mais informações, veja [Codificar elementos](media-services-portal-encode.md)</span><span class="sxs-lookup"><span data-stu-id="40efd-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="40efd-126">Também pode utilizar as funções do Azure tootrigger uma tarefa de codificação baseada num ficheiro chegar no contentor de Olá configurado.</span><span class="sxs-lookup"><span data-stu-id="40efd-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="40efd-127">Para obter mais informações, veja [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="40efd-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="40efd-128">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="40efd-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="40efd-129">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="40efd-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

