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
# <a name="manage-your-azure-search-service-with-powershell"></a>Gerir o serviço de pesquisa do Azure com o PowerShell
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

Este tópico descreve tooperform de comandos do PowerShell Olá muitas das tarefas de gestão de Olá para serviços de pesquisa do Azure. Iremos irá guiá-se a criação de um serviço de pesquisa, dimensionamento-lo e gerir as respetivas chaves de API.
Estes comandos paralela Olá as opções de gestão disponíveis na Olá [API de REST de gestão do Azure Search](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Pré-requisitos
* Tem de ter o Azure PowerShell 1.0 ou superior. Para obter instruções, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).
* Tem de ser registado no tooyour subscrição do Azure no PowerShell, conforme descrito abaixo.

Em primeiro lugar, tem tooAzure de início de sessão com este comando:

    Login-AzureRmAccount

Especifique o endereço de correio eletrónico Olá da sua conta do Azure e a palavra-passe na caixa de diálogo de início de sessão de Microsoft Azure de Olá.

Em alternativa, pode [início de sessão forma não interativa com um principal de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Se tiver várias subscrições do Azure, terá de tooset sua subscrição do Azure. toosee uma lista das suas subscrições atuais, execute este comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify Olá subscrição executar Olá os seguintes comandos. No seguinte exemplo de Olá, nome da subscrição Olá é `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Toohelp comandos começar
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

## <a name="next-steps"></a>Passos Seguintes
Agora que criou o seu serviço, que pode tomar passos Olá: criar um [índice](search-what-is-an-index.md), [consultar um índice](search-query-overview.md)e, finalmente, criar e gerir a sua própria aplicação de pesquisa que utiliza a Azure Search.

* [Criar um índice da Azure Search no portal do Azure de Olá](search-create-index-portal.md)
* [Consultar um índice da Azure Search utilizando o Explorador de pesquisa na Olá portal do Azure](search-explorer.md)
* [Configurar um indexador tooload de dados de outros serviços](search-indexer-overview.md)
* [Como toouse Azure pesquisar no .NET](search-howto-dotnet-sdk.md)
* [Analisar o tráfego de pesquisa do Azure](search-traffic-analytics.md)

