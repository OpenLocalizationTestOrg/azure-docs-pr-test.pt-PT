---
title: "suporte de dados de aaaScale processamento através da adição de unidades de codificação - Azure |  Microsoft Docs"
description: "Saiba como unidades de codificação tooadd toohow com o .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="e3491-103">Como tooscale codificação com o .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e3491-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3491-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e3491-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="e3491-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e3491-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="e3491-106">REST</span><span class="sxs-lookup"><span data-stu-id="e3491-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="e3491-107">Java</span><span class="sxs-lookup"><span data-stu-id="e3491-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="e3491-108">PHP</span><span class="sxs-lookup"><span data-stu-id="e3491-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="e3491-109">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="e3491-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e3491-110">Certifique-se de que tooreview Olá [descrição geral](media-services-scale-media-processing-overview.md) tópico tooget mais informações sobre dimensionamento processamento tópico de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="e3491-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="e3491-111">toochange Olá reservado unidade tipo e Olá número de unidades codificação reservada com o .NET SDK, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="e3491-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="e3491-112">Abrir um pedido de suporte</span><span class="sxs-lookup"><span data-stu-id="e3491-112">Opening a Support Ticket</span></span>
<span data-ttu-id="e3491-113">Por predefinição, cada conta de Media Services pode dimensionar tooup too25 codificação e 5 a pedido de transmissão em fluxo unidades reservadas.</span><span class="sxs-lookup"><span data-stu-id="e3491-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="e3491-114">Pode pedir um limite superior ao abrir um pedido de suporte.</span><span class="sxs-lookup"><span data-stu-id="e3491-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="e3491-115">Abra um pedido de suporte</span><span class="sxs-lookup"><span data-stu-id="e3491-115">Open a support ticket</span></span>
<span data-ttu-id="e3491-116">um pedido de suporte de tooopen Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="e3491-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="e3491-117">Clique em [obter suporte](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="e3491-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="e3491-118">Se não tiver sessão iniciada, terá de ser pedido tooenter as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="e3491-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="e3491-119">Selecione a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="e3491-119">Select your subscription.</span></span>
3. <span data-ttu-id="e3491-120">Em tipo de suporte, selecione "Técnica".</span><span class="sxs-lookup"><span data-stu-id="e3491-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="e3491-121">Clique em "Criar pedido de".</span><span class="sxs-lookup"><span data-stu-id="e3491-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="e3491-122">Selecione "Media Services do Azure" na lista de produto Olá apresentados na página seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="e3491-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="e3491-123">Selecione um "tipo de problema" que é adequado para o seu problema.</span><span class="sxs-lookup"><span data-stu-id="e3491-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="e3491-124">Clique em continuar.</span><span class="sxs-lookup"><span data-stu-id="e3491-124">Click Continue.</span></span>
8. <span data-ttu-id="e3491-125">Siga as instruções na página seguinte e, em seguida, introduza os detalhes sobre o problema.</span><span class="sxs-lookup"><span data-stu-id="e3491-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="e3491-126">Clique em submeter o pedido de suporte do tooopen Olá.</span><span class="sxs-lookup"><span data-stu-id="e3491-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e3491-127">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="e3491-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e3491-128">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="e3491-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

