---
title: "Azure Cosmos DB: Criar uma aplicação web com o .NET e Olá MongoDB API | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET que pode utilizar tooconnect tooand consulta Olá API do Azure Cosmos DB MongoDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="f24b0-103">BD do Azure do Cosmos: Criar uma aplicação de web API do MongoDB com o .NET e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f24b0-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="f24b0-104">O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f24b0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="f24b0-105">Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f24b0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f24b0-106">Este guia de introdução demonstra como toocreate uma conta de base de dados do Azure Cosmos, a base de dados de documento e a coleção a utilizar Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f24b0-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="f24b0-107">Em seguida, irá criar e implementar uma aplicação de web de lista de tarefas incorporada no Olá [controlador MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="f24b0-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f24b0-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f24b0-108">Prerequisites</span></span>

<span data-ttu-id="f24b0-109">Se ainda não tiver o Visual Studio 2017, instalado, pode transferir e utilizar Olá **livre** [edição de Comunidade de 2017 do Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f24b0-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="f24b0-110">Certifique-se de que ativa **programação do Azure** durante a configuração do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="f24b0-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="f24b0-111">Criar uma conta de base de dados</span><span class="sxs-lookup"><span data-stu-id="f24b0-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="f24b0-112">Aplicação de exemplo de Olá do clone</span><span class="sxs-lookup"><span data-stu-id="f24b0-112">Clone hello sample application</span></span>

<span data-ttu-id="f24b0-113">Agora vamos clone uma API de MongoDB aplicação a partir do github, definir a cadeia de ligação de Olá e executá-la.</span><span class="sxs-lookup"><span data-stu-id="f24b0-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="f24b0-114">Verá como é fácil toowork com dados através de programação.</span><span class="sxs-lookup"><span data-stu-id="f24b0-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="f24b0-115">Abra uma janela de terminal do git, tais como o git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f24b0-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="f24b0-116">Execute Olá repositório do comando tooclone Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f24b0-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="f24b0-117">Em seguida, abra o ficheiro de solução Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f24b0-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="f24b0-118">Rever o código de Olá</span><span class="sxs-lookup"><span data-stu-id="f24b0-118">Review hello code</span></span>

<span data-ttu-id="f24b0-119">Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f24b0-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="f24b0-120">Abra Olá **Dal.cs** ficheiro em Olá **DAL** directory e irá encontrar que estas linhas de código criar Olá recursos de base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f24b0-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="f24b0-121">Inicializar Olá Mongo cliente.</span><span class="sxs-lookup"><span data-stu-id="f24b0-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="f24b0-122">Obter a base de dados de Olá e coleção Olá.</span><span class="sxs-lookup"><span data-stu-id="f24b0-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="f24b0-123">Obter todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="f24b0-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="f24b0-124">Atualizar a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="f24b0-124">Update your connection string</span></span>

<span data-ttu-id="f24b0-125">Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f24b0-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="f24b0-126">No Olá [portal do Azure](http://portal.azure.com/), no seu Azure Cosmos DB conta, na Olá deixado navegação clique **cadeia de ligação**e, em seguida, clique em **chaves de leitura e escrita**.</span><span class="sxs-lookup"><span data-stu-id="f24b0-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="f24b0-127">Irá utilizar os botões de cópia de Olá no lado direito de Olá de Olá de toocopy Olá ecrã nome de utilizador, palavra-passe e o anfitrião no ficheiro de Dal.cs Olá no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="f24b0-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="f24b0-128">Abra Olá **Dal.cs** ficheiro Olá **DAL** diretório.</span><span class="sxs-lookup"><span data-stu-id="f24b0-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="f24b0-129">Copiar o **nome de utilizador** valor a partir do portal de Olá (utilizando o botão de copiar Olá) e torná-lo Olá valor Olá **nome de utilizador** no seu **Dal.cs** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="f24b0-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="f24b0-130">Em seguida, copie o **anfitrião** valor a partir do portal de Olá e torná-lo Olá valor Olá **anfitrião** no seu **Dal.cs** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="f24b0-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="f24b0-131">Por fim, copie o **palavra-passe** valor a partir do portal de Olá e torná-lo Olá valor Olá **palavra-passe** no seu **Dal.cs** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="f24b0-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="f24b0-132">Agora atualizou a sua aplicação com todas as informações de Olá tem toocommunicate com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f24b0-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="f24b0-133">Executar a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="f24b0-133">Run hello web app</span></span>

1. <span data-ttu-id="f24b0-134">No Visual Studio, clique com botão direito no projeto Olá no **Explorador de soluções** e, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f24b0-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="f24b0-135">No Olá NuGet **procurar** caixa, escreva *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="f24b0-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="f24b0-136">Resultados de Olá, instalar Olá **MongoDB.Driver** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="f24b0-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="f24b0-137">Esta ação instala o pacote de MongoDB.Driver Olá, bem como todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="f24b0-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="f24b0-138">Clique em CTRL + F5 aplicação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="f24b0-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="f24b0-139">A aplicação é apresentada no browser.</span><span class="sxs-lookup"><span data-stu-id="f24b0-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="f24b0-140">Clique em **criar** no Olá browser e criar algumas novas tarefas na sua aplicação de lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="f24b0-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="f24b0-141">Reveja os SLAs no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f24b0-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="f24b0-142">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="f24b0-142">Clean up resources</span></span>

<span data-ttu-id="f24b0-143">Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f24b0-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="f24b0-144">No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="f24b0-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="f24b0-145">Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="f24b0-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f24b0-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f24b0-146">Next steps</span></span>

<span data-ttu-id="f24b0-147">Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos e execute uma aplicação web através de hello API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f24b0-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="f24b0-148">Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="f24b0-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f24b0-149">Importe dados para a base de dados do Azure Cosmos para Olá API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="f24b0-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

