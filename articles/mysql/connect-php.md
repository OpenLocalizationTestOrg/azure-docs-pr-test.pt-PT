---
title: "Ligação tooAzure da base de dados MySQL de PHP | Microsoft Docs"
description: "Este guia de Introdução fornece vários exemplos de código PHP pode utilizar tooconnect e consultar dados a partir da base de dados do Azure para MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="34979-103">Base de dados do Azure para MySQL: dados de utilização PHP tooconnect e consulta</span><span class="sxs-lookup"><span data-stu-id="34979-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="34979-104">Este guia de introdução demonstra como tooconnect tooan Azure base de dados para utilizar o MySQL um [PHP](http://php.net/manual/intro-whatis.php) aplicação.</span><span class="sxs-lookup"><span data-stu-id="34979-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="34979-105">Mostra como toouse SQL instruções tooquery, inserir, atualizar e eliminar os dados na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="34979-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="34979-106">Este artigo pressupõe que está familiarizado com o desenvolvimento com o PHP, mas que são tooworking nova com base de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="34979-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34979-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="34979-107">Prerequisites</span></span>
<span data-ttu-id="34979-108">Este guia de introdução utiliza recursos Olá criados destes guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="34979-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="34979-109">Criar uma Base de Dados do Azure para o servidor MySQL com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="34979-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="34979-110">Criar uma Base de Dados do Azure para o servidor MySQL com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="34979-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="34979-111">Instalar o PHP</span><span class="sxs-lookup"><span data-stu-id="34979-111">Install PHP</span></span>
<span data-ttu-id="34979-112">Instale o PHP no seu próprio servidor ou crie uma [aplicação Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) do Azure que inclua o PHP.</span><span class="sxs-lookup"><span data-stu-id="34979-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="34979-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="34979-113">MacOS</span></span>
- <span data-ttu-id="34979-114">Transfira a [versão 7.1.4 do PHP](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="34979-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="34979-115">Instalar o PHP e consulte toohello [PHP manual](http://php.net/manual/install.macosx.php) para configuração adicional</span><span class="sxs-lookup"><span data-stu-id="34979-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="34979-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="34979-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="34979-117">Transfira a [versão 7.1.4 do PHP (x64) não segura para threads](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="34979-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="34979-118">Instalar o PHP e consulte toohello [PHP manual](http://php.net/manual/install.unix.php) para configuração adicional</span><span class="sxs-lookup"><span data-stu-id="34979-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="34979-119">Windows</span><span class="sxs-lookup"><span data-stu-id="34979-119">Windows</span></span>
- <span data-ttu-id="34979-120">Transfira a [versão 7.1.4 do PHP (x64) não segura para threads](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="34979-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="34979-121">Instalar o PHP e consulte toohello [PHP manual](http://php.net/manual/install.windows.php) para configuração adicional</span><span class="sxs-lookup"><span data-stu-id="34979-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="34979-122">Obter informações da ligação</span><span class="sxs-lookup"><span data-stu-id="34979-122">Get connection information</span></span>
<span data-ttu-id="34979-123">Obter Olá ligação informações necessárias tooconnect toohello base de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="34979-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="34979-124">Terá de Olá credenciais de início de sessão e nome de servidor completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="34979-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="34979-125">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="34979-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="34979-126">No painel esquerdo Olá, clique em **todos os recursos**e, em seguida, procure servidor Olá criou (por exemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="34979-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="34979-127">Clique no nome do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="34979-127">Click hello server name.</span></span>
4. <span data-ttu-id="34979-128">Servidor de Olá selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="34979-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="34979-129">Tome nota do Olá **nome do servidor** e **nome de início de sessão de administração do servidor**.</span><span class="sxs-lookup"><span data-stu-id="34979-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="34979-130">![Nome do servidor da Base de Dados do Azure para o MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="34979-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="34979-131">Se se esquecer da sua informações de início de sessão do servidor, navegue até toohello **descrição geral** página nome de início de sessão de administrador de servidor Olá tooview e, se necessário, de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="34979-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="34979-132">Ligar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="34979-132">Connect and create a table</span></span>
<span data-ttu-id="34979-133">Code tooconnect a seguir de Olá de utilização e criar uma tabela utilizando **CREATE TABLE** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="34979-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="34979-134">código de Olá utiliza Olá **MySQL melhorada extensão** classe (mysqli) incluído no PHP.</span><span class="sxs-lookup"><span data-stu-id="34979-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="34979-135">Olá, métodos de chamada de código [mysqli_init](http://php.net/manual/mysqli.init.php) e [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="34979-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="34979-136">Em seguida, chama o método [mysqli_query](http://php.net/manual/mysqli.query.php) consulta de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="34979-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="34979-137">Em seguida, chama o método [mysqli_close](http://php.net/manual/mysqli.close.php) ligação de Olá tooclose.</span><span class="sxs-lookup"><span data-stu-id="34979-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="34979-138">Substitua os parâmetros de anfitrião, nome de utilizador, palavra-passe e db_name Olá os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="34979-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="34979-139">Inserir dados</span><span class="sxs-lookup"><span data-stu-id="34979-139">Insert data</span></span>
<span data-ttu-id="34979-140">Code tooconnect a seguir de Olá de utilização e inserir dados, utilizando um **inserir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="34979-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="34979-141">código de Olá utiliza Olá **MySQL melhorada extensão** classe (mysqli) incluído no PHP.</span><span class="sxs-lookup"><span data-stu-id="34979-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="34979-142">código de Olá utiliza o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate um preparado inserir declaração, em seguida, vincula Olá parâmetros para cada valor de coluna inseridas utilizando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="34979-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="34979-143">código de Olá executa a instrução de Olá utilizando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e, posteriormente, fechar Olá instrução utilizando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="34979-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="34979-144">Substitua os parâmetros de anfitrião, nome de utilizador, palavra-passe e db_name Olá os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="34979-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="34979-145">Ler dados</span><span class="sxs-lookup"><span data-stu-id="34979-145">Read data</span></span>
<span data-ttu-id="34979-146">Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **SELECIONE** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="34979-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="34979-147">código de Olá utiliza Olá **MySQL melhorada extensão** classe (mysqli) incluído no PHP.</span><span class="sxs-lookup"><span data-stu-id="34979-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="34979-148">código de Olá utiliza o método [mysqli_query](http://php.net/manual/mysqli.query.php) executar a consulta de sql Olá e utiliza [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) método toofetch Olá linhas resultantes.</span><span class="sxs-lookup"><span data-stu-id="34979-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="34979-149">Substitua os parâmetros de anfitrião, nome de utilizador, palavra-passe e db_name Olá os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="34979-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="34979-150">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="34979-150">Update data</span></span>
<span data-ttu-id="34979-151">Seguinte de Olá utilize code tooconnect e atualizar Olá dados utilizando um **ATUALIZAR** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="34979-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="34979-152">código de Olá utiliza Olá **MySQL melhorada extensão** classe (mysqli) incluído no PHP.</span><span class="sxs-lookup"><span data-stu-id="34979-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="34979-153">código de Olá utiliza o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate uma instrução de atualização preparado, em seguida, vincula parâmetros Olá para cada valor de coluna atualizado utilizando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="34979-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="34979-154">código de Olá executa a instrução de Olá utilizando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e, posteriormente, fechar Olá instrução utilizando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="34979-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="34979-155">Substitua os parâmetros de anfitrião, nome de utilizador, palavra-passe e db_name Olá os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="34979-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="34979-156">Eliminar dados</span><span class="sxs-lookup"><span data-stu-id="34979-156">Delete data</span></span>
<span data-ttu-id="34979-157">Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **eliminar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="34979-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="34979-158">código de Olá utiliza Olá **MySQL melhorada extensão** classe (mysqli) incluído no PHP.</span><span class="sxs-lookup"><span data-stu-id="34979-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="34979-159">código de Olá utiliza o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate um preparado elimine declaração, em seguida, vincula Olá parâmetros para olá onde cláusula na instrução de Olá utilizando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="34979-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="34979-160">código de Olá executa a instrução de Olá utilizando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e, posteriormente, fechar Olá instrução utilizando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="34979-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="34979-161">Substitua os parâmetros de anfitrião, nome de utilizador, palavra-passe e db_name Olá os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="34979-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="34979-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="34979-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="34979-163">Criar uma aplicação Web PHP e MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="34979-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
