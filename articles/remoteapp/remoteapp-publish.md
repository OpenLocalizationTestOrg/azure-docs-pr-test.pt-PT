---
title: "aaaPublish uma aplicação no Azure RemoteApp | Microsoft Docs"
description: "Saiba como toopublish aplicações e recursos no Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="ce90b-103">Como toopublish uma aplicação no RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ce90b-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ce90b-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="ce90b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ce90b-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ce90b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ce90b-106">Depois de criar a coleção do RemoteApp, terá de toopublish Olá aplicações ou recursos que pretende que toomake disponível para os seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="ce90b-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="ce90b-107">Olá imagens de modelo fornecidas com a sua subscrição apenas tem algumas aplicações publicadas por predefinição - tooshare Olá outras aplicações, terá de toopublish-los.</span><span class="sxs-lookup"><span data-stu-id="ce90b-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="ce90b-108">Precisa de tooupdate uma aplicação?</span><span class="sxs-lookup"><span data-stu-id="ce90b-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="ce90b-109">Terá de demasiado[atualização Olá imagem](remoteapp-update.md) primeiro.</span><span class="sxs-lookup"><span data-stu-id="ce90b-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="ce90b-110">No Olá **publicação** separador no portal de Olá, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="ce90b-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="ce90b-111">Ou pode adicionar uma aplicação a partir da imagem de modelo **iniciar** menu ou forneça Olá caminho toowhere Olá aplicação é instalada numa imagem de modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ce90b-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="ce90b-112">Se selecionar tooadd Olá **iniciar** menu, escolha Olá aplicação toopublish Olá lista.</span><span class="sxs-lookup"><span data-stu-id="ce90b-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="ce90b-113">Se escolher tooprovide Olá caminho toohello aplicação, introduza um nome para a aplicação Olá e Olá caminho toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce90b-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="ce90b-114">Utilizar variáveis no caminho de Olá - por exemplo, "% systemdrive %" em vez de "c:\".</span><span class="sxs-lookup"><span data-stu-id="ce90b-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="ce90b-115">Se quiser tooadd a aplicação da Olá **iniciar** menu, terá de toohave *adicionado toohello essa aplicação **iniciar** menu na imagem de modelo.*</span><span class="sxs-lookup"><span data-stu-id="ce90b-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="ce90b-116">Caso contrário, RemoteApp apenas será apresentada que *é* no Olá **iniciar** menu e irá ser confundido.</span><span class="sxs-lookup"><span data-stu-id="ce90b-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="ce90b-117">toomake se a aplicação fica no Olá **iniciar** menu, colocar um ficheiro de atalho - **.lnk** - Olá %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs pasta.</span><span class="sxs-lookup"><span data-stu-id="ce90b-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="ce90b-118">Caso se tenha esquecido tooadd Olá aplicação toohello **iniciar** menu quando criou o modelo de Olá, escolha tooadd Olá caminho toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="ce90b-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="ce90b-119">(Ou recriar a imagem de modelo, mas é bastante um pouco mais trabalho).</span><span class="sxs-lookup"><span data-stu-id="ce90b-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

