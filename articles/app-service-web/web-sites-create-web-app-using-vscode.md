---
title: "aaaCreate uma aplicação web de ASP.NET Core no Visual Studio Code"
description: "Este tutorial ilustra como toocreate um núcleo de ASP.NET web app através do Visual Studio Code."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="b6a7a-103">Criar uma aplicação de web de ASP.NET Core no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b6a7a-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="b6a7a-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="b6a7a-104">Overview</span></span>
<span data-ttu-id="b6a7a-105">Este tutorial mostra como toocreate um núcleo de ASP.NET web app utilizando [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) e implementá-la demasiado[App Service do Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="b6a7a-106">Embora este artigo se refira a aplicações tooweb, também se aplica tooAPI aplicações e aplicações móveis.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="b6a7a-107">ASP.NET Core é uma recriar significativa do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="b6a7a-108">ASP.NET Core é uma nova arquitetura de open source e plataforma para a criação de aplicações web baseados na nuvem modernas utilizando o .NET.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="b6a7a-109">Para obter mais informações, consulte [introdução tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="b6a7a-110">Para obter informações sobre as aplicações web do App Service do Azure, consulte [descrição geral de aplicações Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="b6a7a-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b6a7a-111">Prerequisites</span></span>
* <span data-ttu-id="b6a7a-112">Instalar [o VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="b6a7a-113">Instalar o Git - pode instalá-lo a partir de qualquer um destas localizações: [Chocolatey](https://chocolatey.org/packages/git) ou [git scm.com](http://git-scm.com/downloads). Se for novo tooGit, escolha [git scm.com](http://git-scm.com/downloads) e selecione a opção de Olá demasiado**Git de utilização do Olá linha de comandos do Windows**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="b6a7a-114">Depois de instalar o Git, também terá de nome de utilizador do tooset Olá Git e e-mail conforme for necessário mais tarde no tutorial Olá (quando efetuar uma consolidação a partir do código de VS).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="b6a7a-115">Instalar o ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b6a7a-115">Install ASP.NET Core</span></span>
<span data-ttu-id="b6a7a-116">ASP.NET Core é uma pilha de .NET lean para criação de nuvem moderna e aplicações web que são executados nos X, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="b6a7a-117">Se foram criada de Olá fundo segurança tooprovide uma arquitetura de programação otimizado para aplicações que estão a nuvem toohello implementado ou executado no local.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="b6a7a-118">É composto por componentes modulares com overhead mínimo para manter flexibilidade ao construir as suas soluções.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="b6a7a-119">Este tutorial é concebida tooget começou a criar aplicações com Olá mais recentes desenvolvimento as versões do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="b6a7a-120">Olá seguir instruções é específicas tooWindows.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="b6a7a-121">Para obter instruções de instalação nos X, Linux e Windows, consulte [introdução ao ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="b6a7a-122">Para obter mais instruções de instalação para OS X, Linux e Windows, consulte [instalar o ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="b6a7a-123">Criar aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="b6a7a-123">Create hello web app</span></span>
<span data-ttu-id="b6a7a-124">Esta secção mostra como tooscaffold uma nova aplicação ASP.NET web app através da ferramenta de .NET CLI Olá.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="b6a7a-125">Introduza o seguinte de Olá na Olá linha de comandos toocreate Olá projeto pasta e andaime Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![DotNet CLI - gerador de ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="b6a7a-127">toorestore Olá necessários pacotes NuGet e execute o Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b6a7a-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="b6a7a-128">Executar localmente a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="b6a7a-128">Run hello web app locally</span></span>
<span data-ttu-id="b6a7a-129">Agora que criou a aplicação web de Olá e obter todos os pacotes de NuGet Olá da aplicação Olá, pode executar Olá web aplicação localmente.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="b6a7a-130">Executar a aplicação Olá (Olá `dotnet run` comando irá criar a aplicação Olá quando está desatualizada):</span><span class="sxs-lookup"><span data-stu-id="b6a7a-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="b6a7a-131">Abra um browser e navegue toohello seguinte URL.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="b6a7a-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="b6a7a-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="b6a7a-133">será apresentada a página predefinida de Olá da aplicação web de Olá da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Aplicação local web num browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="b6a7a-135">Feche o browser.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-135">Close your browser.</span></span> <span data-ttu-id="b6a7a-136">No Olá **janela de comando**, prima **Ctrl + C** tooshut baixo aplicação Olá e fechar Olá **janela de comando**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="b6a7a-137">Criar uma aplicação web no Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b6a7a-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="b6a7a-138">Olá passos seguintes irão guiá-lo a criar uma aplicação web no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="b6a7a-139">Inicie sessão no toohello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6a7a-140">Clique em **novo** em Olá parte superior esquerda do Olá Portal.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="b6a7a-141">Clique em **aplicações Web > aplicação Web**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-141">Click **Web Apps > Web App**.</span></span>
   
    ![Nova aplicação de web do Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="b6a7a-143">Introduza um valor para **nome**, tais como **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="b6a7a-144">Tenha em atenção que este nome tem de toobe exclusivo e portal Olá irá impor que quando a tentativa de nome de Olá tooenter.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="b6a7a-145">Por conseguinte, se selecionar uma introduza um valor diferente, terá de toosubstitute valor para cada ocorrência dos **SampleWebAppDemo** que visualiza neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="b6a7a-146">Selecione um existente **plano do App Service** ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="b6a7a-147">Se criar um novo plano, selecione Olá outras opções, localização e escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="b6a7a-148">Para obter mais informações sobre os planos do App Service, consulte o artigo de Olá, [descrição geral dos planos do App Service do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure novo painel de aplicação web](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="b6a7a-150">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-150">Click **Create**.</span></span>
   
    ![Painel aplicação Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="b6a7a-152">Ativar a publicação de Git para a nova aplicação de web Olá</span><span class="sxs-lookup"><span data-stu-id="b6a7a-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="b6a7a-153">Git é um sistema de controlo de versão distribuída que é possível utilizar toodeploy a aplicação web do App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="b6a7a-154">Irá armazenar o código de Olá escrita para a sua aplicação web num repositório de Git local e implementar o código tooAzure ao enviar o repositório remoto tooa.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="b6a7a-155">Iniciar sessão Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6a7a-156">Clique em **Browse** (Procurar).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-156">Click **Browse**.</span></span>
3. <span data-ttu-id="b6a7a-157">Clique em **Web Apps** tooview uma lista de aplicações web de Olá associados à subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="b6a7a-158">Selecione a aplicação de web de Olá que criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="b6a7a-159">No painel de aplicação web de Olá, clique em **definições** > **a implementação contínua**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Anfitrião de aplicação web do Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="b6a7a-161">Clique em **Escolher origem > repositório de Git Local**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="b6a7a-162">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-162">Click **OK**.</span></span>
   
    ![Respository de Git Local do Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="b6a7a-164">Se não anteriormente configurou as credenciais de implementação para publicar uma aplicação web ou outra aplicação de serviço de aplicações, configure-os agora:</span><span class="sxs-lookup"><span data-stu-id="b6a7a-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="b6a7a-165">Clique em **definições** > **as credenciais de implementação**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="b6a7a-166">Olá **definir credenciais de implementação** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="b6a7a-167">Crie um nome de utilizador e uma palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-167">Create a user name and password.</span></span>  <span data-ttu-id="b6a7a-168">Irá precisar desta palavra-passe mais tarde, quando configurar o Git.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="b6a7a-169">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-169">Click **Save**.</span></span>
9. <span data-ttu-id="b6a7a-170">No painel da sua aplicação web, clique em **definições > propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="b6a7a-171">URL de Olá de Olá repositório de Git remoto que vai implementar toois apresentado em **URL do GIT**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="b6a7a-172">Olá cópia **URL do GIT** valor para utilização posterior tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![URL do Git do Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="b6a7a-174">Publicar a sua tooAzure de aplicação web do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="b6a7a-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="b6a7a-175">Nesta secção, irá criar um repositório de Git local e emitir a partir desse toodeploy tooAzure do repositório a tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="b6a7a-176">No VS Code, selecione Olá **Git** opção na barra de navegação esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Ícone de Git no VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="b6a7a-178">Selecione **repositório de git inicializar** toomake se a sua área de trabalho está sob o controlo de origem do git.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Inicializar o Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="b6a7a-180">Abrir Olá janela de comandos e altere o diretório de toohello de diretórios da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="b6a7a-181">Em seguida, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b6a7a-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="b6a7a-182">Este comando impede que um problema sobre texto onde CRLF endings e LF endings estiverem envolvidos.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="b6a7a-183">No VS Code, adicione uma mensagem de consolidação e clique em Olá **todos os consolidação** ícone de verificação.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Consolidação de Git todos](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="b6a7a-185">Depois de Git terminou de processar, verá que existem não existem ficheiros listados na janela do Git Olá na **alterações**.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git sem alterações](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="b6a7a-187">Altere o fundo toohello janela de comando em que linha de comandos Olá pontos toohello diretório onde está localizada a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="b6a7a-188">Crie uma referência remota para enviar atualizações tooyour web app através da utilização de Olá URL do Git (terminar em ".git") que copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="b6a7a-189">Configure o Git toosave as suas credenciais localmente para que estarão disponíveis os comandos de push tooyour anexado automaticamente gerados a partir do código de VS.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="b6a7a-190">Emitir o tooAzure alterações introduzindo Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="b6a7a-191">Após este tooAzure push inicial, será capaz de toodo push de Olá todos os comandos a partir do código de VS.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="b6a7a-192">É-lhe pedido para a palavra-passe de Olá que criou anteriormente no Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="b6a7a-193">**Nota: A palavra-passe não serão visível.**</span><span class="sxs-lookup"><span data-stu-id="b6a7a-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="b6a7a-194">saída de Olá de Olá acima comando termina com uma mensagem que a implementação é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="b6a7a-195">Se efetuar alterações tooyour aplicação, pode voltar a publicar diretamente no VS Code utilizando a funcionalidade de Git incorporada Olá selecionando Olá **consolidar todas as** opção seguido Olá **Push** opção.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="b6a7a-196">Encontrará Olá **Push** opção disponível no Olá menu pendente seguinte toohello **consolidar todas as** e **atualizar** botões.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="b6a7a-197">Se precisar de toocollaborate num projeto, deve considerar a enviar tooGitHub entre enviar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="b6a7a-198">Executar a aplicação Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="b6a7a-198">Run hello app in Azure</span></span>
<span data-ttu-id="b6a7a-199">Agora que implementou a aplicação web, vamos executar a aplicação de Olá enquanto alojado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="b6a7a-200">Pode fazê-lo de duas formas:</span><span class="sxs-lookup"><span data-stu-id="b6a7a-200">This can be done in two ways:</span></span>

* <span data-ttu-id="b6a7a-201">Abra um browser e introduza o nome de Olá da sua aplicação web da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="b6a7a-202">No Olá Portal do Azure, localize o painel de aplicação web Olá para a sua aplicação web e clique em **procurar** tooview a aplicação</span><span class="sxs-lookup"><span data-stu-id="b6a7a-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="b6a7a-203">no seu browser predefinido.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-203">in your default browser.</span></span>

![Aplicação web do Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="b6a7a-205">Resumo</span><span class="sxs-lookup"><span data-stu-id="b6a7a-205">Summary</span></span>
<span data-ttu-id="b6a7a-206">Neste tutorial, aprendeu como toocreate uma aplicação web no VS Code e implementá-la tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b6a7a-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="b6a7a-207">Para mais informações sobre o VS Code, consulte o artigo de Olá, [por que motivo Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="b6a7a-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="b6a7a-208">Para obter informações sobre as web apps do App Service, consulte [descrição geral de aplicações Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a7a-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

