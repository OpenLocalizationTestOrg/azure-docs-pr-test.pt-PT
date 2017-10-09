---
title: "aaaCreate PHP-SQL aplicação web e implementar tooAzure do serviço de aplicações utilizando o Git"
description: "Um tutorial que demonstra como toocreate um PHP web app, que armazena dados numa SQL Database do Azure e utilizar tooAzure de implementação de Git do serviço de aplicações."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="d4032-103">Criar uma aplicação web do PHP-SQL e implementar tooAzure do serviço de aplicações utilizando o Git</span><span class="sxs-lookup"><span data-stu-id="d4032-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="d4032-104">Este tutorial mostra como toocreate um PHP web de aplicação no [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que estabelece ligação tooAzure base de dados SQL e como toodeploy-lo utilizando o Git.</span><span class="sxs-lookup"><span data-stu-id="d4032-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="d4032-105">Este tutorial parte do princípio de que tem [PHP][install-php], [SQL Server Express][install-SQLExpress], Olá [Drivers Microsoft para SQL Server para PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), e [Git] [ install-git] instalado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d4032-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="d4032-106">Após concluir neste guia, terá uma aplicação web de SQL do PHP em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="d4032-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d4032-107">Pode instalar e configurar o PHP, SQL Server Express e Olá Drivers Microsoft para o SQL Server para PHP utilizando Olá [instalador de plataforma Web Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4032-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="d4032-108">Aprenderá:</span><span class="sxs-lookup"><span data-stu-id="d4032-108">You will learn:</span></span>

* <span data-ttu-id="d4032-109">Como toocreate um Azure web app e uma base de dados do SQL Server utilizando Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="d4032-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="d4032-110">Porque o PHP está ativado nas Web Apps do App Service, por predefinição, é nothing especial toorun necessário o código do PHP.</span><span class="sxs-lookup"><span data-stu-id="d4032-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="d4032-111">Como toopublish e Republica a tooAzure de aplicação utilizando o Git.</span><span class="sxs-lookup"><span data-stu-id="d4032-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="d4032-112">Ao seguir este tutorial, irá criar uma aplicação web simples registo PHP.</span><span class="sxs-lookup"><span data-stu-id="d4032-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="d4032-113">Olá aplicação será alojada num Web site do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4032-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="d4032-114">Abaixo é uma captura de ecrã da aplicação Olá concluída:</span><span class="sxs-lookup"><span data-stu-id="d4032-114">A screenshot of hello completed application is below:</span></span>

![Web Site do PHP do Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d4032-116">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="d4032-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d4032-117">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="d4032-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="d4032-118">Criar uma aplicação web do Azure e configurar a publicação de Git</span><span class="sxs-lookup"><span data-stu-id="d4032-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="d4032-119">Siga estes passos toocreate uma aplicação web do Azure e uma base de dados do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="d4032-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="d4032-120">Inicie sessão no toohello [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d4032-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d4032-121">Abra Olá Azure Marketplace, clicando em Olá **novo** ícone na parte superior do Olá esquerda do dashboard de Olá, clique em **Selecionar tudo** seguinte tooMarketplace e selecionando **Web + móvel**.</span><span class="sxs-lookup"><span data-stu-id="d4032-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="d4032-122">No Marketplace Olá, selecione **Web + móvel**.</span><span class="sxs-lookup"><span data-stu-id="d4032-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="d4032-123">Clique em Olá **aplicação Web + SQL** ícone.</span><span class="sxs-lookup"><span data-stu-id="d4032-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="d4032-124">Depois de ler a descrição de Olá da aplicação Web de Olá + aplicação SQL Server, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="d4032-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="d4032-125">Clique em cada parte (**grupo de recursos**, **aplicação Web**, **base de dados**, e **subscrição**) e introduza ou selecione os valores de Olá necessário campos:</span><span class="sxs-lookup"><span data-stu-id="d4032-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="d4032-126">Introduza um nome de URL à sua escolha</span><span class="sxs-lookup"><span data-stu-id="d4032-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="d4032-127">Configure as credenciais do servidor de base de dados</span><span class="sxs-lookup"><span data-stu-id="d4032-127">Configure database server credentials</span></span>
   * <span data-ttu-id="d4032-128">Selecione Olá região mais próxima tooyou</span><span class="sxs-lookup"><span data-stu-id="d4032-128">Select hello region closest tooyou</span></span>
     
     ![configurar a sua aplicação](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="d4032-130">Quando terminar a definição de aplicação web de Olá, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="d4032-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="d4032-131">Quando tiver sido criada a aplicação web de Olá, Olá **notificações** botão será flash um verde **êxito** e Olá, ambos os Olá web app e Olá base de dados SQL no grupo de Olá tooshow aberta de painel do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4032-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="d4032-132">Clique em ícone da aplicação web Olá no painel de Olá recursos grupo Painel tooopen Olá da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="d4032-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![grupo de recursos da aplicação de Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="d4032-134">No **definições** clique **a implementação contínua** > **configurar definições necessárias**.</span><span class="sxs-lookup"><span data-stu-id="d4032-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="d4032-135">Selecione **repositório de Git Local** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4032-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![onde está o código de origem](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="d4032-137">Se não tiver configurado um repositório de Git antes, tem de fornecer um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="d4032-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="d4032-138">toodo, clique em **definições** > **as credenciais de implementação** no painel da aplicação web Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="d4032-139">No **definições** clique em **propriedades** toosee Olá remoto URL do Git terá toouse toodeploy sua aplicação PHP mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d4032-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="d4032-140">Obter informações de ligação de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="d4032-140">Get SQL Database connection information</span></span>
<span data-ttu-id="d4032-141">tooconnect toohello instância de base de dados do SQL Server que está ligado tooyour web app, sua será necessário Olá informações de ligação, o que especificou quando criou a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="d4032-142">Olá tooget informações de ligação de base de dados SQL, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="d4032-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="d4032-143">No painel do grupo de recursos Olá, clique o ícone de Olá SQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="d4032-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="d4032-144">No painel de Olá SQL da base de dados, clique em **definições** > **propriedades**, em seguida, clique em **Mostrar cadeias de ligação de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="d4032-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Ver propriedades de base de dados](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="d4032-146">De Olá **PHP** secção caixa de diálogo resultante de Olá, tome nota dos valores de Olá para `Server`, `SQL Database`, e `User Name`.</span><span class="sxs-lookup"><span data-stu-id="d4032-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="d4032-147">Irá utilizar estes valores mais tarde quando publicar a tooAzure de aplicação web do PHP do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="d4032-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="d4032-148">Criar e testar a aplicação localmente</span><span class="sxs-lookup"><span data-stu-id="d4032-148">Build and test your application locally</span></span>
<span data-ttu-id="d4032-149">Olá aplicação de registo é uma aplicação PHP simples que lhe permite tooregister um evento, fornecendo o nome e endereço de e-mail.</span><span class="sxs-lookup"><span data-stu-id="d4032-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="d4032-150">São apresentadas informações sobre registrants anteriores numa tabela.</span><span class="sxs-lookup"><span data-stu-id="d4032-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="d4032-151">As informações de registo são armazenadas numa instância de base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d4032-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="d4032-152">aplicação Olá consiste em dois ficheiros (código de copiar/colar disponíveis abaixo):</span><span class="sxs-lookup"><span data-stu-id="d4032-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="d4032-153">**Index.php**: apresenta um formulário de registo e uma tabela que contém informações de registrant.</span><span class="sxs-lookup"><span data-stu-id="d4032-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="d4032-154">**createtable.php**: cria Olá tabela de base de dados SQL para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="d4032-155">Este ficheiro só será utilizado uma vez.</span><span class="sxs-lookup"><span data-stu-id="d4032-155">This file will only be used once.</span></span>

<span data-ttu-id="d4032-156">aplicação de Olá toorun localmente, siga os passos de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="d4032-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="d4032-157">Tenha em atenção que estes passos partem do princípio de que tem o PHP e do SQL Server Express configurar no seu computador local e, se tiver ativado o Olá [extensão PDO para o SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="d4032-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="d4032-158">Criar uma base de dados do SQL Server chamado `registration`.</span><span class="sxs-lookup"><span data-stu-id="d4032-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="d4032-159">Pode fazê-lo de Olá `sqlcmd` linha de comandos com estes comandos:</span><span class="sxs-lookup"><span data-stu-id="d4032-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="d4032-160">No diretório de raiz da aplicação, crie dois ficheiros na mesma - um chamado `createtable.php` e outra denominada `index.php`.</span><span class="sxs-lookup"><span data-stu-id="d4032-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="d4032-161">Abra Olá `createtable.php` ficheiro num editor de texto ou IDE e adicione o código de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="d4032-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="d4032-162">Este código será utilizado toocreate Olá `registration_tbl` tabela Olá `registration` base de dados.</span><span class="sxs-lookup"><span data-stu-id="d4032-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="d4032-163">Tenha em atenção que, terá de valores de Olá tooupdate para <code>$user</code> e <code>$pwd</code> com o nome de utilizador local do SQL Server e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="d4032-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="d4032-164">Num terminal no diretório de raiz de Olá da Olá de tipo de aplicação Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d4032-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="d4032-165">Abra um browser e navegue demasiado**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="d4032-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="d4032-166">Esta ação irá criar Olá `registration_tbl` tabela na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="d4032-167">Abra Olá **index.php** ficheiro num editor de texto ou IDE e adicione Olá básico código HTML e CSS para a página Olá (Olá código PHP será adicionado em passos posteriores).</span><span class="sxs-lookup"><span data-stu-id="d4032-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="d4032-168">Dentro de etiquetas PHP Olá, adicione o código do PHP para ligar toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="d4032-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="d4032-169">Novamente, terá de valores de Olá tooupdate para <code>$user</code> e <code>$pwd</code> com o nome de utilizador de MySQL local e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="d4032-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="d4032-170">Seguindo o código de ligação de base de dados de Olá, adicione o código para inserir informações de registo da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="d4032-171">Por fim, seguindo o código de Olá acima, adicione o código para obter dados da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="d4032-172">Agora pode navegar demasiado**http://localhost:8000/index.php** aplicação de Olá tootest.</span><span class="sxs-lookup"><span data-stu-id="d4032-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="d4032-173">Publicar a aplicação</span><span class="sxs-lookup"><span data-stu-id="d4032-173">Publish your application</span></span>
<span data-ttu-id="d4032-174">Depois de ter testado a aplicação localmente, pode publicá-lo tooApp as Web Apps Service utilizando o Git.</span><span class="sxs-lookup"><span data-stu-id="d4032-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="d4032-175">No entanto, primeiro precisa de informações de ligação do tooupdate Olá da base de dados na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="d4032-176">Utilização de informações de ligação de base de dados de Olá que obteve anteriormente (no Olá **informações de ligação de obter a base de dados do SQL** secção), Olá de atualização que seguir as informações no **ambos** Olá `createdatabase.php` e `index.php` ficheiros com Olá adequado valores:</span><span class="sxs-lookup"><span data-stu-id="d4032-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="d4032-177">No Olá <code>$host</code>, valor hello do servidor tem de ser prepended com <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="d4032-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="d4032-178">Agora, está pronto tooset segurança publicação de Git e publicar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="d4032-179">Estes são os mesmos passos indicados no fim de Olá do Olá de Olá **criar uma aplicação web do Azure e configurar a publicação de Git** secção acima.</span><span class="sxs-lookup"><span data-stu-id="d4032-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="d4032-180">Abrir GitBash (ou um terminal, se for Git no seu `PATH`), alterar o diretório de raiz de toohello de diretórios da aplicação (Olá **registo** diretório), e Olá execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d4032-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="d4032-181">Será solicitado para a palavra-passe de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d4032-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="d4032-182">Procurar demasiado**http://[web aplicação name].azurewebsites.net/createtable.php** toocreate tabela na base de dados SQL Olá para aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="d4032-183">Procurar demasiado**http://[web aplicação name].azurewebsites.net/index.php** toobegin utilizando a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d4032-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="d4032-184">Depois de ter publicado a aplicação, pode começar efetuar alterações tooit e utilizar o Git toopublish-los.</span><span class="sxs-lookup"><span data-stu-id="d4032-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="d4032-185">Publicar alterações tooyour aplicação</span><span class="sxs-lookup"><span data-stu-id="d4032-185">Publish changes tooyour application</span></span>
<span data-ttu-id="d4032-186">toopublish alterações tooapplication, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="d4032-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="d4032-187">Efetue as alterações tooyour aplicação localmente.</span><span class="sxs-lookup"><span data-stu-id="d4032-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="d4032-188">Abrir GitBash (ou um terminal, it Git está no seu `PATH`), altere o diretório de raiz de toohello de diretórios da sua aplicação e execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d4032-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="d4032-189">Será solicitado para a palavra-passe de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d4032-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="d4032-190">Procurar demasiado**http://[web aplicação name].azurewebsites.net/index.php** toosee as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="d4032-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d4032-191">O que mudou</span><span class="sxs-lookup"><span data-stu-id="d4032-191">What's changed</span></span>
* <span data-ttu-id="d4032-192">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d4032-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

