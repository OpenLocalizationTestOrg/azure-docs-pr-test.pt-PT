---
title: "aaaUsing Ruby na aplicação Web de serviço de aplicações do Azure no Linux | Microsoft Docs"
description: "Utilizar Ruby na aplicação de Web do App Service do Azure no Linux."
keywords: "serviço de aplicações do Azure, aplicação web, faq, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="3ca1d-104">Utilizar Ruby na aplicação Web no Linux</span><span class="sxs-lookup"><span data-stu-id="3ca1d-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="3ca1d-105">Com Olá mais recente atualização tooour back-end, iremos introduziu o suporte para Ruby v.2.3.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="3ca1d-106">Por definição de configuração de Olá da sua aplicação web do Linux, pode alterar a pilha de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="3ca1d-107">Utilizar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ca1d-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="3ca1d-108">No menu Olá novo no Olá [portal do Azure](https://portal.azure.com), pode escolher toocreate uma aplicação Web no Linux Olá Web + móvel opção conforme mostrado no Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="3ca1d-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Iniciar criação de uma aplicação web no Olá portal do Azure][1]

<span data-ttu-id="3ca1d-110">Em seguida, Olá **painel criar** abre-se conforme mostrado na Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="3ca1d-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Painel de criação de Olá][2]

1. <span data-ttu-id="3ca1d-112">Dê um nome de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-112">Give your web app a name.</span></span>
2. <span data-ttu-id="3ca1d-113">Escolha um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="3ca1d-114">(Consulte regiões disponíveis na Olá [secção limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="3ca1d-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="3ca1d-115">Escolha um plano do App Service do Azure existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="3ca1d-116">(Consulte as notas de plano de serviço de aplicações no Olá [secção limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="3ca1d-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="3ca1d-117">Escolha Olá Ruby pilhas de tempo de execução incorporada Olá.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="3ca1d-118">Depois da aplicação Ruby web é criada, pode implementar tooit utilizando Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="3ca1d-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="3ca1d-119">toolearn mais informações sobre como criar uma aplicação Ruby, verifique Olá [get guia de introdução](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3ca1d-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ca1d-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3ca1d-120">Next steps</span></span>
* [<span data-ttu-id="3ca1d-121">O que é a aplicação Web no Linux?</span><span class="sxs-lookup"><span data-stu-id="3ca1d-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="3ca1d-122">TooAzure de implementação de Git local do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="3ca1d-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="3ca1d-123">Aplicação de Web do App Service do Azure no Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="3ca1d-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="3ca1d-124">Criar uma aplicação Ruby com a aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="3ca1d-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png