---
title: aaaCreate uma base de dados de documento de BD do Cosmos do Azure com o Java | Microsoft Docs | Microsoft Docs
description: "Apresenta um exemplo de código Java, pode utilizar tooconnect tooand consulta Olá API de DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="243e7-103">BD do Azure do Cosmos: Criar uma base de dados de documento utilizando Java e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="243e7-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="243e7-104">O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="243e7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="243e7-105">Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente.</span><span class="sxs-lookup"><span data-stu-id="243e7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="243e7-106">Este guia de introdução cria um documento de base de dados utilizando Olá ferramentas portais do Azure para a base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="243e7-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="243e7-107">Este guia de introdução mostra também como tooquickly criar uma aplicação de consola Java utilizando Olá [API de Java DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="243e7-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="243e7-108">Olá instruções deste guia de introdução podem ser seguidas em qualquer sistema operativo que seja capaz de executar Java.</span><span class="sxs-lookup"><span data-stu-id="243e7-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="243e7-109">Por concluir este guia de introdução estará familiarizado com a criar e modificar recursos de base de dados de documento no Olá IU ou x509securitytokenparameters, optando-se a sua preferência.</span><span class="sxs-lookup"><span data-stu-id="243e7-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="243e7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="243e7-110">Prerequisites</span></span>

