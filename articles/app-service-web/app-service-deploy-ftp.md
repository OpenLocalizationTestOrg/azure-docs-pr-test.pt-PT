---
title: "aaaDeploy tooAzure a aplicação do serviço de aplicações através de FTP/S | Microsoft Docs"
description: "Saiba como toodeploy sua tooAzure de aplicação do serviço de aplicações através de FTP ou FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="24433-103">Implementar a sua tooAzure de aplicação do serviço de aplicações através de FTP/S</span><span class="sxs-lookup"><span data-stu-id="24433-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="24433-104">Este artigo mostra como toouse FTP ou FTPS toodeploy a aplicação web, o back-end da aplicação móvel ou a aplicação API demasiado[App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="24433-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="24433-105">ponto final FTP/S de Olá para a sua aplicação já está ativo.</span><span class="sxs-lookup"><span data-stu-id="24433-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="24433-106">Nenhuma configuração é a implementação de FTP/S tooenable necessário.</span><span class="sxs-lookup"><span data-stu-id="24433-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24433-107">Iremos estão continuamente a demorar passos tooimprove segurança da plataforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="24433-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="24433-108">Como parte deste esforço em curso uma atualização de aplicações Web é planeada de regiões de Datacenters Central e nordeste da Alemanha.</span><span class="sxs-lookup"><span data-stu-id="24433-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="24433-109">Durante este aplicações Web serão estar a desativar a utilização de Olá do protocolo FTP em texto simples para implementações.</span><span class="sxs-lookup"><span data-stu-id="24433-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="24433-110">Os nossos clientes do recomendação tooour é tooswitch tooFTPS para implementações.</span><span class="sxs-lookup"><span data-stu-id="24433-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="24433-111">Esperamos que não seja serviço interrupção tooyour durante esta atualização que está a ser planeada 9/5.</span><span class="sxs-lookup"><span data-stu-id="24433-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="24433-112">Valorizamo-lo suportar deste esforço.</span><span class="sxs-lookup"><span data-stu-id="24433-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="24433-113">Passo 1: Definir credenciais de implementação</span><span class="sxs-lookup"><span data-stu-id="24433-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="24433-114">servidor FTP de Olá tooaccess para a sua aplicação, primeiro precisa de credenciais de implementação.</span><span class="sxs-lookup"><span data-stu-id="24433-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="24433-115">tooset ou repor as credenciais de implementação, consulte [credenciais de implementação de serviço de aplicações do Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="24433-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="24433-116">Este tutorial demonstra a utilização de Olá de credenciais de nível de utilizador.</span><span class="sxs-lookup"><span data-stu-id="24433-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="24433-117">Passo 2: Obter informações de ligação de FTP</span><span class="sxs-lookup"><span data-stu-id="24433-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="24433-118">No Olá [portal do Azure](https://portal.azure.com), abra a aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="24433-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="24433-119">Selecione **descrição geral** no menu à esquerda Olá, em seguida, tenha em atenção os valores de Olá para **utilizador FTP/implementação**, **nome de anfitrião do FTP**, e **nome de anfitrião FTPS**.</span><span class="sxs-lookup"><span data-stu-id="24433-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informações de ligação de FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="24433-121">Olá **utilizador FTP/implementação** valor de utilizador, tal como apresentado pelo Olá Portal do Azure, incluindo o nome da aplicação Olá no contexto de adequada tooprovide ordem para o servidor de Olá FTP.</span><span class="sxs-lookup"><span data-stu-id="24433-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="24433-122">Pode encontrar Olá mesmas informações quando seleciona **propriedades** no menu à esquerda Olá.</span><span class="sxs-lookup"><span data-stu-id="24433-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="24433-123">Além disso, a palavra-passe de implementação de Olá nunca é apresentado.</span><span class="sxs-lookup"><span data-stu-id="24433-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="24433-124">Se se esquecer da sua palavra-passe de implementação, volte atrás demasiado[passo 1](#step1) e repor a palavra-passe de implementação.</span><span class="sxs-lookup"><span data-stu-id="24433-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="24433-125">Passo 3: Implementar tooAzure de ficheiros</span><span class="sxs-lookup"><span data-stu-id="24433-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="24433-126">A partir do seu cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), utilize informações de ligação de Olá que recolheu tooconnect tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="24433-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="24433-127">Copie os ficheiros e os respetivos toohello de estrutura de diretório respetivos [ **/site/wwwroot** diretório](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou Olá **/site/wwwroot/App_Data/tarefas/** diretório para WebJobs).</span><span class="sxs-lookup"><span data-stu-id="24433-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="24433-128">Aplicação de Olá da aplicação tooyour procurar URL tooverify está a funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="24433-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="24433-129">Ao contrário [implementações baseadas em Git](app-service-deploy-local-git.md), implementação de FTP não suporta Olá seguir automatizações de implementação:</span><span class="sxs-lookup"><span data-stu-id="24433-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="24433-130">restauro de dependência (por exemplo, automatizações NuGet, NPM, PIP e compositor)</span><span class="sxs-lookup"><span data-stu-id="24433-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="24433-131">compilação de binários de .NET</span><span class="sxs-lookup"><span data-stu-id="24433-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="24433-132">a geração da Web. config (aqui está uma [exemplo de Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="24433-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="24433-133">Deve restaurar, criar e gerar estes ficheiros necessários manualmente no seu computador local e implementá-las em conjunto com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="24433-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="24433-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="24433-134">Next steps</span></span>

<span data-ttu-id="24433-135">Para cenários de implementação mais avançados, tente [implementar tooAzure com o Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="24433-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="24433-136">Implementação baseada no Git tooAzure permite controlo de versão, o restauro de pacote, MSBuild e muito mais.</span><span class="sxs-lookup"><span data-stu-id="24433-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="24433-137">Mais Recursos</span><span class="sxs-lookup"><span data-stu-id="24433-137">More Resources</span></span>

* <span data-ttu-id="24433-138">[Criar uma aplicação web do PHP MySQL e implementar a utilizar FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="24433-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="24433-139">Credenciais de implementação do App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="24433-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
