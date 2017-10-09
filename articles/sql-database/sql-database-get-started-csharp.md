---
title: "C#: Introdução à Base de Dados SQL do Azure | Microsoft Docs"
description: "Experimente a base de dados SQL para desenvolver aplicações SQL e c# e criar uma base de dados do SQL do Azure com c# utilizando Olá biblioteca de base de dados SQL para .NET."
keywords: experimentar sql, sql c#
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>Utilizar c# toocreate uma base de dados do SQL Server com Olá biblioteca de base de dados SQL para .NET

Saiba como toouse c# toocreate um Azure SQL da base de dados com Olá [biblioteca de gestão do Microsoft Azure SQL para .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). Este artigo descreve como toocreate uma única base de dados com SQL e c#. conjuntos elásticos toocreate, consulte [criar um conjunto elástico](sql-database-elastic-pool-manage-csharp.md).

Olá biblioteca Gestão de base de dados de SQL do Azure para .NET fornece uma [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-API que encapsula num wrapper Olá baseada no [API de REST de base de dados SQL baseada no Resource Manager](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Muitas funcionalidades novas da base de dados SQL só são suportadas quando estiver a utilizar Olá [modelo de implementação Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), pelo que deve sempre utilizar Olá mais recente **biblioteca Gestão de base de dados de SQL do Azure para .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [pacote NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Olá mais antigo [modelo de implementação clássica com base em bibliotecas](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) são suportados para compatibilidade com versões anteriores apenas, pelo que recomendamos que utilize bibliotecas de Gestor de recursos com base mais recentes Olá.
> 
> 

toocomplete Olá passos descritos neste artigo, seguintes elementos terão Olá:

* Uma subscrição do Azure. Se precisar de uma subscrição do Azure, basta clicar em **conta gratuita** no início de Olá desta página e, em seguida, voltar toofinish neste artigo.
* Visual Studio. Para obter uma cópia gratuita do Visual Studio, consulte Olá [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) página.

> [!NOTE]
> Este artigo cria uma nova base de dados SQL em branco. Modificar Olá *CreateOrUpdateDatabase(...)*  método no Olá seguintes bases de dados de exemplo toocopy, dimensionar as bases de dados, criar uma base de dados de agrupamento, etc.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Criar uma aplicação de consola e instalar as bibliotecas de Olá necessário
1. Inicie o Visual Studio.
2. Clique em **Ficheiro** > **ovo** > **Projeto**.
3. Crie uma **Aplicação de Consola** #C e nomeie-a: *SqlDbConsoleApp*

toocreate uma base de dados SQL com c#, carga Olá necessárias bibliotecas de gestão (utilizando Olá [consola do Gestor de pacotes](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. clique em **Ferramentas** > **Gestor de Pacotes NuGet** > **Consola de Gestor de Pacotes**.
2. Tipo `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall Olá mais recente [biblioteca de gestão do Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Tipo `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall Olá [biblioteca do Microsoft Azure Resource Manager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Tipo `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall Olá [biblioteca de autenticação comuns do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Olá exemplos neste artigo utilizam uma forma síncrona de cada pedido de API e bloco até a conclusão da chamada REST Olá Olá serviço subjacente. Existem métodos assíncronos disponíveis.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Criar uma Base de dados SQL, uma regra de firewall e uma base de dados do SQL – exemplo #C
Olá seguinte exemplo cria um grupo de recursos, servidor, regra de firewall e uma base de dados do SQL Server. Ver, [criar um tooaccess principal de serviço recursos](#create-a-service-principal-to-access-resources) tooget Olá `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variáveis.

Substituir conteúdo Olá **Program.cs** com Olá apresentado a seguir e atualização Olá `{variables}` com os valores de aplicação (não incluem Olá `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a>Criar um tooaccess principal do serviço de recursos
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



## <a name="next-steps"></a>Passos seguintes
Agora que já experimentou a base de dados SQL e configurou uma base de dados com c#, está pronto para Olá seguintes artigos:

* [Ligar tooSQL da base de dados com o SQL Server Management Studio e executar uma consulta de T-SQL de exemplo](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Recursos Adicionais
* [Base de Dados SQL](https://azure.microsoft.com/documentation/services/sql-database/)
* [Classe de Base de Dados](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
