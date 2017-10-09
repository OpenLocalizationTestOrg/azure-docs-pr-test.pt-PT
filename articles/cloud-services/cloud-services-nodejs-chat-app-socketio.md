---
title: "aplicação de aaaNode.js utilizando Socket.io | Microsoft Docs"
description: "Saiba como toouse socket.io numa aplicação node.js alojada no Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="694f1-103">Criar uma aplicação de Node.js Chat com Socket.IO num serviço em nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="694f1-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="694f1-104">Socket.IO fornece em tempo real comunicação entre o entre o servidor de node.js e clientes.</span><span class="sxs-lookup"><span data-stu-id="694f1-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="694f1-105">Este tutorial irá guiá-lo através de alojamento um socket. E/s baseado em aplicações de chat no Azure.</span><span class="sxs-lookup"><span data-stu-id="694f1-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="694f1-106">Para obter mais informações sobre Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="694f1-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="694f1-107">Abaixo é uma captura de ecrã da aplicação Olá concluída:</span><span class="sxs-lookup"><span data-stu-id="694f1-107">A screenshot of hello completed application is below:</span></span>

![Uma janela de browser a apresentar serviço Olá alojado no Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="694f1-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="694f1-109">Prerequisites</span></span>
<span data-ttu-id="694f1-110">Certifique-se de que Olá seguintes produtos e versões são instalados toosuccessfully exemplo de Olá concluída neste artigo:</span><span class="sxs-lookup"><span data-stu-id="694f1-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="694f1-111">Instalar o [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="694f1-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="694f1-112">Instalar o [Node. js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="694f1-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="694f1-113">Instalar [Python versão 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="694f1-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="694f1-114">Criar um projeto de serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="694f1-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="694f1-115">Olá passos seguintes criar projeto do serviço de nuvem Olá que irá alojar a aplicação de Socket.IO Olá.</span><span class="sxs-lookup"><span data-stu-id="694f1-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="694f1-116">De Olá **Menu Iniciar** ou **ecrã Iniciar**, procure **do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="694f1-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="694f1-117">Por fim, clique com botão direito **do Windows PowerShell** e selecione **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="694f1-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ícone do PowerShell do Azure][powershell-menu]
2. <span data-ttu-id="694f1-119">Criar um diretório denominado **c:\\nó**.</span><span class="sxs-lookup"><span data-stu-id="694f1-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="694f1-120">Altere os diretórios toohello **c:\\nó** diretório</span><span class="sxs-lookup"><span data-stu-id="694f1-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="694f1-121">Introduza os seguintes comandos toocreate uma nova solução com o nome de Olá **chatapp** e uma função de trabalho com o nome **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="694f1-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="694f1-122">Verá Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="694f1-122">You will see hello following response:</span></span>
   
    ![saída de Olá do novo Olá-azureservice e azurenodeworkerrolecmdlets adicionar](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="694f1-124">Transferir Olá Chat exemplo</span><span class="sxs-lookup"><span data-stu-id="694f1-124">Download hello Chat Example</span></span>
<span data-ttu-id="694f1-125">Para este projeto, utilizamos o exemplo de chat de Olá do Olá [repositório do Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="694f1-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="694f1-126">Efetuar Olá seguinte o exemplo de Olá toodownload de passos e adicione-o projeto de toohello que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="694f1-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="694f1-127">Criar uma cópia local do repositório de Olá utilizando Olá **Clone** botão.</span><span class="sxs-lookup"><span data-stu-id="694f1-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="694f1-128">Também pode utilizar Olá **ZIP** projeto do botão toodownload Olá.</span><span class="sxs-lookup"><span data-stu-id="694f1-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Uma janela do browser ver https://github.com/LearnBoost/socket.io/tree/master/examples/chat, com ícone de transferência Olá ZIP realçado][chat-example-view]
2. <span data-ttu-id="694f1-130">Navegue de estrutura de diretórios Olá do repositório local Olá até chegar à Olá **exemplos\\chat** diretório.</span><span class="sxs-lookup"><span data-stu-id="694f1-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="694f1-131">Copie Olá conteúdo neste diretório toothe **c:\\nó\\chatapp\\WorkerRole1** diretório que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="694f1-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Explorador, apresentando conteúdo Olá exemplos Olá\\diretório de chat extraído de arquivo de Olá][chat-contents]
   
   <span data-ttu-id="694f1-133">Olá itens realçados na captura de ecrã Olá acima são ficheiros Olá copiados Olá **exemplos\\chat** diretório</span><span class="sxs-lookup"><span data-stu-id="694f1-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="694f1-134">No Olá **c:\\nó\\chatapp\\WorkerRole1** diretório, eliminar Olá **server.js** de ficheiros e, em seguida, renomeie Olá **app.js**ficheiro demasiado**server.js**.</span><span class="sxs-lookup"><span data-stu-id="694f1-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="694f1-135">Esta ação remove predefinido Olá **server.js** ficheiro criado anteriormente pela Olá **adicionar AzureNodeWorkerRole** cmdlet e substitui-lo com a aplicação Olá de ficheiros de exemplo de chat de Olá.</span><span class="sxs-lookup"><span data-stu-id="694f1-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="694f1-136">Modificar Server.js e instalar os módulos</span><span class="sxs-lookup"><span data-stu-id="694f1-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="694f1-137">Antes de aplicação Olá teste no Olá emulador do Azure, podemos tem de se algumas alterações secundárias.</span><span class="sxs-lookup"><span data-stu-id="694f1-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="694f1-138">Execute Olá ficheiro de server.js toothe passos a seguir:</span><span class="sxs-lookup"><span data-stu-id="694f1-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="694f1-139">Abra Olá **server.js** ficheiro no Visual Studio ou num editor de texto.</span><span class="sxs-lookup"><span data-stu-id="694f1-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="694f1-140">Determinar Olá **dependências de módulo** secção início Olá de server.js e altere a linha de Olá que contém **sio = require('.. //.. lib//socket.IO')** demasiado**sio = require('socket.io')** conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="694f1-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="694f1-141">aplicação de Olá tooensure escuta a porta correta de Olá, abra server.js no bloco de notas ou o seu editor favorito e, em seguida, altere a linha seguinte, substituindo **3000** com **process.env** conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="694f1-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="694f1-142">Depois de guardar as alterações de Olá demasiado**server.js**, utilize Olá os seguintes passos para instalar os módulos necessários e, em seguida, testar a aplicação Olá no emulador do Azure:</span><span class="sxs-lookup"><span data-stu-id="694f1-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="694f1-143">Utilizar **Azure PowerShell**, altere os diretórios toohello **c:\\nó\\chatapp\\WorkerRole1** Olá diretório e utilize a seguinte Olá tooinstall de comando módulos necessários para esta aplicação:</span><span class="sxs-lookup"><span data-stu-id="694f1-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="694f1-144">Esta ação instalará os módulos de Olá indicados no ficheiro de Package. JSON Olá.</span><span class="sxs-lookup"><span data-stu-id="694f1-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="694f1-145">Após a conclusão do comando de Olá, deverá ver a seguinte de toothe semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="694f1-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![comando de instalação de npm Olá resultado Olá][The-output-of-the-npm-install-command]
2. <span data-ttu-id="694f1-147">Uma vez que este exemplo foi originalmente parte de Olá repositório do Socket.IO GitHub e diretamente referenciada biblioteca de Socket.IO Olá pelo caminho relativo, Socket.IO não foi referenciado no ficheiro de Package. JSON Olá, pelo que, deve instalá-lo através da emissão Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="694f1-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="694f1-148">Testar e implementar</span><span class="sxs-lookup"><span data-stu-id="694f1-148">Test and Deploy</span></span>
1. <span data-ttu-id="694f1-149">Inicie o emulador de Olá emitindo Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="694f1-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="694f1-150">Se ocorrerem problemas com iniciar emulador, ex.: início AzureEmulator: Ocorreu uma falha inesperada.</span><span class="sxs-lookup"><span data-stu-id="694f1-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="694f1-151">Detalhes: Foi encontrado um objeto de comunicação de Olá um erro inesperado, System.ServiceModel.Channels.ServiceChannel, não pode ser utilizado para comunicação porque está a ser Olá estado falhado.</span><span class="sxs-lookup"><span data-stu-id="694f1-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="694f1-152">reinstalar AzureAuthoringTools v 2.7.1 e AzureComputeEmulator v 2.7 - Certifique-se de que a versão corresponde.</span><span class="sxs-lookup"><span data-stu-id="694f1-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="694f1-153">Abra um browser e navegue demasiado**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="694f1-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="694f1-154">Quando abre a janela do browser Olá, introduza uma alcunha e, em seguida, clique em enter.</span><span class="sxs-lookup"><span data-stu-id="694f1-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="694f1-155">Isto irá permitir mensagens toopost como uma alcunha específica.</span><span class="sxs-lookup"><span data-stu-id="694f1-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="694f1-156">funcionalidade de multiutilizador tootest, abra janelas do browser adicionais utilizando o mesmo URL e introduza nicknames diferentes.</span><span class="sxs-lookup"><span data-stu-id="694f1-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Duas janelas do browser que apresenta as mensagens de chat de Utilizador1 e o Utilizador2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="694f1-158">Após a aplicação de Olá teste, pare o emulador de Olá ao emitir o comando seguinte:</span><span class="sxs-lookup"><span data-stu-id="694f1-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="694f1-159">tooAzure de aplicação de Olá toodeploy, utilize o **Publish-AzureServiceProject** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="694f1-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="694f1-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="694f1-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="694f1-161">Ser toouse se um nome exclusivo, caso contrário Olá publicar processo irá falhar.</span><span class="sxs-lookup"><span data-stu-id="694f1-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="694f1-162">Depois de concluída a implementação de Olá, browser Olá irá abrir e navegue serviço toohello implementado.</span><span class="sxs-lookup"><span data-stu-id="694f1-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="694f1-163">Se receber um erro a indicar que Olá fornecido o nome da subscrição não existe na Olá importado o perfil de publicação, tem de transferir e importar o perfil de publicação Olá para a sua subscrição antes de implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="694f1-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="694f1-164">Consulte Olá **implementar Olá aplicação tooAzure** secção [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="694f1-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Uma janela de browser a apresentar serviço Olá alojado no Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="694f1-166">Se receber um erro a indicar que Olá fornecido o nome da subscrição não existe na Olá importado o perfil de publicação, tem de transferir e importar o perfil de publicação Olá para a sua subscrição antes de implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="694f1-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="694f1-167">Consulte Olá **implementar Olá aplicação tooAzure** secção [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="694f1-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="694f1-168">A aplicação está agora em execução no Azure e pode reencaminhar mensagens de chat entre diferentes clientes com o Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="694f1-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="694f1-169">Para uma simplicidade este exemplo está limitado toochatting entre toohello ligado utilizadores mesma instância.</span><span class="sxs-lookup"><span data-stu-id="694f1-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="694f1-170">Isto significa que se o serviço em nuvem Olá cria duas instâncias de função de trabalho, os utilizadores só conseguirão toochat com outros utilizadores ligados toohello mesma instância de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="694f1-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="694f1-171">tooscale Olá toowork de aplicação com várias instâncias de função, pode utilizar uma tecnologia, como o estado de arquivo do Service Bus tooshare Olá Socket.IO em instâncias.</span><span class="sxs-lookup"><span data-stu-id="694f1-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="694f1-172">Para obter exemplos, consulte exemplos de utilização de tópicos e filas do Service Bus Olá no Olá [Azure SDK para o repositório do Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="694f1-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="694f1-173">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="694f1-173">Next steps</span></span>
<span data-ttu-id="694f1-174">Neste tutorial, aprendeu como toocreate uma aplicação de chat básico alojada num serviço em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="694f1-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="694f1-175">toolearn como toohost esta aplicação num Web site do Azure, consulte o artigo [compilar uma aplicação de Chat Node.js com Socket.IO no Web Site um Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="694f1-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="694f1-176">Para obter mais informações, consulte também Olá [Centro para programadores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="694f1-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repositório do Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


