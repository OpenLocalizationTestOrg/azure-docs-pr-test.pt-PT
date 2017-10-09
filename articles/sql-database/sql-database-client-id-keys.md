---
title: "valores de aaaGet para autenticação da aplicação - SQL Database do Azure | Microsoft Docs"
description: "Crie um principal de serviço para aceder à base de dados SQL a partir do código."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a>Obter valores de Olá necessário para autenticar um tooaccess de aplicação de base de dados SQL a partir do código
toocreate e gerir a base de dados SQL a partir do código tem de registar a aplicação no domínio de Azure Active Directory (AAD) Olá na subscrição olá onde os recursos do Azure foram criados.

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a>Criar um tooaccess principal do serviço de recursos de uma aplicação
Precisa de mais recente toohave Olá [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

Olá seguinte script do PowerShell cria aplicações do Olá do Active Directory (AD) e o serviço de Olá principal que precisamos tooauthenticate nossa aplicação c#. script de Olá produz os valores que precisa para Olá precedente c# de exemplo. Para obter informações detalhadas, consulte [utilize o Azure PowerShell toocreate um principal de serviço tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a>Consultar também
* [Criar uma base de dados SQL com c#](sql-database-get-started-csharp.md)
* [Ligar tooSQL da base de dados ao utilizar o Azure autenticação do Active Directory](sql-database-aad-authentication.md)

