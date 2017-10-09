---
title: "Azure Cosmos DB: Desenvolver com Olá Graph API no .NET | Microsoft Docs"
description: "Saiba como toodevelop com a API do Azure Cosmos base de dados DocumentDB através do .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="03840-103">Azure Cosmos DB: Desenvolver com Olá Graph API no .NET</span><span class="sxs-lookup"><span data-stu-id="03840-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="03840-104">BD do Azure do Cosmos é serviço de base de dados com múltiplos modelo global distribuída da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03840-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="03840-105">Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente.</span><span class="sxs-lookup"><span data-stu-id="03840-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="03840-106">Este tutorial demonstra como toocreate uma conta de base de dados do Azure Cosmos utilizando Olá portal do Azure e como toocreate uma base de dados do gráfico e um contentor.</span><span class="sxs-lookup"><span data-stu-id="03840-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="03840-107">aplicação de Olá, em seguida, cria uma rede social simple com quatro pessoas utilizando Olá [Graph API](graph-sdk-dotnet.md) (pré-visualização), em seguida, atravessa e consulta o gráfico de Olá Gremlin a utilizar.</span><span class="sxs-lookup"><span data-stu-id="03840-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="03840-108">Este tutorial abrange Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="03840-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03840-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="03840-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="03840-110">Criar uma base de dados do gráfico e um contentor</span><span class="sxs-lookup"><span data-stu-id="03840-110">Create a graph database and container</span></span>
> * <span data-ttu-id="03840-111">Serializar objetos de too.NET vértices e contornos</span><span class="sxs-lookup"><span data-stu-id="03840-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="03840-112">Adicionar vértices e contornos</span><span class="sxs-lookup"><span data-stu-id="03840-112">Add vertices and edges</span></span>
> * <span data-ttu-id="03840-113">Gráfico de Olá de consulta utilizando Gremlin</span><span class="sxs-lookup"><span data-stu-id="03840-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="03840-114">Gráficos no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="03840-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="03840-115">Pode utilizar a base de dados do Azure Cosmos toocreate, atualização e gráficos de consulta utilizando Olá [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="03840-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="03840-116">biblioteca de Microsoft.Azure.Graph Olá fornece um método de extensão único `CreateGremlinQuery<T>` por cima Olá `DocumentClient` consultas de Gremlin tooexecute de classe.</span><span class="sxs-lookup"><span data-stu-id="03840-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="03840-117">Gremlin é uma linguagem de programação funcional que suporta escrever operações (DML) e as operações de consulta e transversal.</span><span class="sxs-lookup"><span data-stu-id="03840-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="03840-118">Iremos abranger a introdução com Gremlin alguns exemplos tooget neste artigo.</span><span class="sxs-lookup"><span data-stu-id="03840-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="03840-119">Consulte [consultas Gremlin](gremlin-support.md) para instruções detalhadas das capacidades de Gremlin disponíveis do BD Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="03840-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="03840-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="03840-120">Prerequisites</span></span>
<span data-ttu-id="03840-121">Certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="03840-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="03840-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="03840-122">An active Azure account.</span></span> <span data-ttu-id="03840-123">Se não tiver uma, pode inscrever-se numa [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="03840-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="03840-124">Em alternativa, pode utilizar Olá [emulador do DocumentDB do Azure](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="03840-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="03840-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="03840-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="03840-126">Criar conta de base de dados</span><span class="sxs-lookup"><span data-stu-id="03840-126">Create database account</span></span>

<span data-ttu-id="03840-127">Vamos começar por criar uma conta de base de dados do Azure Cosmos no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03840-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="03840-128">Já tem uma conta de base de dados do Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="03840-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="03840-129">Se assim for, avançar diretamente demasiado[configurar a sua solução Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="03840-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="03840-130">Tem uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="03840-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="03840-131">Se Sim, agora a sua conta é uma conta de base de dados do Azure Cosmos e pode avançar diretamente demasiado[configurar a sua solução Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="03840-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="03840-132">Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, siga os passos de Olá em [emulador de BD do Azure Cosmos](local-emulator.md) toosetup Olá emulador e avançar diretamente demasiado[configurar a sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="03840-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="03840-133"><a id="SetupVS"></a>Configurar a sua solução Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03840-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="03840-134">Abra o **Visual Studio** no seu computador.</span><span class="sxs-lookup"><span data-stu-id="03840-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="03840-135">No Olá **ficheiro** menu, selecione **novo**e, em seguida, escolha **projeto**.</span><span class="sxs-lookup"><span data-stu-id="03840-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="03840-136">No Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual c#** / **aplicação de consola (.NET Framework)**, nomeie o projeto e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03840-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="03840-137">No Olá **Explorador de soluções**, o botão direito do rato clique na sua nova aplicação de consola, que está sob a sua solução Visual Studio, e, em seguida, clique em **gerir pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="03840-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="03840-138">No Olá **NuGet** separador, clique em **procurar**e escreva **Microsoft.Azure.Graphs** na caixa de pesquisa de Olá e verificação Olá **incluem as versões de pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="03840-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="03840-139">Nos resultados de Olá, localizar **Microsoft.Azure.Graphs** e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="03840-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="03840-140">Se receber uma mensagem sobre rever alterações toohello solução, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="03840-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="03840-141">Se obtiver uma mensagem sobre a aceitação de licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="03840-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="03840-142">Olá `Microsoft.Azure.Graphs` biblioteca fornece um método de extensão único `CreateGremlinQuery<T>` para executar operações de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="03840-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="03840-143">Gremlin é uma linguagem de programação funcional que suporta escrever operações (DML) e as operações de consulta e transversal.</span><span class="sxs-lookup"><span data-stu-id="03840-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="03840-144">Iremos abranger a introdução com Gremlin alguns exemplos tooget neste artigo.</span><span class="sxs-lookup"><span data-stu-id="03840-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="03840-145">[Consultas de gremlin](gremlin-support.md) tem instruções detalhadas sobre as capacidades de Gremlin do BD Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="03840-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="03840-146"><a id="add-references"></a>Ligar a aplicação</span><span class="sxs-lookup"><span data-stu-id="03840-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="03840-147">Adicione estas duas constantes e a sua *cliente* variável na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="03840-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="03840-148">Em seguida, head fazer uma cópia de toohello [portal do Azure](https://portal.azure.com) tooretrieve o URL de ponto final e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="03840-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="03840-149">URL de ponto final de Olá e a chave primária são necessários para a aplicação toounderstand onde tooconnect e para a base de dados do Azure Cosmos tootrust ligação da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="03840-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="03840-150">No Olá portal do Azure, navegue até a conta de base de dados do Azure Cosmos tooyour, clique em **chaves**e, em seguida, clique em **chaves de leitura e escrita**.</span><span class="sxs-lookup"><span data-stu-id="03840-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="03840-151">Copiar Olá URI a partir do portal de Olá e cole-o ao longo do `Endpoint` na propriedade de ponto final de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="03840-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="03840-152">Em seguida, copiar Olá chave primária no portal de Olá e cole-a Olá `AuthKey` propriedade acima.</span><span class="sxs-lookup"><span data-stu-id="03840-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="03840-153">! [Captura de ecrã do portal do Azure de Olá utilizado por toocreate tutorial Olá uma aplicação c#.</span><span class="sxs-lookup"><span data-stu-id="03840-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="03840-154">Mostra um Olá de conta de base de dados do Azure Cosmos botão chaves realçado no Olá navegação de base de dados do Azure Cosmos e valores URI e a chave primária Olá realçados no Olá painel chaves] [chaves]</span><span class="sxs-lookup"><span data-stu-id="03840-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="03840-155"><a id="instantiate"></a>Instanciar Olá DocumentClient</span><span class="sxs-lookup"><span data-stu-id="03840-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="03840-156">Em seguida, crie uma nova instância do Olá **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="03840-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="03840-157"><a id="create-database"></a>Criar uma base de dados</span><span class="sxs-lookup"><span data-stu-id="03840-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="03840-158">Agora, crie uma base de dados do Azure Cosmos [base de dados](documentdb-resources.md#databases) utilizando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de Olá  **DocumentClient** classe a partir de Olá [SDK do .NET DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="03840-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="03840-159">Criar um gráfico</span><span class="sxs-lookup"><span data-stu-id="03840-159">Create a graph</span></span> 

<span data-ttu-id="03840-160">Em seguida, criar um contentor de gráfico com Olá utilizando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método ou [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de Olá **DocumentClient**  classe.</span><span class="sxs-lookup"><span data-stu-id="03840-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="03840-161">Uma coleção é um contentor de entidades de gráfico.</span><span class="sxs-lookup"><span data-stu-id="03840-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="03840-162"><a id="serializing"></a>Serializar objetos de too.NET vértices e contornos</span><span class="sxs-lookup"><span data-stu-id="03840-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="03840-163">BD do Azure do Cosmos utiliza Olá [formato wire de GraphSON](gremlin-support.md), que define um esquema JSON para vértices, margens e propriedades.</span><span class="sxs-lookup"><span data-stu-id="03840-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="03840-164">Olá SDK .NET da Azure Cosmos DB inclui JSON.NET como uma dependência e Isto permite-nos tooserialize/anular a serialização GraphSON em objetos de .NET que iremos pode trabalhar com o código.</span><span class="sxs-lookup"><span data-stu-id="03840-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="03840-165">Por exemplo, vamos trabalhar com uma rede social simple com quatro pessoas.</span><span class="sxs-lookup"><span data-stu-id="03840-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="03840-166">Vamos ver como toocreate `Person` vértices, adicionar `Knows` relações entre eles, em seguida, consultar e atravessar relações de "amigo do amigo" Olá gráfico toofind.</span><span class="sxs-lookup"><span data-stu-id="03840-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="03840-167">Olá `Microsoft.Azure.Graphs.Elements` espaço de nomes fornece `Vertex`, `Edge`, `Property` e `VertexProperty` classes para anular a serialização dos objetos de .NET definido pelo toowell do GraphSON respostas.</span><span class="sxs-lookup"><span data-stu-id="03840-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="03840-168">Executar Gremlin utilizando CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="03840-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="03840-169">Gremlin, como o SQL, suporta a leitura, escrita e operações de consulta.</span><span class="sxs-lookup"><span data-stu-id="03840-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="03840-170">Por exemplo, hello fragmento seguinte mostra como toocreate vértices, margens, executar algumas consultas de exemplo com `CreateGremlinQuery<T>`e de forma assíncrona itere através destes resultados utilizando `ExecuteNextAsync` e ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="03840-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="03840-171">Adicionar vértices e contornos</span><span class="sxs-lookup"><span data-stu-id="03840-171">Add vertices and edges</span></span>

<span data-ttu-id="03840-172">Vamos ver as instruções Gremlin Olá mostradas na Olá anterior a secção mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="03840-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="03840-173">Primeiro vamos algumas vértices através do Gremlin `addV` método.</span><span class="sxs-lookup"><span data-stu-id="03840-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="03840-174">Por exemplo, hello seguinte fragmento cria um vértice "Blogue ou seja" do tipo "Pessoa", com propriedades de nome próprio, apelido e idade.</span><span class="sxs-lookup"><span data-stu-id="03840-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="03840-175">Em seguida, vamos criar alguns contornos entre estes vértices através do Gremlin `addE` método.</span><span class="sxs-lookup"><span data-stu-id="03840-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="03840-176">Iremos pode atualizar um vértice existente ao utilizar `properties` passo na Gremlin.</span><span class="sxs-lookup"><span data-stu-id="03840-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="03840-177">Vamos ignorar a consulta do Olá chamada tooexecute Olá através de `HasMoreResults` e `ExecuteNextAsync` para restante Olá exemplos Olá.</span><span class="sxs-lookup"><span data-stu-id="03840-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="03840-178">Pode colocar margens e vértices através do Gremlin `drop` passo.</span><span class="sxs-lookup"><span data-stu-id="03840-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="03840-179">Eis um fragmento que mostra como toodelete um vértice e um limite.</span><span class="sxs-lookup"><span data-stu-id="03840-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="03840-180">Tenha em atenção que remover de um vértice efetua um eliminar em cascata de Olá associados contornos.</span><span class="sxs-lookup"><span data-stu-id="03840-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="03840-181">Gráfico de Olá de consulta</span><span class="sxs-lookup"><span data-stu-id="03840-181">Query hello graph</span></span>

<span data-ttu-id="03840-182">Pode executar consultas e traversals também utilizando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="03840-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="03840-183">Por exemplo, Olá fragmento a seguir mostra como toocount Olá número de vértices no gráfico de Olá:</span><span class="sxs-lookup"><span data-stu-id="03840-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="03840-184">Pode efetuar filtros através do Gremlin `has` e `hasLabel` passos e combine-os utilizando `and`, `or`, e `not` toobuild mais complexo filtra:</span><span class="sxs-lookup"><span data-stu-id="03840-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="03840-185">Pode projetar a algumas propriedades nos resultados de consulta Olá utilizando Olá `values` passo:</span><span class="sxs-lookup"><span data-stu-id="03840-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="03840-186">Até ao momento, estamos apenas viu operadores de consulta que funcionam em qualquer base de dados.</span><span class="sxs-lookup"><span data-stu-id="03840-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="03840-187">Gráficos são rápidos e eficientes para operações de transversal quando precisar de toonavigate toorelated margens e vértices.</span><span class="sxs-lookup"><span data-stu-id="03840-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="03840-188">Vamos localizar todos os amigos de blogue.</span><span class="sxs-lookup"><span data-stu-id="03840-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="03840-189">Podemos fazê-lo através do Gremlin `outE` passo toofind Olá todas as out-extremidades do blogue, em seguida, que atravessa toohello nos vértices desses contornos através do Gremlin `inV` passo:</span><span class="sxs-lookup"><span data-stu-id="03840-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="03840-190">executa a consulta seguinte Olá dois saltos toofind todas "amigos de blogue de amigos", chamando `outE` e `inV` duas vezes.</span><span class="sxs-lookup"><span data-stu-id="03840-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="03840-191">Pode construir consultas mais complexas e implementar a lógica do gráfico poderosas transversal utilizando Gremlin, incluindo filtro combinar expressões, efetuar ciclo utilizando Olá `loop` passo e navegação condicional implementar utilizando Olá `choose` passo.</span><span class="sxs-lookup"><span data-stu-id="03840-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="03840-192">Saiba mais sobre o que pode fazer com [suporte Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="03840-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="03840-193">Já está, este tutorial de base de dados do Azure Cosmos está concluído!</span><span class="sxs-lookup"><span data-stu-id="03840-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="03840-194">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="03840-194">Clean up resources</span></span>

<span data-ttu-id="03840-195">Se não toocontinue toouse esta aplicação, utilize Olá seguir toodelete passos todos os recursos criados por este tutorial no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03840-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="03840-196">No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="03840-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="03840-197">Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="03840-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03840-198">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="03840-198">Next Steps</span></span>

<span data-ttu-id="03840-199">Neste tutorial, fez seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="03840-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03840-200">Criar uma conta de base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="03840-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="03840-201">Criar uma base de dados do gráfico e um contentor</span><span class="sxs-lookup"><span data-stu-id="03840-201">Created a graph database and container</span></span>
> * <span data-ttu-id="03840-202">Objetos serializados de vértices e margens da too.NET</span><span class="sxs-lookup"><span data-stu-id="03840-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="03840-203">Foram adicionadas vértices e contornos</span><span class="sxs-lookup"><span data-stu-id="03840-203">Added vertices and edges</span></span>
> * <span data-ttu-id="03840-204">Gráfico de Olá consultado utilizando Gremlin</span><span class="sxs-lookup"><span data-stu-id="03840-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="03840-205">Agora, pode criar consultas mais complexas e implementar lógica poderosa para percorrer gráficos com Gremlin.</span><span class="sxs-lookup"><span data-stu-id="03840-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> <span data-ttu-id="03840-206">[Query using Gremlin](tutorial-query-graph.md) (Utilizar Gremlin para consultar)</span><span class="sxs-lookup"><span data-stu-id="03840-206">[Query using Gremlin](tutorial-query-graph.md)</span></span>
