---
title: "aaaCreate um PHP web de aplicação no Azure | Microsoft Docs"
description: "Implemente em minutos a sua primeira aplicação PHP Hello World nas aplicações Web do serviço de aplicações do Azure."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="65a9a-103">Criar uma aplicação Web PHP no Azure</span><span class="sxs-lookup"><span data-stu-id="65a9a-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="65a9a-104">[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.</span><span class="sxs-lookup"><span data-stu-id="65a9a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="65a9a-105">Este tutorial de início rápido mostra como toodeploy um tooAzure de aplicações do PHP Web Apps.</span><span class="sxs-lookup"><span data-stu-id="65a9a-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="65a9a-106">Criar Olá web app através da Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) na Shell de nuvem e utilizar toodeploy Git exemplo PHP código toohello da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="65a9a-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="65a9a-107">![Aplicação de exemplo em execução no Azure]] (media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="65a9a-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="65a9a-108">Pode seguir os passos seguintes Olá utilizando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="65a9a-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="65a9a-109">Depois de Olá pré-requisitos se encontrem instalados, demora cerca de cinco minutos toocomplete passos Olá.</span><span class="sxs-lookup"><span data-stu-id="65a9a-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65a9a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="65a9a-110">Prerequisites</span></span>

<span data-ttu-id="65a9a-111">toocomplete este guia de introdução:</span><span class="sxs-lookup"><span data-stu-id="65a9a-111">toocomplete this quickstart:</span></span>

* <span data-ttu-id="65a9a-112">[Instale o Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="65a9a-112">[Install Git](https://git-scm.com/)</span></span>
* [<span data-ttu-id="65a9a-113">Instalar o PHP</span><span class="sxs-lookup"><span data-stu-id="65a9a-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="65a9a-114">Transferir o exemplo de Olá localmente</span><span class="sxs-lookup"><span data-stu-id="65a9a-114">Download hello sample locally</span></span>

<span data-ttu-id="65a9a-115">Na janela de terminal, execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="65a9a-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="65a9a-116">Isto será clonar a máquina local de tooyour aplicação de exemplo Olá e navegue até o código de exemplo de Olá contentor do toohello diretório.</span><span class="sxs-lookup"><span data-stu-id="65a9a-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="65a9a-117">Executar localmente a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="65a9a-117">Run hello app locally</span></span>

<span data-ttu-id="65a9a-118">Executar a aplicação Olá localmente ao abrir uma janela de terminal e utilizar Olá `php` comando toolaunch Olá incorporada PHP servidor web.</span><span class="sxs-lookup"><span data-stu-id="65a9a-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="65a9a-119">Abra um browser e navegue até a aplicação de exemplo toohello no http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="65a9a-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="65a9a-120">Consulte Olá **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="65a9a-120">You see hello **Hello World!**</span></span> <span data-ttu-id="65a9a-121">mensagem da aplicação de exemplo de Olá apresentada na página Olá.</span><span class="sxs-lookup"><span data-stu-id="65a9a-121">message from hello sample app displayed in hello page.</span></span>

![Aplicação de exemplo em execução localmente](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="65a9a-123">Na janela do terminal, prima **Ctrl + C** servidor de web de Olá tooexit.</span><span class="sxs-lookup"><span data-stu-id="65a9a-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página da aplicação Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="65a9a-125">Acabou de criar uma nova aplicação Web vazia no Azure.</span><span class="sxs-lookup"><span data-stu-id="65a9a-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="65a9a-126">Procurar toohello aplicação localmente</span><span class="sxs-lookup"><span data-stu-id="65a9a-126">Browse toohello app locally</span></span>

<span data-ttu-id="65a9a-127">Procure a aplicação de toohello implementado utilizando o seu browser.</span><span class="sxs-lookup"><span data-stu-id="65a9a-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="65a9a-128">Olá, código de exemplo do PHP está em execução numa aplicação web App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a9a-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Aplicação de exemplo em execução no Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="65a9a-130">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="65a9a-130">**Congratulations!**</span></span> <span data-ttu-id="65a9a-131">Transferiu o seu primeiro tooApp de aplicações do PHP serviço.</span><span class="sxs-lookup"><span data-stu-id="65a9a-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="65a9a-132">Atualizar localmente e volte a implementar o código de Olá</span><span class="sxs-lookup"><span data-stu-id="65a9a-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="65a9a-133">Com um editor de texto local, abra Olá `index.php` ficheiro dentro da aplicação PHP Olá e faça um texto de toohello pequenas alterações na cadeia de Olá junto demasiado`echo`:</span><span class="sxs-lookup"><span data-stu-id="65a9a-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="65a9a-134">Consolidar as alterações no Git e, em seguida, emitir tooAzure de alterações de código Olá.</span><span class="sxs-lookup"><span data-stu-id="65a9a-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="65a9a-135">Depois de concluída a implementação, mudar a janela do browser back toohello que aberto no Olá **procurar toohello aplicação** passo e página Olá de atualização.</span><span class="sxs-lookup"><span data-stu-id="65a9a-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Aplicação de exemplo atualizada em execução no Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="65a9a-137">Gerir a sua nova aplicação Web do Azure</span><span class="sxs-lookup"><span data-stu-id="65a9a-137">Manage your new Azure web app</span></span>

<span data-ttu-id="65a9a-138">Aceda toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicação que criou.</span><span class="sxs-lookup"><span data-stu-id="65a9a-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="65a9a-139">No menu à esquerda Olá, clique em **serviços aplicacionais**e, em seguida, clique em nome de Olá da sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="65a9a-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="65a9a-141">É apresentada a página de descrição geral da sua aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="65a9a-141">You see your web app's Overview page.</span></span> <span data-ttu-id="65a9a-142">Aqui, pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar.</span><span class="sxs-lookup"><span data-stu-id="65a9a-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Painel Serviço de Aplicações no portal do Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="65a9a-144">menu à esquerda Olá fornece páginas diferentes para configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="65a9a-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="65a9a-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="65a9a-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65a9a-146">PHP com MySQL</span><span class="sxs-lookup"><span data-stu-id="65a9a-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
