---
title: aaaHow toouse io.js com as Web Apps do Azure App Service
description: "Saiba como toouse uma aplicação web no App Service do Azure com o io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="e2d42-103">Como toouse io.js com as Web Apps do Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e2d42-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="e2d42-104">bifurcação de nó popular Olá [io.js] funcionalidades projeto de Node.js vários tooJoyent de diferenças, incluindo um modelo de governação mais aberto, um ciclo de lançamento mais rápido e uma adoção mais rápida das funcionalidades de JavaScript novas e experimental.</span><span class="sxs-lookup"><span data-stu-id="e2d42-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="e2d42-105">Enquanto [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicações Web tem várias versões de Node.js pré-instalado, também permite para um binário de Node.js fornecidos pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="e2d42-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="e2d42-106">Este artigo aborda os dois métodos para ativar a utilização de Olá de io.js na Web Apps do App Service: Olá a utilização de um script de implementação expandida, que configura automaticamente a versão de io.js disponível mais recente do Azure toouse Olá, bem como carregamento manual de Olá de um binário io.js.</span><span class="sxs-lookup"><span data-stu-id="e2d42-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="e2d42-107">Utilizar um Script de implementação</span><span class="sxs-lookup"><span data-stu-id="e2d42-107">Using a Deployment Script</span></span>
<span data-ttu-id="e2d42-108">Após a implementação de uma aplicação Node.js, Web Apps do App Service executa uma série de comandos pequenos tooensure Olá ambiente está corretamente configurado.</span><span class="sxs-lookup"><span data-stu-id="e2d42-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="e2d42-109">Utilizar um script de implementação, este processo pode ser transferências de Olá tooinclude personalizados e a configuração de io.js.</span><span class="sxs-lookup"><span data-stu-id="e2d42-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="e2d42-110">Olá [io.js Script de implementação](https://github.com/felixrieseberg/iojs-azure) está disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2d42-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="e2d42-111">tooenable io.js na sua aplicação web, basta copiar **.deployment**, **deploy.cmd** e **IISNode.yml** toohello raiz da sua pasta de aplicação e implementar aplicações tooWeb.</span><span class="sxs-lookup"><span data-stu-id="e2d42-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="e2d42-112">primeiro ficheiro Olá, **.deployment**, dá instruções ao Web Apps toorun **deploy.cmd** após a implementação.</span><span class="sxs-lookup"><span data-stu-id="e2d42-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="e2d42-113">Este script é executado todos os passos habitual Olá para uma aplicação Node.js, mas também transfere a versão mais recente do Olá do io.js.</span><span class="sxs-lookup"><span data-stu-id="e2d42-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="e2d42-114">Por fim, **IISNode.yml** configura as aplicações Web toouse Olá apenas transferido io.js binário em vez de um binário Node.js pré-instaladas.</span><span class="sxs-lookup"><span data-stu-id="e2d42-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="e2d42-115">Olá tooupdate utilizada io.js binário, basta Reimplementar a sua aplicação - script Olá irá transferir uma nova versão do io.js que todas as aplicações de Olá única vez é implementada.</span><span class="sxs-lookup"><span data-stu-id="e2d42-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="e2d42-116">Utilizar a instalação Manual</span><span class="sxs-lookup"><span data-stu-id="e2d42-116">Using Manual Installation</span></span>
<span data-ttu-id="e2d42-117">instalação manual do Olá de uma versão personalizada io.js inclui apenas dois passos.</span><span class="sxs-lookup"><span data-stu-id="e2d42-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="e2d42-118">Em primeiro lugar, transferir Olá **win x64** binário diretamente a partir de Olá [io.js distribuição].</span><span class="sxs-lookup"><span data-stu-id="e2d42-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="e2d42-119">Necessários são dois ficheiros - **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="e2d42-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="e2d42-120">Guardar ambos os ficheiros tooa pasta dentro da sua aplicação web, por exemplo em **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="e2d42-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="e2d42-121">tooconfigure Web Apps toouse **iojs.exe** em vez de uma versão de nó pré-instaladas, crie um **IISNode.yml** ficheiro na raiz de Olá da sua aplicação e adicione a seguinte linha de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2d42-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="e2d42-122">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="e2d42-122">Next Steps</span></span>
<span data-ttu-id="e2d42-123">Este artigo aprendeu como toouse io.js com o serviço Web Apps do App, utilizando ambos fornecido scripts de implementação, bem como a instalação manual.</span><span class="sxs-lookup"><span data-stu-id="e2d42-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="e2d42-124">IO.js está em desenvolvimento pesado e atualizados mais frequentemente do que Node.js.</span><span class="sxs-lookup"><span data-stu-id="e2d42-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="e2d42-125">Um número de módulos do Node.js poderão não funcionar com io.js -. consulte [io.js no GitHub] para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e2d42-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e2d42-126">O que mudou</span><span class="sxs-lookup"><span data-stu-id="e2d42-126">What's changed</span></span>
* <span data-ttu-id="e2d42-127">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e2d42-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="e2d42-128">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="e2d42-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e2d42-129">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="e2d42-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distribuição]: https://iojs.org/dist/
[io.js no GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
