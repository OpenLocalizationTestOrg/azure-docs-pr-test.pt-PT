---
title: "aaaGet a utilizar o table storage do Azure e o Visual Studio ligado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado utilizando o table storage do Azure num projeto ASP.NET no Visual Studio depois de se ligar a conta de armazenamento de tooa utilizando o Visual Studio ligado Services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: e7ed17098c8742954972dc9e1b50eca77221e327
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="fd56c-103">Introdução ao table storage do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="fd56c-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="fd56c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="fd56c-104">Overview</span></span>

<span data-ttu-id="fd56c-105">Table storage do Azure permite-lhe toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="fd56c-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="fd56c-106">o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd56c-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="fd56c-107">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="fd56c-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="fd56c-108">Este tutorial mostra como toowrite ASP.NET code para alguns cenários comuns utilizando entidades de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd56c-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="fd56c-109">Estes cenários incluem a criação de uma tabela, adicionar, consultar e eliminar as entidades da tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="fd56c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fd56c-110">Prerequisites</span></span>

* [<span data-ttu-id="fd56c-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd56c-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="fd56c-112">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fd56c-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="fd56c-113">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="fd56c-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="fd56c-114">No Olá **Explorador de soluções**, faça duplo clique **controladores**e, no menu de contexto de Olá, selecione **adicionar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador tooan aplicação ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="fd56c-116">No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC 5 – vazio**e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="fd56c-118">No Olá **Adicionar controlador** caixa de diálogo, o controlador de Olá nome *TablesController*e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Controlador MVC do nome Olá](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="fd56c-120">Adicione Olá seguinte *utilizando* diretivas toohello `TablesController.cs` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="fd56c-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="fd56c-121">Criar uma classe de modelo</span><span class="sxs-lookup"><span data-stu-id="fd56c-121">Create a model class</span></span>

<span data-ttu-id="fd56c-122">Muitos dos exemplos de Olá neste artigo que utilize um **TableEntity**-derivados de classe designado **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="fd56c-123">Olá, os seguintes passos guiá-lo através de declarar esta classe como uma classe de modelo:</span><span class="sxs-lookup"><span data-stu-id="fd56c-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="fd56c-124">No Olá **Explorador de soluções**, faça duplo clique **modelos**e, no menu de contexto de Olá, selecione **adicionar -> classe**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="fd56c-125">No Olá **Adicionar Novo Item** caixa de diálogo, a classe do nome Olá, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="fd56c-126">Abra Olá `CustomerEntity.cs` de ficheiros e adicione o seguinte Olá **utilizando** diretiva:</span><span class="sxs-lookup"><span data-stu-id="fd56c-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="fd56c-127">Modificar a classe de Olá, para que, quando terminar, classe Olá está declarado como Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="fd56c-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="fd56c-128">classe de Olá declara uma classe de entidade chamada **CustomerEntity** que utiliza Olá nome do próprio do cliente como chave de linha de Olá e o apelido como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="fd56c-129">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="fd56c-129">Create a table</span></span>

<span data-ttu-id="fd56c-130">Olá passos seguintes mostram como toocreate uma tabela:</span><span class="sxs-lookup"><span data-stu-id="fd56c-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="fd56c-131">Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="fd56c-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="fd56c-132">Abra Olá `TablesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fd56c-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="fd56c-133">Adicione um método denominado **CreateTable** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="fd56c-134">Dentro do Olá **CreateTable** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd56c-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fd56c-135">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="fd56c-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="fd56c-136">Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="fd56c-137">Obter um **CloudTable** objeto que representa o nome de uma tabela pretendido de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="fd56c-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="fd56c-138">Olá **CloudTableClient.GetTableReference** método não faz um pedido de armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="fd56c-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="fd56c-139">referência de Olá é devolvida se ou não existe Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="fd56c-140">Chamar Olá **CloudTable.CreateIfNotExists** tabela de Olá de toocreate método se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="fd56c-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="fd56c-141">Olá **CloudTable.CreateIfNotExists** método devolve **verdadeiro** se Olá tabela não existe e é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="fd56c-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="fd56c-142">Caso contrário, **falso** é devolvido.</span><span class="sxs-lookup"><span data-stu-id="fd56c-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="fd56c-143">Olá atualização **ViewBag** com o nome de Olá da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="fd56c-144">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="fd56c-145">No Olá **Adicionar vista** caixa de diálogo, introduza **CreateTable** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="fd56c-146">Abra `CreateTable.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd56c-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="fd56c-147">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="fd56c-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="fd56c-148">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="fd56c-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="fd56c-149">Executar a aplicação Olá e selecione **criar tabela** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd56c-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Criar tabela](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="fd56c-151">Como mencionado anteriormente, Olá **CloudTable.CreateIfNotExists** método devolve **verdadeiro** apenas quando a tabela de Olá não existe e é criada.</span><span class="sxs-lookup"><span data-stu-id="fd56c-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="fd56c-152">Por conseguinte, se executar a aplicação Olá quando existe Olá tabela, o método de Olá devolve **falso**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="fd56c-153">aplicação de Olá toorun várias vezes, tem de eliminar tabela Olá antes de executar novamente a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="fd56c-154">A eliminar tabela de Olá pode ser feita através de Olá **CloudTable.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="fd56c-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="fd56c-155">Também pode eliminar tabela Olá utilizando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="fd56c-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="fd56c-156">Adicionar uma tabela de tooa entidade</span><span class="sxs-lookup"><span data-stu-id="fd56c-156">Add an entity tooa table</span></span>

<span data-ttu-id="fd56c-157">*Entidades* mapear tooC\# objetos através de uma classe personalizada derivam de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="fd56c-158">tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de Olá de entidade.</span><span class="sxs-lookup"><span data-stu-id="fd56c-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="fd56c-159">Nesta secção, irá ver como toodefine uma classe de entidade que utiliza Olá nome do próprio do cliente como chave de linha de Olá e o apelido como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="fd56c-160">Em conjunto, a partição de uma entidade e a chave de linha de identificar exclusivamente entidade Olá na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="fd56c-161">As entidades com a mesma chave de partição podem ser consultadas mais rapidamente do que as entidades com chaves de partição diferentes, mas a utilização de várias chaves de partição permite uma maior escalabilidade de operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="fd56c-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="fd56c-162">Para qualquer propriedade que deva ser armazenada no serviço de tabela Olá, propriedade Olá tem de ser uma propriedade pública de um tipo suportado que expõe os definir e obter os valores.</span><span class="sxs-lookup"><span data-stu-id="fd56c-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="fd56c-163">classe de entidade de Olá *tem* declarar um construtor sem parâmetros público.</span><span class="sxs-lookup"><span data-stu-id="fd56c-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="fd56c-164">Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="fd56c-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="fd56c-165">Abra Olá `TablesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fd56c-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="fd56c-166">Adicionar Olá seguir diretiva, de modo que Olá código Olá `TablesController.cs` ficheiros podem aceder Olá **CustomerEntity** classe:</span><span class="sxs-lookup"><span data-stu-id="fd56c-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="fd56c-167">Adicione um método denominado **AddEntity** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="fd56c-168">Dentro do Olá **AddEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd56c-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fd56c-169">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="fd56c-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="fd56c-170">Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="fd56c-171">Obter um **CloudTable** objeto que representa uma tabela de toohello referência toowhich vai nova entidade do tooadd Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="fd56c-172">Instanciar e inicializar Olá **CustomerEntity** classe.</span><span class="sxs-lookup"><span data-stu-id="fd56c-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="fd56c-173">Criar um **TableOperation** objeto insere a entidade de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="fd56c-174">Execute a operação de inserção Olá, chamar Olá **Cloudtable** método.</span><span class="sxs-lookup"><span data-stu-id="fd56c-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="fd56c-175">Pode verificar o resultado de Olá da operação de Olá inspecionando Olá **TableResult.HttpStatusCode** propriedade.</span><span class="sxs-lookup"><span data-stu-id="fd56c-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="fd56c-176">Um código de estado de 2xx indica a ação de Olá pedida pelo cliente de Olá foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="fd56c-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="fd56c-177">Por exemplo, com êxito inserções de novas entidades origina um código de estado HTTP de 204, que significa que a operação de Olá foi processada com êxito e servidor Olá não devolveu qualquer conteúdo.</span><span class="sxs-lookup"><span data-stu-id="fd56c-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="fd56c-178">Olá atualização **ViewBag** com o nome da tabela Olá e Olá os resultados da operação de inserção de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="fd56c-179">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="fd56c-180">No Olá **Adicionar vista** caixa de diálogo, introduza **AddEntity** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="fd56c-181">Abra `AddEntity.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd56c-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="fd56c-182">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="fd56c-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="fd56c-183">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="fd56c-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="fd56c-184">Executar a aplicação Olá e selecione **adicionar entidade** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd56c-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Adicionar entidade](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="fd56c-186">Pode verificar se a entidade de Olá foi adicionada ao seguir os passos de Olá na secção de Olá, [obter uma única entidade](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="fd56c-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="fd56c-187">Também pode utilizar Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview Olá todas as entidades para as suas tabelas.</span><span class="sxs-lookup"><span data-stu-id="fd56c-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="fd56c-188">Adicionar um lote de tabela de tooa de entidades</span><span class="sxs-lookup"><span data-stu-id="fd56c-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="fd56c-189">Na adição toobeing capaz de demasiado[adicionar uma tabela de tooa de entidade um cada vez](#add-an-entity-to-a-table), também pode adicionar entidades no batch.</span><span class="sxs-lookup"><span data-stu-id="fd56c-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="fd56c-190">A adição de entidades no batch reduz o número de Olá de ida e volta entre o seu código e Olá serviço tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd56c-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="fd56c-191">Olá, os passos seguintes ilustram como tooadd várias entidades tooa de tabela com uma operação de inserção único:</span><span class="sxs-lookup"><span data-stu-id="fd56c-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="fd56c-192">Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="fd56c-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="fd56c-193">Abra Olá `TablesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fd56c-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="fd56c-194">Adicione um método denominado **AddEntities** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="fd56c-195">Dentro do Olá **AddEntities** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd56c-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fd56c-196">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="fd56c-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="fd56c-197">Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="fd56c-198">Obter um **CloudTable** objeto que representa uma tabela de toohello referência toowhich são novas entidades de contínuo tooadd Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="fd56c-199">Instanciar alguns objetos de cliente com base no Olá **CustomerEntity** classe apresentado na secção de Olá, de modelo [adicionar uma tabela de tooa entidade](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="fd56c-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="fd56c-200">Obter um **TableBatchOperation** objeto.</span><span class="sxs-lookup"><span data-stu-id="fd56c-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="fd56c-201">Adicione o objeto de operação de inserção de lote toohello entidades.</span><span class="sxs-lookup"><span data-stu-id="fd56c-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="fd56c-202">Execute a operação de inserção de lote de Olá, chamar Olá **CloudTable.ExecuteBatch** método.</span><span class="sxs-lookup"><span data-stu-id="fd56c-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="fd56c-203">Olá **CloudTable.ExecuteBatch** método devolve uma lista de **TableResult** objetos onde cada **TableResult** objeto pode ser examinadas toodetermine Olá êxito ou falha de cada operação individual.</span><span class="sxs-lookup"><span data-stu-id="fd56c-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="fd56c-204">Para este exemplo, transmita Olá lista tooa de vista e permitir que a vista de Olá apresentar Olá resultados de cada operação.</span><span class="sxs-lookup"><span data-stu-id="fd56c-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="fd56c-205">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="fd56c-206">No Olá **Adicionar vista** caixa de diálogo, introduza **AddEntities** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="fd56c-207">Abra `AddEntities.cshtml`e modificá-lo de modo a que se parece com Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="fd56c-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="fd56c-208">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="fd56c-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="fd56c-209">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="fd56c-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="fd56c-210">Executar a aplicação Olá e selecione **adicionar entidades** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd56c-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Adicionar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="fd56c-212">Pode verificar se a entidade de Olá foi adicionada ao seguir os passos de Olá na secção de Olá, [obter uma única entidade](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="fd56c-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="fd56c-213">Também pode utilizar Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview Olá todas as entidades para as suas tabelas.</span><span class="sxs-lookup"><span data-stu-id="fd56c-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="fd56c-214">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="fd56c-214">Get a single entity</span></span>

<span data-ttu-id="fd56c-215">Esta secção ilustra como tooget uma única entidade a partir de uma tabela utilizando Olá chave da fila e a chave de partição da entidade.</span><span class="sxs-lookup"><span data-stu-id="fd56c-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="fd56c-216">Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment)e utiliza dados dos [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="fd56c-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="fd56c-217">Abra Olá `TablesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fd56c-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="fd56c-218">Adicione um método denominado **GetSingle** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="fd56c-219">Dentro do Olá **GetSingle** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd56c-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fd56c-220">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="fd56c-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="fd56c-221">Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="fd56c-222">Obter um **CloudTable** objeto que representa uma tabela de toohello referência partir da qual estão a obter a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="fd56c-223">Criar um objeto de operação de obtenção pega num objeto de entidade derivado **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="fd56c-224">Step-by-Olá primeiro parâmetro é Olá *partitionKey*, e o segundo parâmetro de Olá é Olá *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="fd56c-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="fd56c-225">Utilizar Olá **CustomerEntity** classe e os dados apresentados na secção de Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), Olá seguintes tabela da Olá de consultas de fragmento de código para um **CustomerEntity** entidade com uma *partitionKey* valor de "Santos" e um *rowKey* valor de "Bernardo":</span><span class="sxs-lookup"><span data-stu-id="fd56c-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="fd56c-226">Execute a operação de obtenção de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="fd56c-227">Passe Olá resultado toohello da vista apresentação.</span><span class="sxs-lookup"><span data-stu-id="fd56c-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="fd56c-228">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="fd56c-229">No Olá **Adicionar vista** caixa de diálogo, introduza **GetSingle** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="fd56c-230">Abra `GetSingle.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd56c-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="fd56c-231">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="fd56c-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="fd56c-232">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="fd56c-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="fd56c-233">Executar a aplicação Olá e selecione **obter único** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd56c-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter único](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="fd56c-235">Obter todas as entidades numa partição</span><span class="sxs-lookup"><span data-stu-id="fd56c-235">Get all entities in a partition</span></span>

<span data-ttu-id="fd56c-236">Tal como mencionado na secção de Olá, [adicionar uma tabela de tooa entidade](#add-an-entity-to-a-table), combinação de Olá de uma partição e uma chave de linha identificar exclusivamente uma entidade numa tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="fd56c-237">Entidades com a mesma chave de partição podem ser consultadas mais rapidamente do que as entidades com chaves de partição diferentes.</span><span class="sxs-lookup"><span data-stu-id="fd56c-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="fd56c-238">Esta secção ilustra como tooquery uma tabela para todas as entidades de Olá de uma partição especificada.</span><span class="sxs-lookup"><span data-stu-id="fd56c-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="fd56c-239">Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment)e utiliza dados dos [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="fd56c-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="fd56c-240">Abra Olá `TablesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fd56c-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="fd56c-241">Adicione um método denominado **GetPartition** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="fd56c-242">Dentro do Olá **GetPartition** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd56c-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fd56c-243">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="fd56c-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="fd56c-244">Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="fd56c-245">Obter um **CloudTable** objeto que representa uma tabela de toohello referência partir da qual estão a obter entidades Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="fd56c-246">Instanciar um **TableQuery** objeto a especificação de consulta Olá Olá **onde** cláusula.</span><span class="sxs-lookup"><span data-stu-id="fd56c-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="fd56c-247">Utilizar Olá **CustomerEntity** classe e os dados apresentados na secção de Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), tabela Olá de consultas de fragmento para uma todas as entidades de código seguinte Olá, onde Olá  **PartitionKey** (apelido do cliente) tem um valor de "Santos":</span><span class="sxs-lookup"><span data-stu-id="fd56c-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="fd56c-248">Dentro de um ciclo, chamar Olá **CloudTable.ExecuteQuerySegmented** método transmitir o objeto da consulta Olá que instanciado no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="fd56c-249">Olá **CloudTable.ExecuteQuerySegmented** método devolve um **TableContinuationToken** objeto que - quando **nulo** -indica que existem não existem mais entidades tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="fd56c-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="fd56c-250">Dentro do ciclo de Olá, utilize outro tooiterate de ciclo através de Olá devolvido entidades.</span><span class="sxs-lookup"><span data-stu-id="fd56c-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="fd56c-251">No seguinte exemplo de código de Olá, cada entidade devolvida é adicionada tooa lista.</span><span class="sxs-lookup"><span data-stu-id="fd56c-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="fd56c-252">Uma vez Olá extremidades do ciclo, lista de Olá é transmitida tooa vista para apresentar:</span><span class="sxs-lookup"><span data-stu-id="fd56c-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="fd56c-253">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="fd56c-254">No Olá **Adicionar vista** caixa de diálogo, introduza **GetPartition** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="fd56c-255">Abra `GetPartition.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd56c-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="fd56c-256">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="fd56c-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="fd56c-257">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="fd56c-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="fd56c-258">Executar a aplicação Olá e selecione **obter partição** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd56c-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter a partição](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="fd56c-260">Eliminar uma entidade</span><span class="sxs-lookup"><span data-stu-id="fd56c-260">Delete an entity</span></span>

<span data-ttu-id="fd56c-261">Esta secção ilustra como toodelete uma entidade a partir de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="fd56c-262">Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment)e utiliza dados dos [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="fd56c-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="fd56c-263">Abra Olá `TablesController.cs` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fd56c-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="fd56c-264">Adicione um método denominado **DeleteEntity** que devolve um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="fd56c-265">Dentro do Olá **DeleteEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd56c-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fd56c-266">Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)</span><span class="sxs-lookup"><span data-stu-id="fd56c-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="fd56c-267">Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.</span><span class="sxs-lookup"><span data-stu-id="fd56c-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="fd56c-268">Obter um **CloudTable** objeto que representa uma tabela de toohello referência partir do qual está a eliminar a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="fd56c-269">Criar um objeto de operação de eliminação demora um objeto de entidade derivado **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="fd56c-270">Neste caso, vamos utilizar Olá **CustomerEntity** classe e os dados apresentados na secção de Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="fd56c-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="fd56c-271">Olá da entidade **ETag** tem de ser definido um valor válido de tooa.</span><span class="sxs-lookup"><span data-stu-id="fd56c-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="fd56c-272">Execute a operação de eliminação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fd56c-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="fd56c-273">Passe Olá resultado toohello da vista apresentação.</span><span class="sxs-lookup"><span data-stu-id="fd56c-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="fd56c-274">No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="fd56c-275">No Olá **Adicionar vista** caixa de diálogo, introduza **DeleteEntity** para nome da vista Olá e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fd56c-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="fd56c-276">Abra `DeleteEntity.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd56c-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="fd56c-277">No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="fd56c-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="fd56c-278">Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="fd56c-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="fd56c-279">Executar a aplicação Olá e selecione **eliminar entidade** toosee resulta toohello semelhante captura de ecrã a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd56c-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter único](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="fd56c-281">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fd56c-281">Next steps</span></span>
<span data-ttu-id="fd56c-282">Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="fd56c-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="fd56c-283">Introdução ao blob storage do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="fd56c-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="fd56c-284">Introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="fd56c-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
