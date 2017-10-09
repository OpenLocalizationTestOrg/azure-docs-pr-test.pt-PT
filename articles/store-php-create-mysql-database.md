---
title: aaaCreate e ligue-se a base de dados MySQL tooa no Azure
description: "Saiba como toouse Olá toocreate do portal do Azure, uma base de dados MySQL e, em seguida, ligar tooit a partir de uma aplicação web do PHP no Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="6bc6f-103">Criar e ligar tooa de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="6bc6f-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="6bc6f-104">Este tutorial mostra como toocreate um MySQL da base de dados no Olá [portal do Azure](https://portal.azure.com) (fornecedor é [ClearDB](http://www.cleardb.com/)) e como tooconnect tooit de um PHP web de aplicação em execução no [App Service do Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6bc6f-105">Também pode criar uma base de dados MySQL como parte de um [modelo de aplicação Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="6bc6f-106">Criar uma base de dados MySQL no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6bc6f-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="6bc6f-107">toocreate uma base de dados MySQL no portal do Azure, de Olá Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="6bc6f-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="6bc6f-108">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6bc6f-109">No menu à esquerda Olá, clique em **novo** > **dados + armazenamento** > **base de dados MySQL**.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Criar uma base de dados MySQL no Azure - início](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="6bc6f-111">No Olá nova base de dados MySQL [painel](azure-portal-overview.md), configurar a sua nova base de dados MySQL da seguinte forma (*painel*: uma página de portal abre-se horizontalmente):</span><span class="sxs-lookup"><span data-stu-id="6bc6f-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="6bc6f-112">**Nome de base de dados**: escreva um nome de forma exclusiva</span><span class="sxs-lookup"><span data-stu-id="6bc6f-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="6bc6f-113">**Subscrição**: escolha Olá toouse de subscrição</span><span class="sxs-lookup"><span data-stu-id="6bc6f-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="6bc6f-114">**Tipo de base de dados**: selecione **partilhados** de camadas de baixo custo ou livres, ou **dedicado** tooget dedicado recursos.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="6bc6f-115">**Grupo de recursos**: Adicionar Olá MySQL da base de dados tooan existente [grupo de recursos](azure-resource-manager/resource-group-overview.md) ou colocá-la num novo.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="6bc6f-116">Recursos Olá mesmo grupo pode ser facilmente gerido em conjunto.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="6bc6f-117">**Localização**: selecione uma tooyou de fecho de localização.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="6bc6f-118">Ao adicionar tooan existente grupo de recursos, está a localização do grupo de recursos toohello bloqueado.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="6bc6f-119">**Escalão de preço**: clique em **escalão de preço**, em seguida, selecione uma opção de preço (**mercúrio** camada é gratuita) e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="6bc6f-120">**Termos legais**: clique em **termos legais**, reveja os detalhes de compra Olá e clique em **comprar**.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="6bc6f-121">**PIN toodashboard**: selecione se pretende tooaccess-lo diretamente a partir do dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="6bc6f-122">Isto é especialmente útil se não estiver familiarizado com ainda navegação do portal.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="6bc6f-123">Olá seguinte captura de ecrã é apenas um exemplo de como pode configurar a base de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Criar uma base de dados MySQL no Azure - configurar](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="6bc6f-125">Quando terminar, configurar, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-125">When you're done configuring, click **Create**.</span></span>

    ![Criar uma base de dados MySQL no Azure - criar](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="6bc6f-127">Verá uma notificação de pop-up permitindo que sabe que a implementação foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Criar uma base de dados MySQL no Azure - em curso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="6bc6f-129">Irá obter outro pop-up assim que a implementação é concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="6bc6f-130">portal de Olá também irá abrir o painel de base de dados MySQL automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="6bc6f-131">Ligar a base de dados MySQL tooyour</span><span class="sxs-lookup"><span data-stu-id="6bc6f-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="6bc6f-132">informações de ligação de Olá toosee para a sua nova base de dados MySQL, basta clicar **propriedades** no painel da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Criar uma base de dados MySQL no Azure - painel de base de dados MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="6bc6f-134">Agora, pode utilizar essas informações de ligação em qualquer aplicação web.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="6bc6f-135">Um exemplo que mostra como estão disponíveis informações de ligação de Olá toouse a partir de uma aplicação PHP simple [aqui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="6bc6f-136">Ligar uma aplicação de web Laravel (a partir de Olá PHP tutorial de introdução)</span><span class="sxs-lookup"><span data-stu-id="6bc6f-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="6bc6f-137">Suponha tutorial Olá apenas terminar [criar, configurar e implementar uma tooAzure de aplicação web PHP](app-service-web/app-service-web-php-get-started.md) e ter um [Laravel](https://www.laravel.com/) aplicação web em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="6bc6f-138">Pode facilmente adicionar base de dados capacidades tooyour Laravel aplicação.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="6bc6f-139">Basta seguir os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="6bc6f-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="6bc6f-140">Olá seguintes passos assumem que tiver concluído o tutorial Olá [criar, configurar e implementar uma tooAzure de aplicação web PHP](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="6bc6f-141">Configure aplicação de Laravel Olá no desenvolvimento local ambiente toopoint toohello base de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="6bc6f-142">toodo, abra `.env` da sua aplicação Laravel diretório de raiz e configurar opções de base de dados MySQL Olá.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="6bc6f-143">No Olá **propriedades** painel, nome de Olá da base de dados MySQL poderá ou poderá não ser Olá um apresentada no Olá **nome de base de dados** campo.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="6bc6f-144">É melhor toocheck de parâmetro de base de dados de Olá na Olá **cadeia de ligação** campo.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Criar uma base de dados MySQL no Azure - em curso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="6bc6f-146">Olá tooverify de forma mais rápida que têm acesso de MySQL agora é toouse [andaime de autenticação predefinido do Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="6bc6f-147">No terminal da linha de comandos de Olá, execute os seguintes comandos do diretório de raiz da sua aplicação Laravel de Olá:</span><span class="sxs-lookup"><span data-stu-id="6bc6f-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="6bc6f-148">comando primeiro Olá cria tabelas Olá no Azure com base nas migrações predefinidas no Olá `database/migrations` directory e o segundo comando de Olá andaimes Olá básicas vistas e rotas de registo de utilizador e a autenticação.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="6bc6f-149">Execute o servidor de desenvolvimento de Olá agora:</span><span class="sxs-lookup"><span data-stu-id="6bc6f-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="6bc6f-150">No browser Olá, navegue toohttp://localhost:8000 e registar um novo utilizador conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="6bc6f-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Ligar a base de dados de tooMySQL no Azure - registar utilizador](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="6bc6f-152">Siga o registo de linha de comandos Olá concluída Olá IU.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="6bc6f-153">Depois de registo é concluído, será registado no.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-153">Once registration completes, you will be logged in.</span></span>

    ![Ligar a base de dados de tooMySQL no Azure - registar utilizador](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="6bc6f-155">Agora está a desenvolver a sua aplicação em relação a base de dados MySQL Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="6bc6f-156">Agora, basta tooreplicate sua `.env` aplicação de web do Azure tooyour de definições.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="6bc6f-157">Execute Olá os seguintes comandos da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="6bc6f-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="6bc6f-158">Em seguida, consolide e emita tooAzure Olá local as alterações efetuadas anteriormente ao ser executado `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="6bc6f-159">Procure a aplicação de web do Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="6bc6f-160">Inicie sessão com credenciais de utilizador de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-160">Log in using hello user credentials you created earlier.</span></span>

    ![Ligar a base de dados de tooMySQL no Azure - procurar tooAzure web app](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="6bc6f-162">Depois de iniciar sessão, verá o ecrã de início de pós-sessão de amigável Olá.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Ligar tooMySQL base de dados no Azure - com sessão iniciado](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="6bc6f-164">Parabéns, a sua aplicação web do PHP no Azure está agora a aceder aos dados da sua base de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="6bc6f-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bc6f-165">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6bc6f-165">Next steps</span></span>
<span data-ttu-id="6bc6f-166">Para obter mais informações, consulte Olá [Centro para programadores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="6bc6f-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
