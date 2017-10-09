---
title: aaaCreate pipelines de dados utilizando o SDK .NET do Azure | Microsoft Docs
description: "Saiba como tooprogrammatically criar, monitorizar e gerir as fábricas de dados do Azure utilizando o SDK de fábrica de dados."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Criar, monitorizar e gerir fábricas de dados do Azure utilizando o SDK .NET do Azure Data Factory
## <a name="overview"></a>Descrição geral
Pode criar, monitorizar e gerir fábricas de dados do Azure através de programação utilizando o SDK .NET da fábrica de dados. Este artigo contém instruções que pode seguir toocreate uma aplicação de consola .NET de exemplo que cria e monitoriza uma fábrica de dados. 

> [!NOTE]
> Este artigo não abrange todos os Olá API .NET do Data Factory. Consulte [referência de API .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para a documentação completa sobre a .NET API do Data Factory. 

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2012 ou 2013 ou 2015
* Transfira e instale [SDK .NET da Azure](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall Azure PowerShell no seu computador. Utilizar o Azure PowerShell toocreate uma aplicação do Azure Active Directory.

### <a name="create-an-application-in-azure-active-directory"></a>Criar uma Aplicação no Azure Active Directory
Criar uma aplicação do Azure Active Directory, criar um principal de serviço para a aplicação Olá e atribua-lhe toohello **contribuinte da fábrica de dados** função.

1. Inicie o **Azure PowerShell**.
2. Execute Olá os seguintes comandos e introduza o nome de utilizador de Olá e a palavra-passe que utilizam toosign no toohello portal do Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Execute Olá tooview de comando a seguir todas as subscrições de Olá para esta conta.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Execute Olá comando tooselect Olá subscrição que pretende que toowork com os seguintes. Substitua  **&lt;NameOfAzureSubscription** &gt; com o nome de Olá da sua subscrição do Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Tome nota **SubscriptionId** e **TenantId** da saída de Olá deste comando.

5. Criar um grupo de recursos do Azure com o nome **ADFTutorialResourceGroup** executando Olá seguinte comando na Olá do PowerShell.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Se o grupo de recursos de Olá já existe, especifique se tooupdate este (S) ou mantê-lo como (N).

    Se utilizar um grupo de recursos diferente, terá de nome de Olá toouse do seu grupo de recursos em vez de ADFTutorialResourceGroup neste tutorial.
6. Crie uma aplicação do Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    Se obtiver Olá seguinte erro, especifique outro URL e volte a executar o comando de Olá.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Crie Olá principal de serviço do AD.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Adicionar toohello principal de serviço **contribuinte da fábrica de dados** função.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Obter ID de aplicação Olá.

    ```PowerShell
    $azureAdApplication 
    ```
    Tenha em atenção para baixo de ID da aplicação Olá (applicationID) da saída de Olá.

Deve obter os quatro valores seguintes destes passos:

* ID do inquilino
* ID da subscrição
* ID da aplicação
* Palavra-passe (especificada no comando primeiro Olá)

## <a name="walkthrough"></a>Instruções
Instruções de Olá, crie uma fábrica de dados com um pipeline que contém uma atividade de cópia. Olá atividade de cópia copia dados a partir de uma pasta na sua pasta de tooanother de armazenamento de Blobs do Azure no Olá mesmo armazenamento de Blobs. 

Olá atividade de cópia realiza o movimento de dados de Olá no Azure Data Factory. Olá atividade utiliza a tecnologia de um serviço globalmente disponível que pode copiar dados entre vários arquivos de dados de forma segura, fiável e escalável. Consulte [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre Olá atividade de cópia.

1. Com o Visual Studio 2012/2013/2015, crie uma aplicação de consola de C# .NET.
   1. Inicie o **Visual Studio** 2012/2013/2015.
   2. Clique em **ficheiro**, ponto demasiado**novo**e clique em **projeto**.
   3. Expanda **Modelos** e selecione **Visual C#**. Nestas instruções, utiliza C#, mas pode utilizar qualquer linguagem .NET.
   4. Selecione **aplicação de consola** da lista de Olá dos tipos de projeto no Olá à direita.
   5. Introduza **DataFactoryAPITestApp** para Olá nome.
   6. Selecione **C:\ADFGetStarted** para Olá localização.
   7. Clique em **OK** projeto de Olá toocreate.
2. Clique em **ferramentas**, ponto demasiado**Gestor de pacotes NuGet**e clique em **consola do Gestor de pacotes**.
3. No Olá **consola do Gestor de pacotes**, Olá os seguintes passos:
   1. Execute Olá pacote de fábrica de dados de tooinstall de comando a seguir:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Execute Olá seguir o pacote do Azure Active Directory tooinstall de comando (utilizar API do Active Directory no código Olá):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Substituir conteúdo Olá **App. config** ficheiros no projeto Olá com Olá seguinte conteúdo: 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. No ficheiro App. config de Olá, atualize os valores para  **&lt;ID da aplicação&gt;**,  **&lt;palavra-passe&gt;**,  **&lt; ID de subscrição&gt;**, e  **&lt;ID de inquilino&gt;**  com os seus próprios valores.
6. Adicione Olá seguinte **utilizando** instruções toohello **Program.cs** ficheiros no projeto Olá.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. Adicionar Olá seguinte código que cria uma instância de **DataPipelineManagementClient** classe toohello **Main** método. Utilize este objeto toocreate uma fábrica de dados, um serviço ligado, conjuntos de dados de entrada e de saída e um pipeline. Também utilizar este setores de toomonitor do objeto de um conjunto de dados em tempo de execução.

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Substitua o valor Olá **resourceGroupName** com o nome de Olá do seu grupo de recursos do Azure. Pode criar um grupo de recursos com Olá [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.
   >
   > Nome de atualização de Olá data factory (dataFactoryName) toobe exclusivo. Nome do Olá data factory deve ser globalmente exclusivo. Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.
7. Adicionar Olá seguinte código que cria um **fábrica de dados** toohello **Main** método.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. Adicionar Olá seguinte código que cria um **serviço ligado do Storage do Azure** toohello **Main** método.

   > [!IMPORTANT]
   > Substitua **storageaccountname** e **accountkey** pelo nome e chave da sua conta de Armazenamento do Azure.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. Adicionar Olá código que cria os seguintes **conjuntos de dados de entrada e de saída** toohello **Main** método.

    Olá **FolderPath** para o blob de entrada Olá estiver definido demasiado**adftutorial /** onde **adftutorial** é Olá nome do contentor de Olá no seu armazenamento de Blobs. Se este contentor não existe no seu armazenamento de Blobs do Azure, criar um contentor com este nome: **adftutorial** e carregar um contentor de toohello do ficheiro de texto.

    Olá FolderPath para Olá saída blob está definido como: **adftutorial/apifactoryoutput / {setor}** onde **setor** é calculada dinamicamente Olá com base no valor de **SliceStart**(início data-hora de cada setor).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. Adicione a seguinte de Olá código que **cria e ativa um pipeline** toohello **Main** método. Este pipeline tem um **CopyActivity** que assume **BlobSource** como uma origem e **BlobSink** como um sink.

    Olá atividade de cópia realiza o movimento de dados de Olá no Azure Data Factory. Olá atividade utiliza a tecnologia de um serviço globalmente disponível que pode copiar dados entre vários arquivos de dados de forma segura, fiável e escalável. Consulte [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre Olá atividade de cópia.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. Adicionar Olá seguinte código toohello **Main** método tooget Olá Estado um setor de dados de Olá conjunto de dados de saída. Não há apenas um setor esperado neste exemplo.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **(opcional)**  Tooget executar detalhes para um toohello de setor de dados de código seguinte de Olá adicionar **Main** método.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. Adicionar Olá seguinte método de programa auxiliar utilizado pelo Olá **Main** método toohello **programa** classe. Este método faz aparecer uma caixa de diálogo que lhe permite fornecer **nome de utilizador** e **palavra-passe** que utilize toolog no portal de tooAzure.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. Na Olá Explorador de soluções, expanda o projeto de Olá: **DataFactoryAPITestApp**, faça duplo clique **referências**e clique em **Adicionar referência**. Selecione caixa de verificação para `System.Configuration` assemblagem e clique em **OK**.
15. Crie aplicação de consola Olá. Clique em **criar** no menu de Olá e **compilar solução**.
16. Confirme se existe pelo menos um ficheiro no contentor de adftutorial Olá no seu armazenamento de Blobs do Azure. Caso contrário, crie Emp.txt ficheiro no bloco de notas com Olá seguir conteúdo e carregá-la toohello adftutorial contentor.

    ```
    John, Doe
    Jane, Doe
    ```
17. Executar o exemplo de Olá clicando **depurar** -> **iniciar depuração** no menu de Olá. Quando vir Olá **obter detalhes de um setor de dados da execução**, aguarde alguns minutos e prima **ENTER**.
18. Utilize Olá tooverify portal do Azure que fábrica de dados de Olá **APITutorialFactory** é criada com Olá artefactos os seguintes:
    * Serviço ligado: **AzureStorageLinkedService**
    * Conjunto de dados: **DatasetBlobSource** e **DatasetBlobDestination**.
    * Pipeline: **PipelineBlobSample**
19. Certifique-se de que um ficheiro de saída é criado na Olá **apifactoryoutput** pasta Olá **adftutorial** contentor.

## <a name="get-a-list-of-failed-data-slices"></a>Obter uma lista de setores de dados com falhas 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Passos seguintes
Olá seguinte o exemplo para criar um pipeline com o SDK do .NET que copia dados a partir de uma base de dados de SQL do Azure de tooan de armazenamento do BLOBs do Azure, consulte: 

- [Criar dados de toocopy um pipeline do Blob Storage tooSQL da base de dados](data-factory-copy-activity-tutorial-using-dotnet-api.md)
