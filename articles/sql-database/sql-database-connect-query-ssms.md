---
title: 'SSMS: ligar e consultar dados na Base de Dados SQL do Azure | Microsoft Docs'
description: "Saiba como tooconnect tooSQL da base de dados no Azure utilizando o SQL Server Management Studio (SSMS). Em seguida, execute instruções Transact-SQL (T-SQL) tooquery e editar dados."
metacanonical: 
keywords: "ligar a base de dados do toosql studio de gestão do sql server"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a><span data-ttu-id="3891f-105">Base de dados SQL do Azure: Utilize o SQL Server Management Studio tooconnect e consulta de dados</span><span class="sxs-lookup"><span data-stu-id="3891f-105">Azure SQL Database: Use SQL Server Management Studio tooconnect and query data</span></span>

<span data-ttu-id="3891f-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) é um ambiente integrado para a gestão qualquer infraestrutura de SQL Server, a partir do SQL Server tooSQL base de dados do Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="3891f-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span> <span data-ttu-id="3891f-107">Este guia de introdução demonstra como toouse SSMS tooconnect tooan SQL database do Azure e, em seguida, tooquery de instruções de utilização Transact-SQL, inserem, atualizar e eliminar os dados na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-107">This quick start demonstrates how toouse SSMS tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3891f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3891f-108">Prerequisites</span></span>

<span data-ttu-id="3891f-109">Este guia de introdução utiliza como os respetivos recursos Olá de ponto de partida criados destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="3891f-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="3891f-110">Criar BD - Portal</span><span class="sxs-lookup"><span data-stu-id="3891f-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="3891f-111">Criar BD - CLI</span><span class="sxs-lookup"><span data-stu-id="3891f-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="3891f-112">Criar BD - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3891f-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="3891f-113">Antes de começar, certifique-se de que instalou a versão mais recente do Olá do [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="3891f-113">Before you start, make sure you have installed hello newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="3891f-114">Informações de ligação do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="3891f-114">SQL server connection information</span></span>

<span data-ttu-id="3891f-115">Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="3891f-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="3891f-116">Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="3891f-117">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3891f-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3891f-118">Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="3891f-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="3891f-119">No Olá **descrição geral** da base de dados, reveja o nome de servidor completamente qualificado Olá conforme mostrado na imagem de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="3891f-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello image below.</span></span> <span data-ttu-id="3891f-120">Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="3891f-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![informações da ligação](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="3891f-122">Se tenha esquecido informações de início de sessão de Olá para o servidor da SQL Database do Azure, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-122">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="connect-tooyour-database"></a><span data-ttu-id="3891f-123">Ligar a base de dados tooyour</span><span class="sxs-lookup"><span data-stu-id="3891f-123">Connect tooyour database</span></span>

<span data-ttu-id="3891f-124">Utilize o SQL Server Management Studio tooestablish um servidor de SQL Database do Azure de tooyour de ligação.</span><span class="sxs-lookup"><span data-stu-id="3891f-124">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3891f-125">Um servidor lógico da Base de Dados SQL do Azure ouve na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="3891f-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="3891f-126">Se está a tentar efetuar tooconnect tooan SQL Database do Azure servidor lógico de dentro de uma firewall empresarial, esta porta tem de ser aberta na firewall da empresa Olá para toosuccessfully a ligação.</span><span class="sxs-lookup"><span data-stu-id="3891f-126">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

