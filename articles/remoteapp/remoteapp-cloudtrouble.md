---
title: "aaaTroubleshoot RemoteApp as coleções na nuvem - criação | Microsoft Docs"
description: "Saiba como tootroubleshoot RemoteApp cloud falhas na criação de coleção"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="8fe02-103">Criar coleções do RemoteApp na nuvem de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="8fe02-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8fe02-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="8fe02-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8fe02-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="8fe02-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8fe02-106">Se estiver a ter problemas ao criar uma coleção na nuvem, consulte Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="8fe02-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="8fe02-107">A imagem é inválida</span><span class="sxs-lookup"><span data-stu-id="8fe02-107">Your image is invalid</span></span>
<span data-ttu-id="8fe02-108">Se vir uma mensagem como "GoldImageInvalid" quando que está a aguardar tooprovision do Azure a coleção, significa que a imagem de modelo não cumpre os Olá [definido requisitos de imagem](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="8fe02-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="8fe02-109">Por isso, aceda a ler os [requisitos](remoteapp-imagereqs.md), corrija a imagem e tente toocreate a coleção novamente.</span><span class="sxs-lookup"><span data-stu-id="8fe02-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="8fe02-110">Erros comuns vistos no portal de gestão do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8fe02-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="8fe02-111">Coleções de nuvem, muitas vezes, falhar durante a criação devido a está a utilizar imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8fe02-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="8fe02-112">Se vir um Olá acima erros e estiver a utilizar uma coleção de Olá toocreate imagem personalizada, verifique Olá os seguintes aspetos:</span><span class="sxs-lookup"><span data-stu-id="8fe02-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="8fe02-113">Certifique-se de que essa imagem personalizada de Olá carregou cumpre os requisitos de imagem.</span><span class="sxs-lookup"><span data-stu-id="8fe02-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="8fe02-114">Mais frequentemente Olá problema comum é que dessa imagem Olá não foi corretamente syspreped.</span><span class="sxs-lookup"><span data-stu-id="8fe02-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="8fe02-115">Certifique-se de imagem de Olá pode efetuar o arranque no Hyper-V ou tente criar uma VM do IAAS diretamente na sua subscrição do Azure utilizando a imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="8fe02-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="8fe02-116">Se Olá VM falhar tooboot e não iniciar, em seguida, normalmente, isto indica que dessa imagem personalizada Olá não foi preparada corretamente.</span><span class="sxs-lookup"><span data-stu-id="8fe02-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="8fe02-117">Certifique-se de que foi compilada imagem personalizada Olá seguintes Olá como toocreate um modelo personalizado de imagem do RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8fe02-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="8fe02-118">Se estiver a utilizar uma das imagens de Microsoft Olá incluídas na sua subscrição, tente toocreate Olá coleção.</span><span class="sxs-lookup"><span data-stu-id="8fe02-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="8fe02-119">Se Olá problema persistir, contacte o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8fe02-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="8fe02-120">Se vir este erro isto normalmente significa que foram atualizados tooa paga conta, mas que está a tentar toouse uma imagem de Microsoft fornecido é válida apenas durante o modo de avaliação de Olá do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="8fe02-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="8fe02-121">Neste caso, tente toocreate novamente a coleção de nuvem, mas ser toospecify se Olá correto imagem.</span><span class="sxs-lookup"><span data-stu-id="8fe02-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

