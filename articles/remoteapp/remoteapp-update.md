---
title: "aaaUpdate a coleção do Azure RemoteApp | Microsoft Docs"
description: "Saiba como tooupdate a coleção do Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="7eaca-103">Atualizar uma coleção no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7eaca-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7eaca-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="7eaca-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7eaca-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="7eaca-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7eaca-106">Ficará uma hora, inevitavelmente, quando precisa de imagem ou tooupdate Olá aplicações na sua coleção do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7eaca-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="7eaca-107">Se estiver a utilizar uma das imagens de Olá incluídas na sua subscrição do Azure RemoteApp, numa coleção de uma nuvem ou híbrida, atualizações de todos as são processadas pelo Azure RemoteApp, pelo que pode rest fácil.</span><span class="sxs-lookup"><span data-stu-id="7eaca-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="7eaca-108">No entanto, se estiver a utilizar uma imagem personalizada (que criou a partir do zero ou que criou ao modificar uma das nossas imagens), é responsável pela manutenção Olá imagem e das aplicações.</span><span class="sxs-lookup"><span data-stu-id="7eaca-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="7eaca-109">Se precisar de tooupdate imagem ou qualquer uma das aplicações Olá dentro-lo, terá de toocreate uma versão nova e atualizada da imagem de Olá e, em seguida, substituir Olá existente imagem na sua coleção com esta nova imagem atualizada.</span><span class="sxs-lookup"><span data-stu-id="7eaca-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="7eaca-110">Por isso, como deve proceder atualizar a sua coleção?</span><span class="sxs-lookup"><span data-stu-id="7eaca-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="7eaca-111">É bastante simples:</span><span class="sxs-lookup"><span data-stu-id="7eaca-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="7eaca-112">Atualize imagem de Olá que utilizou na sua coleção.</span><span class="sxs-lookup"><span data-stu-id="7eaca-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="7eaca-113">Aplicar qualquer ou as atualizações necessárias e, em seguida, guarde-o com um novo nome.</span><span class="sxs-lookup"><span data-stu-id="7eaca-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="7eaca-114">[Carregar](remoteapp-uploadimage.md) ou [importar](remoteapp-image-on-azurevm.md) tooRemoteApp essa imagem.</span><span class="sxs-lookup"><span data-stu-id="7eaca-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="7eaca-115">Agora, na página de coleção de Olá, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="7eaca-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="7eaca-116">Escolher imagem novo Olá Olá **imagem de modelo** lista.</span><span class="sxs-lookup"><span data-stu-id="7eaca-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="7eaca-117">Segue-se parte tricky Olá - terá toodecide como toodeal com todos os utilizadores que estão atualmente a utilizar uma aplicação na coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="7eaca-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="7eaca-118">Tem Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="7eaca-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="7eaca-119">**Dê 60 minutos após a atualização de Olá aos utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="7eaca-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="7eaca-120">Assim que a atualização de Olá estiver concluída, o Azure RemoteApp apresentará uma mensagem tooany os utilizadores ativos informar toosave respetivo trabalho registo desativado e volte a iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="7eaca-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="7eaca-121">Após 60 minutos, os utilizadores ativos que não tenham sessão terminada automaticamente a sessão serão terminada.</span><span class="sxs-lookup"><span data-stu-id="7eaca-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="7eaca-122">Os utilizadores podem imediatamente iniciar sessão novamente.</span><span class="sxs-lookup"><span data-stu-id="7eaca-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="7eaca-123">**Terminar sessão dos utilizadores imediatamente**.</span><span class="sxs-lookup"><span data-stu-id="7eaca-123">**Sign users out immediately**.</span></span> <span data-ttu-id="7eaca-124">Assim que a atualização de Olá estiver concluída, terminar sessão todos os utilizadores automaticamente, sem qualquer aviso.</span><span class="sxs-lookup"><span data-stu-id="7eaca-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="7eaca-125">Se escolher esta opção, os utilizadores poderão perder dados.</span><span class="sxs-lookup"><span data-stu-id="7eaca-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="7eaca-126">No entanto, estes podem voltar a ligar aplicação toohello imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7eaca-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="7eaca-127">Clique em Olá marca de verificação toostart Olá atualizar.</span><span class="sxs-lookup"><span data-stu-id="7eaca-127">Click hello check mark toostart hello update.</span></span>

