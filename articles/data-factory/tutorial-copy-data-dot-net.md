---
title: Copiar dados do Armazenamento de Blobs do Azure para a Base de Dados SQL | Microsoft Docs
description: "Este tutorial fornece instruções passo a passo para copiar dados do Armazenamento de Blobs do Azure para a Base de Dados SQL do Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 0747ba79529bc2f12f1c5d74cbfcb7b62a62baa8
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="copy-data-from-azure-blob-to-azure-sql-database-using-azure-data-factory"></a>Copiar dados do Blob do Azure para a Base de Dados SQL do Azure utilizando o Azure Data Factory
Neste tutorial, vai criar um pipeline do Data Factory que copia dados do Armazenamento de Blobs do Azure para a Base de Dados SQL do Azure. O padrão de configuração neste tutorial aplica-se à cópia a partir de um arquivo de dados baseado em ficheiros para um arquivo de dados relacional. Para obter uma lista dos arquivos de dados suportados como origens e sinks, consulte [arquivos de dados suportados](copy-activity-overview.md#supported-data-stores-and-formats).

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em pré-visualização. Se estiver a utilizar a versão 1 do serviço Data Factory, que está disponível em geral (GA), veja a [documentação da versão 1 do Data Factory](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


Vai executar os seguintes passos neste tutorial:

> [!div class="checklist"]
> * Criar uma fábrica de dados.
> * Criar os serviços ligados Armazenamento do Microsoft Azure e Base de Dados SQL do Azure.
> * Criar os conjuntos de dados Blob do Azure e Base de Dados SQL do Azure.
> * Criar um pipeline que contém uma atividade de cópia.
> * Iniciar uma execução de pipeline.
> * Monitorizar o pipeline e execuções de atividades.

Este tutorial utiliza o .NET SDK. Pode utilizar outros mecanismos para interagir com o Azure Data Factory. Veja as amostras em "Inícios rápidos".

Se não tiver uma subscrição do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

* **Conta de Armazenamento do Azure**. Utilize o armazenamento de blobs como arquivo de dados de **origem**. Se não tiver uma conta de armazenamento do Azure, veja o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para obter os passos para criar uma.
* **Base de Dados SQL do Azure**. Pode utilizar a base de dados como arquivo de dados **sink**. Se não tiver uma Base de Dados SQL do Azure, veja o artigo [Criar uma base de dados SQL do Azure](../sql-database/sql-database-get-started-portal.md) para obter os passos para criar uma.
* **Visual Studio** 2015 ou 2017. As instruções neste artigo utilizam o Visual Studio 2017.
* **Transferir e instalar o [SDK .NET do Azure](http://azure.microsoft.com/downloads/)**.
* **Crie uma aplicação no Azure Active Directory** ao seguir [estas instruções](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Tome nota dos seguintes valores que vai utilizar em passos posteriores: **ID da aplicação**, **chave de autenticação** e **ID de inquilino**. Atribua a aplicação à função "**Contribuidor**", seguindo as instruções no mesmo artigo.

### <a name="create-a-blob-and-a-sql-table"></a>Criar um blob e uma tabela SQL

Agora, prepare o Blob do Azure e a Base de Dados SQL do Azure para o tutorial ao efetuar os seguintes passos:

#### <a name="create-a-source-blob"></a>Criar um blob de origem

1. Inicie o Bloco de notas. Copie o texto seguinte e guarde-o como ficheiro **input.txt** no disco.

    ```
    John|Doe
    Jane|Doe
    ```

2. Utilize ferramentas como o [Explorador de Armazenamento do Azure](http://storageexplorer.com/) para criar o contentor **adfv2tutorial** e carregar o ficheiro **inputEmp.txt** para o contentor.

#### <a name="create-a-sink-sql-table"></a>Criar uma tabela SQL sink

1. Utilize o seguinte script SQL para criar a tabela **dbo.emp** na Base de Dados SQL do Azure.

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

2. Permita que os serviços do Azure acedam ao servidor SQL. Certifique-se de que a definição **Permitir acesso aos serviços do Azure** está **ATIVADA** para o servidor SQL do Azure para que o serviço Data Factory possa escrever dados no servidor SQL do Azure. Para verificar e ativar desta definição, execute os passos seguintes:

    1. Clique no hub **Mais serviços** à esquerda e clique em **Servidores SQL**.
    2. Selecione o seu servidor e clique em **Firewall** em **DEFINIÇÕES**.
    3. Na página **Definições de firewall**, clique em **ATIVAR** para **Permitir acesso aos serviços do Azure**.


## <a name="create-a-visual-studio-project"></a>Criar um projeto do Visual Studio

Com o Visual Studio 2015/2017, crie uma aplicação de consola de C# .NET.

1. Inicie o **Visual Studio**.
2. Clique em **Ficheiro**, aponte para **Novo** e, em seguida, clique em **Projeto**.
3. Selecione **Consola de Aplicação** -> **de Visual C# (.NET Framework)** na lista de tipos de projeto à direita. É necessária a versão 4.5.2 ou superior do .NET.
4. Introduza **ADFv2Tutorial** para o Nome.
5. Clique em **OK** para criar o projeto.

## <a name="install-nuget-packages"></a>Instalar pacotes NuGet

1. clique em **Ferramentas** -> **Gestor de Pacotes NuGet** -> **Consola de Gestor de Pacotes**.
2. Na **Consola do Gestor de Pacotes**, execute os comandos seguintes para instalar os pacotes:

    ```
    Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
    Install-Package Microsoft.Azure.Management.ResourceManager -Prerelease
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

## <a name="create-a-data-factory-client"></a>Criar um cliente de fábrica de dados

1. Abra **Program.cs** e inclua as seguintes instruções para adicionar referências aos espaços de nomes.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using Microsoft.Rest;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.DataFactory;
    using Microsoft.Azure.Management.DataFactory.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

2. Add the following code to the **Main** method that sets variables. Replace place-holders with your own values. Currently, Data Factory V2 allows you to create data factories only in the East US, East US2, and West Europe regions. The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.

    ```csharp
    // Set variables
    string tenantID = "<your tenant ID>";
    string applicationId = "<your application ID>";
    string authenticationKey = "<your authentication key for the application>";
    string subscriptionId = "<your subscription ID to create the factory>";
    string resourceGroup = "<your resource group to create the factory>";

    string region = "East US";
    string dataFactoryName = "<specify the name of a data factory to create. It must be globally unique.>";

    // Specify the source Azure Blob information
    string storageAccount = "<your storage account name to copy data>";
    string storageKey = "<your storage account key>";
    string inputBlobPath = "adfv2tutorial/";
    string inputBlobName = "inputEmp.txt";

    // Specify the sink Azure SQL Database information
    string azureSqlConnString = "Server=tcp:<your server name>.database.windows.net,1433;Database=<your database name>;User ID=<your username>@<your server name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30";
    string azureSqlTableName = "dbo.emp";

    string storageLinkedServiceName = "AzureStorageLinkedService";
    string sqlDbLinkedServiceName = "AzureSqlDbLinkedService";
    string blobDatasetName = "BlobDataset";
    string sqlDatasetName = "SqlDataset";
    string pipelineName = "Adfv2TutorialBlobToSqlCopy";
    ```

3. Adicione o código seguinte ao método **Main** que cria uma instância da classe **DataFactoryManagementClient**. Utilize este objeto para criar uma fábrica de dados, um serviço ligado, os conjuntos de dados e um pipeline. Também pode utilizar este objeto para monitorizar os detalhes de execução do pipeline.

    ```csharp
    // Authenticate and create a data factory management client
    var context = new AuthenticationContext("https://login.windows.net/" + tenantID);
    ClientCredential cc = new ClientCredential(applicationId, authenticationKey);
    AuthenticationResult result = context.AcquireTokenAsync("https://management.azure.com/", cc).Result;
    ServiceClientCredentials cred = new TokenCredentials(result.AccessToken);
    var client = new DataFactoryManagementClient(cred) { SubscriptionId = subscriptionId };
    ```

## <a name="create-a-data-factory"></a>Criar uma fábrica de dados

Adicione o código seguinte ao método **Main** que cria uma **fábrica de dados**.

```csharp
// Create a data factory
Console.WriteLine("Creating a data factory " + dataFactoryName + "...");
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()

};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
Console.WriteLine(SafeJsonConvert.SerializeObject(dataFactory, client.SerializationSettings));

while (client.Factories.Get(resourceGroup, dataFactoryName).ProvisioningState == "PendingCreation")
{
    System.Threading.Thread.Sleep(1000);
}
```

## <a name="create-linked-services"></a>Criar serviços ligados

Neste tutorial, crie dois serviços ligados para a origem e sink, respetivamente:

### <a name="create-an-azure-storage-linked-service"></a>Criar um serviço ligado do Armazenamento do Azure

Adicione o código seguinte ao método **Main** que cria um **serviço ligado do Armazenamento do Azure**. Saiba mais a partir da secção [Propriedades do serviço ligado do Blob do Azure](connector-azure-blob-storage.md#linked-service-properties) sobre detalhes e propriedades suportadas.

```csharp
// Create an Azure Storage linked service
Console.WriteLine("Creating linked service " + storageLinkedServiceName + "...");

LinkedServiceResource storageLinkedService = new LinkedServiceResource(
    new AzureStorageLinkedService
    {
        ConnectionString = new SecureString("DefaultEndpointsProtocol=https;AccountName=" + storageAccount + ";AccountKey=" + storageKey)
    }
);
client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, storageLinkedServiceName, storageLinkedService);
Console.WriteLine(SafeJsonConvert.SerializeObject(storageLinkedService, client.SerializationSettings));
```

### <a name="create-an-azure-sql-database-linked-service"></a>Criar um serviço ligado da Base de Dados SQL do Azure

Adicione o código seguinte ao método **Main** que cria um **serviço ligado da Base de Dados SQL do Azure**. Saiba mais a partir da secção [Propriedades do serviço ligado da Base de Dados SQL do Azure](connector-azure-sql-database.md#linked-service-properties) sobre detalhes e propriedades suportadas.

```csharp
// Create an Azure SQL Database linked service
Console.WriteLine("Creating linked service " + sqlDbLinkedServiceName + "...");

LinkedServiceResource sqlDbLinkedService = new LinkedServiceResource(
    new AzureSqlDatabaseLinkedService
    {
        ConnectionString = new SecureString(azureSqlConnString)
    }
);
client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, sqlDbLinkedServiceName, sqlDbLinkedService);
Console.WriteLine(SafeJsonConvert.SerializeObject(sqlDbLinkedService, client.SerializationSettings));
```

## <a name="create-datasets"></a>Criar conjuntos de dados

Nesta secção, pode criar dois conjuntos de dados: um para a origem e outro para o sink. 

### <a name="create-a-dataset-for-source-azure-blob"></a>Criar um conjunto de dados para o Blob do Azure de origem

Adicione o código seguinte ao método **Main** que cria um **conjunto de dados do blob do Azure**. Saiba mais a partir da secção [Propriedades do conjunto de dados do Blob do Azure](connector-azure-blob-storage.md#dataset-properties) sobre detalhes e propriedades suportadas.

Defina um conjunto de dados que represente os dados de origem no Blob do Azure. Este conjunto de dados do Blob refere-se ao serviço ligado de Armazenamento do Microsoft Azure que criou no passo anterior e descreve:

- A localização do blob a partir da qual copiar: **FolderPath** e **FileName**;
- O formato de blob que indica como analisar o conteúdo: **TextFormat** e as definições (por exemplo, delimitador de coluna).
- A estrutura de dados, incluindo os tipos de dados e os nomes de coluna que, neste caso, são mapeados para a tabela SQL sink.

```csharp
// Create a Azure Blob dataset
Console.WriteLine("Creating dataset " + blobDatasetName + "...");
DatasetResource blobDataset = new DatasetResource(
    new AzureBlobDataset
    {
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = storageLinkedServiceName
        },
        FolderPath = inputBlobPath,
        FileName = inputBlobName,
        Format = new TextFormat { ColumnDelimiter = "|" },
        Structure = new List<DatasetDataElement>
        {
            new DatasetDataElement
            {
                Name = "FirstName",
                Type = "String"
            },
            new DatasetDataElement
            {
                Name = "LastName",
                Type = "String"
            }
        }
    }
);
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobDatasetName, blobDataset);
Console.WriteLine(SafeJsonConvert.SerializeObject(blobDataset, client.SerializationSettings));
```

### <a name="create-a-dataset-for-sink-azure-sql-database"></a>Criar um conjunto de dados para o Base de Dados SQL do Azure

Adicione o código seguinte ao método **Main** que cria um **conjunto de dados da Base de Dados SQL do Azure**. Saiba mais a partir da secção [Propriedades do conjunto de dados da Base de Dados SQL do Azure](connector-azure-sql-database.md#dataset-properties) sobre detalhes e propriedades suportadas.

Defina um conjunto de dados que representa os dados sink na Base de Dados SQL do Azure. Este conjunto de dados refere-se ao serviço ligado da Base de Dados SQL do Azure que criou no passo anterior. Também especifica a tabela SQL que contém os dados copiados. 

```csharp
// Create a Azure SQL Database dataset
Console.WriteLine("Creating dataset " + sqlDatasetName + "...");
DatasetResource sqlDataset = new DatasetResource(
    new AzureSqlTableDataset
    {
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = sqlDbLinkedServiceName
        },
        TableName = azureSqlTableName
    }
);
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, sqlDatasetName, sqlDataset);
Console.WriteLine(SafeJsonConvert.SerializeObject(sqlDataset, client.SerializationSettings));
```

## <a name="create-a-pipeline"></a>Criar um pipeline

Adicione o código seguinte ao método **Main** que cria um **pipeline com uma atividade de cópia**. Neste tutorial, este pipeline contém uma atividade: a atividade de cópia que aceita o conjunto de dados do Blob como uma origem e o conjunto de dados SQL como um sink. Saiba mais em [Descrição Geral da Atividade de Cópia](copy-activity-overview.md) nos detalhes de atividade de cópia.

```csharp
// Create a pipeline with copy activity
Console.WriteLine("Creating pipeline " + pipelineName + "...");
PipelineResource pipeline = new PipelineResource
{
    Activities = new List<Activity>
    {
        new CopyActivity
        {
            Name = "CopyFromBlobToSQL",
            Inputs = new List<DatasetReference>
            {
                new DatasetReference()
                {
                    ReferenceName = blobDatasetName
                }
            },
            Outputs = new List<DatasetReference>
            {
                new DatasetReference
                {
                    ReferenceName = sqlDatasetName
                }
            },
            Source = new BlobSource { },
            Sink = new SqlSink { }
        }
    }
};
client.Pipelines.CreateOrUpdate(resourceGroup, dataFactoryName, pipelineName, pipeline);
Console.WriteLine(SafeJsonConvert.SerializeObject(pipeline, client.SerializationSettings));
```

## <a name="create-a-pipeline-run"></a>Criar uma execução de pipeline

Adicione o código seguinte ao método **Main** que **aciona uma execução de pipeline**.

```csharp
// Create a pipeline run
Console.WriteLine("Creating pipeline run...");
CreateRunResponse runResponse = client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName).Result.Body;
Console.WriteLine("Pipeline run ID: " + runResponse.RunId);
```

## <a name="monitor-a-pipeline-run"></a>Monitorizar uma execução de pipeline

1. Adicione o código seguinte ao método **Main** para verificar continuamente o estado da execução do pipeline até terminar de copiar os dados.

    ```csharp
    // Monitor the pipeline run
    Console.WriteLine("Checking pipeline run status...");
    PipelineRun pipelineRun;
    while (true)
    {
        pipelineRun = client.PipelineRuns.Get(resourceGroup, dataFactoryName, runResponse.RunId);
        Console.WriteLine("Status: " + pipelineRun.Status);
        if (pipelineRun.Status == "InProgress")
            System.Threading.Thread.Sleep(15000);
        else
            break;
    }
    ```

2. Adicione o código seguinte ao método **Main** que obtém os detalhes da execução da atividade de cópia; por exemplo, o tamanho dos dados lidos/escritos.

    ```csharp
    // Check the copy activity run details
    Console.WriteLine("Checking copy activity run details...");

    List<ActivityRun> activityRuns = client.ActivityRuns.ListByPipelineRun(
    resourceGroup, dataFactoryName, runResponse.RunId, DateTime.UtcNow.AddMinutes(-10), DateTime.UtcNow.AddMinutes(10)).ToList(); 
 
    if (pipelineRun.Status == "Succeeded")
    {
        Console.WriteLine(activityRuns.First().Output);
    }
    else
        Console.WriteLine(activityRuns.First().Error);
    
    Console.WriteLine("\nPress any key to exit...");
    Console.ReadKey();
    ```

## <a name="run-the-code"></a>Executar o código

Crie e inicie a aplicação e, em seguida, verifique a execução de pipeline.

A consola imprime o progresso da criação de uma fábrica de dados, do serviço ligado, dos conjuntos de dados, do pipeline e da execução de pipeline. Em seguida, verifica o estado de execução do pipeline. Aguarde até ver os detalhes da execução da atividade de cópia com o tamanho dos dados lidos/escritos. Em seguida, utilize ferramentas como o SSMS (SQL Server Management Studio) ou o Visual Studio para ligar à sua Base de Dados SQL do Azure de destino e verifique se os dados são copiados para a tabela que especificou.

### <a name="sample-output"></a>Resultado da amostra

```json
Creating a data factory AdfV2Tutorial...
{
  "identity": {
    "type": "SystemAssigned"
  },
  "location": "East US"
}
Creating linked service AzureStorageLinkedService...
{
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": {
        "type": "SecureString",
        "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>"
      }
    }
  }
}
Creating linked service AzureSqlDbLinkedService...
{
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": {
        "type": "SecureString",
        "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
      }
    }
  }
}
Creating dataset BlobDataset...
{
  "properties": {
    "type": "AzureBlob",
    "typeProperties": {
      "folderPath": "adfv2tutorial/",
      "fileName": "inputEmp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "|"
      }
    },
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "linkedServiceName": {
      "type": "LinkedServiceReference",
      "referenceName": "AzureStorageLinkedService"
    }
  }
}
Creating dataset SqlDataset...
{
  "properties": {
    "type": "AzureSqlTable",
    "typeProperties": {
      "tableName": "dbo.emp"
    },
    "linkedServiceName": {
      "type": "LinkedServiceReference",
      "referenceName": "AzureSqlDbLinkedService"
    }
  }
}
Creating pipeline Adfv2TutorialBlobToSqlCopy...
{
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          }
        },
        "inputs": [
          {
            "type": "DatasetReference",
            "referenceName": "BlobDataset"
          }
        ],
        "outputs": [
          {
            "type": "DatasetReference",
            "referenceName": "SqlDataset"
          }
        ],
        "name": "CopyFromBlobToSQL"
      }
    ]
  }
}
Creating pipeline run...
Pipeline run ID: 1cd03653-88a0-4c90-aabc-ae12d843e252
Checking pipeline run status...
Status: InProgress
Status: InProgress
Status: Succeeded
Checking copy activity run details...
{
  "dataRead": 18,
  "dataWritten": 28,
  "rowsCopied": 2,
  "copyDuration": 2,
  "throughput": 0.01,
  "errors": [],
  "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)",
  "usedCloudDataMovementUnits": 2,
  "billedDuration": 2
}

Press any key to exit...
```


## <a name="next-steps"></a>Passos seguintes
O pipeline neste exemplo copia dados de uma localização para outra localização num armazenamento de blobs do Azure. Aprendeu a: 

> [!div class="checklist"]
> * Criar uma fábrica de dados.
> * Criar os serviços ligados Armazenamento do Microsoft Azure e Base de Dados SQL do Azure.
> * Criar os conjuntos de dados Blob do Azure e Base de Dados SQL do Azure.
> * Criar um pipeline que contém uma atividade de cópia.
> * Iniciar uma execução de pipeline.
> * Monitorizar o pipeline e execuções de atividades.


Avance para o tutorial seguinte para saber como copiar dados do local para a cloud: 

> [!div class="nextstepaction"]
>[Copiar dados do local para a cloud](tutorial-hybrid-copy-powershell.md)
