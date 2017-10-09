---
title: aaaManage da Azure Search com scripts do Powershell | Microsoft Docs
description: "Gerir o serviço da Azure Search com scripts do PowerShell. Criar ou atualizar um serviço da Azure Search e gerir chaves de administração de pesquisa do Azure"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="97229-104">Gerir o serviço de pesquisa do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="97229-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97229-105">Portal</span><span class="sxs-lookup"><span data-stu-id="97229-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="97229-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97229-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="97229-107">Este tópico descreve tooperform de comandos do PowerShell Olá muitas das tarefas de gestão de Olá para serviços de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="97229-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="97229-108">Iremos irá guiá-se a criação de um serviço de pesquisa, dimensionamento-lo e gerir as respetivas chaves de API.</span><span class="sxs-lookup"><span data-stu-id="97229-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="97229-109">Estes comandos paralela Olá as opções de gestão disponíveis na Olá [API de REST de gestão do Azure Search](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="97229-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97229-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97229-110">Prerequisites</span></span>
* <span data-ttu-id="97229-111">Tem de ter o Azure PowerShell 1.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="97229-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="97229-112">Para obter instruções, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97229-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="97229-113">Tem de ser registado no tooyour subscrição do Azure no PowerShell, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="97229-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="97229-114">Em primeiro lugar, tem tooAzure de início de sessão com este comando:</span><span class="sxs-lookup"><span data-stu-id="97229-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="97229-115">Especifique o endereço de correio eletrónico Olá da sua conta do Azure e a palavra-passe na caixa de diálogo de início de sessão de Microsoft Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="97229-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="97229-116">Em alternativa, pode [início de sessão forma não interativa com um principal de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="97229-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="97229-117">Se tiver várias subscrições do Azure, terá de tooset sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="97229-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="97229-118">toosee uma lista das suas subscrições atuais, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="97229-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="97229-119">toospecify Olá subscrição executar Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="97229-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="97229-120">No seguinte exemplo de Olá, nome da subscrição Olá é `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="97229-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="97229-121">Toohelp comandos começar</span><span class="sxs-lookup"><span data-stu-id="97229-121">Commands toohelp you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="97229-122">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="97229-122">Next Steps</span></span>
<span data-ttu-id="97229-123">Agora que criou o seu serviço, que pode tomar passos Olá: criar um [índice](search-what-is-an-index.md), [consultar um índice](search-query-overview.md)e, finalmente, criar e gerir a sua própria aplicação de pesquisa que utiliza a Azure Search.</span><span class="sxs-lookup"><span data-stu-id="97229-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="97229-124">Criar um índice da Azure Search no portal do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="97229-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="97229-125">Consultar um índice da Azure Search utilizando o Explorador de pesquisa na Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="97229-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="97229-126">Configurar um indexador tooload de dados de outros serviços</span><span class="sxs-lookup"><span data-stu-id="97229-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="97229-127">Como toouse Azure pesquisar no .NET</span><span class="sxs-lookup"><span data-stu-id="97229-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="97229-128">Analisar o tráfego de pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="97229-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

