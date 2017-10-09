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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Introdução ao table storage do Azure e o Visual Studio ligado serviços (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Descrição geral

Table storage do Azure permite-lhe toostore grandes quantidades de dados estruturados. o serviço de Olá é um arquivo de dados NoSQL que aceita chamadas autenticadas de dentro e fora Olá em nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

Este tutorial mostra como toowrite ASP.NET code para alguns cenários comuns utilizando entidades de armazenamento de tabela do Azure. Estes cenários incluem a criação de uma tabela, adicionar, consultar e eliminar as entidades da tabela. 

##<a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Conta de armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Criar um controlador MVC 

1. No Olá **Explorador de soluções**, faça duplo clique **controladores**e, no menu de contexto de Olá, selecione **adicionar -> controlador**.

    ![Adicionar um controlador tooan aplicação ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC 5 – vazio**e selecione **adicionar**.

    ![Especifique o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. No Olá **Adicionar controlador** caixa de diálogo, o controlador de Olá nome *TablesController*e selecione **adicionar**.

    ![Controlador MVC do nome Olá](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Adicione Olá seguinte *utilizando* diretivas toohello `TablesController.cs` ficheiro:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Criar uma classe de modelo

Muitos dos exemplos de Olá neste artigo que utilize um **TableEntity**-derivados de classe designado **CustomerEntity**. Olá, os seguintes passos guiá-lo através de declarar esta classe como uma classe de modelo:

1. No Olá **Explorador de soluções**, faça duplo clique **modelos**e, no menu de contexto de Olá, selecione **adicionar -> classe**.

1. No Olá **Adicionar Novo Item** caixa de diálogo, a classe do nome Olá, **CustomerEntity**.

1. Abra Olá `CustomerEntity.cs` de ficheiros e adicione o seguinte Olá **utilizando** diretiva:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Modificar a classe de Olá, para que, quando terminar, classe Olá está declarado como Olá seguinte código. classe de Olá declara uma classe de entidade chamada **CustomerEntity** que utiliza Olá nome do próprio do cliente como chave de linha de Olá e o apelido como chave de partição Olá.

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

## <a name="create-a-table"></a>Criar uma tabela

Olá passos seguintes mostram como toocreate uma tabela:

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment). 

1. Abra Olá `TablesController.cs` ficheiro.

1. Adicione um método denominado **CreateTable** que devolve um **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **CreateTable** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa o nome de uma tabela pretendido de toohello de referência. Olá **CloudTableClient.GetTableReference** método não faz um pedido de armazenamento de tabelas. referência de Olá é devolvida se ou não existe Olá tabela. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Chamar Olá **CloudTable.CreateIfNotExists** tabela de Olá de toocreate método se ainda não existir. Olá **CloudTable.CreateIfNotExists** método devolve **verdadeiro** se Olá tabela não existe e é criada com êxito. Caso contrário, **falso** é devolvido.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Olá atualização **ViewBag** com o nome de Olá da tabela de Olá.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **CreateTable** para nome da vista Olá e selecione **adicionar**.

1. Abra `CreateTable.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Executar a aplicação Olá e selecione **criar tabela** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Criar tabela](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Como mencionado anteriormente, Olá **CloudTable.CreateIfNotExists** método devolve **verdadeiro** apenas quando a tabela de Olá não existe e é criada. Por conseguinte, se executar a aplicação Olá quando existe Olá tabela, o método de Olá devolve **falso**. aplicação de Olá toorun várias vezes, tem de eliminar tabela Olá antes de executar novamente a aplicação Olá. A eliminar tabela de Olá pode ser feita através de Olá **CloudTable.Delete** método. Também pode eliminar tabela Olá utilizando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de tooa entidade

*Entidades* mapear tooC\# objetos através de uma classe personalizada derivam de **TableEntity**. tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de Olá de entidade. Nesta secção, irá ver como toodefine uma classe de entidade que utiliza Olá nome do próprio do cliente como chave de linha de Olá e o apelido como chave de partição Olá. Em conjunto, a partição de uma entidade e a chave de linha de identificar exclusivamente entidade Olá na tabela de Olá. As entidades com a mesma chave de partição podem ser consultadas mais rapidamente do que as entidades com chaves de partição diferentes, mas a utilização de várias chaves de partição permite uma maior escalabilidade de operações simultâneas. Para qualquer propriedade que deva ser armazenada no serviço de tabela Olá, propriedade Olá tem de ser uma propriedade pública de um tipo suportado que expõe os definir e obter os valores.
classe de entidade de Olá *tem* declarar um construtor sem parâmetros público.

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).

1. Abra Olá `TablesController.cs` ficheiro.

1. Adicionar Olá seguir diretiva, de modo que Olá código Olá `TablesController.cs` ficheiros podem aceder Olá **CustomerEntity** classe:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Adicione um método denominado **AddEntity** que devolve um **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **AddEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello referência toowhich vai nova entidade do tooadd Olá. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Instanciar e inicializar Olá **CustomerEntity** classe.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Criar um **TableOperation** objeto insere a entidade de cliente Olá.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Execute a operação de inserção Olá, chamar Olá **Cloudtable** método. Pode verificar o resultado de Olá da operação de Olá inspecionando Olá **TableResult.HttpStatusCode** propriedade. Um código de estado de 2xx indica a ação de Olá pedida pelo cliente de Olá foi processada com êxito. Por exemplo, com êxito inserções de novas entidades origina um código de estado HTTP de 204, que significa que a operação de Olá foi processada com êxito e servidor Olá não devolveu qualquer conteúdo.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Olá atualização **ViewBag** com o nome da tabela Olá e Olá os resultados da operação de inserção de Olá.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **AddEntity** para nome da vista Olá e selecione **adicionar**.

1. Abra `AddEntity.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Executar a aplicação Olá e selecione **adicionar entidade** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Adicionar entidade](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Pode verificar se a entidade de Olá foi adicionada ao seguir os passos de Olá na secção de Olá, [obter uma única entidade](#get-a-single-entity). Também pode utilizar Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview Olá todas as entidades para as suas tabelas.

## <a name="add-a-batch-of-entities-tooa-table"></a>Adicionar um lote de tabela de tooa de entidades

Na adição toobeing capaz de demasiado[adicionar uma tabela de tooa de entidade um cada vez](#add-an-entity-to-a-table), também pode adicionar entidades no batch. A adição de entidades no batch reduz o número de Olá de ida e volta entre o seu código e Olá serviço tabela do Azure. Olá, os passos seguintes ilustram como tooadd várias entidades tooa de tabela com uma operação de inserção único:

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment).

1. Abra Olá `TablesController.cs` ficheiro.

1. Adicione um método denominado **AddEntities** que devolve um **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **AddEntities** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello referência toowhich são novas entidades de contínuo tooadd Olá. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Instanciar alguns objetos de cliente com base no Olá **CustomerEntity** classe apresentado na secção de Olá, de modelo [adicionar uma tabela de tooa entidade](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Obter um **TableBatchOperation** objeto.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Adicione o objeto de operação de inserção de lote toohello entidades.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Execute a operação de inserção de lote de Olá, chamar Olá **CloudTable.ExecuteBatch** método.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Olá **CloudTable.ExecuteBatch** método devolve uma lista de **TableResult** objetos onde cada **TableResult** objeto pode ser examinadas toodetermine Olá êxito ou falha de cada operação individual. Para este exemplo, transmita Olá lista tooa de vista e permitir que a vista de Olá apresentar Olá resultados de cada operação. 
 
    ```csharp
    return View(results);
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **AddEntities** para nome da vista Olá e selecione **adicionar**.

1. Abra `AddEntities.cshtml`e modificá-lo de modo a que se parece com Olá seguinte.

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

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Executar a aplicação Olá e selecione **adicionar entidades** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Adicionar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Pode verificar se a entidade de Olá foi adicionada ao seguir os passos de Olá na secção de Olá, [obter uma única entidade](#get-a-single-entity). Também pode utilizar Olá [Explorador de armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview Olá todas as entidades para as suas tabelas.

## <a name="get-a-single-entity"></a>Obter uma única entidade

Esta secção ilustra como tooget uma única entidade a partir de uma tabela utilizando Olá chave da fila e a chave de partição da entidade. 

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment)e utiliza dados dos [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). 

1. Abra Olá `TablesController.cs` ficheiro.

1. Adicione um método denominado **GetSingle** que devolve um **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **GetSingle** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello referência partir da qual estão a obter a entidade de Olá. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Criar um objeto de operação de obtenção pega num objeto de entidade derivado **TableEntity**. Step-by-Olá primeiro parâmetro é Olá *partitionKey*, e o segundo parâmetro de Olá é Olá *rowKey*. Utilizar Olá **CustomerEntity** classe e os dados apresentados na secção de Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), Olá seguintes tabela da Olá de consultas de fragmento de código para um **CustomerEntity** entidade com uma *partitionKey* valor de "Santos" e um *rowKey* valor de "Bernardo":

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Execute a operação de obtenção de Olá.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Passe Olá resultado toohello da vista apresentação.

    ```csharp
    return View(result);
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **GetSingle** para nome da vista Olá e selecione **adicionar**.

1. Abra `GetSingle.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

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

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Executar a aplicação Olá e selecione **obter único** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Obter único](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Obter todas as entidades numa partição

Tal como mencionado na secção de Olá, [adicionar uma tabela de tooa entidade](#add-an-entity-to-a-table), combinação de Olá de uma partição e uma chave de linha identificar exclusivamente uma entidade numa tabela. Entidades com a mesma chave de partição podem ser consultadas mais rapidamente do que as entidades com chaves de partição diferentes. Esta secção ilustra como tooquery uma tabela para todas as entidades de Olá de uma partição especificada.  

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment)e utiliza dados dos [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). 

1. Abra Olá `TablesController.cs` ficheiro.

1. Adicione um método denominado **GetPartition** que devolve um **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **GetPartition** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello referência partir da qual estão a obter entidades Olá. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Instanciar um **TableQuery** objeto a especificação de consulta Olá Olá **onde** cláusula. Utilizar Olá **CustomerEntity** classe e os dados apresentados na secção de Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), tabela Olá de consultas de fragmento para uma todas as entidades de código seguinte Olá, onde Olá  **PartitionKey** (apelido do cliente) tem um valor de "Santos":

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. Dentro de um ciclo, chamar Olá **CloudTable.ExecuteQuerySegmented** método transmitir o objeto da consulta Olá que instanciado no passo anterior Olá.  Olá **CloudTable.ExecuteQuerySegmented** método devolve um **TableContinuationToken** objeto que - quando **nulo** -indica que existem não existem mais entidades tooretrieve. Dentro do ciclo de Olá, utilize outro tooiterate de ciclo através de Olá devolvido entidades. No seguinte exemplo de código de Olá, cada entidade devolvida é adicionada tooa lista. Uma vez Olá extremidades do ciclo, lista de Olá é transmitida tooa vista para apresentar: 

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

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **GetPartition** para nome da vista Olá e selecione **adicionar**.

1. Abra `GetPartition.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

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

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Executar a aplicação Olá e selecione **obter partição** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Obter a partição](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Eliminar uma entidade

Esta secção ilustra como toodelete uma entidade a partir de uma tabela.

> [!NOTE]
> 
> Esta secção assume que concluiu as fases de Olá no [configurar o ambiente de desenvolvimento de Olá](#set-up-the-development-environment)e utiliza dados dos [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). 

1. Abra Olá `TablesController.cs` ficheiro.

1. Adicione um método denominado **DeleteEntity** que devolve um **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro do Olá **DeleteEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá armazenamento cadeia e o armazenamento conta informações de ligação da configuração de serviço do Azure Olá de código seguinte Olá de utilização: (alteração  *&lt;nome da conta de armazenamento >* nome toohello Olá storage do Azure conta que está a aceder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obter um **CloudTableClient** objeto representa um cliente do serviço tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello referência partir do qual está a eliminar a entidade de Olá. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Criar um objeto de operação de eliminação demora um objeto de entidade derivado **TableEntity**. Neste caso, vamos utilizar Olá **CustomerEntity** classe e os dados apresentados na secção de Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). Olá da entidade **ETag** tem de ser definido um valor válido de tooa.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Execute a operação de eliminação de Olá.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Passe Olá resultado toohello da vista apresentação.

    ```csharp
    return View(result);
    ```

1. No Olá **Explorador de soluções**, expanda Olá **vistas** pasta, faça duplo clique **tabelas**e no menu de contexto de Olá, selecione **adicionar -> vista**.

1. No Olá **Adicionar vista** caixa de diálogo, introduza **DeleteEntity** para nome da vista Olá e selecione **adicionar**.

1. Abra `DeleteEntity.cshtml`e modificá-lo de modo a que se parece com Olá seguinte fragmento de código:

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

1. No Olá **Explorador de soluções**, expanda Olá **vistas -> partilhados** pasta e abra `_Layout.cshtml`.

1. Depois de Olá último **Html.ActionLink**, adicione Olá seguinte **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Executar a aplicação Olá e selecione **eliminar entidade** toosee resulta toohello semelhante captura de ecrã a seguir:
  
    ![Obter único](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Passos seguintes
Ver mais toolearn de guias de funcionalidades sobre as opções adicionais para armazenar dados no Azure.

  * [Introdução ao blob storage do Azure e o Visual Studio ligado serviços (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introdução ao armazenamento de filas do Azure e o Visual Studio ligado serviços (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
