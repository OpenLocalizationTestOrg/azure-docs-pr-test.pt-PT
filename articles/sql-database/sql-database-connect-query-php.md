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
# <a name="use-php-tooquery-an-azure-sql-database"></a>Utilize o PHP tooquery uma base de dados SQL do Azure

Este tutorial de início rápido demonstra como toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan de tooconnect um programa Azure SQL da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápida neste tutorial de início, certifique-se de que tem o seguinte Olá:

- Uma base de dados SQL do Azure. Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos: 

   - [Criar BD - Portal](sql-database-get-started-portal.md)
   - [Criar BD - CLI](sql-database-get-started-cli.md)
   - [Criar BD - PowerShell](sql-database-get-started-powershell.md)

- A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.

- Ter instalado o PHP e software relacionado para o seu sistema operativo.

    - **MacOS**: Homebrew instalar PHP, instalar o controlador ODBC Olá e SQLCMD e, em seguida, instale Olá controladores PHP para SQL Server. Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: instalar o PHP e outros necessário pacotes e, em seguida, instalar Olá controladores PHP para SQL Server. Veja os [Passos 1.2 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: versão mais recente do Olá de instalação do PHP para o IIS Express, a versão mais recente do Olá do Microsoft Drivers para SQL Server Express de IIS, Chocolatey, o controlador ODBC Olá e SQLCMD. Veja os [Passos 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>Informações de ligação do servidor SQL

Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure. Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página. 
3. No Olá **descrição geral** página para a base de dados, consulte Olá nome completamente qualificado servidor conforme mostrado no Olá seguinte imagem. Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se se esquecer da sua informações de início de sessão do servidor, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.     
    
## <a name="insert-code-tooquery-sql-database"></a>Inserir código tooquery SQL da base de dados

1. No seu editor de texto favorito, crie um novo ficheiro, **sqltest.php**.  

2. Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.

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

## <a name="run-hello-code"></a>Executar código Olá

1. Na linha de comandos Olá, execute Olá os seguintes comandos:

   ```php
   php sqltest.php
   ```

2. Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.

## <a name="next-steps"></a>Passos seguintes
- [Criar a sua primeira base de dados SQL do Azure](sql-database-design-first-database.md)
- [Controlador Microsoft PHP para SQL Server](https://github.com/Microsoft/msphpsql/)
- [Report issues or ask questions](https://github.com/Microsoft/msphpsql/issues) (Comunicar problemas ou fazer perguntas)
