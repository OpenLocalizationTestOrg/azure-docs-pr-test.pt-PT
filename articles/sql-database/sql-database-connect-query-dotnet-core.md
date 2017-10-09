---
title: aaaUse .NET Core tooquery SQL Database do Azure | Microsoft Docs
description: "Este tópico mostra-lhe como toouse .NET Core toocreate um programa que liga tooan SQL Database do Azure e consultar com instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="8cfc9-103">Utilize o .NET Core (c#) tooquery uma base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8cfc9-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="8cfc9-104">Este tutorial de início rápido demonstra como toouse [.NET Core](https://www.microsoft.com/net/) no Linux/Windows/macOS toocreate um c# programa tooconnect tooan SQL do Azure da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cfc9-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8cfc9-105">Prerequisites</span></span>

<span data-ttu-id="8cfc9-106">toocomplete rápida neste tutorial de início, certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="8cfc9-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="8cfc9-107">Uma base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-107">An Azure SQL database.</span></span> <span data-ttu-id="8cfc9-108">Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="8cfc9-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="8cfc9-109">Criar BD - Portal</span><span class="sxs-lookup"><span data-stu-id="8cfc9-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8cfc9-110">Criar BD - CLI</span><span class="sxs-lookup"><span data-stu-id="8cfc9-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8cfc9-111">Criar BD - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cfc9-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8cfc9-112">A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="8cfc9-113">Já instalou o [.NET Core para o seu sistema operativo](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="8cfc9-114">Informações de ligação do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="8cfc9-114">SQL server connection information</span></span>

<span data-ttu-id="8cfc9-115">Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="8cfc9-116">Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="8cfc9-117">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8cfc9-118">Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8cfc9-119">No Olá **descrição geral** página para a base de dados, consulte Olá nome completamente qualificado servidor conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="8cfc9-120">Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8cfc9-122">Se se esquecer da sua informações de início de sessão do servidor de SQL Database do Azure, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="8cfc9-123">Pode repor a palavra-passe de Olá se necessário.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="8cfc9-124">Clique em **Mostrar cadeias de ligação da base de dados**.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="8cfc9-125">Olá revisão concluída **ADO.NET** cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Cadeia de ligação de ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="8cfc9-127">Tem de ter uma regra de firewall no local para o endereço IP público de Olá do computador Olá em que executar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="8cfc9-128">Se estiver num computador diferente ou ter um endereço IP público diferentes, crie um [através de regra de firewall ao nível do servidor Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="8cfc9-129">Criar um novo projeto .NET</span><span class="sxs-lookup"><span data-stu-id="8cfc9-129">Create a new .NET project</span></span>

1. <span data-ttu-id="8cfc9-130">Abra uma linha de comandos e crie uma pasta com o nome *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="8cfc9-131">Navegue toohello pasta que cria e executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8cfc9-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="8cfc9-132">Abra ***sqltest.csproj*** com o editor de texto favorito e adicionar SqlClient como uma dependência utilizando Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="8cfc9-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="8cfc9-133">Inserir código tooquery SQL da base de dados</span><span class="sxs-lookup"><span data-stu-id="8cfc9-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="8cfc9-134">No seu ambiente de desenvolvimento ou editor de texto favorito, abra **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="8cfc9-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="8cfc9-135">Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="8cfc9-136">Executar código Olá</span><span class="sxs-lookup"><span data-stu-id="8cfc9-136">Run hello code</span></span>

1. <span data-ttu-id="8cfc9-137">Na linha de comandos Olá, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="8cfc9-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="8cfc9-138">Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="8cfc9-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8cfc9-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8cfc9-139">Next steps</span></span>

- <span data-ttu-id="8cfc9-140">[Introdução ao .NET Core em Windows/Linux/macOS utilizando a linha de comandos Olá](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="8cfc9-141">Saiba como demasiado[ligar e consultar uma base de dados SQL do Azure utilizando Olá .NET framework e o Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="8cfc9-142">Saiba como demasiado[conceber a sua primeira SQL database do Azure com o SSMS](sql-database-design-first-database.md) ou [conceber a sua primeira SQL database do Azure através do .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="8cfc9-143">Para obter mais informações sobre o .NET, veja a [Documentação .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="8cfc9-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
