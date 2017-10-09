---
title: aaaUse PHP tooquery SQL Database do Azure | Microsoft Docs
description: "Este tópico mostra como toouse PHP toocreate um programa que liga tooan SQL Database do Azure e a consulta utilizando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="0c5fe-103">Utilize o PHP tooquery uma base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0c5fe-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="0c5fe-104">Este tutorial de início rápido demonstra como toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan de tooconnect um programa Azure SQL da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c5fe-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c5fe-105">Prerequisites</span></span>

<span data-ttu-id="0c5fe-106">toocomplete rápida neste tutorial de início, certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="0c5fe-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="0c5fe-107">Uma base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-107">An Azure SQL database.</span></span> <span data-ttu-id="0c5fe-108">Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="0c5fe-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="0c5fe-109">Criar BD - Portal</span><span class="sxs-lookup"><span data-stu-id="0c5fe-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="0c5fe-110">Criar BD - CLI</span><span class="sxs-lookup"><span data-stu-id="0c5fe-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="0c5fe-111">Criar BD - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c5fe-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="0c5fe-112">A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="0c5fe-113">Ter instalado o PHP e software relacionado para o seu sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="0c5fe-114">**MacOS**: Homebrew instalar PHP, instalar o controlador ODBC Olá e SQLCMD e, em seguida, instale Olá controladores PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="0c5fe-115">Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="0c5fe-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="0c5fe-116">**Ubuntu**: instalar o PHP e outros necessário pacotes e, em seguida, instalar Olá controladores PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="0c5fe-117">Veja os [Passos 1.2 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="0c5fe-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="0c5fe-118">**Windows**: versão mais recente do Olá de instalação do PHP para o IIS Express, a versão mais recente do Olá do Microsoft Drivers para SQL Server Express de IIS, Chocolatey, o controlador ODBC Olá e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="0c5fe-119">Veja os [Passos 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="0c5fe-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="0c5fe-120">Informações de ligação do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="0c5fe-120">SQL server connection information</span></span>

<span data-ttu-id="0c5fe-121">Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="0c5fe-122">Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="0c5fe-123">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0c5fe-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0c5fe-124">Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="0c5fe-125">No Olá **descrição geral** página para a base de dados, consulte Olá nome completamente qualificado servidor conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="0c5fe-126">Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="0c5fe-128">Se se esquecer da sua informações de início de sessão do servidor, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="0c5fe-129">Inserir código tooquery SQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="0c5fe-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="0c5fe-130">No seu editor de texto favorito, crie um novo ficheiro, **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="0c5fe-131">Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a><span data-ttu-id="0c5fe-132">Executar código Olá</span><span class="sxs-lookup"><span data-stu-id="0c5fe-132">Run hello code</span></span>

1. <span data-ttu-id="0c5fe-133">Na linha de comandos Olá, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0c5fe-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="0c5fe-134">Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="0c5fe-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c5fe-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0c5fe-135">Next steps</span></span>
- [<span data-ttu-id="0c5fe-136">Criar a sua primeira base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0c5fe-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="0c5fe-137">Controlador Microsoft PHP para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0c5fe-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- <span data-ttu-id="0c5fe-138">[Report issues or ask questions](https://github.com/Microsoft/msphpsql/issues) (Comunicar problemas ou fazer perguntas)</span><span class="sxs-lookup"><span data-stu-id="0c5fe-138">[Report issues or ask questions](https://github.com/Microsoft/msphpsql/issues)</span></span>
