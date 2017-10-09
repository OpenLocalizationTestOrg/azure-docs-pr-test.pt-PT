---
title: "aaaNode.js web app através da Olá serviço de tabela do Azure"
description: "Este tutorial informa como toouse Olá tabelas do Azure service toostore dados a partir de uma aplicação Node.js que está alojado nas Web Apps do Azure App Service."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="7f11c-103">Aplicação de web do node.js utilizando Olá serviço de tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="7f11c-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="7f11c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="7f11c-104">Overview</span></span>
<span data-ttu-id="7f11c-105">Este tutorial mostra como serviço de tabela toouse forneceu dados de toostore e acesso de gestão de dados do Azure de um [nó] aplicação alojada em [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7f11c-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="7f11c-106">Este tutorial parte do princípio de que tem alguma experiência anterior com o nó e [Git].</span><span class="sxs-lookup"><span data-stu-id="7f11c-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="7f11c-107">Aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7f11c-107">You will learn:</span></span>

* <span data-ttu-id="7f11c-108">Como toouse npm (Gestor de pacotes do nó) tooinstall Olá módulos de nó</span><span class="sxs-lookup"><span data-stu-id="7f11c-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="7f11c-109">Como toowork com Olá serviço tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="7f11c-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="7f11c-110">Como toouse Olá toocreate CLI do Azure numa aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7f11c-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="7f11c-111">Ao seguir este tutorial, irá criar uma simples baseada na web aplicação de "lista de tarefas", que permite criar, obter e concluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="7f11c-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="7f11c-112">tarefas de Olá são armazenadas no Olá serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="7f11c-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="7f11c-113">Segue-se a aplicação Olá concluída:</span><span class="sxs-lookup"><span data-stu-id="7f11c-113">Here is hello completed application:</span></span>

![Uma página web que apresenta um tasklist vazio][node-table-finished]

> [!NOTE]
> <span data-ttu-id="7f11c-115">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="7f11c-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7f11c-116">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="7f11c-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7f11c-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f11c-117">Prerequisites</span></span>
<span data-ttu-id="7f11c-118">Antes de seguir as instruções de Olá neste artigo, certifique-se de que tem o seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="7f11c-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="7f11c-119">[nó] versão 0.10.24 ou superior</span><span class="sxs-lookup"><span data-stu-id="7f11c-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="7f11c-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="7f11c-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="7f11c-121">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7f11c-121">Create a storage account</span></span>
<span data-ttu-id="7f11c-122">Crie uma conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-122">Create an Azure storage account.</span></span> <span data-ttu-id="7f11c-123">aplicação Olá irá utilizar itens de tarefas nesta conta toostore Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="7f11c-124">Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7f11c-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7f11c-125">Clique em Olá **novo** ícone na parte inferior de Olá esquerda do portal de Olá, em seguida, clique em **dados + armazenamento** > **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="7f11c-126">Dê um nome exclusivo de conta de armazenamento Olá e crie um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="7f11c-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Botão novo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="7f11c-128">Quando tiver sido criada a conta de armazenamento Olá, Olá **notificações** botão será flash um verde **êxito** e painel de conta de armazenamento a Olá está aberta tooshow que pertence toohello novo recurso do grupo criar.</span><span class="sxs-lookup"><span data-stu-id="7f11c-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="7f11c-129">No painel de conta de armazenamento a Olá, clique em **definições** > **chaves**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="7f11c-130">Área de transferência da chave toohello de acesso primária do Olá de cópia.</span><span class="sxs-lookup"><span data-stu-id="7f11c-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Chave de acesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="7f11c-132">Instalar módulos e gerar andaime</span><span class="sxs-lookup"><span data-stu-id="7f11c-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="7f11c-133">Nesta secção irá criar uma nova aplicação de nó e utilizar pacotes de módulo de tooadd npm.</span><span class="sxs-lookup"><span data-stu-id="7f11c-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="7f11c-134">Para esta aplicação utilizará Olá [Express] e [Azure] módulos.</span><span class="sxs-lookup"><span data-stu-id="7f11c-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="7f11c-135">módulo de Express de Olá fornece uma arquitetura de controlador de vista de modelo para o nó, ao hello módulos do Azure fornece o serviço de tabela de toohello de conectividade.</span><span class="sxs-lookup"><span data-stu-id="7f11c-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="7f11c-136">Instalação rápida e gerar andaime</span><span class="sxs-lookup"><span data-stu-id="7f11c-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="7f11c-137">A partir da linha de comandos Olá, criar um novo diretório designado **tasklist** e comutador toothat diretório.</span><span class="sxs-lookup"><span data-stu-id="7f11c-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="7f11c-138">Introduza Olá seguir o módulo do comando tooinstall Olá rápida.</span><span class="sxs-lookup"><span data-stu-id="7f11c-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="7f11c-139">Consoante o sistema de operativo Olá, poderá ser necessário tooput 'sudo' antes de comando de Olá:</span><span class="sxs-lookup"><span data-stu-id="7f11c-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="7f11c-140">saída de Olá aparece toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7f11c-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="7f11c-141">Olá "-g' parâmetro instala o módulo Olá global.</span><span class="sxs-lookup"><span data-stu-id="7f11c-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="7f11c-142">Dessa forma, podemos utilizar **rápida** toogenerate andaime de aplicação web sem ter tootype nas informações de caminho adicionais.</span><span class="sxs-lookup"><span data-stu-id="7f11c-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="7f11c-143">andaime de Olá toocreate para aplicação Olá, introduza Olá **rápida** comando:</span><span class="sxs-lookup"><span data-stu-id="7f11c-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="7f11c-144">é apresentado toohello semelhante seguinte o exemplo de resultado de Olá deste comando:</span><span class="sxs-lookup"><span data-stu-id="7f11c-144">hello output of this command appears similar toohello following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="7f11c-145">Agora, tem várias novos diretórios e ficheiros no Olá **tasklist** diretório.</span><span class="sxs-lookup"><span data-stu-id="7f11c-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="7f11c-146">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="7f11c-146">Install additional modules</span></span>
<span data-ttu-id="7f11c-147">Um dos Olá ficheiros que **rápida** cria é **Package. JSON**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="7f11c-148">Este ficheiro contém uma lista de dependências de módulo.</span><span class="sxs-lookup"><span data-stu-id="7f11c-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="7f11c-149">Mais tarde, quando implementar Olá aplicação tooApp serviço Web Apps, este determina quais os módulos que precisam de toobe instalado no Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="7f11c-150">No Olá da linha de comandos, introduza Olá seguintes módulos de Olá comando tooinstall descritos Olá **Package. JSON** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="7f11c-151">Poderá ser necessário toouse 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="7f11c-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="7f11c-152">é apresentado toohello semelhante seguinte o exemplo de resultado de Olá deste comando:</span><span class="sxs-lookup"><span data-stu-id="7f11c-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="7f11c-153">Em seguida, introduza Olá Olá tooinstall de comando a seguir [azure], [uuid de nó], [nconf] e [async] módulos:</span><span class="sxs-lookup"><span data-stu-id="7f11c-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="7f11c-154">Olá **– guardar** sinalizador Adiciona entradas para estes módulos toohello **Package. JSON** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="7f11c-155">é apresentado toohello semelhante seguinte o exemplo de resultado de Olá deste comando:</span><span class="sxs-lookup"><span data-stu-id="7f11c-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="7f11c-156">Criar aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="7f11c-156">Create hello application</span></span>
<span data-ttu-id="7f11c-157">Agora, estamos a aplicação de Olá toobuild pronto.</span><span class="sxs-lookup"><span data-stu-id="7f11c-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="7f11c-158">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="7f11c-158">Create a model</span></span>
<span data-ttu-id="7f11c-159">A *modelo* é um objeto que representa dados Olá na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="7f11c-160">Para a aplicação Olá, Olá apenas é um objeto de tarefa, que representa um item na lista de tarefas Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="7f11c-161">Tarefas terão Olá seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="7f11c-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="7f11c-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="7f11c-162">PartitionKey</span></span>
* <span data-ttu-id="7f11c-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="7f11c-163">RowKey</span></span>
* <span data-ttu-id="7f11c-164">nome (cadeia)</span><span class="sxs-lookup"><span data-stu-id="7f11c-164">name (string)</span></span>
* <span data-ttu-id="7f11c-165">categoria (cadeia)</span><span class="sxs-lookup"><span data-stu-id="7f11c-165">category (string)</span></span>
* <span data-ttu-id="7f11c-166">foi concluído (valor boleano)</span><span class="sxs-lookup"><span data-stu-id="7f11c-166">completed (Boolean)</span></span>

<span data-ttu-id="7f11c-167">**PartitionKey** e **RowKey** são utilizados pelo Olá serviço tabela como chaves de tabela.</span><span class="sxs-lookup"><span data-stu-id="7f11c-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="7f11c-168">Para obter mais informações, consulte [modelo de dados de serviço tabela de Olá compreender](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f11c-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="7f11c-169">No Olá **tasklist** directory, criar um novo diretório designado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="7f11c-170">No Olá **modelos** directory, crie um novo ficheiro designado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="7f11c-171">Este ficheiro irá conter o modelo de Olá para tarefas de Olá criado pela sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="7f11c-172">Início de Olá do Olá **task.js** ficheiro, adicione Olá bibliotecas do código tooreference necessário os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7f11c-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="7f11c-173">Adicione o seguinte Olá code toodefine e exportar o objeto de tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="7f11c-174">Este objeto é responsável por ligar toohello tabela.</span><span class="sxs-lookup"><span data-stu-id="7f11c-174">This object is responsible for connecting toohello table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="7f11c-175">Adicione Olá seguindo métodos adicionais do código toodefine do objeto de tarefa Olá, que permite interações com os dados armazenados na tabela de Olá:</span><span class="sxs-lookup"><span data-stu-id="7f11c-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="7f11c-176">Guarde e feche Olá **task.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="7f11c-177">Criar um controlador</span><span class="sxs-lookup"><span data-stu-id="7f11c-177">Create a controller</span></span>
<span data-ttu-id="7f11c-178">A *controlador* processa os pedidos HTTP e apresenta-resposta Olá HTML.</span><span class="sxs-lookup"><span data-stu-id="7f11c-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="7f11c-179">No Olá **tasklist/rotas** directory, crie um novo ficheiro designado **tasklist.js** e abri-lo no editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7f11c-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="7f11c-180">Adicionar Olá seguinte código demasiado**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="7f11c-181">Esta ação carregue Olá do azure e async módulos, que são utilizados pelo **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="7f11c-182">Isto também define Olá **TaskList** função, o que é transmitida uma instância de Olá **tarefas** objeto definido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7f11c-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="7f11c-183">Definir um **TaskList** objeto.</span><span class="sxs-lookup"><span data-stu-id="7f11c-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="7f11c-184">Adicionar Olá demasiado os seguintes métodos**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="7f11c-184">Add hello following methods too**TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="7f11c-185">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="7f11c-185">Modify app.js</span></span>
1. <span data-ttu-id="7f11c-186">De Olá **tasklist** Olá diretório, abra **app.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="7f11c-187">Este ficheiro foi criado anteriormente executando Olá **rápida** comando.</span><span class="sxs-lookup"><span data-stu-id="7f11c-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="7f11c-188">Início de Olá do ficheiro de Olá, adicione Olá tooload Olá azure módulo, o nome de tabela do conjunto Olá, chave de partição e as credenciais de armazenamento do conjunto Olá utilizadas por este exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f11c-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="7f11c-189">nconf irá carregar os valores de configuração de Olá de variáveis de ambiente ou Olá **config** ficheiro, que iremos criar mais tarde.</span><span class="sxs-lookup"><span data-stu-id="7f11c-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="7f11c-190">No ficheiro de app.js Olá, desloque para baixo toowhere vir Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="7f11c-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="7f11c-191">Substitua Olá acima linhas com o código de Olá mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7f11c-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="7f11c-192">Isto irá inicializar uma instância de <strong>tarefas</strong> com uma conta de armazenamento de tooyour de ligação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="7f11c-193">Isto é transmitido toohello <strong>TaskList</strong>, que irá utilizar toocommunicate com Olá serviço tabela:</span><span class="sxs-lookup"><span data-stu-id="7f11c-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="7f11c-194">Guardar Olá **app.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="7f11c-195">Modificar a vista de índice de Olá</span><span class="sxs-lookup"><span data-stu-id="7f11c-195">Modify hello index view</span></span>
1. <span data-ttu-id="7f11c-196">Abra Olá **tasklist/views/index.jade** ficheiro num editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7f11c-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="7f11c-197">Substitua conteúdos integrais do Olá do ficheiro de Olá Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="7f11c-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="7f11c-198">Isto define uma vista que apresenta tarefas existentes e inclui um formulário para adicionar novas tarefas e marcar existentes como concluído.</span><span class="sxs-lookup"><span data-stu-id="7f11c-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="7f11c-199">Guarde e feche **Index. jade** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="7f11c-200">Modificar esquema global Olá</span><span class="sxs-lookup"><span data-stu-id="7f11c-200">Modify hello global layout</span></span>
<span data-ttu-id="7f11c-201">Olá **jade** ficheiro Olá **vistas** diretório é um modelo global para outros **. jade** ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7f11c-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="7f11c-202">Neste passo, irá modificá-la toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um toolkit que torna mais fácil toodesign uma aplicação de web looking nice.</span><span class="sxs-lookup"><span data-stu-id="7f11c-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="7f11c-203">Transferir e extrair os ficheiros de Olá para [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="7f11c-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="7f11c-204">Olá cópia **bootstrap.min.css** ficheiros do arranque de Olá **css** pasta para Olá **público/tramas** diretório da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="7f11c-205">De Olá **vistas** pasta, abra **jade** e substitua os conteúdos integrais Olá pelo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="7f11c-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="7f11c-206">Criar um ficheiro de configuração</span><span class="sxs-lookup"><span data-stu-id="7f11c-206">Create a config file</span></span>
<span data-ttu-id="7f11c-207">localmente toorun Olá aplicação, vamos pôr em prática as credenciais do armazenamento do Azure para um ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="7f11c-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="7f11c-208">Crie um ficheiro denominado **config* * com Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f11c-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="7f11c-209">Substitua **nome da conta de armazenamento** com o nome de Olá de armazenamento de Olá conta que criou anteriormente e substitua **chave de acesso de armazenamento** com a chave de acesso primária de Olá para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7f11c-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="7f11c-210">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7f11c-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="7f11c-211">Guarde este ficheiro *nível superior de um diretório* que Olá **tasklist** diretório, como esta:</span><span class="sxs-lookup"><span data-stu-id="7f11c-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="7f11c-212">motivo de Olá para efetuar este procedimento é tooavoid a verificar o ficheiro de configuração de Olá para controlo de origem, onde poderá ficar público.</span><span class="sxs-lookup"><span data-stu-id="7f11c-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="7f11c-213">Iremos implementar tooAzure de aplicação Olá, utilizaremos as variáveis de ambiente em vez de um ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="7f11c-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="7f11c-214">Executar a aplicação Olá localmente</span><span class="sxs-lookup"><span data-stu-id="7f11c-214">Run hello application locally</span></span>
<span data-ttu-id="7f11c-215">aplicação de Olá tootest no seu computador local, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7f11c-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="7f11c-216">De Olá da linha de comandos, altere os diretórios toohello **tasklist** diretório.</span><span class="sxs-lookup"><span data-stu-id="7f11c-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="7f11c-217">Utilize Olá aplicação localmente do comando toolaunch Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7f11c-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="7f11c-218">Abra um browser e navegue toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="7f11c-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="7f11c-219">É apresentada uma página web de toohello semelhante seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="7f11c-219">A web page similar toohello following example appears.</span></span>
   
    ![Uma página Web que apresenta um tasklist vazio][node-table-finished]
4. <span data-ttu-id="7f11c-221">toocreate um novo item de tarefas, introduza um nome e a categoria e clique em **Adicionar Item**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="7f11c-222">toomark uma tarefa como concluída, verifique **concluída** e clique em **tarefas de actualização**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Uma imagem de Olá novo item na lista de Olá de tarefas][node-table-list-items]

