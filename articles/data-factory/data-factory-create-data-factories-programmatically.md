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
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="df259-103">Criar, monitorizar e gerir fábricas de dados do Azure utilizando o SDK .NET do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="df259-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="df259-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="df259-104">Overview</span></span>
<span data-ttu-id="df259-105">Pode criar, monitorizar e gerir fábricas de dados do Azure através de programação utilizando o SDK .NET da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="df259-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="df259-106">Este artigo contém instruções que pode seguir toocreate uma aplicação de consola .NET de exemplo que cria e monitoriza uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="df259-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="df259-107">Este artigo não abrange todos os Olá API .NET do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df259-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="df259-108">Consulte [referência de API .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para a documentação completa sobre a .NET API do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df259-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="df259-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df259-109">Prerequisites</span></span>
* <span data-ttu-id="df259-110">Visual Studio 2012 ou 2013 ou 2015</span><span class="sxs-lookup"><span data-stu-id="df259-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="df259-111">Transfira e instale [SDK .NET da Azure](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="df259-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="df259-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df259-112">Azure PowerShell.</span></span> <span data-ttu-id="df259-113">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall Azure PowerShell no seu computador.</span><span class="sxs-lookup"><span data-stu-id="df259-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="df259-114">Utilizar o Azure PowerShell toocreate uma aplicação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df259-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="df259-115">Criar uma Aplicação no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df259-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="df259-116">Criar uma aplicação do Azure Active Directory, criar um principal de serviço para a aplicação Olá e atribua-lhe toohello **contribuinte da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="df259-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="df259-117">Inicie o **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="df259-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="df259-118">Execute Olá os seguintes comandos e introduza o nome de utilizador de Olá e a palavra-passe que utilizam toosign no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="df259-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="df259-119">Execute Olá tooview de comando a seguir todas as subscrições de Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="df259-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="df259-120">Execute Olá comando tooselect Olá subscrição que pretende que toowork com os seguintes.</span><span class="sxs-lookup"><span data-stu-id="df259-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="df259-121">Substitua  **&lt;NameOfAzureSubscription** &gt; com o nome de Olá da sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="df259-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="df259-122">Tome nota **SubscriptionId** e **TenantId** da saída de Olá deste comando.</span><span class="sxs-lookup"><span data-stu-id="df259-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="df259-123">Criar um grupo de recursos do Azure com o nome **ADFTutorialResourceGroup** executando Olá seguinte comando na Olá do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df259-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="df259-124">Se o grupo de recursos de Olá já existe, especifique se tooupdate este (S) ou mantê-lo como (N).</span><span class="sxs-lookup"><span data-stu-id="df259-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="df259-125">Se utilizar um grupo de recursos diferente, terá de nome de Olá toouse do seu grupo de recursos em vez de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="df259-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="df259-126">Crie uma aplicação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df259-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="df259-127">Se obtiver Olá seguinte erro, especifique outro URL e volte a executar o comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="df259-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="df259-128">Crie Olá principal de serviço do AD.</span><span class="sxs-lookup"><span data-stu-id="df259-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="df259-129">Adicionar toohello principal de serviço **contribuinte da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="df259-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="df259-130">Obter ID de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="df259-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="df259-131">Tenha em atenção para baixo de ID da aplicação Olá (applicationID) da saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="df259-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="df259-132">Deve obter os quatro valores seguintes destes passos:</span><span class="sxs-lookup"><span data-stu-id="df259-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="df259-133">ID do inquilino</span><span class="sxs-lookup"><span data-stu-id="df259-133">Tenant ID</span></span>
* <span data-ttu-id="df259-134">ID da subscrição</span><span class="sxs-lookup"><span data-stu-id="df259-134">Subscription ID</span></span>
* <span data-ttu-id="df259-135">ID da aplicação</span><span class="sxs-lookup"><span data-stu-id="df259-135">Application ID</span></span>
* <span data-ttu-id="df259-136">Palavra-passe (especificada no comando primeiro Olá)</span><span class="sxs-lookup"><span data-stu-id="df259-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="df259-137">Instruções</span><span class="sxs-lookup"><span data-stu-id="df259-137">Walkthrough</span></span>
<span data-ttu-id="df259-138">Instruções de Olá, crie uma fábrica de dados com um pipeline que contém uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="df259-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="df259-139">Olá atividade de cópia copia dados a partir de uma pasta na sua pasta de tooanother de armazenamento de Blobs do Azure no Olá mesmo armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="df259-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="df259-140">Olá atividade de cópia realiza o movimento de dados de Olá no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df259-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="df259-141">Olá atividade utiliza a tecnologia de um serviço globalmente disponível que pode copiar dados entre vários arquivos de dados de forma segura, fiável e escalável.</span><span class="sxs-lookup"><span data-stu-id="df259-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="df259-142">Consulte [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre Olá atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="df259-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="df259-143">Com o Visual Studio 2012/2013/2015, crie uma aplicação de consola de C# .NET.</span><span class="sxs-lookup"><span data-stu-id="df259-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="df259-144">Inicie o **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="df259-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="df259-145">Clique em **ficheiro**, ponto demasiado**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="df259-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="df259-146">Expanda **Modelos** e selecione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="df259-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="df259-147">Nestas instruções, utiliza C#, mas pode utilizar qualquer linguagem .NET.</span><span class="sxs-lookup"><span data-stu-id="df259-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="df259-148">Selecione **aplicação de consola** da lista de Olá dos tipos de projeto no Olá à direita.</span><span class="sxs-lookup"><span data-stu-id="df259-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="df259-149">Introduza **DataFactoryAPITestApp** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="df259-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="df259-150">Selecione **C:\ADFGetStarted** para Olá localização.</span><span class="sxs-lookup"><span data-stu-id="df259-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="df259-151">Clique em **OK** projeto de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="df259-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="df259-152">Clique em **ferramentas**, ponto demasiado**Gestor de pacotes NuGet**e clique em **consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="df259-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="df259-153">No Olá **consola do Gestor de pacotes**, Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="df259-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="df259-154">Execute Olá pacote de fábrica de dados de tooinstall de comando a seguir:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="df259-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="df259-155">Execute Olá seguir o pacote do Azure Active Directory tooinstall de comando (utilizar API do Active Directory no código Olá):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="df259-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="df259-156">Substituir conteúdo Olá **App. config** ficheiros no projeto Olá com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="df259-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
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
5. <span data-ttu-id="df259-157">No ficheiro App. config de Olá, atualize os valores para  **&lt;ID da aplicação&gt;**,  **&lt;palavra-passe&gt;**,  **&lt; ID de subscrição&gt;**, e  **&lt;ID de inquilino&gt;**  com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="df259-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="df259-158">Adicione Olá seguinte **utilizando** instruções toohello **Program.cs** ficheiros no projeto Olá.</span><span class="sxs-lookup"><span data-stu-id="df259-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

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
6. <span data-ttu-id="df259-159">Adicionar Olá seguinte código que cria uma instância de **DataPipelineManagementClient** classe toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="df259-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="df259-160">Utilize este objeto toocreate uma fábrica de dados, um serviço ligado, conjuntos de dados de entrada e de saída e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="df259-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="df259-161">Também utilizar este setores de toomonitor do objeto de um conjunto de dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="df259-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="df259-162">Substitua o valor Olá **resourceGroupName** com o nome de Olá do seu grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="df259-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="df259-163">Pode criar um grupo de recursos com Olá [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="df259-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="df259-164">Nome de atualização de Olá data factory (dataFactoryName) toobe exclusivo.</span><span class="sxs-lookup"><span data-stu-id="df259-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="df259-165">Nome do Olá data factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="df259-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="df259-166">Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df259-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="df259-167">Adicionar Olá seguinte código que cria um **fábrica de dados** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="df259-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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
8. <span data-ttu-id="df259-168">Adicionar Olá seguinte código que cria um **serviço ligado do Storage do Azure** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="df259-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="df259-169">Substitua **storageaccountname** e **accountkey** pelo nome e chave da sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="df259-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="df259-170">Adicionar Olá código que cria os seguintes **conjuntos de dados de entrada e de saída** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="df259-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="df259-171">Olá **FolderPath** para o blob de entrada Olá estiver definido demasiado**adftutorial /** onde **adftutorial** é Olá nome do contentor de Olá no seu armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="df259-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="df259-172">Se este contentor não existe no seu armazenamento de Blobs do Azure, criar um contentor com este nome: **adftutorial** e carregar um contentor de toohello do ficheiro de texto.</span><span class="sxs-lookup"><span data-stu-id="df259-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="df259-173">Olá FolderPath para Olá saída blob está definido como: **adftutorial/apifactoryoutput / {setor}** onde **setor** é calculada dinamicamente Olá com base no valor de **SliceStart**(início data-hora de cada setor).</span><span class="sxs-lookup"><span data-stu-id="df259-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="df259-174">Adicione a seguinte de Olá código que **cria e ativa um pipeline** toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="df259-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="df259-175">Este pipeline tem um **CopyActivity** que assume **BlobSource** como uma origem e **BlobSink** como um sink.</span><span class="sxs-lookup"><span data-stu-id="df259-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="df259-176">Olá atividade de cópia realiza o movimento de dados de Olá no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df259-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="df259-177">Olá atividade utiliza a tecnologia de um serviço globalmente disponível que pode copiar dados entre vários arquivos de dados de forma segura, fiável e escalável.</span><span class="sxs-lookup"><span data-stu-id="df259-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="df259-178">Consulte [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre Olá atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="df259-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

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
12. <span data-ttu-id="df259-179">Adicionar Olá seguinte código toohello **Main** método tooget Olá Estado um setor de dados de Olá conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="df259-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="df259-180">Não há apenas um setor esperado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="df259-180">There is only one slice expected in this sample.</span></span>

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
13. <span data-ttu-id="df259-181">**(opcional)**  Tooget executar detalhes para um toohello de setor de dados de código seguinte de Olá adicionar **Main** método.</span><span class="sxs-lookup"><span data-stu-id="df259-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
14. <span data-ttu-id="df259-182">Adicionar Olá seguinte método de programa auxiliar utilizado pelo Olá **Main** método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="df259-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="df259-183">Este método faz aparecer uma caixa de diálogo que lhe permite fornecer **nome de utilizador** e **palavra-passe** que utilize toolog no portal de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="df259-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

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

15. <span data-ttu-id="df259-184">Na Olá Explorador de soluções, expanda o projeto de Olá: **DataFactoryAPITestApp**, faça duplo clique **referências**e clique em **Adicionar referência**.</span><span class="sxs-lookup"><span data-stu-id="df259-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="df259-185">Selecione caixa de verificação para `System.Configuration` assemblagem e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="df259-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="df259-186">Crie aplicação de consola Olá.</span><span class="sxs-lookup"><span data-stu-id="df259-186">Build hello console application.</span></span> <span data-ttu-id="df259-187">Clique em **criar** no menu de Olá e **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="df259-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="df259-188">Confirme se existe pelo menos um ficheiro no contentor de adftutorial Olá no seu armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="df259-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="df259-189">Caso contrário, crie Emp.txt ficheiro no bloco de notas com Olá seguir conteúdo e carregá-la toohello adftutorial contentor.</span><span class="sxs-lookup"><span data-stu-id="df259-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="df259-190">Executar o exemplo de Olá clicando **depurar** -> **iniciar depuração** no menu de Olá.</span><span class="sxs-lookup"><span data-stu-id="df259-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="df259-191">Quando vir Olá **obter detalhes de um setor de dados da execução**, aguarde alguns minutos e prima **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="df259-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="df259-192">Utilize Olá tooverify portal do Azure que fábrica de dados de Olá **APITutorialFactory** é criada com Olá artefactos os seguintes:</span><span class="sxs-lookup"><span data-stu-id="df259-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="df259-193">Serviço ligado: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="df259-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="df259-194">Conjunto de dados: **DatasetBlobSource** e **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="df259-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="df259-195">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="df259-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="df259-196">Certifique-se de que um ficheiro de saída é criado na Olá **apifactoryoutput** pasta Olá **adftutorial** contentor.</span><span class="sxs-lookup"><span data-stu-id="df259-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="df259-197">Obter uma lista de setores de dados com falhas</span><span class="sxs-lookup"><span data-stu-id="df259-197">Get a list of failed data slices</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="df259-198">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="df259-198">Next steps</span></span>
<span data-ttu-id="df259-199">Olá seguinte o exemplo para criar um pipeline com o SDK do .NET que copia dados a partir de uma base de dados de SQL do Azure de tooan de armazenamento do BLOBs do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="df259-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="df259-200">Criar dados de toocopy um pipeline do Blob Storage tooSQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="df259-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
