---
title: "Azure Cosmos DB: Tutorial de introdução da API do DocumentDB com NET Core | Microsoft Docs"
description: "Um tutorial que cria uma base de dados online e a aplicação de consola do c# com Olá Azure Cosmos DB API Core SDK do .NET DocumentDB."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure Cosmos DB: Introdução Olá API do DocumentDB e .NET Core
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bem-vindo toohello DocumentDB API para Azure Cosmos DB introdução tutorial de .NET Core! Depois de seguir este tutorial, terá de uma aplicação de consola que cria e consulta recursos do Cosmos DB.

Iremos abranger:

* Criar e ligar-se a conta de base de dados do Azure Cosmos tooan
* Configuração da sua Solução Visual Studio
* Criação de uma base de dados online
* Criação de uma coleção
* Criação de documentos JSON
* Consulta de coleção de Olá
* Substituir um documento
* Eliminar um documento
* Eliminar Olá base de dados

Não tem tempo? Não se preocupe! solução completa de Olá está disponível no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Ir toohello [obter a secção de solução completa de Olá](#GetSolution) para instruções rápidas.

Pretende toobuild um Xamarin iOS, Android ou formulários através da aplicação Olá API do DocumentDB e SDK do .NET Core? Consulte [criar aplicações móveis com o Xamarin e base de dados do Azure Cosmos](mobile-apps-with-xamarin.md).

> [!NOTE]
> Olá Cosmos DB SDK .NET da Azure Core utilizado neste tutorial ainda não é compatível com as aplicações da plataforma Universal do Windows (UWP). Para uma versão de pré-visualização de Olá .NET Core SDK que suportam aplicações UWP, enviar correio eletrónico demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

Agora comecemos!

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que tem o seguinte Olá:

* Uma conta ativa do Azure. Se não tiver uma, pode inscrever-se numa [conta gratuita](https://azure.microsoft.com/free/). 
    * Em alternativa, pode utilizar Olá [emulador de BD do Azure Cosmos](local-emulator.md) para este tutorial.
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * Se estiver a trabalhar no MacOS ou Linux, pode desenvolver aplicações de .NET Core a partir da linha de comandos Olá instalando Olá [.NET Core SDK](https://www.microsoft.com/net/core#macos) para a plataforma de Olá à sua escolha. 
    * Se estiver a trabalhar no Windows, pode desenvolver aplicações de .NET Core a partir da linha de comandos Olá instalando Olá [.NET Core SDK](https://www.microsoft.com/net/core#windows). 
    * Pode utilizar o seu próprio editor ou transferir o [Visual Studio Code](https://code.visualstudio.com/), que é gratuito e funciona em Windows, Linux e MacOS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passo 1: Criar uma conta do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se já tiver uma conta que pretende toouse, pode avançar diretamente demasiado[configurar a sua solução do Visual Studio](#SetupVS). Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, siga os passos de Olá em [emulador de BD do Azure Cosmos](local-emulator.md) toosetup Olá emulador e avançar diretamente demasiado[configurar a sua solução do Visual Studio](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Passo 2: Configurar a sua Solução Visual Studio
1. Abra o **Visual Studio 2017** no seu computador.
2. No Olá **ficheiro** menu, selecione **novo**e, em seguida, escolha **projeto**.
3. No Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual c#** / **.NET Core** / **Aplicação de consola (.NET Core)**, nomeie o projeto **DocumentDBGettingStarted**e, em seguida, clique em **OK**.

   ![Captura de ecrã da janela novo projeto de Olá](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. No Olá **Explorador de soluções**, clique em **DocumentDBGettingStarted**.
5. Em seguida, sem sair menu Olá, clique em **gerir pacotes NuGet...** .

   ![Captura de ecrã da direita Olá Clicked Menu para Olá projeto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. No Olá **NuGet** separador, clique em **procurar** em Olá parte superior da janela de Olá e escreva **o azure documentdb** na caixa de pesquisa de Olá.
7. Nos resultados de Olá, localizar **Microsoft.Azure.DocumentDB.Core** e clique em **instalar**.
   ID de pacote Olá Olá biblioteca de clientes do DocumentDB para .NET Core é [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Se tiver como destino uma versão do .NET Framework (como net461) que não é suportada por este pacote.NET Core NuGet, utilize o [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) que suporta todas as versões do .NET Framework, desde o .NET Framework 4.5.
8. Em pedidos de Olá, aceite as instalações de pacotes de NuGet Olá e contrato de licença de Olá.

Ótimo! Agora que Concluímos a configuração de Olá, comecemos a escrever certos códigos. Pode encontrar um projeto de código completo deste tutorial em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a id="Connect"></a>Passo 3: Ligar a conta de base de dados do Azure Cosmos tooan
Primeiro, adicione estes referencia toohello início da sua aplicação c#, no ficheiro Program.cs de Olá:

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> Na ordem toocomplete neste tutorial, certifique-se de que adicionar as dependências de Olá acima.

Agora, adicione estas duas constantes e a sua variável de *Cliente* por baixo do seu *Programa* de classe pública.

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

Em seguida, aceda toohello [Portal do Azure](https://portal.azure.com) tooretrieve seu URI e a chave primária. Olá Azure Cosmos DB URI e a chave primária são necessários para a aplicação toounderstand onde tooconnect e para a base de dados do Azure Cosmos tootrust ligação da sua aplicação.

No Olá Portal do Azure, navegue conta de base de dados do Azure Cosmos tooyour e, em seguida, clique em **chaves**.

Copie Olá URI a partir do portal de Olá e colar na `<your endpoint URI>` no ficheiro program.cs de Olá. Em seguida, Olá chave primária no portal de Olá de copiar e colar na `<your key>`. Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, utilize `https://localhost:8081` como ponto final de Olá e a chave de autorização definida especificamente Olá de [como toodevelop utilizando Olá emulador de BD do Azure Cosmos](local-emulator.md). Certifique-se de que tooremove Olá < e >, mas deixe Olá aspas à volta do ponto final e a chave.

![Captura de ecrã da Olá Portal do Azure utilizado pelo Olá toocreate de tutorial NoSQL uma aplicação de consola c#. Mostra uma base de dados do Azure Cosmos conta, com Olá ACTIVE hub realçado, Olá botão chaves realçado no painel de conta de base de dados do Azure Cosmos Olá e valores de Olá URI, chave primária e chave secundária realçados no Olá painel chaves][keys]

Iremos começar aplicação de introdução Olá criando uma nova instância do Olá **DocumentClient**.

Abaixo Olá **Main** método, adicione esta nova tarefa assíncrona designada **GetStartedDemo**, que irá criar a instância novo **DocumentClient**.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Adicione a seguinte de Olá código toorun a tarefa assíncrona a partir do seu **Main** método. Olá **Main** método irá capturar as exceções e escrevê-las toohello consola.

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

Olá prima **DocumentDBGettingStarted** botão toobuild e executar a aplicação Olá.

Parabéns! Ter ligado com êxito a conta de base de dados do Azure Cosmos tooan, vamos agora observe trabalhar com recursos do Azure Cosmos DB.  

## <a name="step-4-create-a-database"></a>Passo 4: Criar uma base de dados
Antes de adicionar código Olá para criar uma base de dados, adicione um método de programa auxiliar para escrever toohello consola.

Copie e cole Olá **WriteToConsoleAndPromptToContinue** por baixo Olá do método **GetStartedDemo** método.

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

A base de dados do Azure Cosmos [base de dados](documentdb-resources.md#databases) podem ser criados utilizando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método de Olá **DocumentClient** classe. Uma base de dados é o contentor lógico do Olá JSON do armazenamento de documentos particionado em coleções.

Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da criação de cliente Olá do método. Esta ação irá criar uma base de dados designada *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Criou uma base de dados do Azure Cosmos DB com êxito.  

## <a id="CreateColl"></a>Passo 5: Criar uma coleção
> [!WARNING]
> **CreateDocumentCollectionAsync** irá criar uma nova coleção com débito reservado, tendo repercussões sobre os preços. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).

A [coleção](documentdb-resources.md#collections) podem ser criados utilizando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método de Olá **DocumentClient** classe. Uma coleção é um contentor de documentos JSON e a lógica da aplicação associada JavaScript.

Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da criação da base de dados de Olá do método. Desta forma, é criada uma coleção de documentos com o nome *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Criou uma coleção de documentos do Azure Cosmos DB com êxito.  

## <a id="CreateDoc"></a>Passo 6: Criar documentos JSON
A [documento](documentdb-resources.md#documents) podem ser criados utilizando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de Olá **DocumentClient** classe. Os documentos são conteúdos (arbitrários) JSON definidos pelo utilizador. Podemos agora inserir um ou mais documentos. Se já tiver dados que pretende toostore na base de dados, pode utilizar da BD do Azure Cosmos [ferramenta de migração de dados](import-data.md).

Em primeiro lugar, temos toocreate um **família** classe que irá representar objetos armazenados na base de dados do Azure Cosmos neste exemplo. Também iremos criar subclasses **Principal**, **Subordinado**, **Animal de estimação** e **Endereço** utilizadas dentro da **Família**. Tenha em atenção que os documentos têm de ter um **Id** propriedade serializado como **id** no JSON. Crie estas classes ao adicionar Olá seguir internas após Olá **GetStartedDemo** método.

Copie e cole Olá **família**, **principal**, **subordinado**, **animal de estimação**, e **endereço** classes por baixo Olá **WriteToConsoleAndPromptToContinue** método.

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

Copie e cole Olá **CreateFamilyDocumentIfNotExists** por baixo do método sua **CreateDocumentCollectionIfNotExists** método.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

E insira dois documentos, cada um para hello, ou seja família e Olá família Wakefield.

Copie e cole o código de Olá que se segue `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** por baixo da criação de coleção de documentos Olá do método.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Criou dois documentos do Azure Cosmos DB com êxito.  

![Diagrama que ilustra Olá relação hierárquica entre conta Olá, base de dados online Olá, coleção Olá e os documentos de Olá utilizados pelo Olá toocreate de tutorial NoSQL uma aplicação de consola c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Passo 7: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB suporta [consultas](documentdb-sql-query.md) extensas de documentos JSON armazenados em cada coleção.  Olá código de exemplo seguinte mostra várias consultas - utilizando ambas as BD SQL do Azure Cosmos Olá sintaxe, bem como LINQ - que possamos executar contra documentos que são inseridos no passo anterior Olá.

Copie e cole Olá **ExecuteSimpleQuery** por baixo do método sua **CreateFamilyDocumentIfNotExists** método.

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** método por baixo da criação do Olá segundo documento.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Consultou com êxito uma coleção do Azure Cosmos DB.

Olá diagrama seguinte ilustra como consultas de base de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de Olá criou e hello mesma lógica aplica toohello consulta LINQ.

![Diagrama que ilustra o âmbito de Olá e o significado da consulta de Olá utilizado pelo Olá NoSQL tutorial toocreate uma aplicação de consola c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional na consulta de Olá porque as consultas de base de dados do Azure Cosmos já estão confinadas tooa única coleção. Por conseguinte, "FROM Families f" pode ser trocada por "FROM root r" ou qualquer outra variável de nome escolher. O DocumentDB irá inferir que famílias, raiz ou o nome da variável Olá escolheu, referência Olá atual coleção por predefinição.

## <a id="ReplaceDocument"></a>Passo 8: Substituir um documento JSON
O Azure Cosmos DB suporta a substituição de documentos JSON.  

Copie e cole Olá **ReplaceFamilyDocument** por baixo do método sua **ExecuteSimpleQuery** método.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da execução da consulta Olá do método. Depois de substituir o documento de Olá, este irá executar Olá mesmo consultar novamente tooview Olá alterado o documento.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Substituiu documentos do Azure Cosmos DB com êxito.

## <a id="DeleteDocument"></a>Passo 9: Eliminar um documento JSON
O Azure Cosmos DB suporta a eliminação de documentos JSON.  

Copie e cole Olá **DeleteFamilyDocument** por baixo do método sua **ReplaceFamilyDocument** método.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da segunda execução de consulta Olá do método.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Eliminou documentos do Azure Cosmos DB com êxito.

## <a id="DeleteDatabase"></a>Passo 10: Eliminar a base de dados de Olá
A eliminar Olá criada base de dados irá remover a base de dados de Olá e todos os recursos subordinados (coleções, documentos, etc.).

Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo do documento Olá do método eliminar toodelete Olá completa da base de dados e todos os recursos subordinados.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.

Parabéns! Eliminou bases de dados do Azure Cosmos DB com êxito.

## <a id="Run"></a>Passo 11: Executar a sua aplicação de consola C# em conjunto!
Olá prima **DocumentDBGettingStarted** botão na aplicação do Visual Studio toobuild Olá no modo de depuração.

Deverá ver um resultado de Olá da sua aplicação introdução na janela de consola Olá. saída de Olá mostrará Olá os resultados da Olá consultas que adicionámos e deverá corresponder ao texto de exemplo de Olá abaixo.

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

Parabéns! Concluiu o tutorial Olá e ter uma aplicação de consola de c# da trabalho!

## <a id="GetSolution"></a>Obter a solução completa do tutorial Olá
toobuild Olá solução GetStarted que contém todas as amostras de Olá neste artigo, irá necessitar de seguinte Olá:

* Uma conta ativa do Azure. Se não tiver uma, pode inscrever-se numa [conta gratuita](https://azure.microsoft.com/free/).
* Um [conta de base de dados do Azure Cosmos][create-documentdb-dotnet.md#create-account].
* Olá [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solução disponível no GitHub.

toorestore Olá referências toohello API do DocumentDB para Cosmos DB SDK .NET da Azure núcleos no Visual Studio, clique com botão direito Olá **GetStarted** solução no Explorador de soluções e, em seguida, clique **ativar restauro do pacote NuGet**. Em seguida, no ficheiro Program.cs de Olá, atualize os valores EndpointUrl e authorizationkey, de Olá conforme descrito em [ligar a conta de base de dados do Azure Cosmos tooan](#Connect).

## <a name="next-steps"></a>Passos seguintes
* Quer um tutorial ASP.NET MVC mais complexo? Consulte [Tutorial de ASP.NET MVC: programação de aplicações com a base de dados do Azure Cosmos Web](documentdb-dotnet-application.md).
* Pretende toodevelop um Xamarin iOS, Android ou formulários através da aplicação Olá DocumentDB API para o Azure Cosmos DB .NET Core SDK? Consulte [criar aplicações móveis com o Xamarin e base de dados do Azure Cosmos](mobile-apps-with-xamarin.md).
* Pretende tooperform dimensionamento e desempenho testar com a base de dados do Azure Cosmos? Consulte [desempenho e dimensionamento de teste com base de dados do Azure Cosmos](performance-testing.md)
* Saiba como demasiado[pedidos, utilização e armazenamento de base de dados do Monitor Azure Cosmos](monitor-accounts.md).
* Executar consultas no nosso conjunto de dados de exemplo no Olá [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn mais informações sobre o modelo de programação Olá, consulte [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