<span data-ttu-id="7f11c-224">Apesar de aplicação Olá é executada localmente, este é armazenar dados de Olá no Olá serviço de Azure Table.</span><span class="sxs-lookup"><span data-stu-id="7f11c-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="7f11c-225">Implementar a aplicação tooAzure</span><span class="sxs-lookup"><span data-stu-id="7f11c-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="7f11c-226">Olá passos nesta secção utilizam ferramentas de linha de comandos do Azure de Olá toocreate uma nova aplicação web no App Service e, em seguida, utilizarem a aplicação de toodeploy de Git.</span><span class="sxs-lookup"><span data-stu-id="7f11c-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="7f11c-227">tooperform estes passos têm de ter uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7f11c-228">Estes passos podem também ser executados utilizando Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7f11c-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7f11c-229">Consulte [criar e implementar uma aplicação de web de Node.js no App Service do Azure].</span><span class="sxs-lookup"><span data-stu-id="7f11c-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="7f11c-230">Se este for Olá primeira aplicação web que criou, tem de utilizar Olá Portal do Azure toodeploy esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="7f11c-231">tooget iniciado, instalar Olá [CLI do Azure] introduzindo Olá os seguintes comandos Olá linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="7f11c-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="7f11c-232">Importar definições de publicação</span><span class="sxs-lookup"><span data-stu-id="7f11c-232">Import publishing settings</span></span>
<span data-ttu-id="7f11c-233">Neste passo, irá transferir um ficheiro que contém informações sobre a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="7f11c-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="7f11c-234">Introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7f11c-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="7f11c-235">Este comando inicia um browser e navega toohello página de transferência.</span><span class="sxs-lookup"><span data-stu-id="7f11c-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="7f11c-236">Se lhe for solicitado, inicie sessão com a conta Olá com a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="7f11c-237">transferência de ficheiros de Olá começa automaticamente; Se não existir, pode clicar em ligação Olá início Olá de Olá toomanually transferência Olá do ficheiro de paginação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="7f11c-238">Guarde Olá de ficheiros e nota Olá caminho do ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7f11c-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="7f11c-239">Introduza Olá definições do comando tooimport Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7f11c-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="7f11c-240">Especifique o nome de ficheiro e caminho de Olá do Olá a publicação do ficheiro de definições que transferiu no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="7f11c-241">Depois das definições de Olá são importadas, eliminar Olá publicar o ficheiro de definições.</span><span class="sxs-lookup"><span data-stu-id="7f11c-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="7f11c-242">Já não é necessária e contém informações confidenciais relativas à sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="7f11c-243">Criar um aplicação web do app Service</span><span class="sxs-lookup"><span data-stu-id="7f11c-243">Create an App Service web app</span></span>
1. <span data-ttu-id="7f11c-244">De Olá da linha de comandos, altere os diretórios toohello **tasklist** diretório.</span><span class="sxs-lookup"><span data-stu-id="7f11c-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="7f11c-245">Utilize Olá os seguintes comandos toocreate uma nova aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7f11c-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="7f11c-246">Será solicitado para o nome da aplicação web Olá e localização.</span><span class="sxs-lookup"><span data-stu-id="7f11c-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="7f11c-247">Forneça um nome exclusivo e selecione Olá mesma localização geográfica da sua conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="7f11c-248">Olá `--git` parâmetro cria um repositório de Git no Azure para esta aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7f11c-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="7f11c-249">Também inicializa um repositório de Git no diretório atual Olá se nenhum existir e adiciona uma [Git remoto] com o nome "azure", que é utilizado toopublish Olá aplicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="7f11c-250">Por fim, cria um **Web. config** ficheiro que contém as definições utilizadas por aplicações de nó toohost do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="7f11c-251">Se omitir Olá `--git` parâmetro mas Olá diretório contém um repositório de Git, o comando de Olá ainda criará remoto Olá "azure".</span><span class="sxs-lookup"><span data-stu-id="7f11c-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="7f11c-252">Assim que este comando foi concluída, verá a seguinte de toohello semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="7f11c-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="7f11c-253">Tenha em atenção que Olá linha a partir **Web site criado em** contém Olá URL da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="7f11c-254">Se este for Olá primeira aplicação web do app Service para a sua subscrição, será aplicação web de Olá toocreate instruiu toouse Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="7f11c-255">Para obter mais informações, consulte [criar e implementar uma aplicação de web de Node.js no App Service do Azure].</span><span class="sxs-lookup"><span data-stu-id="7f11c-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="7f11c-256">Variáveis de ambiente de conjunto</span><span class="sxs-lookup"><span data-stu-id="7f11c-256">Set environment variables</span></span>
<span data-ttu-id="7f11c-257">Neste passo, irá adicionar configuração de aplicação de web de tooyour de variáveis de ambiente no Azure.</span><span class="sxs-lookup"><span data-stu-id="7f11c-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="7f11c-258">Olá linha de comandos, introduza o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="7f11c-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="7f11c-259">Substitua  **<storage account name>**  com o nome de Olá de armazenamento de Olá conta que criou anteriormente e substitua  **<storage access key>**  com a chave de acesso primária de Olá para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7f11c-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="7f11c-260">(Utilizar o mesmo valores de Olá como ficheiro de config Olá que criou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="7f11c-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="7f11c-261">Em alternativa, pode definir variáveis de ambiente no Olá [Portal do Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="7f11c-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="7f11c-262">Abra o painel da aplicação web Olá clicando **procurar** > **Web Apps** > nome da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7f11c-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="7f11c-263">No painel da sua aplicação web, clique em **todas as definições** > **definições da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="7f11c-264">Desloque para baixo toohello **as definições de aplicação** secção e adicionar os pares chave/valor de Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Definições de aplicação](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="7f11c-266">Clique em **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="7f11c-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="7f11c-267">Publicar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="7f11c-267">Publish hello application</span></span>
<span data-ttu-id="7f11c-268">aplicação do toopublish Olá, consolide Olá código ficheiros tooGit e, em seguida, emita tooazure/principal.</span><span class="sxs-lookup"><span data-stu-id="7f11c-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="7f11c-269">Defina as suas credenciais de implementação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="7f11c-270">Adicionar e consolidar os ficheiros da aplicação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="7f11c-271">Push Olá consolidação toohello aplicação web do app Service:</span><span class="sxs-lookup"><span data-stu-id="7f11c-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="7f11c-272">Utilize **mestre** como ramo de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="7f11c-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="7f11c-273">No final de Olá da implementação de Olá, verá um toohello semelhante de instrução seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7f11c-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="7f11c-274">Depois de concluída a operação de push Olá, procure o URL da aplicação web toohello devolvido anteriormente por Olá `azure create site` comando tooview a aplicação.</span><span class="sxs-lookup"><span data-stu-id="7f11c-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f11c-275">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7f11c-275">Next steps</span></span>
<span data-ttu-id="7f11c-276">Enquanto os passos descritos neste artigo Olá descrevem a utilizar as informações de toostore do serviço tabela Olá, também pode utilizar [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="7f11c-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f11c-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7f11c-277">Additional resources</span></span>
<span data-ttu-id="7f11c-278">[CLI do Azure]</span><span class="sxs-lookup"><span data-stu-id="7f11c-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="7f11c-279">O que mudou</span><span class="sxs-lookup"><span data-stu-id="7f11c-279">What's changed</span></span>
* <span data-ttu-id="7f11c-280">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7f11c-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[criar e implementar uma aplicação de web de Node.js no App Service do Azure]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nó]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI do Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid de nó]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
