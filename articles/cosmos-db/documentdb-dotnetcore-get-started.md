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
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="d531a-103">Azure Cosmos DB: Introdução Olá API do DocumentDB e .NET Core</span><span class="sxs-lookup"><span data-stu-id="d531a-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d531a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d531a-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="d531a-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d531a-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="d531a-106">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="d531a-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="d531a-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="d531a-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="d531a-108">Java</span><span class="sxs-lookup"><span data-stu-id="d531a-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="d531a-109">C++</span><span class="sxs-lookup"><span data-stu-id="d531a-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="d531a-110">Bem-vindo toohello DocumentDB API para Azure Cosmos DB introdução tutorial de .NET Core!</span><span class="sxs-lookup"><span data-stu-id="d531a-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="d531a-111">Depois de seguir este tutorial, terá de uma aplicação de consola que cria e consulta recursos do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d531a-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="d531a-112">Iremos abranger:</span><span class="sxs-lookup"><span data-stu-id="d531a-112">We'll cover:</span></span>

* <span data-ttu-id="d531a-113">Criar e ligar-se a conta de base de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="d531a-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="d531a-114">Configuração da sua Solução Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d531a-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="d531a-115">Criação de uma base de dados online</span><span class="sxs-lookup"><span data-stu-id="d531a-115">Creating an online database</span></span>
* <span data-ttu-id="d531a-116">Criação de uma coleção</span><span class="sxs-lookup"><span data-stu-id="d531a-116">Creating a collection</span></span>
* <span data-ttu-id="d531a-117">Criação de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="d531a-117">Creating JSON documents</span></span>
* <span data-ttu-id="d531a-118">Consulta de coleção de Olá</span><span class="sxs-lookup"><span data-stu-id="d531a-118">Querying hello collection</span></span>
* <span data-ttu-id="d531a-119">Substituir um documento</span><span class="sxs-lookup"><span data-stu-id="d531a-119">Replacing a document</span></span>
* <span data-ttu-id="d531a-120">Eliminar um documento</span><span class="sxs-lookup"><span data-stu-id="d531a-120">Deleting a document</span></span>
* <span data-ttu-id="d531a-121">Eliminar Olá base de dados</span><span class="sxs-lookup"><span data-stu-id="d531a-121">Deleting hello database</span></span>

