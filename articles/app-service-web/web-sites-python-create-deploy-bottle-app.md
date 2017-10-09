---
title: "aplicações web de aaaPython com Bottle no Azure"
description: "Um tutorial que explica toorunning uma aplicação web do Python nas Web Apps do Azure App Service."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="d1f41-103">Criar web apps com Bottle no Azure</span><span class="sxs-lookup"><span data-stu-id="d1f41-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="d1f41-104">Este tutorial descreve como tooget iniciado a executar o Python nas Web Apps do Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d1f41-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="d1f41-105">As Web Apps fornecem um alojamento gratuito e uma implementação rápida e pode utilizar o Python!</span><span class="sxs-lookup"><span data-stu-id="d1f41-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="d1f41-106">Olá, como a sua aplicação cresce, pode mudar de alojamento toopaid e também pode integrar com todos os outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f41-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="d1f41-107">Irá criar uma aplicação web utilizando a estrutura de web Bottle Olá (ver versões alternativas deste tutorial para [Django](web-sites-python-create-deploy-django-app.md) e [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="d1f41-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="d1f41-108">Irá criar aplicação web de Olá Olá Azure Marketplace, configurar a implementação de Git e clonar o repositório de Olá localmente.</span><span class="sxs-lookup"><span data-stu-id="d1f41-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="d1f41-109">Em seguida, irá executar a aplicação web de Olá localmente, efetuar alterações, consolidar e emiti-las demasiado[Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d1f41-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="d1f41-110">Olá tutorial mostra como toodo esta do Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="d1f41-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d1f41-111">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="d1f41-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d1f41-112">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="d1f41-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d1f41-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d1f41-113">Prerequisites</span></span>
* <span data-ttu-id="d1f41-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="d1f41-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="d1f41-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="d1f41-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="d1f41-116">setuptools, pip, virtualenv (apenas no Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="d1f41-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="d1f41-117">Git</span><span class="sxs-lookup"><span data-stu-id="d1f41-117">Git</span></span>
* <span data-ttu-id="d1f41-118">[Ferramentas do Python 2.2 para Visual Studio][Ferramentas do Python 2.2 para Visual Studio] (PTVS) – Nota: Isto é opcional</span><span class="sxs-lookup"><span data-stu-id="d1f41-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="d1f41-119">**Nota**: de momento, a publicação do TFS não é suportada para projetos Python.</span><span class="sxs-lookup"><span data-stu-id="d1f41-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="d1f41-120">Windows</span><span class="sxs-lookup"><span data-stu-id="d1f41-120">Windows</span></span>
<span data-ttu-id="d1f41-121">Se ainda não tiver o Python 2.7 ou 3.4 instalado (32 bits), recomendamos que instale o [Azure SDK para Python 2.7] ou o [Azure SDK para Python 3.4] utilizando o Instalador de Plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="d1f41-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="d1f41-122">Esta ação instala a versão de 32 bits de Olá do Python, setuptools, pip, virtualenv, etc. (o Python de 32 bits é o que é instalado em máquinas de anfitrião do Azure de Olá).</span><span class="sxs-lookup"><span data-stu-id="d1f41-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="d1f41-123">Em alternativa, pode obter o Python de [python.org].</span><span class="sxs-lookup"><span data-stu-id="d1f41-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="d1f41-124">Para Git, recomendamos o [Git para Windows] ou o [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="d1f41-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="d1f41-125">Se utilizar o Visual Studio, pode utilizar o suporte de Git Olá integrado.</span><span class="sxs-lookup"><span data-stu-id="d1f41-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="d1f41-126">Também recomendamos que instale as [Ferramentas do Python 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d1f41-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="d1f41-127">Isto é opcional, mas se tiver [Visual Studio], incluindo Olá livre Visual Studio Community 2013 ou Visual Studio Express 2013 para a Web, em seguida, isto irá dar-lhe um excelente IDE do Python.</span><span class="sxs-lookup"><span data-stu-id="d1f41-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="d1f41-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="d1f41-128">Mac/Linux</span></span>
<span data-ttu-id="d1f41-129">Já deve ter Python e Git já instalado, mas certifique-se de que tem o Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="d1f41-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="d1f41-130">Criação da aplicação Web no Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d1f41-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="d1f41-131">Olá primeiro passo na criação da sua aplicação é toocreate Olá web app através de Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1f41-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="d1f41-132">Inicie sessão no Portal do Azure de Olá e clique em Olá **novo** botão no canto inferior esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="d1f41-133">Na caixa de pesquisa de Olá, escreva "python".</span><span class="sxs-lookup"><span data-stu-id="d1f41-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="d1f41-134">Nos resultados de pesquisa de Olá, selecione **Bottle**, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="d1f41-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="d1f41-135">Configure Olá nova Bottle aplicação, tais como criar um novo plano de serviço de aplicações e um novo grupo de recursos para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="d1f41-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="d1f41-136">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d1f41-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="d1f41-137">Configurar a publicação de Git para a sua aplicação web recentemente criada ao seguir as instruções de Olá em [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d1f41-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="d1f41-138">Descrição Geral da Aplicação</span><span class="sxs-lookup"><span data-stu-id="d1f41-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="d1f41-139">Conteúdo do repositório de Git</span><span class="sxs-lookup"><span data-stu-id="d1f41-139">Git repository contents</span></span>
<span data-ttu-id="d1f41-140">Eis uma descrição geral dos ficheiros de Olá, encontrará no repositório de Git inicial Olá, que iremos clonar na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="d1f41-141">Origens principais para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-141">Main sources for hello application.</span></span> <span data-ttu-id="d1f41-142">Consiste em 3 páginas (índice, acerca de, contacto) com um esquema do modelo global.</span><span class="sxs-lookup"><span data-stu-id="d1f41-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="d1f41-143">O conteúdo estático e os scripts incluem arranque, jquery, modernizr e responder.</span><span class="sxs-lookup"><span data-stu-id="d1f41-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="d1f41-144">Suporte de servidor de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="d1f41-144">Local development server support.</span></span> <span data-ttu-id="d1f41-145">Utilize esta aplicação de Olá toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="d1f41-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="d1f41-146">Os ficheiros de projeto para utilização com as [Ferramentas do Python para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d1f41-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="d1f41-147">Proxy do IIS para ambientes virtuais e suporte de depuração remota do PTVS.</span><span class="sxs-lookup"><span data-stu-id="d1f41-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="d1f41-148">Pacotes externos necessários para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="d1f41-148">External packages needed by this application.</span></span> <span data-ttu-id="d1f41-149">script de implementação de Olá irá instalar os pacotes de Olá listados neste ficheiro através do pip.</span><span class="sxs-lookup"><span data-stu-id="d1f41-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="d1f41-150">Ficheiros de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="d1f41-150">IIS configuration files.</span></span> <span data-ttu-id="d1f41-151">script de implementação de Olá vai utilizar x.y. config adequado de Olá e copiá-lo como Web. config.</span><span class="sxs-lookup"><span data-stu-id="d1f41-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="d1f41-152">Ficheiros opcionais - personalizar a implementação</span><span class="sxs-lookup"><span data-stu-id="d1f41-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="d1f41-153">Ficheiros opcionais - runtime do Python</span><span class="sxs-lookup"><span data-stu-id="d1f41-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="d1f41-154">Ficheiros adicionais no servidor</span><span class="sxs-lookup"><span data-stu-id="d1f41-154">Additional files on server</span></span>
<span data-ttu-id="d1f41-155">Alguns ficheiros existem no servidor de Olá, mas não foram adicionados toohello repositório de git.</span><span class="sxs-lookup"><span data-stu-id="d1f41-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="d1f41-156">Estes são criados pelo script de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="d1f41-157">Ficheiro de configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="d1f41-157">IIS configuration file.</span></span> <span data-ttu-id="d1f41-158">Criado a partir de web.x.y.config em todas as implementações.</span><span class="sxs-lookup"><span data-stu-id="d1f41-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="d1f41-159">Ambiente virtual do Python.</span><span class="sxs-lookup"><span data-stu-id="d1f41-159">Python virtual environment.</span></span> <span data-ttu-id="d1f41-160">Se um ambiente virtual compatível ainda não existir na aplicação web de Olá, criados durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="d1f41-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="d1f41-161">Os pacotes listados em requirements.txt são instalados pelo pip, mas o pip saltará a instalação se Olá pacotes já estiverem instalados.</span><span class="sxs-lookup"><span data-stu-id="d1f41-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="d1f41-162">Olá 3 secções seguintes descrevem como tooproceed com Olá web desenvolvimento de aplicações em 3 ambientes diferentes:</span><span class="sxs-lookup"><span data-stu-id="d1f41-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="d1f41-163">Windows, com as Ferramentas do Python para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1f41-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="d1f41-164">Windows, com linha de comandos</span><span class="sxs-lookup"><span data-stu-id="d1f41-164">Windows, with command line</span></span>
* <span data-ttu-id="d1f41-165">Mac/Linux, com linha de comandos</span><span class="sxs-lookup"><span data-stu-id="d1f41-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="d1f41-166">Web App desenvolvimento – Windows – ferramentas do Python para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1f41-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="d1f41-167">Repositório de Olá clone</span><span class="sxs-lookup"><span data-stu-id="d1f41-167">Clone hello repository</span></span>
<span data-ttu-id="d1f41-168">Em primeiro lugar, clone o repositório de Olá utilizando o url de Olá fornecido no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f41-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="d1f41-169">Para obter mais informações, consulte [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d1f41-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="d1f41-170">Abra o ficheiro de solução de Olá (. sln) que está incluído na raiz de Olá do repositório de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="d1f41-171">Criar ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="d1f41-171">Create virtual environment</span></span>
<span data-ttu-id="d1f41-172">Agora, vamos criar um ambiente virtual para o desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="d1f41-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="d1f41-173">Clique com o botão direito do rato em **Ambientes do Python** e selecione **Adicionar Ambiente Virtual...**.</span><span class="sxs-lookup"><span data-stu-id="d1f41-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="d1f41-174">Certifique-se de nome de Olá do ambiente de Olá `env`.</span><span class="sxs-lookup"><span data-stu-id="d1f41-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="d1f41-175">Selecione o interpretador base Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-175">Select hello base interpreter.</span></span> <span data-ttu-id="d1f41-176">Certifique-se toouse Olá a mesma versão do Python selecionada para a sua aplicação web (no runtime.txt ou Olá **definições da aplicação** painel da sua aplicação web no Portal do Azure de Olá).</span><span class="sxs-lookup"><span data-stu-id="d1f41-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="d1f41-177">Certifique-se de pacotes de toodownload e a instalação da opção Olá está marcada.</span><span class="sxs-lookup"><span data-stu-id="d1f41-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="d1f41-178">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d1f41-178">Click **Create**.</span></span> <span data-ttu-id="d1f41-179">Isto irá criar ambiente virtual Olá e instalar dependências listadas no requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="d1f41-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="d1f41-180">Executar com o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d1f41-180">Run using development server</span></span>
<span data-ttu-id="d1f41-181">Prima F5 toostart depuração e o seu browser abrirá automaticamente página toohello executar localmente.</span><span class="sxs-lookup"><span data-stu-id="d1f41-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="d1f41-182">Pode definir pontos de interrupção nas origens Olá, utilize Olá janelas, etc. Consulte Olá [ferramentas do Python para Visual Studio documentação] para obter mais informações sobre Olá várias funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="d1f41-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="d1f41-183">Efetuar alterações</span><span class="sxs-lookup"><span data-stu-id="d1f41-183">Make changes</span></span>
<span data-ttu-id="d1f41-184">Agora, pode experimentar efetuando alterações toohello aplicação origens e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="d1f41-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="d1f41-185">Depois de ter testado as suas alterações, confirmá-las toohello repositório de Git:</span><span class="sxs-lookup"><span data-stu-id="d1f41-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="d1f41-186">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="d1f41-186">Install more packages</span></span>
<span data-ttu-id="d1f41-187">A aplicação pode ter dependências que ultrapassam o Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="d1f41-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d1f41-188">É possível instalar pacotes adicionais através do pip.</span><span class="sxs-lookup"><span data-stu-id="d1f41-188">You can install additional packages using pip.</span></span> <span data-ttu-id="d1f41-189">tooinstall um pacote, clique com botão direito no ambiente virtual Olá e selecione **Instalar pacote do Python**.</span><span class="sxs-lookup"><span data-stu-id="d1f41-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="d1f41-190">Por exemplo, tooinstall Olá Azure SDK para Python, que permite-lhe aceder tooAzure armazenamento, o service bus e outros serviços do Azure, introduza `azure`:</span><span class="sxs-lookup"><span data-stu-id="d1f41-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="d1f41-191">Clique com o botão direito no ambiente virtual Olá e selecione **gerar requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="d1f41-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="d1f41-192">Em seguida, confirme o repositório de Git do Olá alterações toorequirements.txt toohello.</span><span class="sxs-lookup"><span data-stu-id="d1f41-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="d1f41-193">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="d1f41-193">Deploy tooAzure</span></span>
<span data-ttu-id="d1f41-194">tootrigger uma implementação, clique em **sincronização** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="d1f41-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="d1f41-195">A sincronização envia e recebe.</span><span class="sxs-lookup"><span data-stu-id="d1f41-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="d1f41-196">primeira implementação de Olá irá demorar algum tempo, irá criar um ambiente virtual, instalar pacotes, etc.</span><span class="sxs-lookup"><span data-stu-id="d1f41-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="d1f41-197">Visual Studio não mostra o progresso de Olá da implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1f41-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="d1f41-198">Se gostaria de saída de Olá tooreview, consulte a secção de Olá no [resolução de problemas - implementação](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="d1f41-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="d1f41-199">Procure toohello Azure URL tooview as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="d1f41-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="d1f41-200">A linha de comandos - Windows - desenvolvimento da aplicação Web</span><span class="sxs-lookup"><span data-stu-id="d1f41-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="d1f41-201">Repositório de Olá clone</span><span class="sxs-lookup"><span data-stu-id="d1f41-201">Clone hello repository</span></span>
<span data-ttu-id="d1f41-202">Em primeiro lugar, clone repositório de Olá utilizando o URL de Olá fornecido no Portal do Azure de Olá e adicione Olá repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="d1f41-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="d1f41-203">Para obter mais informações, consulte [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d1f41-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="d1f41-204">Criar ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="d1f41-204">Create virtual environment</span></span>
<span data-ttu-id="d1f41-205">Vamos criar um novo ambiente virtual para fins de desenvolvimento (não o adicione toohello repositório).</span><span class="sxs-lookup"><span data-stu-id="d1f41-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="d1f41-206">Ambientes virtuais no Python não são relocalizáveis, pelo que cada programador que trabalha na aplicação Olá irá criar os seus próprios localmente.</span><span class="sxs-lookup"><span data-stu-id="d1f41-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="d1f41-207">Certifique-se toouse Olá a mesma versão do Python selecionada para a sua aplicação web (no runtime.txt ou Olá painel Definições da aplicação para a sua aplicação web no Olá Portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="d1f41-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="d1f41-208">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="d1f41-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="d1f41-209">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="d1f41-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="d1f41-210">Instale quaisquer pacotes externos exigidos pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d1f41-210">Install any external packages required by your application.</span></span> <span data-ttu-id="d1f41-211">Pode utilizar o ficheiro requirements.txt de Olá na raiz de Olá de pacotes de Olá Olá repositório tooinstall num ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="d1f41-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="d1f41-212">Executar com o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d1f41-212">Run using development server</span></span>
<span data-ttu-id="d1f41-213">Pode iniciar a aplicação Olá num servidor de desenvolvimento com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d1f41-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="d1f41-214">consola de Olá irá apresentar URL Olá e porta Olá server escuta a para:</span><span class="sxs-lookup"><span data-stu-id="d1f41-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="d1f41-215">Em seguida, abra o seu URL de toothat do web browser.</span><span class="sxs-lookup"><span data-stu-id="d1f41-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="d1f41-216">Efetuar alterações</span><span class="sxs-lookup"><span data-stu-id="d1f41-216">Make changes</span></span>
<span data-ttu-id="d1f41-217">Agora, pode experimentar efetuando alterações toohello aplicação origens e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="d1f41-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="d1f41-218">Depois de ter testado as suas alterações, confirmá-las toohello repositório de Git:</span><span class="sxs-lookup"><span data-stu-id="d1f41-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="d1f41-219">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="d1f41-219">Install more packages</span></span>
<span data-ttu-id="d1f41-220">A aplicação pode ter dependências que ultrapassam o Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="d1f41-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d1f41-221">É possível instalar pacotes adicionais através do pip.</span><span class="sxs-lookup"><span data-stu-id="d1f41-221">You can install additional packages using pip.</span></span> <span data-ttu-id="d1f41-222">Por exemplo, tooinstall Olá Azure SDK para Python, que dá-lhe aceder tooAzure armazenamento, o service bus e outros serviços do Azure, o tipo:</span><span class="sxs-lookup"><span data-stu-id="d1f41-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="d1f41-223">Certifique-se de que tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="d1f41-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="d1f41-224">Consolide alterações de Olá:</span><span class="sxs-lookup"><span data-stu-id="d1f41-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="d1f41-225">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="d1f41-225">Deploy tooAzure</span></span>
<span data-ttu-id="d1f41-226">tootrigger uma implementação, Olá push altera tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d1f41-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="d1f41-227">Irá ver o resultado de Olá do script de implementação de Olá, incluindo a criação do ambiente virtual, instalação de pacotes e criação de Web. config.</span><span class="sxs-lookup"><span data-stu-id="d1f41-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="d1f41-228">Procure toohello Azure URL tooview as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="d1f41-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="d1f41-229">Implementação da aplicação Web – Mac/Linux – linha de comandos</span><span class="sxs-lookup"><span data-stu-id="d1f41-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="d1f41-230">Repositório de Olá clone</span><span class="sxs-lookup"><span data-stu-id="d1f41-230">Clone hello repository</span></span>
<span data-ttu-id="d1f41-231">Em primeiro lugar, clone repositório de Olá utilizando o URL de Olá fornecido no Portal do Azure de Olá e adicione Olá repositório do Azure como um remoto.</span><span class="sxs-lookup"><span data-stu-id="d1f41-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="d1f41-232">Para obter mais informações, consulte [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d1f41-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="d1f41-233">Criar ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="d1f41-233">Create virtual environment</span></span>
<span data-ttu-id="d1f41-234">Vamos criar um novo ambiente virtual para fins de desenvolvimento (não o adicione toohello repositório).</span><span class="sxs-lookup"><span data-stu-id="d1f41-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="d1f41-235">Ambientes virtuais no Python não são relocalizáveis, pelo que cada programador que trabalha na aplicação Olá irá criar os seus próprios localmente.</span><span class="sxs-lookup"><span data-stu-id="d1f41-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="d1f41-236">Certifique-se toouse Olá a mesma versão do Python selecionada para a sua aplicação web (no runtime.txt ou Olá painel de definições da aplicação da sua aplicação web no Portal do Azure de Olá).</span><span class="sxs-lookup"><span data-stu-id="d1f41-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="d1f41-237">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="d1f41-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="d1f41-238">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="d1f41-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="d1f41-239">ou pyvenv env</span><span class="sxs-lookup"><span data-stu-id="d1f41-239">or pyvenv env</span></span>

<span data-ttu-id="d1f41-240">Instale quaisquer pacotes externos exigidos pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d1f41-240">Install any external packages required by your application.</span></span> <span data-ttu-id="d1f41-241">Pode utilizar o ficheiro requirements.txt de Olá na raiz de Olá de pacotes de Olá Olá repositório tooinstall num ambiente virtual:</span><span class="sxs-lookup"><span data-stu-id="d1f41-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="d1f41-242">Executar com o servidor de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d1f41-242">Run using development server</span></span>
<span data-ttu-id="d1f41-243">Pode iniciar a aplicação Olá num servidor de desenvolvimento com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d1f41-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="d1f41-244">consola de Olá irá apresentar URL Olá e porta Olá server escuta a para:</span><span class="sxs-lookup"><span data-stu-id="d1f41-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="d1f41-245">Em seguida, abra o seu URL de toothat do web browser.</span><span class="sxs-lookup"><span data-stu-id="d1f41-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="d1f41-246">Efetuar alterações</span><span class="sxs-lookup"><span data-stu-id="d1f41-246">Make changes</span></span>
<span data-ttu-id="d1f41-247">Agora, pode experimentar efetuando alterações toohello aplicação origens e/ou modelos.</span><span class="sxs-lookup"><span data-stu-id="d1f41-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="d1f41-248">Depois de ter testado as suas alterações, confirmá-las toohello repositório de Git:</span><span class="sxs-lookup"><span data-stu-id="d1f41-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="d1f41-249">Instalar mais pacotes</span><span class="sxs-lookup"><span data-stu-id="d1f41-249">Install more packages</span></span>
<span data-ttu-id="d1f41-250">A aplicação pode ter dependências que ultrapassam o Python e Bottle.</span><span class="sxs-lookup"><span data-stu-id="d1f41-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d1f41-251">É possível instalar pacotes adicionais através do pip.</span><span class="sxs-lookup"><span data-stu-id="d1f41-251">You can install additional packages using pip.</span></span> <span data-ttu-id="d1f41-252">Por exemplo, tooinstall Olá Azure SDK para Python, que dá-lhe aceder tooAzure armazenamento, o service bus e outros serviços do Azure, o tipo:</span><span class="sxs-lookup"><span data-stu-id="d1f41-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="d1f41-253">Certifique-se de que tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="d1f41-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="d1f41-254">Consolide alterações de Olá:</span><span class="sxs-lookup"><span data-stu-id="d1f41-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="d1f41-255">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="d1f41-255">Deploy tooAzure</span></span>
<span data-ttu-id="d1f41-256">tootrigger uma implementação, Olá push altera tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d1f41-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="d1f41-257">Irá ver o resultado de Olá do script de implementação de Olá, incluindo a criação do ambiente virtual, instalação de pacotes e criação de Web. config.</span><span class="sxs-lookup"><span data-stu-id="d1f41-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="d1f41-258">Procure toohello Azure URL tooview as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="d1f41-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="d1f41-259">Resolução de problemas - Instalação do Pacote</span><span class="sxs-lookup"><span data-stu-id="d1f41-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="d1f41-260">Resolução de problemas - Ambiente Virtual</span><span class="sxs-lookup"><span data-stu-id="d1f41-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="d1f41-261">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="d1f41-261">Next Steps</span></span>
<span data-ttu-id="d1f41-262">Siga estes toolearn ligações mais informações sobre Bottle e das ferramentas do Python para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d1f41-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="d1f41-263">[Documentação de Bottle]</span><span class="sxs-lookup"><span data-stu-id="d1f41-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="d1f41-264">[ferramentas do Python para Visual Studio documentação]</span><span class="sxs-lookup"><span data-stu-id="d1f41-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="d1f41-265">Para obter informações sobre como utilizar o Table Storage do Azure e MongoDB:</span><span class="sxs-lookup"><span data-stu-id="d1f41-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="d1f41-266">[Bottle e MongoDB no Azure com ferramentas do Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d1f41-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="d1f41-267">[Bottle e Table Storage do Azure no Azure com ferramentas do Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d1f41-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d1f41-268">O que mudou</span><span class="sxs-lookup"><span data-stu-id="d1f41-268">What's changed</span></span>
* <span data-ttu-id="d1f41-269">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d1f41-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle e MongoDB no Azure com ferramentas do Python para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle e Table Storage do Azure no Azure com ferramentas do Python para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Azure SDK para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Ferramentas do Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas do Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[ferramentas do Python para Visual Studio documentação]: http://aka.ms/ptvsdocs 
[Documentação de Bottle]: http://bottlepy.org/docs/dev/index.html