1. <span data-ttu-id="3891f-127">Abra o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="3891f-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="3891f-128">No Olá **ligar tooServer** caixa de diálogo, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3891f-128">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="3891f-129">Definição</span><span class="sxs-lookup"><span data-stu-id="3891f-129">Setting</span></span>       | <span data-ttu-id="3891f-130">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="3891f-130">Suggested value</span></span> | <span data-ttu-id="3891f-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="3891f-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3891f-132">**Tipo de servidor**</span><span class="sxs-lookup"><span data-stu-id="3891f-132">**Server type**</span></span> | <span data-ttu-id="3891f-133">Motor de base de dados</span><span class="sxs-lookup"><span data-stu-id="3891f-133">Database engine</span></span> | <span data-ttu-id="3891f-134">Este valor é preciso.</span><span class="sxs-lookup"><span data-stu-id="3891f-134">This value is required.</span></span> |
   | <span data-ttu-id="3891f-135">**Nome do servidor**</span><span class="sxs-lookup"><span data-stu-id="3891f-135">**Server name**</span></span> | <span data-ttu-id="3891f-136">nome de servidor completamente qualificado Olá</span><span class="sxs-lookup"><span data-stu-id="3891f-136">hello fully qualified server name</span></span> | <span data-ttu-id="3891f-137">Olá nome deve ser algo semelhante ao seguinte: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="3891f-137">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="3891f-138">**Autenticação**</span><span class="sxs-lookup"><span data-stu-id="3891f-138">**Authentication**</span></span> | <span data-ttu-id="3891f-139">Autenticação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="3891f-139">SQL Server Authentication</span></span> | <span data-ttu-id="3891f-140">Autenticação de SQL é o tipo de autenticação apenas de Olá que configurámos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3891f-140">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="3891f-141">**Início de sessão**</span><span class="sxs-lookup"><span data-stu-id="3891f-141">**Login**</span></span> | <span data-ttu-id="3891f-142">conta de administrador do servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="3891f-142">hello server admin account</span></span> | <span data-ttu-id="3891f-143">Esta é a conta de Olá que especificou quando criou o servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-143">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="3891f-144">**Palavra-passe**</span><span class="sxs-lookup"><span data-stu-id="3891f-144">**Password**</span></span> | <span data-ttu-id="3891f-145">Olá palavra-passe da sua conta de administrador do servidor</span><span class="sxs-lookup"><span data-stu-id="3891f-145">hello password for your server admin account</span></span> | <span data-ttu-id="3891f-146">Esta é a palavra-passe de Olá que especificou quando criou o servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-146">This is hello password that you specified when you created hello server.</span></span> |

   ![ligar tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="3891f-148">Clique em **opções** no Olá **ligar tooserver** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3891f-148">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="3891f-149">No Olá **ligar toodatabase** secção, introduza **mySampleDatabase** base de dados do tooconnect toothis.</span><span class="sxs-lookup"><span data-stu-id="3891f-149">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![ligar toodb no servidor](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="3891f-151">Clique em **Ligar**.</span><span class="sxs-lookup"><span data-stu-id="3891f-151">Click **Connect**.</span></span> <span data-ttu-id="3891f-152">é aberta a janela do Explorador de objetos de Olá no SSMS.</span><span class="sxs-lookup"><span data-stu-id="3891f-152">hello Object Explorer window opens in SSMS.</span></span> 

   ![tooserver ligado](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="3891f-154">No Object Explorer, expanda **bases de dados** e, em seguida, expanda **mySampleDatabase** objetos de Olá tooview na base de dados de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="3891f-155">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="3891f-155">Query data</span></span>

<span data-ttu-id="3891f-156">Seguinte de Olá de utilização código tooquery para produtos de primeiros 20 Olá por categoria utilizando Olá [SELECIONE](https://msdn.microsoft.com/library/ms189499.aspx) instrução Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3891f-156">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3891f-157">No Object Explorer, clique com o botão direito do rato em **mySampleDatabase** e, em seguida, clique em **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="3891f-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="3891f-158">Uma janela de consulta em branco abre-se que está ligado tooyour base de dados.</span><span class="sxs-lookup"><span data-stu-id="3891f-158">A blank query window opens that is connected tooyour database.</span></span>
2. <span data-ttu-id="3891f-159">Na janela de consulta Olá, introduza Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="3891f-159">In hello query window, enter hello following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="3891f-160">Na barra de ferramentas Olá, clique em **executar** tooretrieve dados das tabelas de produto e ProductCategory Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-160">On hello toolbar, click **Execute** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![consulta](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="3891f-162">Inserir dados</span><span class="sxs-lookup"><span data-stu-id="3891f-162">Insert data</span></span>

<span data-ttu-id="3891f-163">Utilize Olá seguinte código tooinsert novo produto na tabela de SalesLT.Product Olá utilizando Olá [inserir](https://msdn.microsoft.com/library/ms174335.aspx) instrução Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3891f-163">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3891f-164">Na janela de consulta Olá, substitua a consulta anterior Olá com Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="3891f-164">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="3891f-165">Na barra de ferramentas Olá, clique em **executar** tooinsert uma nova linha na tabela de produto Olá.</span><span class="sxs-lookup"><span data-stu-id="3891f-165">On hello toolbar, click **Execute**  tooinsert a new row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="3891f-166">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="3891f-166">Update data</span></span>

<span data-ttu-id="3891f-167">Seguinte de Olá de utilização código tooupdate Olá novo produto que adicionou anteriormente utilizando Olá [ATUALIZAÇÃO](https://msdn.microsoft.com/library/ms177523.aspx) instrução Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3891f-167">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3891f-168">Na janela de consulta Olá, substitua a consulta anterior Olá com Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="3891f-168">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="3891f-169">Na barra de ferramentas Olá, clique em **executar** tooupdate Olá especificado linha Olá produto tabela.</span><span class="sxs-lookup"><span data-stu-id="3891f-169">On hello toolbar, click **Execute** tooupdate hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="3891f-170">Eliminar dados</span><span class="sxs-lookup"><span data-stu-id="3891f-170">Delete data</span></span>

<span data-ttu-id="3891f-171">Seguinte de Olá de utilização código toodelete Olá novo produto que adicionou anteriormente utilizando Olá [eliminar](https://msdn.microsoft.com/library/ms189835.aspx) instrução Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3891f-171">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="3891f-172">Na janela de consulta Olá, substitua a consulta anterior Olá com Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="3891f-172">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="3891f-173">Na barra de ferramentas Olá, clique em **executar** toodelete Olá especificado linha Olá produto tabela.</span><span class="sxs-lookup"><span data-stu-id="3891f-173">On hello toolbar, click **Execute** toodelete hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="3891f-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3891f-174">Next steps</span></span>

- <span data-ttu-id="3891f-175">toolearn sobre como criar e gerir servidores e bases de dados com o Transact-SQL, consulte [Saiba mais sobre os servidores de base de dados do Azure SQL Server e bases de dados](sql-database-servers-databases.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-175">toolearn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="3891f-176">Para obter informações sobre o SSMS, consulte o artigo [Use SQL Server Management Studio (Utilizar o SQL Server Management Studio)](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="3891f-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="3891f-177">tooconnect e consulta utilizando o Visual Studio Code, consulte [ligar e consultar com o Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-177">tooconnect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="3891f-178">tooconnect e a consulta utilizando o .NET, consulte [ligar e consultar com .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-178">tooconnect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="3891f-179">tooconnect e consulta com o PHP, consulte [ligar e consultar com o PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-179">tooconnect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="3891f-180">tooconnect e a consulta com o Node.js, consulte [ligar e consultar com o Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-180">tooconnect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="3891f-181">tooconnect e consulta utilizando Java, consulte [ligar e consultar com o Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-181">tooconnect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="3891f-182">tooconnect e a consulta com o Python, consulte [ligar e consultar com o Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-182">tooconnect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="3891f-183">tooconnect e consulta utilizando Ruby, consulte [ligar e consultar com Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="3891f-183">tooconnect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
