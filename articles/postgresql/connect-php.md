---
title: aaaConnect tooAzure da base de dados PostgreSQL linguagem PHP | Microsoft Docs
description: "Este guia de Introdução fornece um exemplo de código do PHP, pode utilizar tooconnect e consultar dados a partir da base de dados do Azure para PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Base de dados do Azure para PostgreSQL: dados de utilização PHP tooconnect e consulta
Este guia de introdução demonstra como tooconnect tooan Azure base de dados de utilização de PostgreSQL um [PHP](http://php.net/manual/intro-whatis.php) aplicação. Mostra como toouse SQL instruções tooquery, inserir, atualizar e eliminar os dados na base de dados de Olá. Este artigo pressupõe que está familiarizado com o desenvolvimento com o PHP, mas que são tooworking nova com base de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de introdução utiliza recursos Olá criados destes guias como um ponto de partida:
- [Criar BD - Portal](quickstart-create-server-database-portal.md)
- [Criar BD - CLI do Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Instalar o PHP
Instale o PHP no seu próprio servidor ou crie uma [aplicação Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) do Azure que inclua o PHP.

### <a name="windows"></a>Windows
- Transfira a [versão 7.1.4 do PHP (x64) não segura para threads](http://windows.php.net/download#php-7.1)
- Instalar o PHP e consulte toohello [PHP manual](http://php.net/manual/install.windows.php) para configuração adicional
- código de Olá utiliza Olá **pgsql** classe (ext/php_pgsql.dll) que está incluído na Olá instalação do PHP. 
- Olá ativado **pgsql** extensão editando o ficheiro de configuração do php.ini Olá, normalmente localizado no `C:\Program Files\PHP\v7.1\php.ini`. ficheiro de configuração de Olá deve conter uma linha com o texto de Olá `extension=php_pgsql.so`. Se não for apresentado, adicionar Olá texto e guarde o ficheiro de Olá. Se estiver presente, texto Olá comentado, mas com um prefixo de ponto e vírgula, anule os comentários texto Olá por ponto e vírgula de Olá a remover.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Transfira a [versão 7.1.4 do PHP (x64) não segura para threads](http://php.net/downloads.php) 
- Instalar o PHP e consulte toohello [PHP manual](http://php.net/manual/install.unix.php) para configuração adicional
- código de Olá utiliza Olá **pgsql** classe (php_pgsql.so). Instale-o ao executar `sudo apt-get install php-pgsql`.
- Olá ativado **pgsql** extensão editando Olá `/etc/php/7.0/mods-available/pgsql.ini` ficheiro de configuração. ficheiro de configuração de Olá deve conter uma linha com o texto de Olá `extension=php_pgsql.so`. Se não for apresentado, adicionar Olá texto e guarde o ficheiro de Olá. Se estiver presente, texto Olá comentado, mas com um prefixo de ponto e vírgula, anule os comentários texto Olá por ponto e vírgula de Olá a remover.

### <a name="macos"></a>MacOS
- Transfira a [versão 7.1.4 do PHP](http://php.net/downloads.php)
- Instalar o PHP e consulte toohello [PHP manual](http://php.net/manual/install.macosx.php) para configuração adicional

## <a name="get-connection-information"></a>Obter informações da ligação
Obter Olá ligação informações necessárias tooconnect toohello base de dados do Azure para PostgreSQL. Terá de Olá credenciais de início de sessão e nome de servidor completamente qualificado.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. No menu da esquerda Olá, no portal do Azure, clique em **todos os recursos** e procure o servidor de Olá que criou, tais como **mypgserver 20170401**.
3. Clique no nome do servidor de Olá **mypgserver 20170401**.
4. Servidor de Olá selecione **descrição geral** página. Tome nota do Olá **nome do servidor** e **nome de início de sessão de administração do servidor**.
 ![Base de Dados do Azure para o PostgreSQL – Início de sessão de administrador do servidor](./media/connect-php/1-connection-string.png)
5. Se se esquecer da sua informações de início de sessão do servidor, navegue até toohello **descrição geral** página nome de início de sessão de administrador de servidor Olá tooview e, se necessário, de reposição de palavra-passe de Olá.

## <a name="connect-and-create-a-table"></a>Ligar-se e criar uma tabela
Code tooconnect a seguir de Olá de utilização e criar uma tabela utilizando **CREATE TABLE** instrução de SQL, seguida de **INSERT INTO** linhas de tooadd instruções SQL na tabela de Olá.

método de chamada de código de Olá [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure da base de dados PostgreSQL. Em seguida, chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) várias vezes toorun vários comandos, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se um erro de cada vez. Em seguida, chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) ligação de Olá tooclose.

Substitua Olá `$host`, `$database`, `$user`, e `$password` parâmetros com os seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a>Ler dados
Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **SELECIONE** instrução SQL. 

 método de chamada de código de Olá [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure da base de dados PostgreSQL. Em seguida, chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Olá comando de selecção, mantendo os resultados de Olá num conjunto de resultados, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se Ocorreu um erro.  conjunto de resultados de Olá tooread, método [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) denomina-se num ciclo, uma vez por linha de linha de Olá e os dados são obtidos numa matriz `$row`, com o valor de uma de dados por coluna em cada posição da matriz.  conjunto de resultados de Olá toofree, método [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) é chamado. Em seguida, chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) ligação de Olá tooclose.

Substitua Olá `$host`, `$database`, `$user`, e `$password` parâmetros com os seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a>Atualizar dados
Seguinte de Olá utilize code tooconnect e atualizar Olá dados utilizando um **ATUALIZAR** instrução SQL.

método de chamada de código de Olá [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure da base de dados PostgreSQL. Em seguida, chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun um comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se Ocorreu um erro. Em seguida, chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) ligação de Olá tooclose.

Substitua Olá `$host`, `$database`, `$user`, e `$password` parâmetros com os seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a>Eliminar dados
Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **eliminar** instrução SQL. 

 método de chamada de código de Olá [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect base de dados demasiado do Azure para PostgreSQL. Em seguida, chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun um comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se Ocorreu um erro. Em seguida, chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) ligação de Olá tooclose.

Substitua Olá `$host`, `$database`, `$user`, e `$password` parâmetros com os seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a>Passos seguintes
> [!div class="nextstepaction"]
> [Migrar a base de dados com Exportar e Importar](./howto-migrate-using-export-and-import.md)
