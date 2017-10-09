---
title: aaaUse Python tooquery SQL Database do Azure | Microsoft Docs
description: "Este tópico mostra como toouse Python toocreate um programa que liga tooan SQL Database do Azure e a consulta utilizando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="db84c-103">Utilizar o Python tooquery uma base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="db84c-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="db84c-104">Este guia de introdução demonstra como toouse [Python](https://python.org) tooconnect tooan SQL do Azure da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="db84c-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db84c-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="db84c-105">Prerequisites</span></span>

<span data-ttu-id="db84c-106">toocomplete rápida neste tutorial de início, certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="db84c-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="db84c-107">Uma base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="db84c-107">An Azure SQL database.</span></span> <span data-ttu-id="db84c-108">Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="db84c-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="db84c-109">Criar BD - Portal</span><span class="sxs-lookup"><span data-stu-id="db84c-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="db84c-110">Criar BD - CLI</span><span class="sxs-lookup"><span data-stu-id="db84c-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="db84c-111">Criar BD - PowerShell</span><span class="sxs-lookup"><span data-stu-id="db84c-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="db84c-112">A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="db84c-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="db84c-113">Ter instalado o Python e software relacionado para o seu sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="db84c-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="db84c-114">**MacOS**: Homebrew instalar o Python, instalar o controlador ODBC Olá e SQLCMD e, em seguida, instalar Olá controlador do Python para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db84c-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="db84c-115">Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="db84c-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="db84c-116">**Ubuntu**: instalar o Python e outros necessário pacotes e, em seguida, instalar Olá controlador do Python para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db84c-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="db84c-117">Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="db84c-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="db84c-118">**Windows**: instalar a versão mais recente do Olá do Python (variável de ambiente está agora configurada por si), instale o controlador ODBC Olá e SQLCMD e, em seguida, instalar Olá Python controlador para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db84c-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="db84c-119">Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="db84c-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="db84c-120">Informações de ligação do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="db84c-120">SQL server connection information</span></span>

<span data-ttu-id="db84c-121">Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="db84c-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="db84c-122">Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="db84c-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="db84c-123">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="db84c-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="db84c-124">Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="db84c-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="db84c-125">No Olá **descrição geral** página para a base de dados, consulte Olá nome completamente qualificado servidor conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="db84c-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="db84c-126">Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="db84c-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="db84c-128">Se se esquecer da sua informações de início de sessão do servidor, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="db84c-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="db84c-129">Inserir código tooquery SQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="db84c-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="db84c-130">No seu editor de texto favorito, crie um novo ficheiro, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="db84c-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="db84c-131">Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="db84c-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="db84c-132">Executar código Olá</span><span class="sxs-lookup"><span data-stu-id="db84c-132">Run hello code</span></span>

1. <span data-ttu-id="db84c-133">Na linha de comandos Olá, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="db84c-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="db84c-134">Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="db84c-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db84c-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="db84c-135">Next steps</span></span>

- [<span data-ttu-id="db84c-136">Criar a sua primeira base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="db84c-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="db84c-137">Controladores Python da Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="db84c-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="db84c-138">Centro para Programadores do Python</span><span class="sxs-lookup"><span data-stu-id="db84c-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

