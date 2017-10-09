---
title: "aaaBuild uma aplicação ASP.NET no Azure com a base de dados SQL | Microsoft Docs"
description: "Saiba como tooget um ASP.NET aplicação a funcionar no Azure, com tooa de ligação da base de dados do SQL Server."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="e3539-103">Criar uma aplicação ASP.NET no Azure com a base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e3539-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="e3539-104">[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.</span><span class="sxs-lookup"><span data-stu-id="e3539-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e3539-105">Este tutorial mostra como toodeploy um ASP.NET condicionada por dados web de aplicação no Azure e ligá-lo demasiado[SQL Database do Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3539-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="e3539-106">Quando tiver terminado, tem uma aplicação ASP.NET em execução no [App Service do Azure](../app-service/app-service-value-prop-what-is.md) e ligado tooSQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="e3539-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Aplicação de ASP.NET publicada na aplicação web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="e3539-108">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="e3539-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e3539-109">Criar uma base de dados do SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="e3539-110">Ligar um tooSQL de aplicação do ASP.NET da base de dados</span><span class="sxs-lookup"><span data-stu-id="e3539-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="e3539-111">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="e3539-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e3539-112">Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="e3539-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e3539-113">Transmitir os registos do Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="e3539-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="e3539-114">Gerir a aplicação Olá no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3539-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3539-115">Prerequisites</span></span>

<span data-ttu-id="e3539-116">toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="e3539-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="e3539-117">Instalar [Visual Studio 2017](https://www.visualstudio.com/downloads/) com Olá seguintes cargas de trabalho:</span><span class="sxs-lookup"><span data-stu-id="e3539-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="e3539-118">**Desenvolvimento do ASP.NET e Web**</span><span class="sxs-lookup"><span data-stu-id="e3539-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="e3539-119">**Desenvolvimento do Azure**</span><span class="sxs-lookup"><span data-stu-id="e3539-119">**Azure development**</span></span>

  ![Desenvolvimento do ASP.NET e Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="e3539-121">Transferir o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="e3539-121">Download hello sample</span></span>

<span data-ttu-id="e3539-122">[Transferir o projeto de exemplo de Olá](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="e3539-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="e3539-123">Extrair (deszipe) Olá *dotnet-sqldb-tutorial-master.zip* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e3539-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="e3539-124">projeto de exemplo de Olá contém num nível básico [ASP.NET MVC](https://www.asp.net/mvc) CRUD (criar-leitura-atualizar-eliminar) utilizando a aplicação [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="e3539-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="e3539-125">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="e3539-125">Run hello app</span></span>

<span data-ttu-id="e3539-126">Abra Olá *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* ficheiro no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3539-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="e3539-127">Tipo `Ctrl+F5` toorun Olá aplicação sem a depuração.</span><span class="sxs-lookup"><span data-stu-id="e3539-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="e3539-128">aplicação Olá é apresentada no seu browser predefinido.</span><span class="sxs-lookup"><span data-stu-id="e3539-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="e3539-129">Selecione Olá **criar novo** ligar e criar alguns *tarefas* itens.</span><span class="sxs-lookup"><span data-stu-id="e3539-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Caixa de diálogo Novo Projeto ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="e3539-131">Olá teste **editar**, **detalhes**, e **eliminar** ligações.</span><span class="sxs-lookup"><span data-stu-id="e3539-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="e3539-132">aplicação Olá utiliza um tooconnect de contexto de base de dados com base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3539-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="e3539-133">Neste exemplo, o contexto de base de dados de Olá utiliza uma cadeia de ligação com o nome `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="e3539-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="e3539-134">a cadeia de ligação Olá está definida no Olá *Web. config* de ficheiros e Olá referenciada na *Models/MyDatabaseContext.cs* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="e3539-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="e3539-135">nome de cadeia de ligação de Olá é utilizado mais tarde na Olá tutorial tooconnect Olá web do Azure aplicação tooan SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="e3539-136">Publicar tooAzure com base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e3539-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="e3539-137">No Olá **Explorador de soluções**, clique com botão direito do **DotNetAppSqlDb** projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publicar a partir do Explorador de Soluções](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="e3539-139">Certifique-se de que o **Serviço de Aplicações do Microsoft Azure** está selecionado e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publicar a partir da página de descrição geral do projeto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="e3539-141">Publicação abre Olá **criar App Service** caixa de diálogo, Olá, que ajuda a criar todos os recursos do Azure, terá de toorun a aplicação web do ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="e3539-142">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="e3539-142">Sign in tooAzure</span></span>

<span data-ttu-id="e3539-143">No Olá **criar App Service** caixa de diálogo, clique em **adicionar uma conta**e, em seguida, inicie sessão tooyour subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="e3539-144">Se já tiver sessão iniciada numa conta Microsoft, confirme que esta inclui a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="e3539-145">Se Olá com sessão iniciada conta Microsoft não tem a sua subscrição do Azure, clique no mesmo tooadd Olá correta da conta.</span><span class="sxs-lookup"><span data-stu-id="e3539-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Inicie sessão no tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="e3539-147">Depois de iniciar sessão, está pronto toocreate que Olá todos os recursos que necessários para a sua aplicação web do Azure nesta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3539-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="e3539-148">Configurar o nome da aplicação Olá web</span><span class="sxs-lookup"><span data-stu-id="e3539-148">Configure hello web app name</span></span>

<span data-ttu-id="e3539-149">Pode manter o nome da aplicação web Olá gerado ou alterá-la tooanother exclusivo (carateres válidos são `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="e3539-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="e3539-150">nome da aplicação Olá web é utilizado como parte do URL do Olá predefinido para a sua aplicação (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome da aplicação web).</span><span class="sxs-lookup"><span data-stu-id="e3539-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="e3539-151">nome da aplicação web Olá tem toobe exclusivo em todas as aplicações no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Criar caixa de diálogo do app service](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="e3539-153">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e3539-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="e3539-154">Seguinte demasiado**grupo de recursos**, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="e3539-154">Next too**Resource Group**, click **New**.</span></span>

![TooResource seguinte grupo, clique em novo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="e3539-156">Grupo de recursos do nome Olá **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="e3539-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="e3539-157">Não clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-157">Do not click **Create**.</span></span> <span data-ttu-id="e3539-158">Terá primeiro de tooset segurança uma base de dados do SQL Server num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="e3539-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e3539-159">Crie um plano do Serviço de Aplicações</span><span class="sxs-lookup"><span data-stu-id="e3539-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e3539-160">Seguinte demasiado**plano do App Service**, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="e3539-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="e3539-161">No Olá **configurar plano do App Service** caixa de diálogo, configurar o plano de serviço aplicacional novo Olá com Olá seguintes definições:</span><span class="sxs-lookup"><span data-stu-id="e3539-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Criar plano do App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="e3539-163">Definição</span><span class="sxs-lookup"><span data-stu-id="e3539-163">Setting</span></span>  | <span data-ttu-id="e3539-164">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="e3539-164">Suggested value</span></span> | <span data-ttu-id="e3539-165">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="e3539-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="e3539-166">**Plano do App Service**</span><span class="sxs-lookup"><span data-stu-id="e3539-166">**App Service Plan**</span></span>| <span data-ttu-id="e3539-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e3539-167">myAppServicePlan</span></span> | [<span data-ttu-id="e3539-168">Planos do Serviço de Aplicações</span><span class="sxs-lookup"><span data-stu-id="e3539-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="e3539-169">**Localização**</span><span class="sxs-lookup"><span data-stu-id="e3539-169">**Location**</span></span>| <span data-ttu-id="e3539-170">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="e3539-170">West Europe</span></span> | [<span data-ttu-id="e3539-171">Regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="e3539-172">**Tamanho**</span><span class="sxs-lookup"><span data-stu-id="e3539-172">**Size**</span></span>| <span data-ttu-id="e3539-173">Gratuito</span><span class="sxs-lookup"><span data-stu-id="e3539-173">Free</span></span> | [<span data-ttu-id="e3539-174">Escalões de preço</span><span class="sxs-lookup"><span data-stu-id="e3539-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="e3539-175">Criar uma instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="e3539-175">Create a SQL Server instance</span></span>

<span data-ttu-id="e3539-176">Antes de criar uma base de dados, é necessário um [servidor lógico da SQL Database do Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="e3539-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="e3539-177">Um servidor lógico contém um grupo de bases de dados geridas como um grupo.</span><span class="sxs-lookup"><span data-stu-id="e3539-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="e3539-178">Selecione **explorar serviços Azure adicionais**.</span><span class="sxs-lookup"><span data-stu-id="e3539-178">Select **Explore additional Azure services**.</span></span>

![Configurar o nome da aplicação Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="e3539-180">No Olá **serviços** separador, clique em Olá  **+**  ícone seguinte demasiado**base de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="e3539-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![No separador de serviços de Olá, clique em Olá + ícone tooSQL seguinte base de dados.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="e3539-182">No Olá **configurar a base de dados do SQL** caixa de diálogo, clique em **novo** seguinte demasiado**do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e3539-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="e3539-183">É gerado um nome de servidor único.</span><span class="sxs-lookup"><span data-stu-id="e3539-183">A unique server name is generated.</span></span> <span data-ttu-id="e3539-184">Este nome é utilizado como parte do URL do Olá predefinido para o servidor lógico, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e3539-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="e3539-185">Tem de ser exclusivo em todas as instâncias de servidor lógico no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="e3539-186">Pode alterar o nome do servidor Olá, mas para este tutorial, mantenha o valor de Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="e3539-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="e3539-187">Adicionar um nome de utilizador administrador e a palavra-passe e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3539-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="e3539-188">Para requisitos de complexidade de palavra-passe, consulte [política de palavra-passe](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="e3539-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="e3539-189">Lembre-se de que este nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="e3539-189">Remember this username and password.</span></span> <span data-ttu-id="e3539-190">Tem servidor lógico de Olá toomanage instância mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e3539-190">You need them toomanage hello logical server instance later.</span></span>

![Criar a instância do SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="e3539-192">Criar uma Base de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="e3539-192">Create a SQL Database</span></span>

<span data-ttu-id="e3539-193">No Olá **configurar a base de dados do SQL** diálogo:</span><span class="sxs-lookup"><span data-stu-id="e3539-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="e3539-194">Manter as predefinições de Olá gerada **nome de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="e3539-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="e3539-195">No **nome da cadeia de ligação**, tipo *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="e3539-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="e3539-196">Este nome tem de corresponder à cadeia de ligação de Olá é referenciada em *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="e3539-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="e3539-197">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3539-197">Select **OK**.</span></span>

![Configurar a base de dados SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="e3539-199">Olá **criar App Service** recursos Olá de mostra a caixa de diálogo que criou.</span><span class="sxs-lookup"><span data-stu-id="e3539-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="e3539-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-200">Click **Create**.</span></span> 

![recursos de Olá criou](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="e3539-202">Depois do Assistente de Olá acaba de criar Olá recursos do Azure, publica a tooAzure de aplicação do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e3539-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="e3539-203">O browser predefinido é iniciado com Olá URL toohello implementado aplicação.</span><span class="sxs-lookup"><span data-stu-id="e3539-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="e3539-204">Adicione alguns itens de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e3539-204">Add a few to-do items.</span></span>

![Aplicação de ASP.NET publicada na aplicação web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="e3539-206">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e3539-206">Congratulations!</span></span> <span data-ttu-id="e3539-207">A aplicação de ASP.NET condicionada por dados está em execução no App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="e3539-208">Acesso Olá base de dados SQL localmente</span><span class="sxs-lookup"><span data-stu-id="e3539-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="e3539-209">Visual Studio permite-lhe explorar e gerir a sua nova base de dados do SQL Server facilmente no Olá **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e3539-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="e3539-210">Criar uma ligação de base de dados</span><span class="sxs-lookup"><span data-stu-id="e3539-210">Create a database connection</span></span>

<span data-ttu-id="e3539-211">De Olá **vista** menu, selecione **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e3539-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="e3539-212">Na parte superior de Olá de **SQL Server Object Explorer**, clique em Olá **adicionar SQL Server** botão.</span><span class="sxs-lookup"><span data-stu-id="e3539-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="e3539-213">Configurar a ligação de base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="e3539-213">Configure hello database connection</span></span>

<span data-ttu-id="e3539-214">No Olá **Connect** caixa de diálogo, expanda Olá **Azure** nós.</span><span class="sxs-lookup"><span data-stu-id="e3539-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="e3539-215">Todas as instâncias de base de dados SQL no Azure estão listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="e3539-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="e3539-216">Selecione Olá `DotNetAppSqlDb` base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e3539-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="e3539-217">ligação de Olá que criou anteriormente é preenchida automaticamente na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3539-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="e3539-218">Escreva a palavra-passe Olá da base de dados administrador que criou anteriormente e clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e3539-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Configure a ligação de base de dados do Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="e3539-220">Permitir a ligação de cliente do computador</span><span class="sxs-lookup"><span data-stu-id="e3539-220">Allow client connection from your computer</span></span>

<span data-ttu-id="e3539-221">Olá **criar uma nova regra de firewall** abrir a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3539-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="e3539-222">Por predefinição, a instância de base de dados SQL só permite ligações a partir de serviços do Azure, tais como a sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="e3539-223">tooconnect tooyour da base de dados, crie uma regra de firewall na instância de base de dados SQL Olá.</span><span class="sxs-lookup"><span data-stu-id="e3539-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="e3539-224">regra de firewall de Olá permite que o endereço IP público Olá do computador local.</span><span class="sxs-lookup"><span data-stu-id="e3539-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="e3539-225">caixa de diálogo Olá já é preenchida com endereço IP público do seu computador.</span><span class="sxs-lookup"><span data-stu-id="e3539-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="e3539-226">Certifique-se de que **Adicionar IP do cliente** está selecionada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3539-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Configurar a firewall para a instância de base de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="e3539-228">Depois do Visual Studio acaba de criar a definição da firewall Olá para a instância de base de dados do SQL Server, a ligação que aparecem no **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e3539-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="e3539-229">Aqui, pode realizar Olá mais comuns da base de dados operações, tais como executadas consultas, criar vistas e procedimentos armazenados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="e3539-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="e3539-230">Clique com o botão direito no Olá `Todoes` tabela e selecione **ver dados**.</span><span class="sxs-lookup"><span data-stu-id="e3539-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Explorar os objetos de base de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="e3539-232">Atualizar a aplicação com código de migrações primeiro</span><span class="sxs-lookup"><span data-stu-id="e3539-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="e3539-233">Pode utilizar ferramentas familiares do Olá no Visual Studio tooupdate a base de dados e a aplicação web no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="e3539-234">Neste passo, utilize migrações primeiro código do Entity Framework toomake um esquema de base de dados de tooyour de alteração e publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e3539-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="e3539-235">Para obter mais informações sobre como utilizar o Entity Framework Code primeiro migrações, consulte [introdução Entity Framework 6 Code First utilizando MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="e3539-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="e3539-236">Atualizar o modelo de dados</span><span class="sxs-lookup"><span data-stu-id="e3539-236">Update your data model</span></span>

<span data-ttu-id="e3539-237">Abra _Models\Todo.cs_ num editor de código Olá.</span><span class="sxs-lookup"><span data-stu-id="e3539-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="e3539-238">Adicionar Olá seguinte propriedade toohello `ToDo` classe:</span><span class="sxs-lookup"><span data-stu-id="e3539-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="e3539-239">Execute migrações primeiro código localmente</span><span class="sxs-lookup"><span data-stu-id="e3539-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="e3539-240">Execute alguns comandos toomake atualizações tooyour local da base de dados.</span><span class="sxs-lookup"><span data-stu-id="e3539-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="e3539-241">De Olá **ferramentas** menu, clique em **Gestor de pacotes NuGet** > **consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="e3539-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="e3539-242">Na janela consola do Gestor de pacote Olá, ative migrações primeiro código:</span><span class="sxs-lookup"><span data-stu-id="e3539-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="e3539-243">Adicione uma migração:</span><span class="sxs-lookup"><span data-stu-id="e3539-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="e3539-244">Atualize a base de dados local Olá:</span><span class="sxs-lookup"><span data-stu-id="e3539-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="e3539-245">Tipo `Ctrl+F5` toorun Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="e3539-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="e3539-246">Olá teste editar detalhes e criar ligações.</span><span class="sxs-lookup"><span data-stu-id="e3539-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="e3539-247">Se a aplicação Olá carrega sem erros, em seguida, migrações primeiro código foi bem sucedida.</span><span class="sxs-lookup"><span data-stu-id="e3539-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="e3539-248">No entanto, a procura de ainda página Olá mesmo porque a lógica de aplicação não está a utilizar esta propriedade novo com ainda.</span><span class="sxs-lookup"><span data-stu-id="e3539-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="e3539-249">Utilize a nova propriedade de Olá</span><span class="sxs-lookup"><span data-stu-id="e3539-249">Use hello new property</span></span>

<span data-ttu-id="e3539-250">Faça algumas alterações no seu Olá de toouse código `Done` propriedade.</span><span class="sxs-lookup"><span data-stu-id="e3539-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="e3539-251">De simplicidade neste tutorial, que só vai toochange Olá `Index` e `Create` vistas propriedade de Olá toosee em ação.</span><span class="sxs-lookup"><span data-stu-id="e3539-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="e3539-252">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="e3539-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="e3539-253">Determinar Olá `Create()` método e adicione `Done` toohello lista de propriedades no Olá `Bind` atributo.</span><span class="sxs-lookup"><span data-stu-id="e3539-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="e3539-254">Quando tiver terminado, a `Create()` assinatura do método aspeto Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="e3539-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="e3539-255">Abra _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e3539-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="e3539-256">No código Razor Olá, deverá ver uma `<div class="form-group">` elemento que utiliza `model.Description`e, em seguida, outra `<div class="form-group">` elemento que utiliza `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="e3539-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="e3539-257">Imediatamente a seguir estes dois elementos, adicione outro `<div class="form-group">` elemento que utiliza `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="e3539-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="e3539-258">Abra _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e3539-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="e3539-259">Procure Olá vazio `<th></th>` elemento.</span><span class="sxs-lookup"><span data-stu-id="e3539-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="e3539-260">Apenas acima este elemento, adicione Olá código Razor os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e3539-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="e3539-261">Determinar Olá `<td>` elemento que contenha Olá `Html.ActionLink()` métodos de programa auxiliar.</span><span class="sxs-lookup"><span data-stu-id="e3539-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="e3539-262">Apenas acima este elemento, adicione Olá código Razor os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e3539-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="e3539-263">É tudo o que precisa toosee alterações Olá Olá `Index` e `Create` vistas.</span><span class="sxs-lookup"><span data-stu-id="e3539-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="e3539-264">Tipo `Ctrl+F5` toorun Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="e3539-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="e3539-265">Agora pode adicionar um item de tarefas e verifique **feito**.</span><span class="sxs-lookup"><span data-stu-id="e3539-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="e3539-266">Em seguida, deve agora mostrar cópias de segurança na sua home page como um item concluído.</span><span class="sxs-lookup"><span data-stu-id="e3539-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="e3539-267">Lembre-se de que Olá `Edit` vista não mostra Olá `Done` campo, porque não foi alterado Olá `Edit` vista.</span><span class="sxs-lookup"><span data-stu-id="e3539-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="e3539-268">Ativar migrações primeiro do código no Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="e3539-269">Agora que o seu código alterar funciona, incluindo a migração de base de dados, publicá-lo tooyour aplicação de web do Azure e atualizar a base de dados do SQL Server com o código de migrações primeiro demasiado.</span><span class="sxs-lookup"><span data-stu-id="e3539-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="e3539-270">Tal como anteriormente, clique no seu projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="e3539-271">Clique em **definições** tooopen Olá publicar assistente.</span><span class="sxs-lookup"><span data-stu-id="e3539-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Definições de publicação aberta](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="e3539-273">No Assistente de Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="e3539-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="e3539-274">Certifique-se essa cadeia de ligação Olá para a base de dados SQL é preenchida no **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="e3539-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="e3539-275">Poderá ser necessário tooselect Olá **myToDoAppDb** base de dados da lista pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="e3539-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="e3539-276">Selecione **executar código primeiro migrações (em execução no início da aplicação)**, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Ativar migrações primeiro código na aplicação web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="e3539-278">Publicar as suas alterações</span><span class="sxs-lookup"><span data-stu-id="e3539-278">Publish your changes</span></span>

<span data-ttu-id="e3539-279">Agora que ativou migrações primeiro código na sua aplicação web do Azure, publique as suas alterações de código.</span><span class="sxs-lookup"><span data-stu-id="e3539-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="e3539-280">No Olá publicar página, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="e3539-281">Tente novamente adicionar itens de tarefas e selecione **feito**, e estes deverão aparecer na sua home page como um item concluído.</span><span class="sxs-lookup"><span data-stu-id="e3539-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Aplicação web do Azure após a migração primeiro código](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="e3539-283">Todos os seus itens de tarefas existentes ainda são apresentados.</span><span class="sxs-lookup"><span data-stu-id="e3539-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="e3539-284">Quando voltar a publicar a aplicação ASP.NET, os dados existentes na sua base de dados do SQL Server não são perdidos.</span><span class="sxs-lookup"><span data-stu-id="e3539-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="e3539-285">Além disso, migrações primeiro código apenas alterações de esquema de dados de Olá e mantém os dados existentes intactas.</span><span class="sxs-lookup"><span data-stu-id="e3539-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="e3539-286">Registos de aplicações de fluxo</span><span class="sxs-lookup"><span data-stu-id="e3539-286">Stream application logs</span></span>

<span data-ttu-id="e3539-287">Pode transmitir mensagens de rastreio diretamente a partir do seu tooVisual de aplicação web do Azure Studio.</span><span class="sxs-lookup"><span data-stu-id="e3539-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="e3539-288">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="e3539-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="e3539-289">Cada ação começa com um `Trace.WriteLine()` método.</span><span class="sxs-lookup"><span data-stu-id="e3539-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="e3539-290">Este código é adicionado tooshow, como o rastreio tooadd mensagens tooyour aplicação de web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="e3539-291">Explorador de servidores aberta</span><span class="sxs-lookup"><span data-stu-id="e3539-291">Open Server Explorer</span></span>

<span data-ttu-id="e3539-292">De Olá **vista** menu, selecione **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="e3539-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="e3539-293">Pode configurar o registo para a sua aplicação web do Azure no **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="e3539-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="e3539-294">Ativar o registo de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="e3539-294">Enable log streaming</span></span>

<span data-ttu-id="e3539-295">No **Explorador de servidores**, expanda **Azure** > **do serviço de aplicações**.</span><span class="sxs-lookup"><span data-stu-id="e3539-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="e3539-296">Expanda Olá **myResourceGroup** grupo de recursos que criou quando criou Olá aplicação de web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="e3539-297">A aplicação web do Azure com o botão direito e selecione **ver registos de transmissão em fluxo**.</span><span class="sxs-lookup"><span data-stu-id="e3539-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Ativar o registo de transmissão em fluxo](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="e3539-299">Olá registos são agora transmissão em fluxo em Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="e3539-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Registo de transmissão em fluxo numa janela de saída](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="e3539-301">No entanto, não vir qualquer uma das mensagens hello do rastreio ainda.</span><span class="sxs-lookup"><span data-stu-id="e3539-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="e3539-302">Da porque quando primeiro selecione **ver registos de transmissão em fluxo**, a aplicação web do Azure define o nível de rastreio de Olá demasiado`Error`, que apenas os registos de eventos de erro (com Olá `Trace.TraceError()` método).</span><span class="sxs-lookup"><span data-stu-id="e3539-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="e3539-303">Níveis de rastreio de alterações</span><span class="sxs-lookup"><span data-stu-id="e3539-303">Change trace levels</span></span>

<span data-ttu-id="e3539-304">rastreio de Olá toochange níveis toooutput outras mensagens de rastreio, acedas novamente demasiado**Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="e3539-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="e3539-305">Faça duplo clique novamente a aplicação web do Azure e selecione **definições**.</span><span class="sxs-lookup"><span data-stu-id="e3539-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="e3539-306">No Olá **registo na aplicação (sistema de ficheiros)** lista pendente, selecione **verboso**.</span><span class="sxs-lookup"><span data-stu-id="e3539-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="e3539-307">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e3539-307">Click **Save**.</span></span>

![Alterar tooVerbose de nível de rastreio](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="e3539-309">Pode experimentar a toosee de níveis de rastreio de diferentes tipos de mensagens são apresentados para cada nível.</span><span class="sxs-lookup"><span data-stu-id="e3539-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="e3539-310">Por exemplo, Olá **informações** nível inclui todos os registos criados pela `Trace.TraceInformation()`, `Trace.TraceWarning()`, e `Trace.TraceError()`, mas não os registos criados pela `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="e3539-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="e3539-311">No seu browser, tente clicar em torno da aplicação de lista de tarefas Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="e3539-312">mensagens Hello do rastreio estão agora transmissão em fluxo toohello **saída** janela no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3539-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="e3539-313">Parar o registo de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="e3539-313">Stop log streaming</span></span>

<span data-ttu-id="e3539-314">toostop Olá o serviço de registo para transmissão em fluxo, clique em Olá **parar a monitorização** botão no Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="e3539-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Parar o registo de transmissão em fluxo](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e3539-316">Gerir a sua aplicação web do Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-316">Manage your Azure web app</span></span>

<span data-ttu-id="e3539-317">Aceda toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicação que criou.</span><span class="sxs-lookup"><span data-stu-id="e3539-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="e3539-318">No menu à esquerda Olá, clique em **do serviço de aplicações**, em seguida, clique no nome de Olá da sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3539-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="e3539-320">Atingiu na página da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e3539-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="e3539-321">Por predefinição, o portal de Olá mostra Olá **descrição geral** página.</span><span class="sxs-lookup"><span data-stu-id="e3539-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="e3539-322">Esta página proporciona-lhe uma vista do desempenho da aplicação.</span><span class="sxs-lookup"><span data-stu-id="e3539-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e3539-323">Aqui, também pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar.</span><span class="sxs-lookup"><span data-stu-id="e3539-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="e3539-324">separadores Olá no lado esquerdo do Olá da página Olá mostram páginas de configuração diferente Olá que pode abrir.</span><span class="sxs-lookup"><span data-stu-id="e3539-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Página Serviço de Aplicações no portal do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e3539-326">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e3539-326">Next steps</span></span>

<span data-ttu-id="e3539-327">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="e3539-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e3539-328">Criar uma base de dados do SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="e3539-329">Ligar um tooSQL de aplicação do ASP.NET da base de dados</span><span class="sxs-lookup"><span data-stu-id="e3539-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="e3539-330">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="e3539-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e3539-331">Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="e3539-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e3539-332">Transmitir os registos do Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="e3539-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="e3539-333">Gerir a aplicação Olá no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e3539-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="e3539-334">Avançar toohello toolearn de tutorial seguinte como toomap um DNS personalizado nome toohello web app.</span><span class="sxs-lookup"><span data-stu-id="e3539-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3539-335">Mapear um existente personalizado DNS nome tooAzure aplicações Web</span><span class="sxs-lookup"><span data-stu-id="e3539-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
