---
title: "Ligação tooAzure da base de dados MySQL do C++ | Microsoft Docs"
description: "Este guia de Introdução fornece um exemplo de código de C++, pode utilizar tooconnect e consultar dados a partir da base de dados do Azure para MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="93362-103">Base de dados do Azure para MySQL: tooconnect e consulta de dados de utilização conector/C++</span><span class="sxs-lookup"><span data-stu-id="93362-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="93362-104">Este guia de introdução demonstra como tooconnect tooan Azure base de dados para MySQL utilizando uma aplicação de C++.</span><span class="sxs-lookup"><span data-stu-id="93362-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="93362-105">Mostra como toouse SQL instruções tooquery, inserir, atualizar e eliminar os dados na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="93362-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="93362-106">Olá passos deste artigo partem do princípio de que está familiarizado com o desenvolvimento utilizando C++ e que é novo tooworking com base de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="93362-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93362-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93362-107">Prerequisites</span></span>
<span data-ttu-id="93362-108">Este guia de introdução utiliza recursos Olá criados destes guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="93362-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="93362-109">Criar uma Base de Dados do Azure para o servidor MySQL com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="93362-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="93362-110">Criar uma Base de Dados do Azure para o servidor MySQL com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="93362-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="93362-111">Também tem de:</span><span class="sxs-lookup"><span data-stu-id="93362-111">You also need to:</span></span>
- <span data-ttu-id="93362-112">Instalar o [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="93362-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="93362-113">Instalar o [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="93362-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="93362-114">Instalar o [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="93362-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="93362-115">Instalar o [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="93362-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="93362-116">Instalar o Visual Studio e .NET</span><span class="sxs-lookup"><span data-stu-id="93362-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="93362-117">Olá passos nesta secção partem do princípio de que está familiarizado com o desenvolvimento através do .NET.</span><span class="sxs-lookup"><span data-stu-id="93362-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="93362-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="93362-118">**Windows**</span></span>
1. <span data-ttu-id="93362-119">Instale o Visual Studio 2017 Community, o qual é um IDE gratuito, extensível e repleto de funcionalidades para criar aplicações modernas para Android, iOS e Windows, bem como aplicações Web e de bases de dados e serviços cloud.</span><span class="sxs-lookup"><span data-stu-id="93362-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="93362-120">Pode instalar o Olá completa do .NET Framework ou apenas .NET Core.</span><span class="sxs-lookup"><span data-stu-id="93362-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="93362-121">Olá fragmentos de código em projetos de início rápido Olá com uma.</span><span class="sxs-lookup"><span data-stu-id="93362-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="93362-122">Se já tiver o Visual Studio instalado no seu computador, ignore Olá junto dois passos.</span><span class="sxs-lookup"><span data-stu-id="93362-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="93362-123">Transferir Olá [instalador do Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="93362-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="93362-124">Execute o instalador Olá e siga Olá instalação pede toocomplete Olá instalação.</span><span class="sxs-lookup"><span data-stu-id="93362-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="93362-125">**Configurar o Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="93362-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="93362-126">Propriedade do projeto do Visual Studio, > propriedades de configuração > C/C++ > linker > geral > diretórios de bibliotecas adicionais, adicione o diretório de lib\opt Olá (ou seja,: C:\Program Files (x86) \MySQL\MySQL conector C++ 1.1.9\lib\opt) de Olá c + + conector.</span><span class="sxs-lookup"><span data-stu-id="93362-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="93362-127">No Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span><span class="sxs-lookup"><span data-stu-id="93362-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="93362-128">Adicione o diretório include/ do conector C++ (ou seja: C:\Programas (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="93362-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="93362-129">Adicione o diretório de raiz da biblioteca Boost (ou seja: C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="93362-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="93362-130">Propriedade do projeto do Visual Studio, > propriedades de configuração > C/C++ > linker > entrada > dependências adicionais, adicionar o campo de texto Olá mysqlcppconn.lib</span><span class="sxs-lookup"><span data-stu-id="93362-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="93362-131">O mysqlcppconn.dll de cópia de Olá c + + conector pasta de biblioteca no passo 3 toohello mesmo diretório que o executável da aplicação Olá ou adicioná-la toohello variável de ambiente para a aplicação possa encontrar.</span><span class="sxs-lookup"><span data-stu-id="93362-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="93362-132">Obter informações da ligação</span><span class="sxs-lookup"><span data-stu-id="93362-132">Get connection information</span></span>
<span data-ttu-id="93362-133">Obter Olá ligação informações necessárias tooconnect toohello base de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="93362-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="93362-134">Terá de Olá credenciais de início de sessão e nome de servidor completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="93362-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="93362-135">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="93362-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="93362-136">No menu da esquerda Olá, no portal do Azure, clique em **todos os recursos** e procure o servidor de Olá que criou, tais como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="93362-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="93362-137">Clique no nome do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="93362-137">Click hello server name.</span></span>
4. <span data-ttu-id="93362-138">Servidor de Olá selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="93362-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="93362-139">Tome nota do Olá **nome do servidor** e **nome de início de sessão de administração do servidor**.</span><span class="sxs-lookup"><span data-stu-id="93362-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="93362-140">![Nome do servidor da Base de Dados do Azure para o MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="93362-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="93362-141">Se se esquecer da sua informações de início de sessão do servidor, navegue até toohello **descrição geral** página nome de início de sessão de administrador de servidor Olá tooview e, se necessário, de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="93362-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="93362-142">Ligar, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="93362-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="93362-143">Seguinte Olá de utilização code tooconnect e carregar dados de Olá utilizando **CREATE TABLE** e **INSERT INTO** instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="93362-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="93362-144">código de Olá utiliza sql::Driver classe com Olá connect() método tooestablish tooMySQL uma ligação.</span><span class="sxs-lookup"><span data-stu-id="93362-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="93362-145">Em seguida, o código de Olá utiliza método createStatement() e execute () toorun Olá da base de dados comandos.</span><span class="sxs-lookup"><span data-stu-id="93362-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="93362-146">Substitua os parâmetros de anfitrião, DBName, utilizador e palavra-passe de Olá valores Olá que especificou quando criou o servidor de Olá e base de dados.</span><span class="sxs-lookup"><span data-stu-id="93362-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="93362-147">Ler dados</span><span class="sxs-lookup"><span data-stu-id="93362-147">Read data</span></span>

<span data-ttu-id="93362-148">Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **SELECIONE** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="93362-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="93362-149">código de Olá utiliza sql::Driver classe com Olá connect() método tooestablish tooMySQL uma ligação.</span><span class="sxs-lookup"><span data-stu-id="93362-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="93362-150">Em seguida, código de Olá utiliza o método prepareStatement() e executeQuery() toorun Olá selecione comandos.</span><span class="sxs-lookup"><span data-stu-id="93362-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="93362-151">Por fim, o código de Olá utiliza next() tooadvance toohello registos nos resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="93362-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="93362-152">Em seguida, o código de Olá utiliza valores de Olá tooparse getInt() e GetString () no registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="93362-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="93362-153">Substitua os parâmetros de anfitrião, DBName, utilizador e palavra-passe de Olá valores Olá que especificou quando criou o servidor de Olá e base de dados.</span><span class="sxs-lookup"><span data-stu-id="93362-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="93362-154">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="93362-154">Update data</span></span>
<span data-ttu-id="93362-155">Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **ATUALIZAÇÃO** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="93362-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="93362-156">código de Olá utiliza sql::Driver classe com Olá connect() método tooestablish tooMySQL uma ligação.</span><span class="sxs-lookup"><span data-stu-id="93362-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="93362-157">Em seguida, o código de Olá utiliza método prepareStatement() e executeQuery() toorun Olá comandos de atualização.</span><span class="sxs-lookup"><span data-stu-id="93362-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="93362-158">Substitua os parâmetros de anfitrião, DBName, utilizador e palavra-passe de Olá valores Olá que especificou quando criou o servidor de Olá e base de dados.</span><span class="sxs-lookup"><span data-stu-id="93362-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="93362-159">Eliminar dados</span><span class="sxs-lookup"><span data-stu-id="93362-159">Delete data</span></span>
<span data-ttu-id="93362-160">Seguinte de Olá utilize code tooconnect e ler Olá dados utilizando um **eliminar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="93362-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="93362-161">código de Olá utiliza sql::Driver classe com Olá connect() método tooestablish tooMySQL uma ligação.</span><span class="sxs-lookup"><span data-stu-id="93362-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="93362-162">Em seguida, o código de Olá utiliza prepareStatement() de método e executeQuery() toorun Olá eliminar comandos.</span><span class="sxs-lookup"><span data-stu-id="93362-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="93362-163">Substitua os parâmetros de anfitrião, DBName, utilizador e palavra-passe de Olá valores Olá que especificou quando criou o servidor de Olá e base de dados.</span><span class="sxs-lookup"><span data-stu-id="93362-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="93362-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="93362-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="93362-165">Migrar o tooAzure de base de dados MySQL da base de dados para utilizar a captura e restauro de MySQL</span><span class="sxs-lookup"><span data-stu-id="93362-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
