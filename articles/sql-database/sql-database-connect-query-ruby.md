---
title: aaaUse tooquery Ruby SQL Database do Azure | Microsoft Docs
description: "Este tópico mostra como toouse toocreate Ruby um programa que liga tooan SQL Database do Azure e a consulta utilizando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="02dbe-103">Utilizar tooquery Ruby uma base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="02dbe-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="02dbe-104">Este tutorial de início rápido demonstra como toouse [Ruby](https://www.ruby-lang.org) toocreate tooan de tooconnect um programa Azure SQL da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="02dbe-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02dbe-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="02dbe-105">Prerequisites</span></span>

<span data-ttu-id="02dbe-106">toocomplete rápida neste tutorial de início, certifique-se de que tem os seguintes pré-requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="02dbe-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="02dbe-107">Uma base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="02dbe-107">An Azure SQL database.</span></span> <span data-ttu-id="02dbe-108">Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="02dbe-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="02dbe-109">Criar BD - Portal</span><span class="sxs-lookup"><span data-stu-id="02dbe-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="02dbe-110">Criar BD - CLI</span><span class="sxs-lookup"><span data-stu-id="02dbe-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="02dbe-111">Criar BD - PowerShell</span><span class="sxs-lookup"><span data-stu-id="02dbe-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="02dbe-112">A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="02dbe-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="02dbe-113">Ter instalado o Ruby e software relacionado para o seu sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02dbe-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="02dbe-114">**MacOS**: instale o Homebrew, instale o rbenv e o ruby-build, instale o Ruby e, em seguida, instale o FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="02dbe-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="02dbe-115">Veja os [Passos 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="02dbe-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="02dbe-116">**Ubuntu**: instale os pré-requisitos para Ruby, instale o rbenv e o ruby-build, instale o Ruby e, em seguida, instale o FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="02dbe-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="02dbe-117">Veja os [Passos 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="02dbe-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="02dbe-118">Informações de ligação do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="02dbe-118">SQL server connection information</span></span>

<span data-ttu-id="02dbe-119">Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="02dbe-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="02dbe-120">Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="02dbe-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="02dbe-121">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02dbe-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="02dbe-122">Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="02dbe-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="02dbe-123">No Olá **descrição geral** da base de dados, reveja o nome de servidor completamente qualificado Olá.</span><span class="sxs-lookup"><span data-stu-id="02dbe-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="02dbe-124">Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção, conforme mostrado no Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="02dbe-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="02dbe-126">Se tenha esquecido informações de início de sessão de Olá para o servidor da SQL Database do Azure, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="02dbe-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02dbe-127">Tem de ter uma regra de firewall no local para o endereço IP público de Olá do computador Olá em que executar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="02dbe-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="02dbe-128">Se estiver num computador diferente ou ter um endereço IP público diferentes, crie um [através de regra de firewall ao nível do servidor Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="02dbe-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="02dbe-129">Inserir código tooquery SQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="02dbe-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="02dbe-130">No seu editor de texto favorito, crie um ficheiro novo, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="02dbe-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="02dbe-131">Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="02dbe-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a><span data-ttu-id="02dbe-132">Executar código Olá</span><span class="sxs-lookup"><span data-stu-id="02dbe-132">Run hello code</span></span>

1. <span data-ttu-id="02dbe-133">Na linha de comandos Olá, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="02dbe-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="02dbe-134">Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="02dbe-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="02dbe-135">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="02dbe-135">Next Steps</span></span>
- [<span data-ttu-id="02dbe-136">Criar a sua primeira base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="02dbe-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="02dbe-137">Repositório do GitHub para TinyTDS</span><span class="sxs-lookup"><span data-stu-id="02dbe-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- <span data-ttu-id="02dbe-138">[Report issues or ask questions about TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues) (Comunicar problemas ou fazer perguntas sobre o TinyTDS)</span><span class="sxs-lookup"><span data-stu-id="02dbe-138">[Report issues or ask questions about TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)</span></span>
- [<span data-ttu-id="02dbe-139">Controladores Ruby para SQL Server</span><span class="sxs-lookup"><span data-stu-id="02dbe-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
