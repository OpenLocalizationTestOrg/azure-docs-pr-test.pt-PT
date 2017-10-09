---
title: "aaaSpecifying uma versão do Node.js"
description: "Saiba como toospecify Olá versão do Node.js utilizados pelo Azure Web Sites e serviços em nuvem"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="a0104-103">Especificar uma versão do Node.js numa aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="a0104-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="a0104-104">Quando a alojar uma aplicação Node.js, poderá pretender tooensure que a sua aplicação utiliza uma versão específica do Node.js.</span><span class="sxs-lookup"><span data-stu-id="a0104-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="a0104-105">Existem várias formas tooaccomplish isto para aplicações alojadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="a0104-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="a0104-106">Versões de predefinido</span><span class="sxs-lookup"><span data-stu-id="a0104-106">Default versions</span></span>
<span data-ttu-id="a0104-107">versões de Node.js Olá fornecidas pelo Azure são atualizadas constantemente.</span><span class="sxs-lookup"><span data-stu-id="a0104-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="a0104-108">Salvo especificação em contrário, Olá versão predefinida que é especificado no Olá `WEBSITE_NODE_DEFAULT_VERSION` variável de ambiente será utilizada.</span><span class="sxs-lookup"><span data-stu-id="a0104-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="a0104-109">toooverride este valor predefinido, siga os passos de Olá nas seguintes secções deste artigo</span><span class="sxs-lookup"><span data-stu-id="a0104-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="a0104-110">Se estiver a alojar a aplicação num serviço em nuvem do Azure (função web ou de trabalho) e é Olá pela primeira vez que implementou a aplicação Olá, Azure tentará toouse Olá a mesma versão do Node.js que instalou no seu ambiente de desenvolvimento se-la corresponde a uma das versões de predefinição Olá disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="a0104-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="a0104-111">Controlo de versões com Package. JSON</span><span class="sxs-lookup"><span data-stu-id="a0104-111">Versioning with package.json</span></span>
<span data-ttu-id="a0104-112">Pode especificar a versão de Olá do toobe Node.js utilizado ao adicionar Olá seguir tooyour **Package. JSON** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="a0104-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="a0104-113">Onde *versão* é toouse de número de versão específica de Olá.</span><span class="sxs-lookup"><span data-stu-id="a0104-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="a0104-114">Pode especificar as condições mais complexas para versão, tais como:</span><span class="sxs-lookup"><span data-stu-id="a0104-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="a0104-115">Uma vez que 0.6.22 não é uma das versões de Olá disponíveis no ambiente de alojamento de Olá, hello versão mais recente do Olá 0.8 série que está disponível será utilizado em vez disso, - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="a0104-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="a0104-116">Controlo de versões sites com as definições de aplicação</span><span class="sxs-lookup"><span data-stu-id="a0104-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="a0104-117">Se estiver a alojar aplicações Olá num Web site, pode definir a variável de ambiente de Olá **WEBSITE_NODE_DEFAULT_VERSION** versão pretendida do toohello.</span><span class="sxs-lookup"><span data-stu-id="a0104-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="a0104-118">Serviços de Cloud de controlo de versões com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0104-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="a0104-119">Se estiver a alojar aplicações Olá num serviço em nuvem e estiver a implementar aplicações de Olá com o Azure PowerShell, pode substituir versão do Node.js predefinida Olá utilizando Olá **conjunto AzureServiceProjectRole** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0104-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="a0104-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a0104-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="a0104-121">Nota Olá parâmetros Olá acima instrução diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a0104-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="a0104-122">Pode verificar a versão correta do Olá do Node.js tiver sido selecionada, verificando Olá **motores** propriedade da função de **Package. JSON**.</span><span class="sxs-lookup"><span data-stu-id="a0104-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="a0104-123">Também pode utilizar Olá **Get-AzureServiceProjectRoleRuntime** tooretrieve uma lista das versões de Node.js disponíveis para aplicações alojadas como um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a0104-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="a0104-124">Verifique sempre a versão de Olá do Node.js depende do seu projeto estiver nesta lista.</span><span class="sxs-lookup"><span data-stu-id="a0104-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="a0104-125">Utilizar uma versão personalizada com Web sites do Azure</span><span class="sxs-lookup"><span data-stu-id="a0104-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="a0104-126">Enquanto o Azure oferece várias versões de predefinição de Node.js, poderá pretender toouse uma versão que não é fornecida por predefinição.</span><span class="sxs-lookup"><span data-stu-id="a0104-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="a0104-127">Se a aplicação será alojada como um Web site do Azure, pode conseguir isto utilizando Olá **iisnode.yml** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a0104-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="a0104-128">Olá seguintes passos guiá-lo através do processo de Olá de utilizar uma versão personalizada do Node.Js com um Web site do Azure:</span><span class="sxs-lookup"><span data-stu-id="a0104-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="a0104-129">Criar um novo diretório e, em seguida, crie um **server.js** ficheiros dentro do diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="a0104-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="a0104-130">Olá **server.js** ficheiro deve conter a seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a0104-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="a0104-131">Esta ação apresenta a versão do Node.js Olá a ser utilizado quando o utilizador procura site Olá.</span><span class="sxs-lookup"><span data-stu-id="a0104-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="a0104-132">Crie um novo Web site e um nome de Olá nota do site de Olá.</span><span class="sxs-lookup"><span data-stu-id="a0104-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="a0104-133">Por exemplo, o seguinte Olá utiliza Olá [ferramentas da linha de comandos do Azure] toocreate um novo Web site do Azure com o nome **mywebsite**e, em seguida, ative um repositório de Git para o Web site Olá.</span><span class="sxs-lookup"><span data-stu-id="a0104-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="a0104-134">Criar um novo diretório designado **bin** como subordinado de diretório Olá Olá **server.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a0104-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="a0104-135">Transferir a versão específica do Olá do **node.exe** (versão do Windows hello) que pretende toouse com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="a0104-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="a0104-136">Por exemplo, Olá seguintes utiliza **curl** versão toodownload 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="a0104-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="a0104-137">Guardar Olá **node.exe** ficheiro para Olá **bin** pasta criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a0104-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="a0104-138">Criar um **iisnode.yml** ficheiros Olá mesmo diretório como Olá **server.js** de ficheiros e, em seguida, adicionar Olá seguir toohello conteúdo **iisnode.yml** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="a0104-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="a0104-139">Este caminho é onde hello **node.exe** ficheiros dentro do seu projeto estarão localizados assim que tiver publicado a toohello de aplicação Web site do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0104-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="a0104-140">Publica a aplicação.</span><span class="sxs-lookup"><span data-stu-id="a0104-140">Publish your application.</span></span> <span data-ttu-id="a0104-141">Por exemplo, uma vez que criar um novo Web site com o parâmetro de – git Olá anteriormente, hello seguintes comandos irão adicionar Olá aplicação ficheiros toomy repositório de Git local e emiti-las toohello repositório de Web site:</span><span class="sxs-lookup"><span data-stu-id="a0104-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="a0104-142">Depois de tem publicado aplicações Olá, abra o Web site de Olá num browser.</span><span class="sxs-lookup"><span data-stu-id="a0104-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="a0104-143">Deverá ver uma mensagem a indicar "Olá da versão de nó do Azure em execução: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="a0104-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0104-144">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="a0104-144">Next Steps</span></span>
<span data-ttu-id="a0104-145">Agora que compreende como versão de Olá toospecify do Node.js utilizadas pela sua aplicação, saiba como demasiado[funcionam com módulos], [criar e implementar um Site Web do Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [como toouse hello do Azure Ferramentas de linha de comandos para Mac e Linux].</span><span class="sxs-lookup"><span data-stu-id="a0104-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="a0104-146">Para obter mais informações, consulte Olá [Centro para programadores do Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a0104-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[como toouse hello do Azure Ferramentas de linha de comandos para Mac e Linux]:cli-install-nodejs.md
[ferramentas da linha de comandos do Azure]:cli-install-nodejs.md
[funcionam com módulos]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