<span data-ttu-id="d531a-122">Não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="d531a-122">Don't have time?</span></span> <span data-ttu-id="d531a-123">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="d531a-123">Don't worry!</span></span> <span data-ttu-id="d531a-124">solução completa de Olá está disponível no [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d531a-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="d531a-125">Ir toohello [obter a secção de solução completa de Olá](#GetSolution) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="d531a-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="d531a-126">Pretende toobuild um Xamarin iOS, Android ou formulários através da aplicação Olá API do DocumentDB e SDK do .NET Core?</span><span class="sxs-lookup"><span data-stu-id="d531a-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="d531a-127">Consulte [criar aplicações móveis com o Xamarin e base de dados do Azure Cosmos](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="d531a-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d531a-128">Olá Cosmos DB SDK .NET da Azure Core utilizado neste tutorial ainda não é compatível com as aplicações da plataforma Universal do Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="d531a-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="d531a-129">Para uma versão de pré-visualização de Olá .NET Core SDK que suportam aplicações UWP, enviar correio eletrónico demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d531a-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="d531a-130">Agora comecemos!</span><span class="sxs-lookup"><span data-stu-id="d531a-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d531a-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d531a-131">Prerequisites</span></span>
<span data-ttu-id="d531a-132">Certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="d531a-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="d531a-133">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d531a-133">An active Azure account.</span></span> <span data-ttu-id="d531a-134">Se não tiver uma, pode inscrever-se numa [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d531a-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="d531a-135">Em alternativa, pode utilizar Olá [emulador de BD do Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d531a-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="d531a-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d531a-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="d531a-137">Se estiver a trabalhar no MacOS ou Linux, pode desenvolver aplicações de .NET Core a partir da linha de comandos Olá instalando Olá [.NET Core SDK](https://www.microsoft.com/net/core#macos) para a plataforma de Olá à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d531a-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="d531a-138">Se estiver a trabalhar no Windows, pode desenvolver aplicações de .NET Core a partir da linha de comandos Olá instalando Olá [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="d531a-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="d531a-139">Pode utilizar o seu próprio editor ou transferir o [Visual Studio Code](https://code.visualstudio.com/), que é gratuito e funciona em Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="d531a-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="d531a-140">Passo 1: Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d531a-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="d531a-141">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d531a-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="d531a-142">Se já tiver uma conta que pretende toouse, pode avançar diretamente demasiado[configurar a sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d531a-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="d531a-143">Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, siga os passos de Olá em [emulador de BD do Azure Cosmos](local-emulator.md) toosetup Olá emulador e avançar diretamente demasiado[configurar a sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d531a-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="d531a-144"><a id="SetupVS"></a>Passo 2: Configurar a sua Solução Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d531a-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="d531a-145">Abra o **Visual Studio 2017** no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d531a-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="d531a-146">No Olá **ficheiro** menu, selecione **novo**e, em seguida, escolha **projeto**.</span><span class="sxs-lookup"><span data-stu-id="d531a-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="d531a-147">No Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual c#** / **.NET Core** / **Aplicação de consola (.NET Core)**, nomeie o projeto **DocumentDBGettingStarted**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d531a-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Captura de ecrã da janela novo projeto de Olá](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="d531a-149">No Olá **Explorador de soluções**, clique em **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="d531a-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="d531a-150">Em seguida, sem sair menu Olá, clique em **gerir pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d531a-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Captura de ecrã da direita Olá Clicked Menu para Olá projeto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="d531a-152">No Olá **NuGet** separador, clique em **procurar** em Olá parte superior da janela de Olá e escreva **o azure documentdb** na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="d531a-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="d531a-153">Nos resultados de Olá, localizar **Microsoft.Azure.DocumentDB.Core** e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="d531a-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="d531a-154">ID de pacote Olá Olá biblioteca de clientes do DocumentDB para .NET Core é [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="d531a-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="d531a-155">Se tiver como destino uma versão do .NET Framework (como net461) que não é suportada por este pacote.NET Core NuGet, utilize o [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) que suporta todas as versões do .NET Framework, desde o .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d531a-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="d531a-156">Em pedidos de Olá, aceite as instalações de pacotes de NuGet Olá e contrato de licença de Olá.</span><span class="sxs-lookup"><span data-stu-id="d531a-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="d531a-157">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="d531a-157">Great!</span></span> <span data-ttu-id="d531a-158">Agora que Concluímos a configuração de Olá, comecemos a escrever certos códigos.</span><span class="sxs-lookup"><span data-stu-id="d531a-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="d531a-159">Pode encontrar um projeto de código completo deste tutorial em [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d531a-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="d531a-160"><a id="Connect"></a>Passo 3: Ligar a conta de base de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="d531a-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="d531a-161">Primeiro, adicione estes referencia toohello início da sua aplicação c#, no ficheiro Program.cs de Olá:</span><span class="sxs-lookup"><span data-stu-id="d531a-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

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
> <span data-ttu-id="d531a-162">Na ordem toocomplete neste tutorial, certifique-se de que adicionar as dependências de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="d531a-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="d531a-163">Agora, adicione estas duas constantes e a sua variável de *Cliente* por baixo do seu *Programa* de classe pública.</span><span class="sxs-lookup"><span data-stu-id="d531a-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="d531a-164">Em seguida, aceda toohello [Portal do Azure](https://portal.azure.com) tooretrieve seu URI e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="d531a-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="d531a-165">Olá Azure Cosmos DB URI e a chave primária são necessários para a aplicação toounderstand onde tooconnect e para a base de dados do Azure Cosmos tootrust ligação da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="d531a-166">No Olá Portal do Azure, navegue conta de base de dados do Azure Cosmos tooyour e, em seguida, clique em **chaves**.</span><span class="sxs-lookup"><span data-stu-id="d531a-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="d531a-167">Copie Olá URI a partir do portal de Olá e colar na `<your endpoint URI>` no ficheiro program.cs de Olá.</span><span class="sxs-lookup"><span data-stu-id="d531a-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="d531a-168">Em seguida, Olá chave primária no portal de Olá de copiar e colar na `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="d531a-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="d531a-169">Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, utilize `https://localhost:8081` como ponto final de Olá e a chave de autorização definida especificamente Olá de [como toodevelop utilizando Olá emulador de BD do Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="d531a-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="d531a-170">Certifique-se de que tooremove Olá < e >, mas deixe Olá aspas à volta do ponto final e a chave.</span><span class="sxs-lookup"><span data-stu-id="d531a-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Captura de ecrã da Olá Portal do Azure utilizado pelo Olá toocreate de tutorial NoSQL uma aplicação de consola c#.][keys]

<span data-ttu-id="d531a-173">Iremos começar aplicação de introdução Olá criando uma nova instância do Olá **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d531a-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="d531a-174">Abaixo Olá **Main** método, adicione esta nova tarefa assíncrona designada **GetStartedDemo**, que irá criar a instância novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d531a-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

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

<span data-ttu-id="d531a-175">Adicione a seguinte de Olá código toorun a tarefa assíncrona a partir do seu **Main** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="d531a-176">Olá **Main** método irá capturar as exceções e escrevê-las toohello consola.</span><span class="sxs-lookup"><span data-stu-id="d531a-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="d531a-177">Olá prima **DocumentDBGettingStarted** botão toobuild e executar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d531a-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="d531a-178">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-178">Congratulations!</span></span> <span data-ttu-id="d531a-179">Ter ligado com êxito a conta de base de dados do Azure Cosmos tooan, vamos agora observe trabalhar com recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d531a-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="d531a-180">Passo 4: Criar uma base de dados</span><span class="sxs-lookup"><span data-stu-id="d531a-180">Step 4: Create a database</span></span>
<span data-ttu-id="d531a-181">Antes de adicionar código Olá para criar uma base de dados, adicione um método de programa auxiliar para escrever toohello consola.</span><span class="sxs-lookup"><span data-stu-id="d531a-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="d531a-182">Copie e cole Olá **WriteToConsoleAndPromptToContinue** por baixo Olá do método **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="d531a-183">A base de dados do Azure Cosmos [base de dados](documentdb-resources.md#databases) podem ser criados utilizando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método de Olá **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="d531a-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="d531a-184">Uma base de dados é o contentor lógico do Olá JSON do armazenamento de documentos particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="d531a-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="d531a-185">Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da criação de cliente Olá do método.</span><span class="sxs-lookup"><span data-stu-id="d531a-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="d531a-186">Esta ação irá criar uma base de dados designada *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="d531a-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="d531a-187">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-188">Congratulations!</span></span> <span data-ttu-id="d531a-189">Criou uma base de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d531a-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="d531a-190"><a id="CreateColl"></a>Passo 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="d531a-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="d531a-191">**CreateDocumentCollectionAsync** irá criar uma nova coleção com débito reservado, tendo repercussões sobre os preços.</span><span class="sxs-lookup"><span data-stu-id="d531a-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="d531a-192">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d531a-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="d531a-193">A [coleção](documentdb-resources.md#collections) podem ser criados utilizando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método de Olá **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="d531a-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="d531a-194">Uma coleção é um contentor de documentos JSON e a lógica da aplicação associada JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d531a-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="d531a-195">Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da criação da base de dados de Olá do método.</span><span class="sxs-lookup"><span data-stu-id="d531a-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="d531a-196">Desta forma, é criada uma coleção de documentos com o nome *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="d531a-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="d531a-197">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-198">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-198">Congratulations!</span></span> <span data-ttu-id="d531a-199">Criou uma coleção de documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d531a-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="d531a-200"><a id="CreateDoc"></a>Passo 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="d531a-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="d531a-201">A [documento](documentdb-resources.md#documents) podem ser criados utilizando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de Olá **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="d531a-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="d531a-202">Os documentos são conteúdos (arbitrários) JSON definidos pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="d531a-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="d531a-203">Podemos agora inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="d531a-203">We can now insert one or more documents.</span></span> <span data-ttu-id="d531a-204">Se já tiver dados que pretende toostore na base de dados, pode utilizar da BD do Azure Cosmos [ferramenta de migração de dados](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="d531a-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="d531a-205">Em primeiro lugar, temos toocreate um **família** classe que irá representar objetos armazenados na base de dados do Azure Cosmos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="d531a-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="d531a-206">Também iremos criar subclasses **Principal**, **Subordinado**, **Animal de estimação** e **Endereço** utilizadas dentro da **Família**.</span><span class="sxs-lookup"><span data-stu-id="d531a-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="d531a-207">Tenha em atenção que os documentos têm de ter um **Id** propriedade serializado como **id** no JSON.</span><span class="sxs-lookup"><span data-stu-id="d531a-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="d531a-208">Crie estas classes ao adicionar Olá seguir internas após Olá **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="d531a-209">Copie e cole Olá **família**, **principal**, **subordinado**, **animal de estimação**, e **endereço** classes por baixo Olá **WriteToConsoleAndPromptToContinue** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="d531a-210">Copie e cole Olá **CreateFamilyDocumentIfNotExists** por baixo do método sua **CreateDocumentCollectionIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

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

<span data-ttu-id="d531a-211">E insira dois documentos, cada um para hello, ou seja família e Olá família Wakefield.</span><span class="sxs-lookup"><span data-stu-id="d531a-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="d531a-212">Copie e cole o código de Olá que se segue `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** por baixo da criação de coleção de documentos Olá do método.</span><span class="sxs-lookup"><span data-stu-id="d531a-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

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

<span data-ttu-id="d531a-213">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-214">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-214">Congratulations!</span></span> <span data-ttu-id="d531a-215">Criou dois documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d531a-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que ilustra Olá relação hierárquica entre conta Olá, base de dados online Olá, coleção Olá e os documentos de Olá utilizados pelo Olá toocreate de tutorial NoSQL uma aplicação de consola c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="d531a-217"><a id="Query"></a>Passo 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d531a-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="d531a-218">O Azure Cosmos DB suporta [consultas](documentdb-sql-query.md) extensas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="d531a-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="d531a-219">Olá código de exemplo seguinte mostra várias consultas - utilizando ambas as BD SQL do Azure Cosmos Olá sintaxe, bem como LINQ - que possamos executar contra documentos que são inseridos no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="d531a-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="d531a-220">Copie e cole Olá **ExecuteSimpleQuery** por baixo do método sua **CreateFamilyDocumentIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="d531a-221">Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** método por baixo da criação do Olá segundo documento.</span><span class="sxs-lookup"><span data-stu-id="d531a-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="d531a-222">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-223">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-223">Congratulations!</span></span> <span data-ttu-id="d531a-224">Consultou com êxito uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d531a-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="d531a-225">Olá diagrama seguinte ilustra como consultas de base de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de Olá criou e hello mesma lógica aplica toohello consulta LINQ.</span><span class="sxs-lookup"><span data-stu-id="d531a-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagrama que ilustra o âmbito de Olá e o significado da consulta de Olá utilizado pelo Olá NoSQL tutorial toocreate uma aplicação de consola c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="d531a-227">Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional na consulta de Olá porque as consultas de base de dados do Azure Cosmos já estão confinadas tooa única coleção.</span><span class="sxs-lookup"><span data-stu-id="d531a-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="d531a-228">Por conseguinte, "FROM Families f" pode ser trocada por "FROM root r" ou qualquer outra variável de nome escolher.</span><span class="sxs-lookup"><span data-stu-id="d531a-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="d531a-229">O DocumentDB irá inferir que famílias, raiz ou o nome da variável Olá escolheu, referência Olá atual coleção por predefinição.</span><span class="sxs-lookup"><span data-stu-id="d531a-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="d531a-230"><a id="ReplaceDocument"></a>Passo 8: Substituir um documento JSON</span><span class="sxs-lookup"><span data-stu-id="d531a-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="d531a-231">O Azure Cosmos DB suporta a substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d531a-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="d531a-232">Copie e cole Olá **ReplaceFamilyDocument** por baixo do método sua **ExecuteSimpleQuery** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

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

<span data-ttu-id="d531a-233">Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da execução da consulta Olá do método.</span><span class="sxs-lookup"><span data-stu-id="d531a-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="d531a-234">Depois de substituir o documento de Olá, este irá executar Olá mesmo consultar novamente tooview Olá alterado o documento.</span><span class="sxs-lookup"><span data-stu-id="d531a-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="d531a-235">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-236">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-236">Congratulations!</span></span> <span data-ttu-id="d531a-237">Substituiu documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d531a-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="d531a-238"><a id="DeleteDocument"></a>Passo 9: Eliminar um documento JSON</span><span class="sxs-lookup"><span data-stu-id="d531a-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="d531a-239">O Azure Cosmos DB suporta a eliminação de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d531a-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="d531a-240">Copie e cole Olá **DeleteFamilyDocument** por baixo do método sua **ReplaceFamilyDocument** método.</span><span class="sxs-lookup"><span data-stu-id="d531a-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

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

<span data-ttu-id="d531a-241">Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo da segunda execução de consulta Olá do método.</span><span class="sxs-lookup"><span data-stu-id="d531a-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="d531a-242">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-243">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-243">Congratulations!</span></span> <span data-ttu-id="d531a-244">Eliminou documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d531a-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="d531a-245"><a id="DeleteDatabase"></a>Passo 10: Eliminar a base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="d531a-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="d531a-246">A eliminar Olá criada base de dados irá remover a base de dados de Olá e todos os recursos subordinados (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="d531a-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="d531a-247">Copiar e colar seguinte de Olá code tooyour **GetStartedDemo** por baixo do documento Olá do método eliminar toodelete Olá completa da base de dados e todos os recursos subordinados.</span><span class="sxs-lookup"><span data-stu-id="d531a-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="d531a-248">Olá prima **DocumentDBGettingStarted** botão toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="d531a-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="d531a-249">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-249">Congratulations!</span></span> <span data-ttu-id="d531a-250">Eliminou bases de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="d531a-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="d531a-251"><a id="Run"></a>Passo 11: Executar a sua aplicação de consola C# em conjunto!</span><span class="sxs-lookup"><span data-stu-id="d531a-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="d531a-252">Olá prima **DocumentDBGettingStarted** botão na aplicação do Visual Studio toobuild Olá no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="d531a-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="d531a-253">Deverá ver um resultado de Olá da sua aplicação introdução na janela de consola Olá.</span><span class="sxs-lookup"><span data-stu-id="d531a-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="d531a-254">saída de Olá mostrará Olá os resultados da Olá consultas que adicionámos e deverá corresponder ao texto de exemplo de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="d531a-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

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

<span data-ttu-id="d531a-255">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d531a-255">Congratulations!</span></span> <span data-ttu-id="d531a-256">Concluiu o tutorial Olá e ter uma aplicação de consola de c# da trabalho!</span><span class="sxs-lookup"><span data-stu-id="d531a-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="d531a-257"><a id="GetSolution"></a>Obter a solução completa do tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="d531a-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="d531a-258">toobuild Olá solução GetStarted que contém todas as amostras de Olá neste artigo, irá necessitar de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="d531a-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="d531a-259">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d531a-259">An active Azure account.</span></span> <span data-ttu-id="d531a-260">Se não tiver uma, pode inscrever-se numa [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d531a-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d531a-261">Um [conta de base de dados do Azure Cosmos][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="d531a-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="d531a-262">Olá [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solução disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d531a-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="d531a-263">toorestore Olá referências toohello API do DocumentDB para Cosmos DB SDK .NET da Azure núcleos no Visual Studio, clique com botão direito Olá **GetStarted** solução no Explorador de soluções e, em seguida, clique **ativar restauro do pacote NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d531a-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="d531a-264">Em seguida, no ficheiro Program.cs de Olá, atualize os valores EndpointUrl e authorizationkey, de Olá conforme descrito em [ligar a conta de base de dados do Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="d531a-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d531a-265">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d531a-265">Next steps</span></span>
* <span data-ttu-id="d531a-266">Quer um tutorial ASP.NET MVC mais complexo?</span><span class="sxs-lookup"><span data-stu-id="d531a-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="d531a-267">Consulte [Tutorial de ASP.NET MVC: programação de aplicações com a base de dados do Azure Cosmos Web](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="d531a-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="d531a-268">Pretende toodevelop um Xamarin iOS, Android ou formulários através da aplicação Olá DocumentDB API para o Azure Cosmos DB .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="d531a-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="d531a-269">Consulte [criar aplicações móveis com o Xamarin e base de dados do Azure Cosmos](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="d531a-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="d531a-270">Pretende tooperform dimensionamento e desempenho testar com a base de dados do Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="d531a-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="d531a-271">Consulte [desempenho e dimensionamento de teste com base de dados do Azure Cosmos](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="d531a-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="d531a-272">Saiba como demasiado[pedidos, utilização e armazenamento de base de dados do Monitor Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="d531a-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="d531a-273">Executar consultas no nosso conjunto de dados de exemplo no Olá [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="d531a-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="d531a-274">toolearn mais informações sobre o modelo de programação Olá, consulte [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d531a-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
