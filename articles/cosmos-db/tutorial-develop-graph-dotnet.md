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
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB: Desenvolver com Olá Graph API no .NET
BD do Azure do Cosmos é serviço de base de dados com múltiplos modelo global distribuída da Microsoft. Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente. 

Este tutorial demonstra como toocreate uma conta de base de dados do Azure Cosmos utilizando Olá portal do Azure e como toocreate uma base de dados do gráfico e um contentor. aplicação de Olá, em seguida, cria uma rede social simple com quatro pessoas utilizando Olá [Graph API](graph-sdk-dotnet.md) (pré-visualização), em seguida, atravessa e consulta o gráfico de Olá Gremlin a utilizar.

Este tutorial abrange Olá seguintes tarefas:

> [!div class="checklist"]
> * Criar uma conta do Azure Cosmos DB 
> * Criar uma base de dados do gráfico e um contentor
> * Serializar objetos de too.NET vértices e contornos
> * Adicionar vértices e contornos
> * Gráfico de Olá de consulta utilizando Gremlin

## <a name="graphs-in-azure-cosmos-db"></a>Gráficos no Azure Cosmos DB
Pode utilizar a base de dados do Azure Cosmos toocreate, atualização e gráficos de consulta utilizando Olá [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteca. biblioteca de Microsoft.Azure.Graph Olá fornece um método de extensão único `CreateGremlinQuery<T>` por cima Olá `DocumentClient` consultas de Gremlin tooexecute de classe.

Gremlin é uma linguagem de programação funcional que suporta escrever operações (DML) e as operações de consulta e transversal. Iremos abranger a introdução com Gremlin alguns exemplos tooget neste artigo. Consulte [consultas Gremlin](gremlin-support.md) para instruções detalhadas das capacidades de Gremlin disponíveis do BD Azure Cosmos. 

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que tem o seguinte Olá:

* Uma conta ativa do Azure. Se não tiver uma, pode inscrever-se numa [conta gratuita](https://azure.microsoft.com/free/). 
    * Em alternativa, pode utilizar Olá [emulador do DocumentDB do Azure](local-emulator.md) para este tutorial.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Criar conta de base de dados

Vamos começar por criar uma conta de base de dados do Azure Cosmos no Olá portal do Azure.  

> [!TIP]
> * Já tem uma conta de base de dados do Azure Cosmos? Se assim for, avançar diretamente demasiado[configurar a sua solução Visual Studio](#SetupVS)
> * Tem uma conta do Azure DocumentDB? Se Sim, agora a sua conta é uma conta de base de dados do Azure Cosmos e pode avançar diretamente demasiado[configurar a sua solução Visual Studio](#SetupVS).  
> * Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, siga os passos de Olá em [emulador de BD do Azure Cosmos](local-emulator.md) toosetup Olá emulador e avançar diretamente demasiado[configurar a sua solução do Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Configurar a sua solução Visual Studio
1. Abra o **Visual Studio** no seu computador.
2. No Olá **ficheiro** menu, selecione **novo**e, em seguida, escolha **projeto**.
3. No Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual c#** / **aplicação de consola (.NET Framework)**, nomeie o projeto e, em seguida, clique em **OK**.
4. No Olá **Explorador de soluções**, o botão direito do rato clique na sua nova aplicação de consola, que está sob a sua solução Visual Studio, e, em seguida, clique em **gerir pacotes NuGet...**
5. No Olá **NuGet** separador, clique em **procurar**e escreva **Microsoft.Azure.Graphs** na caixa de pesquisa de Olá e verificação Olá **incluem as versões de pré-lançamento**.
6. Nos resultados de Olá, localizar **Microsoft.Azure.Graphs** e clique em **instalar**.
   
   Se receber uma mensagem sobre rever alterações toohello solução, clique em **OK**. Se obtiver uma mensagem sobre a aceitação de licença, clique em **Aceito**.
   
    Olá `Microsoft.Azure.Graphs` biblioteca fornece um método de extensão único `CreateGremlinQuery<T>` para executar operações de Gremlin. Gremlin é uma linguagem de programação funcional que suporta escrever operações (DML) e as operações de consulta e transversal. Iremos abranger a introdução com Gremlin alguns exemplos tooget neste artigo. [Consultas de gremlin](gremlin-support.md) tem instruções detalhadas sobre as capacidades de Gremlin do BD Azure Cosmos.

## <a id="add-references"></a>Ligar a aplicação

Adicione estas duas constantes e a sua *cliente* variável na sua aplicação. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Em seguida, head fazer uma cópia de toohello [portal do Azure](https://portal.azure.com) tooretrieve o URL de ponto final e a chave primária. URL de ponto final de Olá e a chave primária são necessários para a aplicação toounderstand onde tooconnect e para a base de dados do Azure Cosmos tootrust ligação da sua aplicação. 

No Olá portal do Azure, navegue até a conta de base de dados do Azure Cosmos tooyour, clique em **chaves**e, em seguida, clique em **chaves de leitura e escrita**. 

Copiar Olá URI a partir do portal de Olá e cole-o ao longo do `Endpoint` na propriedade de ponto final de Olá acima. Em seguida, copiar Olá chave primária no portal de Olá e cole-a Olá `AuthKey` propriedade acima. 

! [Captura de ecrã do portal do Azure de Olá utilizado por toocreate tutorial Olá uma aplicação c#. Mostra um Olá de conta de base de dados do Azure Cosmos botão chaves realçado no Olá navegação de base de dados do Azure Cosmos e valores URI e a chave primária Olá realçados no Olá painel chaves] [chaves] 
 
## <a id="instantiate"></a>Instanciar Olá DocumentClient 
Em seguida, crie uma nova instância do Olá **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Criar uma base de dados 

Agora, crie uma base de dados do Azure Cosmos [base de dados](documentdb-resources.md#databases) utilizando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de Olá  **DocumentClient** classe a partir de Olá [SDK do .NET DocumentDB](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Criar um gráfico 

Em seguida, criar um contentor de gráfico com Olá utilizando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método ou [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de Olá **DocumentClient**  classe. Uma coleção é um contentor de entidades de gráfico. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Serializar objetos de too.NET vértices e contornos
BD do Azure do Cosmos utiliza Olá [formato wire de GraphSON](gremlin-support.md), que define um esquema JSON para vértices, margens e propriedades. Olá SDK .NET da Azure Cosmos DB inclui JSON.NET como uma dependência e Isto permite-nos tooserialize/anular a serialização GraphSON em objetos de .NET que iremos pode trabalhar com o código.

Por exemplo, vamos trabalhar com uma rede social simple com quatro pessoas. Vamos ver como toocreate `Person` vértices, adicionar `Knows` relações entre eles, em seguida, consultar e atravessar relações de "amigo do amigo" Olá gráfico toofind. 

Olá `Microsoft.Azure.Graphs.Elements` espaço de nomes fornece `Vertex`, `Edge`, `Property` e `VertexProperty` classes para anular a serialização dos objetos de .NET definido pelo toowell do GraphSON respostas.

## <a name="run-gremlin-using-creategremlinquery"></a>Executar Gremlin utilizando CreateGremlinQuery
Gremlin, como o SQL, suporta a leitura, escrita e operações de consulta. Por exemplo, hello fragmento seguinte mostra como toocreate vértices, margens, executar algumas consultas de exemplo com `CreateGremlinQuery<T>`e de forma assíncrona itere através destes resultados utilizando `ExecuteNextAsync` e ' HasMoreResults.

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

## <a name="add-vertices-and-edges"></a>Adicionar vértices e contornos

Vamos ver as instruções Gremlin Olá mostradas na Olá anterior a secção mais detalhes. Primeiro vamos algumas vértices através do Gremlin `addV` método. Por exemplo, hello seguinte fragmento cria um vértice "Blogue ou seja" do tipo "Pessoa", com propriedades de nome próprio, apelido e idade.

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

Em seguida, vamos criar alguns contornos entre estes vértices através do Gremlin `addE` método. 

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

Iremos pode atualizar um vértice existente ao utilizar `properties` passo na Gremlin. Vamos ignorar a consulta do Olá chamada tooexecute Olá através de `HasMoreResults` e `ExecuteNextAsync` para restante Olá exemplos Olá.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Pode colocar margens e vértices através do Gremlin `drop` passo. Eis um fragmento que mostra como toodelete um vértice e um limite. Tenha em atenção que remover de um vértice efetua um eliminar em cascata de Olá associados contornos.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Gráfico de Olá de consulta

Pode executar consultas e traversals também utilizando Gremlin. Por exemplo, Olá fragmento a seguir mostra como toocount Olá número de vértices no gráfico de Olá:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Pode efetuar filtros através do Gremlin `has` e `hasLabel` passos e combine-os utilizando `and`, `or`, e `not` toobuild mais complexo filtra:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Pode projetar a algumas propriedades nos resultados de consulta Olá utilizando Olá `values` passo:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Até ao momento, estamos apenas viu operadores de consulta que funcionam em qualquer base de dados. Gráficos são rápidos e eficientes para operações de transversal quando precisar de toonavigate toorelated margens e vértices. Vamos localizar todos os amigos de blogue. Podemos fazê-lo através do Gremlin `outE` passo toofind Olá todas as out-extremidades do blogue, em seguida, que atravessa toohello nos vértices desses contornos através do Gremlin `inV` passo:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

executa a consulta seguinte Olá dois saltos toofind todas "amigos de blogue de amigos", chamando `outE` e `inV` duas vezes. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Pode construir consultas mais complexas e implementar a lógica do gráfico poderosas transversal utilizando Gremlin, incluindo filtro combinar expressões, efetuar ciclo utilizando Olá `loop` passo e navegação condicional implementar utilizando Olá `choose` passo. Saiba mais sobre o que pode fazer com [suporte Gremlin](gremlin-support.md)!

Já está, este tutorial de base de dados do Azure Cosmos está concluído! 

## <a name="clean-up-resources"></a>Limpar recursos

Se não toocontinue toouse esta aplicação, utilize Olá seguir toodelete passos todos os recursos criados por este tutorial no Olá portal do Azure.  

1. No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou. 
2. Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos Seguintes

Neste tutorial, fez seguinte Olá:

> [!div class="checklist"]
> * Criar uma conta de base de dados do Azure Cosmos 
> * Criar uma base de dados do gráfico e um contentor
> * Objetos serializados de vértices e margens da too.NET
> * Foram adicionadas vértices e contornos
> * Gráfico de Olá consultado utilizando Gremlin

Agora, pode criar consultas mais complexas e implementar lógica poderosa para percorrer gráficos com Gremlin. 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md) (Utilizar Gremlin para consultar)
