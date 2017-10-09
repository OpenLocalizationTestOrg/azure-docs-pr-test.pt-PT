---
title: "aaaWeb aplicação rápidas (Node.js) | Microsoft Docs"
description: "Um tutorial que baseia-se no tutorial de serviço de nuvem Olá e demonstra como toouse Olá módulo rápida."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="cf0ce-103">Criar uma aplicação de web do Node.js utilizando rápida num serviço em nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="cf0ce-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="cf0ce-104">NODE.js inclui um conjunto mínimo de funcionalidades no tempo de execução do Olá core.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="cf0ce-105">Os programadores utilizam frequentemente 3rd terceiros módulos tooprovide funcionalidades adicionais quando desenvolver uma aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="cf0ce-106">Este tutorial irá criar uma nova aplicação com Olá [Express] [ Express] módulo, que fornece uma arquitetura MVC para criar aplicações web do Node.js.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="cf0ce-107">Abaixo é uma captura de ecrã da aplicação Olá concluída:</span><span class="sxs-lookup"><span data-stu-id="cf0ce-107">A screenshot of hello completed application is below:</span></span>

![Um browser a apresentar tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="cf0ce-109">Criar um projeto de serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="cf0ce-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="cf0ce-110">Execute o seguinte Olá passos toocreate um novo projeto de serviço de nuvem com o nome 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="cf0ce-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="cf0ce-111">De Olá **Menu Iniciar** ou **ecrã Iniciar**, procure **do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="cf0ce-112">Por fim, clique com botão direito **do Windows PowerShell** e selecione **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ícone do PowerShell do Azure](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="cf0ce-114">Altere os diretórios toohello **c:\\nó** diretório e, em seguida, introduza os seguintes comandos toocreate uma nova solução com o nome de Olá **expressapp** e uma função da web com o nome **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="cf0ce-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="cf0ce-115">Por predefinição, **Add-AzureNodeWebRole** utiliza uma versão antiga do Node.js.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="cf0ce-116">Olá **conjunto AzureServiceProjectRole** acima da declaração dá instruções ao Azure toouse v0.10.21 do nó.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="cf0ce-117">Tenha em atenção de que os parâmetros de Olá diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="cf0ce-118">Pode verificar a versão correta do Olá do Node.js tiver sido selecionada, verificando Olá **motores** propriedade no **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="cf0ce-119">Instalação rápida</span><span class="sxs-lookup"><span data-stu-id="cf0ce-119">Install Express</span></span>
1. <span data-ttu-id="cf0ce-120">Instale o gerador do Express Olá emitindo Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="cf0ce-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="cf0ce-121">saída de Olá do comando de npm Olá deverá ter um aspeto semelhante resultado toohello abaixo.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Saída de apresentação Olá do Windows PowerShell de npm Olá instalar comando rápido.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="cf0ce-123">Altere os diretórios toohello **WebRole1** diretório e utilize Olá comando rápida toogenerate uma nova aplicação:</span><span class="sxs-lookup"><span data-stu-id="cf0ce-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="cf0ce-124">Poderá é pedido toooverwrite a aplicação anterior.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="cf0ce-125">Introduza **y** ou **Sim** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="cf0ce-126">Express irá gerar ficheiro de app.js Olá e uma estrutura de pasta para criar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![saída de Olá do comando rápida Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="cf0ce-128">tooinstall dependências adicionais definidas no ficheiro de Package. JSON Olá, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="cf0ce-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando de instalação de npm Olá resultado Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="cf0ce-130">Seguinte de Olá utilize comando toocopy Olá **bin/www** ficheiro demasiado**server.js**.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="cf0ce-131">Isto é para que o serviço em nuvem Olá possa encontrar o ponto de entrada Olá para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="cf0ce-132">Depois de concluída este comando, deve ter um **server.js** ficheiro no diretório de Olá WebRole1.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="cf0ce-133">Modificar Olá **server.js** tooremove um Olá '.' carateres de Olá seguinte linha.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="cf0ce-134">Depois de efetuar esta alteração, linha Olá deverá aparecer da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="cf0ce-135">Esta alteração é necessária uma vez que foi movida ficheiro Olá (anteriormente **bin/www**,) toohello mesmo diretório do ficheiro da aplicação Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="cf0ce-136">Depois de efetuar esta alteração, guarde Olá **server.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="cf0ce-137">Utilize Olá seguintes aplicações de Olá toorun comando no Olá emulador do Azure:</span><span class="sxs-lookup"><span data-stu-id="cf0ce-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Uma página web que contém tooexpress boas-vindas.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="cf0ce-139">Modificar Olá vista</span><span class="sxs-lookup"><span data-stu-id="cf0ce-139">Modifying hello View</span></span>
<span data-ttu-id="cf0ce-140">Modificar agora a mensagem de saudação do Olá vista toodisplay "Boas-vindas tooExpress no Azure".</span><span class="sxs-lookup"><span data-stu-id="cf0ce-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="cf0ce-141">Introduza Olá seguintes comandos tooopen Olá Index. jade ficheiro:</span><span class="sxs-lookup"><span data-stu-id="cf0ce-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Olá conteúdo de Olá Index. jade ficheiro.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="cf0ce-143">Jade é o motor de vista Olá predefinido utilizado por aplicações rápida.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="cf0ce-144">Para obter mais informações sobre o motor de vista Jade Olá, consulte [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="cf0ce-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="cf0ce-145">Modificar a última linha de Olá de texto, acrescentando **no Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![ficheiro de index. jade Olá, a última linha de Olá lê: p de boas-vindas demasiado\#{title} no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="cf0ce-147">Guarde o ficheiro de Olá e sair do bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="cf0ce-148">Atualize o browser e verá as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Uma janela do browser, a página Olá contém tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="cf0ce-150">Após a aplicação de Olá teste, utilize Olá **Stop-AzureEmulator** emulador do cmdlet toostop Olá.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="cf0ce-151">Publicação tooAzure de aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="cf0ce-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="cf0ce-152">Na janela do PowerShell do Azure Olá, utilize Olá **Publish-AzureServiceProject** cmdlet toodeploy Olá aplicação tooa o serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="cf0ce-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="cf0ce-153">Uma vez concluída a operação de implementação de Olá, o seu browser abrir e apresentar a página web de Olá.</span><span class="sxs-lookup"><span data-stu-id="cf0ce-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Um browser apresentar página Olá, Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="cf0ce-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cf0ce-156">Next steps</span></span>
<span data-ttu-id="cf0ce-157">Para obter mais informações, consulte Olá [Centro para programadores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="cf0ce-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


