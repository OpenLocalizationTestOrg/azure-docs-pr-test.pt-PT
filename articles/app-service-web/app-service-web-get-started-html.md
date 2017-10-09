---
title: "aplicação web de aaaCreate um HTML estático no Azure | Microsoft Docs"
description: "Saiba como aplicação de exemplo toorun as web apps no App Service do Azure ao implementar um HTML estático."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="1b0e2-103">Criar uma aplicação Web HTML estática no Azure</span><span class="sxs-lookup"><span data-stu-id="1b0e2-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="1b0e2-104">[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1b0e2-105">Este guia de introdução mostra como toodeploy HTML + CSS básico site tooAzure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="1b0e2-106">Criar Olá web app através da Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e utilizar a aplicação web de conteúdo toohello HTML Git toodeploy exemplo.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Página inicial da aplicação de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="1b0e2-108">Pode seguir os passos seguintes Olá utilizando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1b0e2-109">Depois de Olá pré-requisitos se encontrem instalados, demora cerca de cinco minutos toocomplete passos Olá.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b0e2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b0e2-110">Prerequisites</span></span>

<span data-ttu-id="1b0e2-111">toocomplete este guia de introdução:</span><span class="sxs-lookup"><span data-stu-id="1b0e2-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="1b0e2-112">[Instale o Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="1b0e2-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1b0e2-113">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1b0e2-114">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1b0e2-115">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1b0e2-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="1b0e2-116">Transferir o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="1b0e2-116">Download hello sample</span></span>

<span data-ttu-id="1b0e2-117">Numa janela de terminal, execute Olá os seguintes comandos tooclone Olá exemplo aplicação repositório tooyour computador local.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="1b0e2-118">Utilize toorun desta janela de terminal todos os comandos de Olá neste guia de introdução.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="1b0e2-119">Ver Olá HTML</span><span class="sxs-lookup"><span data-stu-id="1b0e2-119">View hello HTML</span></span>

<span data-ttu-id="1b0e2-120">Navegue toohello diretório que contém o exemplo de Olá HTML.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="1b0e2-121">Abra Olá *index.html* ficheiros no seu browser.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-121">Open hello *index.html* file in your browser.</span></span>

![Home page da aplicação de exemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página da aplicação Web vazia](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="1b0e2-124">Acabou de criar uma nova aplicação Web vazia no Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="1b0e2-125">Procurar aplicações toohello</span><span class="sxs-lookup"><span data-stu-id="1b0e2-125">Browse toohello app</span></span>

<span data-ttu-id="1b0e2-126">Num browser, aceda toohello URL da aplicação web do Azure:</span><span class="sxs-lookup"><span data-stu-id="1b0e2-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1b0e2-127">página Olá está em execução como uma aplicação web do App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-127">hello page is running as an Azure App Service web app.</span></span>

![Home page da aplicação de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="1b0e2-129">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="1b0e2-129">**Congratulations!**</span></span> <span data-ttu-id="1b0e2-130">Transferiu o seu primeiro tooApp de aplicação HTML serviço.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="1b0e2-131">Atualizar e volte a implementar a aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="1b0e2-131">Update and redeploy hello app</span></span>

<span data-ttu-id="1b0e2-132">Abra Olá *index.html* ficheiro num editor de texto e de marcação de toohello uma alteração.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="1b0e2-133">Por exemplo, altere o cabeçalho de Olá H1 de toojust "Azure App Service - exemplo estático HTML o Site" "do serviço de aplicações do Azure".</span><span class="sxs-lookup"><span data-stu-id="1b0e2-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="1b0e2-134">Consolidar as alterações no Git e, em seguida, emitir tooAzure de alterações de código Olá.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="1b0e2-135">Depois de concluída a implementação, Atualize as suas alterações do browser toosee Olá.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Página inicial atualizada da aplicação de exemplo](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1b0e2-137">Gerir a sua nova aplicação Web do Azure</span><span class="sxs-lookup"><span data-stu-id="1b0e2-137">Manage your new Azure web app</span></span>

<span data-ttu-id="1b0e2-138">Aceda toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicação que criou.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="1b0e2-139">No menu à esquerda Olá, clique em **serviços aplicacionais**e, em seguida, clique em nome de Olá da sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="1b0e2-141">É apresentada a página de descrição geral da sua aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-141">You see your web app's Overview page.</span></span> <span data-ttu-id="1b0e2-142">Aqui, pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Painel Serviço de Aplicações no portal do Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="1b0e2-144">menu à esquerda Olá fornece páginas diferentes para configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="1b0e2-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1b0e2-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1b0e2-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b0e2-146">Mapear domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="1b0e2-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
