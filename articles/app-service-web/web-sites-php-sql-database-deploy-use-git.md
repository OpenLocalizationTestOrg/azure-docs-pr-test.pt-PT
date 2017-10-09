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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Criar uma aplicação web do PHP-SQL e implementar tooAzure do serviço de aplicações utilizando o Git
Este tutorial mostra como toocreate um PHP web de aplicação no [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que estabelece ligação tooAzure base de dados SQL e como toodeploy-lo utilizando o Git. Este tutorial parte do princípio de que tem [PHP][install-php], [SQL Server Express][install-SQLExpress], Olá [Drivers Microsoft para SQL Server para PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), e [Git] [ install-git] instalado no seu computador. Após concluir neste guia, terá uma aplicação web de SQL do PHP em execução no Azure.

> [!NOTE]
> Pode instalar e configurar o PHP, SQL Server Express e Olá Drivers Microsoft para o SQL Server para PHP utilizando Olá [instalador de plataforma Web Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Aprenderá:

* Como toocreate um Azure web app e uma base de dados do SQL Server utilizando Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Porque o PHP está ativado nas Web Apps do App Service, por predefinição, é nothing especial toorun necessário o código do PHP.
* Como toopublish e Republica a tooAzure de aplicação utilizando o Git.

Ao seguir este tutorial, irá criar uma aplicação web simples registo PHP. Olá aplicação será alojada num Web site do Azure. Abaixo é uma captura de ecrã da aplicação Olá concluída:

![Web Site do PHP do Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Criar uma aplicação web do Azure e configurar a publicação de Git
Siga estes passos toocreate uma aplicação web do Azure e uma base de dados do SQL Server:

1. Inicie sessão no toohello [Portal do Azure](https://portal.azure.com/).
2. Abra Olá Azure Marketplace, clicando em Olá **novo** ícone na parte superior do Olá esquerda do dashboard de Olá, clique em **Selecionar tudo** seguinte tooMarketplace e selecionando **Web + móvel**.
3. No Marketplace Olá, selecione **Web + móvel**.
4. Clique em Olá **aplicação Web + SQL** ícone.
5. Depois de ler a descrição de Olá da aplicação Web de Olá + aplicação SQL Server, selecione **criar**.
6. Clique em cada parte (**grupo de recursos**, **aplicação Web**, **base de dados**, e **subscrição**) e introduza ou selecione os valores de Olá necessário campos:
   
   * Introduza um nome de URL à sua escolha    
   * Configure as credenciais do servidor de base de dados
   * Selecione Olá região mais próxima tooyou
     
     ![configurar a sua aplicação](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Quando terminar a definição de aplicação web de Olá, clique em **criar**.
   
    Quando tiver sido criada a aplicação web de Olá, Olá **notificações** botão será flash um verde **êxito** e Olá, ambos os Olá web app e Olá base de dados SQL no grupo de Olá tooshow aberta de painel do grupo de recursos.
8. Clique em ícone da aplicação web Olá no painel de Olá recursos grupo Painel tooopen Olá da aplicação web.
   
    ![grupo de recursos da aplicação de Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. No **definições** clique **a implementação contínua** > **configurar definições necessárias**. Selecione **repositório de Git Local** e clique em **OK**.
   
    ![onde está o código de origem](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Se não tiver configurado um repositório de Git antes, tem de fornecer um nome de utilizador e palavra-passe. toodo, clique em **definições** > **as credenciais de implementação** no painel da aplicação web Olá.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. No **definições** clique em **propriedades** toosee Olá remoto URL do Git terá toouse toodeploy sua aplicação PHP mais tarde.

## <a name="get-sql-database-connection-information"></a>Obter informações de ligação de base de dados SQL
tooconnect toohello instância de base de dados do SQL Server que está ligado tooyour web app, sua será necessário Olá informações de ligação, o que especificou quando criou a base de dados de Olá. Olá tooget informações de ligação de base de dados SQL, siga estes passos:

1. No painel do grupo de recursos Olá, clique o ícone de Olá SQL da base de dados.
2. No painel de Olá SQL da base de dados, clique em **definições** > **propriedades**, em seguida, clique em **Mostrar cadeias de ligação de base de dados**. 
   
    ![Ver propriedades de base de dados](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. De Olá **PHP** secção caixa de diálogo resultante de Olá, tome nota dos valores de Olá para `Server`, `SQL Database`, e `User Name`. Irá utilizar estes valores mais tarde quando publicar a tooAzure de aplicação web do PHP do serviço de aplicações.

## <a name="build-and-test-your-application-locally"></a>Criar e testar a aplicação localmente
Olá aplicação de registo é uma aplicação PHP simples que lhe permite tooregister um evento, fornecendo o nome e endereço de e-mail. São apresentadas informações sobre registrants anteriores numa tabela. As informações de registo são armazenadas numa instância de base de dados SQL. aplicação Olá consiste em dois ficheiros (código de copiar/colar disponíveis abaixo):

* **Index.php**: apresenta um formulário de registo e uma tabela que contém informações de registrant.
* **createtable.php**: cria Olá tabela de base de dados SQL para a aplicação Olá. Este ficheiro só será utilizado uma vez.

aplicação de Olá toorun localmente, siga os passos de Olá abaixo. Tenha em atenção que estes passos partem do princípio de que tem o PHP e do SQL Server Express configurar no seu computador local e, se tiver ativado o Olá [extensão PDO para o SQL Server][pdo-sqlsrv].

1. Criar uma base de dados do SQL Server chamado `registration`. Pode fazê-lo de Olá `sqlcmd` linha de comandos com estes comandos:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. No diretório de raiz da aplicação, crie dois ficheiros na mesma - um chamado `createtable.php` e outra denominada `index.php`.
3. Abra Olá `createtable.php` ficheiro num editor de texto ou IDE e adicione o código de Olá abaixo. Este código será utilizado toocreate Olá `registration_tbl` tabela Olá `registration` base de dados.
   
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
   
    Tenha em atenção que, terá de valores de Olá tooupdate para <code>$user</code> e <code>$pwd</code> com o nome de utilizador local do SQL Server e a palavra-passe.
4. Num terminal no diretório de raiz de Olá da Olá de tipo de aplicação Olá os seguintes comandos:
   
        php -S localhost:8000
5. Abra um browser e navegue demasiado**http://localhost:8000/createtable.php**. Esta ação irá criar Olá `registration_tbl` tabela na base de dados de Olá.
6. Abra Olá **index.php** ficheiro num editor de texto ou IDE e adicione Olá básico código HTML e CSS para a página Olá (Olá código PHP será adicionado em passos posteriores).
   
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
7. Dentro de etiquetas PHP Olá, adicione o código do PHP para ligar toohello base de dados.
   
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
   
    Novamente, terá de valores de Olá tooupdate para <code>$user</code> e <code>$pwd</code> com o nome de utilizador de MySQL local e a palavra-passe.
8. Seguindo o código de ligação de base de dados de Olá, adicione o código para inserir informações de registo da base de dados de Olá.
   
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
9. Por fim, seguindo o código de Olá acima, adicione o código para obter dados da base de dados de Olá.
   
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

Agora pode navegar demasiado**http://localhost:8000/index.php** aplicação de Olá tootest.

## <a name="publish-your-application"></a>Publicar a aplicação
Depois de ter testado a aplicação localmente, pode publicá-lo tooApp as Web Apps Service utilizando o Git. No entanto, primeiro precisa de informações de ligação do tooupdate Olá da base de dados na aplicação Olá. Utilização de informações de ligação de base de dados de Olá que obteve anteriormente (no Olá **informações de ligação de obter a base de dados do SQL** secção), Olá de atualização que seguir as informações no **ambos** Olá `createdatabase.php` e `index.php` ficheiros com Olá adequado valores:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> No Olá <code>$host</code>, valor hello do servidor tem de ser prepended com <code>tcp:</code>.
> 
> 

Agora, está pronto tooset segurança publicação de Git e publicar a aplicação Olá.

> [!NOTE]
> Estes são os mesmos passos indicados no fim de Olá do Olá de Olá **criar uma aplicação web do Azure e configurar a publicação de Git** secção acima.
> 
> 

1. Abrir GitBash (ou um terminal, se for Git no seu `PATH`), alterar o diretório de raiz de toohello de diretórios da aplicação (Olá **registo** diretório), e Olá execute os seguintes comandos:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Será solicitado para a palavra-passe de Olá que criou anteriormente.
2. Procurar demasiado**http://[web aplicação name].azurewebsites.net/createtable.php** toocreate tabela na base de dados SQL Olá para aplicação Olá.
3. Procurar demasiado**http://[web aplicação name].azurewebsites.net/index.php** toobegin utilizando a aplicação Olá.

Depois de ter publicado a aplicação, pode começar efetuar alterações tooit e utilizar o Git toopublish-los. 

## <a name="publish-changes-tooyour-application"></a>Publicar alterações tooyour aplicação
toopublish alterações tooapplication, siga estes passos:

1. Efetue as alterações tooyour aplicação localmente.
2. Abrir GitBash (ou um terminal, it Git está no seu `PATH`), altere o diretório de raiz de toohello de diretórios da sua aplicação e execute Olá os seguintes comandos:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Será solicitado para a palavra-passe de Olá que criou anteriormente.
3. Procurar demasiado**http://[web aplicação name].azurewebsites.net/index.php** toosee as suas alterações.

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

