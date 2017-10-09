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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Criar e ligar tooa de dados MySQL no Azure
Este tutorial mostra como toocreate um MySQL da base de dados no Olá [portal do Azure](https://portal.azure.com) (fornecedor é [ClearDB](http://www.cleardb.com/)) e como tooconnect tooit de um PHP web de aplicação em execução no [App Service do Azure](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Também pode criar uma base de dados MySQL como parte de um [modelo de aplicação Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Criar uma base de dados MySQL no portal do Azure
toocreate uma base de dados MySQL no portal do Azure, de Olá Olá seguintes:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda Olá, clique em **novo** > **dados + armazenamento** > **base de dados MySQL**.

    ![Criar uma base de dados MySQL no Azure - início](./media/store-php-create-mysql-database/create-db-1-start.png)
3. No Olá nova base de dados MySQL [painel](azure-portal-overview.md), configurar a sua nova base de dados MySQL da seguinte forma (*painel*: uma página de portal abre-se horizontalmente):

   * **Nome de base de dados**: escreva um nome de forma exclusiva
   * **Subscrição**: escolha Olá toouse de subscrição
   * **Tipo de base de dados**: selecione **partilhados** de camadas de baixo custo ou livres, ou **dedicado** tooget dedicado recursos.
   * **Grupo de recursos**: Adicionar Olá MySQL da base de dados tooan existente [grupo de recursos](azure-resource-manager/resource-group-overview.md) ou colocá-la num novo. Recursos Olá mesmo grupo pode ser facilmente gerido em conjunto.
   * **Localização**: selecione uma tooyou de fecho de localização. Ao adicionar tooan existente grupo de recursos, está a localização do grupo de recursos toohello bloqueado.
   * **Escalão de preço**: clique em **escalão de preço**, em seguida, selecione uma opção de preço (**mercúrio** camada é gratuita) e, em seguida, clique em **selecione**.
   * **Termos legais**: clique em **termos legais**, reveja os detalhes de compra Olá e clique em **comprar**.
   * **PIN toodashboard**: selecione se pretende tooaccess-lo diretamente a partir do dashboard de Olá. Isto é especialmente útil se não estiver familiarizado com ainda navegação do portal.

     Olá seguinte captura de ecrã é apenas um exemplo de como pode configurar a base de dados MySQL.  
     ![Criar uma base de dados MySQL no Azure - configurar](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Quando terminar, configurar, clique em **criar**.

    ![Criar uma base de dados MySQL no Azure - criar](./media/store-php-create-mysql-database/create-db-3-create.png)

    Verá uma notificação de pop-up permitindo que sabe que a implementação foi iniciada.

    ![Criar uma base de dados MySQL no Azure - em curso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Irá obter outro pop-up assim que a implementação é concluída com êxito. portal de Olá também irá abrir o painel de base de dados MySQL automaticamente.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Ligar a base de dados MySQL tooyour
informações de ligação de Olá toosee para a sua nova base de dados MySQL, basta clicar **propriedades** no painel da sua aplicação web.

![Criar uma base de dados MySQL no Azure - painel de base de dados MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Agora, pode utilizar essas informações de ligação em qualquer aplicação web. Um exemplo que mostra como estão disponíveis informações de ligação de Olá toouse a partir de uma aplicação PHP simple [aqui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Ligar uma aplicação de web Laravel (a partir de Olá PHP tutorial de introdução)
Suponha tutorial Olá apenas terminar [criar, configurar e implementar uma tooAzure de aplicação web PHP](app-service-web/app-service-web-php-get-started.md) e ter um [Laravel](https://www.laravel.com/) aplicação web em execução no Azure. Pode facilmente adicionar base de dados capacidades tooyour Laravel aplicação. Basta seguir os passos de Olá abaixo:

> [!NOTE]
> Olá seguintes passos assumem que tiver concluído o tutorial Olá [criar, configurar e implementar uma tooAzure de aplicação web PHP](app-service-web/app-service-web-php-get-started.md).
>
>

1. Configure aplicação de Laravel Olá no desenvolvimento local ambiente toopoint toohello base de dados MySQL. toodo, abra `.env` da sua aplicação Laravel diretório de raiz e configurar opções de base de dados MySQL Olá.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > No Olá **propriedades** painel, nome de Olá da base de dados MySQL poderá ou poderá não ser Olá um apresentada no Olá **nome de base de dados** campo. É melhor toocheck de parâmetro de base de dados de Olá na Olá **cadeia de ligação** campo.    
   >
   > ![Criar uma base de dados MySQL no Azure - em curso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Olá tooverify de forma mais rápida que têm acesso de MySQL agora é toouse [andaime de autenticação predefinido do Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   No terminal da linha de comandos de Olá, execute os seguintes comandos do diretório de raiz da sua aplicação Laravel de Olá:

         php artisan migrate
         php artisan make:auth

    comando primeiro Olá cria tabelas Olá no Azure com base nas migrações predefinidas no Olá `database/migrations` directory e o segundo comando de Olá andaimes Olá básicas vistas e rotas de registo de utilizador e a autenticação.
3. Execute o servidor de desenvolvimento de Olá agora:

        php artisan serve
4. No browser Olá, navegue toohttp://localhost:8000 e registar um novo utilizador conforme mostrado:

    ![Ligar a base de dados de tooMySQL no Azure - registar utilizador](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Siga o registo de linha de comandos Olá concluída Olá IU. Depois de registo é concluído, será registado no.

    ![Ligar a base de dados de tooMySQL no Azure - registar utilizador](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Agora está a desenvolver a sua aplicação em relação a base de dados MySQL Olá no Azure.
5. Agora, basta tooreplicate sua `.env` aplicação de web do Azure tooyour de definições. Execute Olá os seguintes comandos da CLI do Azure:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Em seguida, consolide e emita tooAzure Olá local as alterações efetuadas anteriormente ao ser executado `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Procure a aplicação de web do Azure toohello.

        azure site browse
8. Inicie sessão com credenciais de utilizador de Olá que criou anteriormente.

    ![Ligar a base de dados de tooMySQL no Azure - procurar tooAzure web app](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Depois de iniciar sessão, verá o ecrã de início de pós-sessão de amigável Olá.

    ![Ligar tooMySQL base de dados no Azure - com sessão iniciado](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Parabéns, a sua aplicação web do PHP no Azure está agora a aceder aos dados da sua base de dados MySQL.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá [Centro para programadores do PHP](/develop/php/).
