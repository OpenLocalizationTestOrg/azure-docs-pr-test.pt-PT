---
title: "Azure Cosmos DB: Criar uma aplicação com o Node.js e Olá DocumentDB API | Microsoft Docs"
description: "Apresenta um exemplo de código Node.js, pode utilizar tooconnect tooand consulta Olá API de DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="06ad9-103">BD do Azure do Cosmos: Criar uma aplicação API do DocumentDB com o Node.js e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="06ad9-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="06ad9-104">O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06ad9-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="06ad9-105">Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente.</span><span class="sxs-lookup"><span data-stu-id="06ad9-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="06ad9-106">Este guia de introdução demonstra como toocreate uma conta de base de dados do Azure Cosmos, a base de dados de documento e a coleção a utilizar Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="06ad9-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="06ad9-107">Em seguida, criar e executar uma aplicação de consola incorporada no Olá [DocumentDB Node.js API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="06ad9-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06ad9-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="06ad9-108">Prerequisites</span></span>

* <span data-ttu-id="06ad9-109">Antes de poder executar este exemplo, tem de ter Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="06ad9-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="06ad9-110">Versão de [Node.js](https://nodejs.org/en/) v0.10.29 ou superior</span><span class="sxs-lookup"><span data-stu-id="06ad9-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="06ad9-111">Git</span><span class="sxs-lookup"><span data-stu-id="06ad9-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="06ad9-112">Criar uma conta de base de dados</span><span class="sxs-lookup"><span data-stu-id="06ad9-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="06ad9-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="06ad9-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="06ad9-114">Aplicação de exemplo de Olá do clone</span><span class="sxs-lookup"><span data-stu-id="06ad9-114">Clone hello sample application</span></span>

<span data-ttu-id="06ad9-115">Agora vamos aplicação clone uma API de DocumentDB a partir do github, definir a cadeia de ligação de Olá e executá-la.</span><span class="sxs-lookup"><span data-stu-id="06ad9-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="06ad9-116">Pode ver como é fácil toowork com dados através de programação.</span><span class="sxs-lookup"><span data-stu-id="06ad9-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="06ad9-117">Abra uma janela de terminal do git, tais como o git bash, e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="06ad9-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="06ad9-118">Execute Olá repositório do comando tooclone Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="06ad9-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="06ad9-119">Rever o código de Olá</span><span class="sxs-lookup"><span data-stu-id="06ad9-119">Review hello code</span></span>

<span data-ttu-id="06ad9-120">Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="06ad9-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="06ad9-121">Abra Olá `app.js` ficheiro e localizar que estas linhas de código criar Olá recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06ad9-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="06ad9-122">Olá `documentClient` está inicializado.</span><span class="sxs-lookup"><span data-stu-id="06ad9-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="06ad9-123">É criada uma nova base de dados.</span><span class="sxs-lookup"><span data-stu-id="06ad9-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="06ad9-124">É criada uma nova coleção.</span><span class="sxs-lookup"><span data-stu-id="06ad9-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="06ad9-125">São criados alguns documentos.</span><span class="sxs-lookup"><span data-stu-id="06ad9-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="06ad9-126">É feita uma consulta SQL através de JSON.</span><span class="sxs-lookup"><span data-stu-id="06ad9-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="06ad9-127">Atualizar a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="06ad9-127">Update your connection string</span></span>

<span data-ttu-id="06ad9-128">Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="06ad9-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="06ad9-129">No Olá [portal do Azure](http://portal.azure.com/), no seu Azure Cosmos DB conta, na Olá deixado navegação clique **chaves**e, em seguida, clique em **chaves de leitura e escrita**.</span><span class="sxs-lookup"><span data-stu-id="06ad9-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="06ad9-130">Irá utilizar botões de cópia de Olá no lado direito de Olá de Olá de toocopy Olá ecrã URI e a chave primária para Olá `config.js` ficheiro no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="06ad9-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="06ad9-132">No Olá abra `config.js` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="06ad9-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="06ad9-133">Copie o valor URI do portal de Olá (utilizando o botão de copiar Olá) e torná-lo Olá valor da chave de ponto final de Olá no `config.js`.</span><span class="sxs-lookup"><span data-stu-id="06ad9-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="06ad9-134">Em seguida, copie o valor de chave primária do portal de Olá e torná-lo Olá valor Olá `config.primaryKey` no `config.js`.</span><span class="sxs-lookup"><span data-stu-id="06ad9-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="06ad9-135">Agora atualizou a sua aplicação com todas as informações de Olá tem toocommunicate com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="06ad9-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="06ad9-136">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="06ad9-136">Run hello app</span></span>
1. <span data-ttu-id="06ad9-137">Executar `npm install` um terminal tooinstall necessário módulos npm</span><span class="sxs-lookup"><span data-stu-id="06ad9-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="06ad9-138">Executar `node app.js` num terminal toostart a aplicação de nó.</span><span class="sxs-lookup"><span data-stu-id="06ad9-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="06ad9-139">Agora pode voltar atrás tooData Explorador e ver a consulta, modificar e trabalhar com estes novos dados.</span><span class="sxs-lookup"><span data-stu-id="06ad9-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="06ad9-140">Reveja os SLAs no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="06ad9-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="06ad9-141">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="06ad9-141">Clean up resources</span></span>

<span data-ttu-id="06ad9-142">Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="06ad9-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="06ad9-143">No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="06ad9-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="06ad9-144">Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="06ad9-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06ad9-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06ad9-145">Next steps</span></span>

<span data-ttu-id="06ad9-146">Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos, criar uma coleção utilizando Olá Explorador de dados e executar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="06ad9-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="06ad9-147">Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="06ad9-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> <span data-ttu-id="06ad9-148">[Import data into Azure Cosmos DB](import-data.md) (Importar dados para o Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="06ad9-148">[Import data into Azure Cosmos DB](import-data.md)</span></span>