* [<span data-ttu-id="243e7-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="243e7-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="243e7-112">Ubuntu, executado `apt-get install default-jdk` tooinstall Olá JDK.</span><span class="sxs-lookup"><span data-stu-id="243e7-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="243e7-113">Ser tooset se Olá JAVA_HOME ambiente toopoint variável toohello pasta onde Olá JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="243e7-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="243e7-114">[Transferir](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um arquivo binário [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="243e7-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="243e7-115">No Ubuntu, pode executar `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="243e7-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="243e7-116">Git</span><span class="sxs-lookup"><span data-stu-id="243e7-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="243e7-117">No Ubuntu, pode executar `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="243e7-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="243e7-118">Criar uma conta de base de dados</span><span class="sxs-lookup"><span data-stu-id="243e7-118">Create a database account</span></span>

<span data-ttu-id="243e7-119">Antes de poder criar uma base de dados de documento, terá de toocreate uma conta de base de dados SQL (DocumentDB) com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="243e7-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="243e7-120">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="243e7-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="243e7-121">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="243e7-121">Add sample data</span></span>

<span data-ttu-id="243e7-122">Agora pode adicionar dados tooyour nova coleção com o Explorador de dados.</span><span class="sxs-lookup"><span data-stu-id="243e7-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="243e7-123">No Explorador de dados nova base de dados Olá aparece no painel de coleções de Olá.</span><span class="sxs-lookup"><span data-stu-id="243e7-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="243e7-124">Expanda Olá **tarefas** da base de dados, expanda Olá **itens** coleção, clique em **documentos**e, em seguida, clique em **novos documentos**.</span><span class="sxs-lookup"><span data-stu-id="243e7-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Criar novos documentos no Explorador de dados no Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="243e7-126">Agora, adicione uma coleção de toohello documentos com Olá seguir a estrutura.</span><span class="sxs-lookup"><span data-stu-id="243e7-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="243e7-127">Depois de adicionar Olá json toohello **documentos** separador, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="243e7-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiar dados json e clique em Guardar no Explorador de dados no Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="243e7-129">Criar e guardar um documento mais onde inserir um valor exclusivo para Olá `id` propriedade e alteração Olá outras propriedades como julgar.</span><span class="sxs-lookup"><span data-stu-id="243e7-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="243e7-130">Agora, os documentos podem ter qualquer estrutura que queira criar, uma vez que o Azure Cosmos DB não impõe qualquer esquema aos seus dados.</span><span class="sxs-lookup"><span data-stu-id="243e7-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="243e7-131">Pode agora utilizar as consultas no Explorador de dados tooretrieve os dados clicando Olá **Editar filtro** e **aplicar filtro** botões.</span><span class="sxs-lookup"><span data-stu-id="243e7-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="243e7-132">Por predefinição, o Explorador de dados utiliza `SELECT * FROM c` tooretrieve todos os documentos numa coleção de Olá, mas pode alterar esse tooa diferentes [consulta SQL](documentdb-sql-query.md), tais como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos os documentos de Olá por ordem descendente, com base no os seus timestamp.</span><span class="sxs-lookup"><span data-stu-id="243e7-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="243e7-133">Também pode utilizar os procedimentos de toocreate armazenado do Explorador de dados, UDFs e lógica de negócio do lado do servidor de tooperform de acionadores bem como o débito de escala.</span><span class="sxs-lookup"><span data-stu-id="243e7-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="243e7-134">Explorador de dados expõe todos os Olá incorporada programático acesso aos dados disponível no Olá APIs, mas fornece acesso fácil tooyour dados no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="243e7-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="243e7-135">Aplicação de exemplo de Olá do clone</span><span class="sxs-lookup"><span data-stu-id="243e7-135">Clone hello sample application</span></span>

<span data-ttu-id="243e7-136">Agora vamos comutador tooworking com o código.</span><span class="sxs-lookup"><span data-stu-id="243e7-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="243e7-137">Vamos de clone de uma aplicação API do DocumentDB a partir do GitHub, definir a cadeia de ligação de Olá e executá-la.</span><span class="sxs-lookup"><span data-stu-id="243e7-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="243e7-138">Pode ver como é fácil toowork com dados através de programação.</span><span class="sxs-lookup"><span data-stu-id="243e7-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="243e7-139">Abra uma janela de terminal do git, tais como o git bash, e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="243e7-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="243e7-140">Execute Olá repositório do comando tooclone Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="243e7-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="243e7-141">Rever o código de Olá</span><span class="sxs-lookup"><span data-stu-id="243e7-141">Review hello code</span></span>

<span data-ttu-id="243e7-142">Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="243e7-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="243e7-143">Abra Olá `Program.java` ficheiros da pasta de \src\GetStarted Olá e localizar estas linhas de código que criar Olá recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="243e7-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="243e7-144">Olá `DocumentClient` está inicializado.</span><span class="sxs-lookup"><span data-stu-id="243e7-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="243e7-145">É criada uma nova base de dados.</span><span class="sxs-lookup"><span data-stu-id="243e7-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="243e7-146">É criada uma nova coleção.</span><span class="sxs-lookup"><span data-stu-id="243e7-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="243e7-147">São criados alguns documentos.</span><span class="sxs-lookup"><span data-stu-id="243e7-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="243e7-148">É feita uma consulta SQL através de JSON.</span><span class="sxs-lookup"><span data-stu-id="243e7-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="243e7-149">Atualizar a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="243e7-149">Update your connection string</span></span>

<span data-ttu-id="243e7-150">Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="243e7-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="243e7-151">Este procedimento activará a toocommunicate de aplicação com a base de dados alojada.</span><span class="sxs-lookup"><span data-stu-id="243e7-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="243e7-152">No Olá [portal do Azure](http://portal.azure.com/), no seu Azure Cosmos DB conta, na Olá deixado navegação clique **chaves**e, em seguida, clique em **chaves de leitura e escrita**.</span><span class="sxs-lookup"><span data-stu-id="243e7-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="243e7-153">Irá utilizar botões de cópia de Olá no lado direito de Olá de Olá de toocopy Olá ecrã URI e a chave primária para Olá `Program.java` ficheiro no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="243e7-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="243e7-155">No Olá abra `Program.java` ficheiro, copie o valor URI do portal de Olá (utilizando o botão de copiar Olá) e torná-lo Olá valor Olá endpoint toohello DocumentClient o construtor no `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="243e7-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="243e7-156">Em seguida, copie o valor de chave primária do portal de Olá e cole-o através de "FILLME", tornando Olá segundo parâmetro no construtor do Olá DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="243e7-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="243e7-157">Agora atualizou a sua aplicação com todas as informações de Olá tem toocommunicate com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="243e7-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="243e7-158">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="243e7-158">Run hello app</span></span>

1. <span data-ttu-id="243e7-159">Na janela de terminal git Olá, `cd` pasta azure-cosmos-db-documentdb-java-getting-started toohello.</span><span class="sxs-lookup"><span data-stu-id="243e7-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="243e7-160">Na janela de terminal git Olá, escreva `mvn package` tooinstall Olá necessário pacotes de Java.</span><span class="sxs-lookup"><span data-stu-id="243e7-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="243e7-161">Na janela de terminal git Olá, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` no Olá toostart de janela de terminal, a aplicação de Java.</span><span class="sxs-lookup"><span data-stu-id="243e7-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="243e7-162">Na janela de terminal Olá, irá receber a notificação Olá FamilyDB base de dados foi criado e toopress toocontinue uma chave.</span><span class="sxs-lookup"><span data-stu-id="243e7-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="243e7-163">Prima uma base de dados de Olá toocreate chave, em seguida, mude toohello Explorador de dados e verá que agora contém uma base de dados FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="243e7-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="243e7-164">Continuar toopress chaves toocreate Olá coleção e Olá documentos e, em seguida, executar uma consulta.</span><span class="sxs-lookup"><span data-stu-id="243e7-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="243e7-165">Quando tiver concluído o projeto de Olá, recursos de Olá são eliminados da sua conta.</span><span class="sxs-lookup"><span data-stu-id="243e7-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="243e7-167">Reveja os SLAs no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="243e7-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="243e7-168">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="243e7-168">Clean up resources</span></span>

<span data-ttu-id="243e7-169">Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="243e7-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="243e7-170">No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="243e7-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="243e7-171">Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="243e7-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="243e7-172">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="243e7-172">Next steps</span></span>

<span data-ttu-id="243e7-173">Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos, base de dados de documento e coleção utilizando Olá Explorador de dados e executar uma aplicação toodo Olá mesma coisa através de programação.</span><span class="sxs-lookup"><span data-stu-id="243e7-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="243e7-174">Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="243e7-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> <span data-ttu-id="243e7-175">[Import data into Azure Cosmos DB](import-data.md) (Importar dados para o Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="243e7-175">[Import data into Azure Cosmos DB](import-data.md)</span></span>


