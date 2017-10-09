---
title: "aaaGet começar a utilizar Mobile Apps do Azure App Service para aplicações xamarin. IOS | Microsoft Docs"
description: "Siga este tutorial tooget começar a utilizar Mobile Apps para o desenvolvimento de xamarin. IOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="60cf5-103">Criar uma aplicação Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="60cf5-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="60cf5-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="60cf5-104">Overview</span></span>
<span data-ttu-id="60cf5-105">Este tutorial mostra como tooadd um back-end baseado na nuvem serviço de aplicações móveis do tooa xamarin. IOS utilizando um back-end de aplicação móvel do Azure.</span><span class="sxs-lookup"><span data-stu-id="60cf5-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="60cf5-106">Pode criar tanto um novo back-end da aplicação móvel assim como uma simples aplicação Xamarin.iOS de uma *Lista de tarefas* que armazena dados da aplicação no Azure.</span><span class="sxs-lookup"><span data-stu-id="60cf5-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="60cf5-107">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais do xamarin. IOS sobre como utilizar a funcionalidade de aplicações móveis Olá no App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="60cf5-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60cf5-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="60cf5-108">Prerequisites</span></span>
<span data-ttu-id="60cf5-109">toocomplete neste tutorial, terá de Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="60cf5-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="60cf5-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="60cf5-110">An active Azure account.</span></span> <span data-ttu-id="60cf5-111">Se não tiver uma conta, inscreva-se uma versão de avaliação do Azure e obter cópias de segurança too10 mobile apps gratuitas que pode continuar a utilizar mesmo após o final da avaliação.</span><span class="sxs-lookup"><span data-stu-id="60cf5-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="60cf5-112">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60cf5-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="60cf5-113">Visual Studio com Xamarin.</span><span class="sxs-lookup"><span data-stu-id="60cf5-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="60cf5-114">Para obter instruções, consulte [Configuração e instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="60cf5-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="60cf5-115">Um Mac com Xcode v7.0 ou posterior e Xamarin Studio Community instalado.</span><span class="sxs-lookup"><span data-stu-id="60cf5-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="60cf5-116">Consulte [Configuração e instalação do Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configuração, instalação e verificações para utilizadores Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="60cf5-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="60cf5-117">Criar um back-end da Aplicação Móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="60cf5-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="60cf5-118">Siga estes passos toocreate um back-end de aplicação móvel.</span><span class="sxs-lookup"><span data-stu-id="60cf5-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="60cf5-119">Configurar o projeto de servidor Olá</span><span class="sxs-lookup"><span data-stu-id="60cf5-119">Configure hello server project</span></span>
<span data-ttu-id="60cf5-120">Acabou de aprovisionar um back-end da Aplicação Móvel do Azure que pode ser utilizado pelas suas aplicações cliente móveis.</span><span class="sxs-lookup"><span data-stu-id="60cf5-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="60cf5-121">Em seguida, transferir um projeto de servidor para um simples "todo list" back-end e publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="60cf5-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="60cf5-122">Siga os seguintes passos tooconfigure Olá servidor projeto toouse de Olá ou Olá Node.js ou .NET back-end.</span><span class="sxs-lookup"><span data-stu-id="60cf5-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="60cf5-123">Transferir e executar a aplicação xamarin. IOS de Olá</span><span class="sxs-lookup"><span data-stu-id="60cf5-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="60cf5-124">Abra Olá [portal do Azure] numa janela do browser.</span><span class="sxs-lookup"><span data-stu-id="60cf5-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="60cf5-125">No painel de definições de Olá da aplicação móvel, clique em **começar** > **xamarin. IOS**.</span><span class="sxs-lookup"><span data-stu-id="60cf5-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="60cf5-126">No passo 3, clique em **Criar uma nova aplicação**, se a opção ainda não estiver selecionada.</span><span class="sxs-lookup"><span data-stu-id="60cf5-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="60cf5-127">Em seguida clique em Olá **transferir** botão.</span><span class="sxs-lookup"><span data-stu-id="60cf5-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="60cf5-128">Uma aplicação cliente que estabelece ligação back-end móvel tooyour é transferida.</span><span class="sxs-lookup"><span data-stu-id="60cf5-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="60cf5-129">Guarde o ficheiro de projeto comprimido Olá para o seu computador local e tome nota do local onde o guardou.</span><span class="sxs-lookup"><span data-stu-id="60cf5-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="60cf5-130">Extraia o projeto de Olá que transferiu e, em seguida, abra-o no Xamarin Studio (ou Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="60cf5-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="60cf5-131">Prima o projeto de Olá Olá F5 toobuild chave e iniciar a aplicação de Olá no emulador do iPhone Olá.</span><span class="sxs-lookup"><span data-stu-id="60cf5-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="60cf5-132">Na aplicação Olá, digite um texto significativo, tal como *saiba Xamarin*e, em seguida, clique em Olá  **+**  botão.</span><span class="sxs-lookup"><span data-stu-id="60cf5-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="60cf5-133">Dados de pedido de Olá são inseridos na tabela TodoItem de Olá.</span><span class="sxs-lookup"><span data-stu-id="60cf5-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="60cf5-134">Os itens armazenados na tabela de Olá são devolvidos pelo back-end de aplicação móvel de Olá, e os dados são apresentados na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="60cf5-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="60cf5-135">Pode rever Olá código que acede ao seu tooquery de back-end da aplicação móvel e inserir dados no Olá ficheiro QSTodoService.cs c#.</span><span class="sxs-lookup"><span data-stu-id="60cf5-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="60cf5-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="60cf5-136">Next steps</span></span>
* [<span data-ttu-id="60cf5-137">Adicionar aplicação tooyour de Sincronização Offline</span><span class="sxs-lookup"><span data-stu-id="60cf5-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="60cf5-138">Adicionar autenticação tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="60cf5-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="60cf5-139">Adicionar a aplicação de xamarin. Android de tooyour de notificações push</span><span class="sxs-lookup"><span data-stu-id="60cf5-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="60cf5-140">Como toouse Olá geridos cliente para Mobile Apps do Azure</span><span class="sxs-lookup"><span data-stu-id="60cf5-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portal do Azure]: https://portal.azure.com/
