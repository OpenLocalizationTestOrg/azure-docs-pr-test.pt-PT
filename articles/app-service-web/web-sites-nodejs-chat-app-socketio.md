---
title: "aaaCreate uma aplicação de chat Node.js com Socket.IO no App Service do Azure"
description: "Um tutorial que demonstra com socket.io numa aplicação web node.js alojada no Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="42098-103">Criar uma aplicação de chat Node.js com o Socket.IO no App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="42098-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="42098-104">Socket.IO fornece em tempo real comunicação entre o servidor de node.js e clientes que utilizam WebSockets.</span><span class="sxs-lookup"><span data-stu-id="42098-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="42098-105">Também suporta transportes de contingência tooother (tais como a consulta muito) que funcionam com os browsers mais antigos.</span><span class="sxs-lookup"><span data-stu-id="42098-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="42098-106">Este tutorial irá guiá-lo através de alojamento uma aplicação de chat Socket.IO com base em como uma aplicação web do Azure e mostrar-lhe como tooscale Olá a aplicação utilizar [a Cache de Redis do Azure].</span><span class="sxs-lookup"><span data-stu-id="42098-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="42098-107">Para obter mais informações sobre Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="42098-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="42098-108">procedimentos de Olá nesta tarefa aplicam-se demasiado[Web Apps do App Service]; para serviços em nuvem, consulte [compilar uma aplicação de Chat Node.js com Socket.IO num serviço em nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="42098-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="42098-109">Transferir o exemplo de chat de Olá</span><span class="sxs-lookup"><span data-stu-id="42098-109">Download hello chat example</span></span>
<span data-ttu-id="42098-110">Para este projeto, utilizamos o exemplo de chat de Olá do Olá [repositório do Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="42098-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="42098-111">Efetuar Olá seguinte o exemplo de Olá toodownload de passos e adicione-o projeto de toohello que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="42098-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="42098-112">Transferir um [ZIP ou GZ arquivados versão] do projeto de Socket.IO Olá (versão 1.3.5 foi utilizado para este documento)</span><span class="sxs-lookup"><span data-stu-id="42098-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="42098-113">Extrair Olá de arquivo e copie Olá **exemplos\\chat** nova localização do diretório tooa.</span><span class="sxs-lookup"><span data-stu-id="42098-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="42098-114">Por exemplo,  **\\nó\\chat**.</span><span class="sxs-lookup"><span data-stu-id="42098-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="42098-115">Modificar app.js e instalar os módulos</span><span class="sxs-lookup"><span data-stu-id="42098-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="42098-116">Mudar o nome Olá **index.js** ficheiro demasiado**app.js**.</span><span class="sxs-lookup"><span data-stu-id="42098-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="42098-117">Isto permite toodetect do Azure que se trata de uma aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="42098-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="42098-118">Abra Olá **app.js** ficheiro num editor de texto.</span><span class="sxs-lookup"><span data-stu-id="42098-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="42098-119">Linha de Olá de alteração que contém `var io = require('../..')(server);` conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="42098-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="42098-120">Abra Olá **Package. JSON** de ficheiros e adicionar um toosocket.io de referência em `dependencies`, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="42098-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="42098-121">Na Olá da linha de comandos, altere toohello  **\\nó\\chat** diretório e utilize npm tooinstall Olá módulos necessários para esta aplicação:</span><span class="sxs-lookup"><span data-stu-id="42098-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="42098-122">Esta ação instalará os módulos de Olá para uma subpasta denominada **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="42098-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="42098-123">Criar uma aplicação Web do Azure</span><span class="sxs-lookup"><span data-stu-id="42098-123">Create an Azure Web App</span></span>
<span data-ttu-id="42098-124">Siga estes passos toocreate uma aplicação web do Azure, ativar a publicação de Git e, em seguida, ativar o suporte de WebSocket para a aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="42098-125">toocomplete neste tutorial, precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="42098-126">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="42098-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="42098-127">Para obter mais detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Avaliação Gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="42098-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="42098-128">Instalar Olá Interface de linha de comandos do Azure (CLI do Azure) e ligar tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="42098-129">Consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="42098-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="42098-130">Se esta for a primeira hora configurar um repositório no Azure, terá das credenciais de início de sessão toocreate.</span><span class="sxs-lookup"><span data-stu-id="42098-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="42098-131">No Olá CLI do Azure, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="42098-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="42098-132">Alterar toohello  **\\node\chat** diretório e seguinte Olá de utilização de comandos toocreate uma nova aplicação web do Azure e um repositório de Git local.</span><span class="sxs-lookup"><span data-stu-id="42098-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="42098-133">Este comando também cria um Git remoto nomeado 'azure'.</span><span class="sxs-lookup"><span data-stu-id="42098-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="42098-134">Tem de substituir 'mysitename' com um nome exclusivo para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="42098-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="42098-135">Consolide Olá existente ficheiros toohello repositório local utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="42098-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="42098-136">Emita o repositório de Web Apps do Azure Olá ficheiros toohello com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="42098-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="42098-137">Quando lhe for pedido, introduza as credenciais do passo 2.</span><span class="sxs-lookup"><span data-stu-id="42098-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="42098-138">Irá receber mensagens de estado conforme os módulos são importados no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="42098-139">Após a conclusão deste processo, Olá aplicação será alojada na sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42098-140">Durante a instalação do módulo, poderá reparar erros que ' Olá projeto importado... não foi encontrado '.</span><span class="sxs-lookup"><span data-stu-id="42098-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="42098-141">Estes podem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="42098-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="42098-142">Socket.IO utiliza WebSockets, que não estão ativados por predefinição no Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="42098-143">tooenable os sockets web, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="42098-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="42098-144">Se lhe for solicitado, introduza o nome de Olá da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42098-145">Olá, será de comando 'do azure site set -w' funcionam apenas com a versão 0.7.4 ou superior do Olá Interface de linha de comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="42098-146">Também pode ativar o suporte de WebSocket utilizando Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42098-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="42098-147">tooenable WebSockets utilizando Olá Portal do Azure, clique em Olá web aplicação a partir do painel de aplicações Web Olá, clique em **todas as definições** > **definições da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="42098-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="42098-148">Em **Web Sockets**, clique em **no**.</span><span class="sxs-lookup"><span data-stu-id="42098-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="42098-149">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="42098-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="42098-150">aplicação de web de Olá tooview no seguinte de Olá do Azure, utilize comando toolaunch o browser e navegue toohello alojado web app:</span><span class="sxs-lookup"><span data-stu-id="42098-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="42098-151">A aplicação está agora em execução no Azure e pode reencaminhar mensagens de chat entre diferentes clientes com o Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="42098-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="42098-152">Aumentar horizontalmente</span><span class="sxs-lookup"><span data-stu-id="42098-152">Scale out</span></span>
<span data-ttu-id="42098-153">Podem ser ampliadas Socket.IO aplicações utilizando um **adaptador** toodistribute eventos entre várias instâncias de aplicações e as mensagens.</span><span class="sxs-lookup"><span data-stu-id="42098-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="42098-154">Enquanto existem vários adaptadores disponíveis, Olá [socket.io redis] adaptador pode ser utilizado facilmente com funcionalidade de Cache de Redis do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="42098-155">Um requisito adicional para aumentar horizontalmente uma solução de Socket.IO é suporte para sessões temporária.</span><span class="sxs-lookup"><span data-stu-id="42098-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="42098-156">Sessões temporária estão ativadas por predefinição para Web Apps do Azure através do encaminhamento de pedidos do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="42098-157">Para obter mais informações, consulte [afinidade de instância de Web Sites no Azure].</span><span class="sxs-lookup"><span data-stu-id="42098-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="42098-158">Criar uma cache de Redis</span><span class="sxs-lookup"><span data-stu-id="42098-158">Create a Redis cache</span></span>
<span data-ttu-id="42098-159">Efetue os passos de Olá em [criar uma cache na Cache de Redis do Azure] toocreate uma nova cache.</span><span class="sxs-lookup"><span data-stu-id="42098-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="42098-160">Guardar Olá **nome de anfitrião** e **chave primária** para a sua cache, como estes serão necessários no Olá próximos passos.</span><span class="sxs-lookup"><span data-stu-id="42098-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="42098-161">Adicionar redis Olá e módulos socket.io redis</span><span class="sxs-lookup"><span data-stu-id="42098-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="42098-162">De uma linha de comandos, altere toohello  **\\nó\\chat** Olá de diretório e utilize os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="42098-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="42098-163">versões de Olá especificadas neste comando são versões Olá utilizadas ao testar este artigo.</span><span class="sxs-lookup"><span data-stu-id="42098-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="42098-164">Modificar Olá **app.js** seguinte do ficheiro tooadd Olá linhas imediatamente após`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="42098-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="42098-165">Substitua **redishostname** e **rediskey** com o nome de anfitrião Olá e a chave para a sua cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="42098-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="42098-166">Este procedimento cria um publicar e subscrever toohello de cliente criada anteriormente a cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="42098-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="42098-167">os clientes de Olá, em seguida, são utilizados com Olá adaptador tooconfigure cache de Redis Socket.IO toouse Olá para passar os eventos e as mensagens entre instâncias da aplicação</span><span class="sxs-lookup"><span data-stu-id="42098-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42098-168">Ao hello **socket.io redis** adaptador pode comunicar diretamente tooRedis, a versão atual do Olá não suporta a autenticação de Olá necessária para a cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="42098-169">Para que a ligação inicial Olá é criada utilizando o Olá **redis** módulo, o cliente de Olá, em seguida, é passada toohello **socket.io redis** adaptador.</span><span class="sxs-lookup"><span data-stu-id="42098-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="42098-170">Enquanto a Cache de Redis do Azure suporta ligações seguras através da porta 6380, módulos de Olá utilizados neste exemplo não suportam ligações seguras a partir de 14/7/2014.</span><span class="sxs-lookup"><span data-stu-id="42098-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="42098-171">Olá acima código utiliza Olá, porta não segura do 6379.</span><span class="sxs-lookup"><span data-stu-id="42098-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="42098-172">Olá guardar modificado **app.js**</span><span class="sxs-lookup"><span data-stu-id="42098-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="42098-173">Consolidar as alterações e volte a implementar</span><span class="sxs-lookup"><span data-stu-id="42098-173">Commit changes and redeploy</span></span>
<span data-ttu-id="42098-174">Na linha de comandos no Olá Olá  **\\nó\\chat** diretório, utilize Olá seguintes alterações de toocommit de comandos e volte a implementar aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="42098-175">Depois das alterações de Olá tem sido feito o Push toohello servidor, pode dimensionar o seu site em múltiplas instâncias utilizando Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="42098-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="42098-176">Onde  **#**  é o número de Olá de toocreate de instâncias.</span><span class="sxs-lookup"><span data-stu-id="42098-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="42098-177">Pode ligar aplicação web de tooyour de vários tooverify browsers ou computadores clientes tooall corretamente são enviadas as mensagens.</span><span class="sxs-lookup"><span data-stu-id="42098-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="42098-178">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="42098-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="42098-179">Limites de ligação</span><span class="sxs-lookup"><span data-stu-id="42098-179">Connection limits</span></span>
<span data-ttu-id="42098-180">As aplicações Web do Azure está disponível em vários SKUs, que determinam o site do Olá recursos tooyour disponíveis.</span><span class="sxs-lookup"><span data-stu-id="42098-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="42098-181">Isto inclui o número de Olá de ligações de WebSocket permitido.</span><span class="sxs-lookup"><span data-stu-id="42098-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="42098-182">Para obter mais informações, consulte Olá [página de preços de aplicações Web].</span><span class="sxs-lookup"><span data-stu-id="42098-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="42098-183">As mensagens não são enviadas utilizando WebSockets</span><span class="sxs-lookup"><span data-stu-id="42098-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="42098-184">Se os browsers cliente mantém reverter toolong consulta em vez de utilizar WebSockets, poderá ser devido a um dos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="42098-185">**Tente limitar Olá transporte toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="42098-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="42098-186">Por ordem para Socket.IO toouse WebSockets como Olá mensagens transporte tanto o servidor de Olá como o cliente tem de suportar WebSockets.</span><span class="sxs-lookup"><span data-stu-id="42098-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="42098-187">Se um ou Olá outro não, Socket.IO negociará transporte outro, tais como a consulta longa.</span><span class="sxs-lookup"><span data-stu-id="42098-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="42098-188">lista de predefinição Olá de transportes utilizado pelo Socket.IO é ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="42098-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="42098-189">Pode forçar-tooonly utilize WebSockets adicionando Olá seguinte código toohello **app.js** ficheiro, após Olá linha contendo `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="42098-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="42098-190">Tenha em atenção que browsers antigos que não suporta WebSockets não será capaz de tooconnect toohello site enquanto Olá acima código está ativo, como restringe apenas tooWebSockets de comunicação.</span><span class="sxs-lookup"><span data-stu-id="42098-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="42098-191">**Utilizar SSL**</span><span class="sxs-lookup"><span data-stu-id="42098-191">**Use SSL**</span></span>
  
    <span data-ttu-id="42098-192">Os WebSockets baseia-se em algum menor utilizados cabeçalhos de HTTP, tais como Olá **atualizar** cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="42098-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="42098-193">Alguns dispositivos de rede intermédio, por exemplo, web proxies, podem remover estes cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="42098-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="42098-194">tooavoid este problema, pode estabelecer ligação de WebSocket Olá através de SSL.</span><span class="sxs-lookup"><span data-stu-id="42098-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="42098-195">Uma forma fácil tooaccomplish é demasiado tooconfigure Socket.IO`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="42098-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="42098-196">Isto dá instruções ao hello comunicação Socket.IO toosecure WebSockets igual Olá originadas HTTP/HTTPS pedido Olá da página web.</span><span class="sxs-lookup"><span data-stu-id="42098-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="42098-197">Se um browser utiliza um HTTPS URL toovisit seu Web site, subsequentes comunicações de WebSocket através de Socket.IO esteja protegidas através de SSL.</span><span class="sxs-lookup"><span data-stu-id="42098-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="42098-198">toomodify tooenable este exemplo nesta configuração, adicionar Olá seguinte código toohello **app.js** ficheiro após Olá linha contendo `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="42098-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="42098-199">**Verifique as definições da Web. config**</span><span class="sxs-lookup"><span data-stu-id="42098-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="42098-200">Aplicações web do Azure que alojam aplicações Node.js utilizam Olá **Web. config** tooroute de ficheiros recebido pedidos de aplicação de Node.js toohello.</span><span class="sxs-lookup"><span data-stu-id="42098-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="42098-201">Para WebSockets toofunction corretamente com aplicações Node.js, Olá **Web. config** tem de conter Olá seguir entrada.</span><span class="sxs-lookup"><span data-stu-id="42098-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="42098-202">Isto desativa o módulo de IIS WebSockets Olá, que inclui a sua própria implementação de WebSockets e entra em conflito com o Node.js módulos de WebSocket específicos, tais como Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="42098-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="42098-203">Se esta linha não está presente ou está definida demasiado`true`, isto pode dever-razão de Olá transporte de WebSocket Olá não está a trabalhar para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="42098-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="42098-204">Normalmente, aplicações Node.js não incluem um **Web. config** de ficheiros, para Web sites do Azure irá gerar automaticamente um para as aplicações Node.js quando estão implementadas.</span><span class="sxs-lookup"><span data-stu-id="42098-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="42098-205">Uma vez que este ficheiro é gerado automaticamente no servidor de Olá, tem de utilizar Olá, FTP ou FTPS URL para o Web site tooview este ficheiro.</span><span class="sxs-lookup"><span data-stu-id="42098-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="42098-206">Pode encontrar Olá FTP e FTPS URLs para o seu site no portal clássico Olá ao selecionar a sua aplicação web e, em seguida, Olá **Dashboard** ligação.</span><span class="sxs-lookup"><span data-stu-id="42098-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="42098-207">Olá URLs são apresentados no Olá **leitura rápida** secção.</span><span class="sxs-lookup"><span data-stu-id="42098-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="42098-208">Olá **Web. config** ficheiro só é gerado por Web sites do Azure, se a aplicação não fornecer um.</span><span class="sxs-lookup"><span data-stu-id="42098-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="42098-209">Se fornecer um **Web. config** ficheiro na raiz de Olá do seu projeto de aplicação, será utilizado pelo Web Apps do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="42098-210">Se a entrada Olá não está presente ou é definir o valor de tooa da `true`, em seguida, deve criar um **Web. config** no Olá raiz da sua aplicação Node.js e especifique um valor de `false`.</span><span class="sxs-lookup"><span data-stu-id="42098-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="42098-211">Para referência, Olá abaixo está um predefinido **Web. config** para uma aplicação que utiliza **app.js** como ponto de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="42098-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="42098-212">Se a sua aplicação utiliza um ponto de entrada diferente de **app.js**, tem de substituir todas as ocorrências de **app.js** com Olá corrigir o ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="42098-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="42098-213">Por exemplo, substituindo **app.js** com **server.js**.</span><span class="sxs-lookup"><span data-stu-id="42098-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="42098-214">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service], onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="42098-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="42098-215">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="42098-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="42098-216">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="42098-216">Next steps</span></span>
<span data-ttu-id="42098-217">Neste tutorial, aprendeu como toocreate uma aplicação de chat alojada numa aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="42098-218">Também pode alojar esta aplicação como um serviço em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="42098-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="42098-219">Para obter os passos sobre como tooaccomplish esta, consulte [compilar uma aplicação de Chat Node.js com Socket.IO num serviço em nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="42098-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="42098-220">Para obter mais informações, consulte também Olá [Centro para programadores do Node.js].</span><span class="sxs-lookup"><span data-stu-id="42098-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="42098-221">O que mudou</span><span class="sxs-lookup"><span data-stu-id="42098-221">What's changed</span></span>
* <span data-ttu-id="42098-222">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes].</span><span class="sxs-lookup"><span data-stu-id="42098-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[a Cache de Redis do Azure]: /documentation/services/redis-cache/
[Web Apps do App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[página de preços de aplicações Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[compilar uma aplicação de Chat Node.js com Socket.IO num serviço em nuvem do Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[App Service do Azure e o respetivo impacto nos serviços do Azure existentes]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro para programadores do Node.js]: /develop/nodejs/
[experimentar o App Service]: https://azure.microsoft.com/try/app-service/
[afinidade de instância de Web Sites no Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[criar uma cache na Cache de Redis do Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[repositório do Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP ou GZ arquivados versão]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
