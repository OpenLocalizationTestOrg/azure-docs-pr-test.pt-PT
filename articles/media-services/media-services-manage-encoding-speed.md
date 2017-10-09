---
title: velocidade de gerir AAA e simultaneidade da sua encoding com Media Services do Azure | Microsoft Docs
description: "Este artigo fornece uma breve descrição geral de como pode gerir velocidade e simultaneidade das suas tarefas/tarefas codificação com Media Services do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="7eb42-103">Gerir velocidade e simultaneidade da codificação</span><span class="sxs-lookup"><span data-stu-id="7eb42-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="7eb42-104">Este artigo fornece uma breve descrição geral de como pode gerir velocidade e simultaneidade de tarefas as codificação/tarefas.</span><span class="sxs-lookup"><span data-stu-id="7eb42-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="7eb42-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="7eb42-105">Overview</span></span>

<span data-ttu-id="7eb42-106">Nos Media Services, um **um tipo de unidade reservado** determina a velocidade de Olá com que o suporte de dados de processamento de tarefas é processados.</span><span class="sxs-lookup"><span data-stu-id="7eb42-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="7eb42-107">Pode escolher entre seguinte Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="7eb42-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="7eb42-108">Por exemplo, Olá mesma tarefa de codificação é executada mais rapidamente quando utilizar Olá **S2** tipo de unidade reservada comparar toohello **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="7eb42-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="7eb42-109">Olá [dimensionamento unidades de codificação](media-services-scale-media-processing-overview.md) tópico mostra uma tabela que o ajuda a tomar a decisão ao escolher entre diferentes velocidades de codificação.</span><span class="sxs-lookup"><span data-stu-id="7eb42-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="7eb42-110">Além disso toospecifying Olá reservados de um tipo de unidade, pode especificar a conta com tooprovision **unidades reservadas**.</span><span class="sxs-lookup"><span data-stu-id="7eb42-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="7eb42-111">número de Olá de unidades reservadas aprovisionados determina o número de Olá das tarefas de suporte de dados que podem ser processados em simultâneo numa conta especificada.</span><span class="sxs-lookup"><span data-stu-id="7eb42-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="7eb42-112">Por exemplo, se a sua conta tem cinco unidades reservadas, em seguida, as tarefas de suporte de dados de cinco estarão em execução em simultâneo desde como existem toobe tarefas processado.</span><span class="sxs-lookup"><span data-stu-id="7eb42-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="7eb42-113">tarefas restantes Olá irão aguardar na fila de Olá e irão obter captadas para processar sequencialmente quando terminar, uma tarefa em execução.</span><span class="sxs-lookup"><span data-stu-id="7eb42-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="7eb42-114">Se uma conta não tem quaisquer unidades reservadas aprovisionadas, em seguida, tarefas irão estar captadas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="7eb42-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="7eb42-115">Neste caso, Olá Aguarde algum tempo entre uma tarefa a concluir a e hello iniciar junto de um dependerá da disponibilidade de Olá dos recursos no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eb42-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="7eb42-116">Para obter informações detalhadas e exemplos que mostram como unidades de codificação tooscale, consulte [isto](media-services-scale-media-processing-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="7eb42-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="7eb42-117">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="7eb42-117">Next step</span></span>

[<span data-ttu-id="7eb42-118">Unidades de codificação de escala</span><span class="sxs-lookup"><span data-stu-id="7eb42-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="7eb42-119">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="7eb42-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7eb42-120">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="7eb42-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

