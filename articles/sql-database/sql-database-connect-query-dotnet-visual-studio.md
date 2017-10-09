---
title: aaaUse Visual Studio e .NET tooquery SQL Database do Azure | Microsoft Docs
description: "Este tópico mostra como toouse Visual Studio toocreate um programa que liga tooan SQL Database do Azure e a consulta utilizando instruções Transact-SQL."
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
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a>Utilize o .NET (c#) com o Visual Studio tooconnect e consultar uma base de dados SQL do Azure

Este tutorial de início rápido demonstra como toouse Olá [.NET framework](https://www.microsoft.com/net/) toocreate um c# programa com o Visual Studio tooconnect tooan SQL database do Azure e utilizar os dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápida neste tutorial de início, certifique-se de que tem o seguinte Olá:

- Uma base de dados SQL do Azure. Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos: 

   - [Criar BD - Portal](sql-database-get-started-portal.md)
   - [Criar BD - CLI](sql-database-get-started-cli.md)
   - [Criar BD - PowerShell](sql-database-get-started-powershell.md)

- A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.
- Uma instalação do [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).

## <a name="sql-server-connection-information"></a>Informações de ligação do servidor SQL

Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure. Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página. 
3. No Olá **descrição geral** página para a base de dados, consulte Olá nome completamente qualificado servidor conforme mostrado no Olá seguinte imagem. Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se se esquecer da sua informações de início de sessão do servidor de SQL Database do Azure, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor. Pode repor a palavra-passe de Olá se necessário.

5. Clique em **Mostrar cadeias de ligação da base de dados**.

6. Olá revisão concluída **ADO.NET** cadeia de ligação.

    ![Cadeia de ligação de ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> Tem de ter uma regra de firewall no local para o endereço IP público de Olá do computador Olá em que executar este tutorial. Se estiver num computador diferente ou ter um endereço IP público diferentes, crie um [através de regra de firewall ao nível do servidor Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 
>
  
## <a name="create-a-new-visual-studio-project"></a>Criar um novo projeto do Visual Studio

1. No Visual Studio, escolha **Ficheiro**, **Novo**, **Projeto**. 
2. No Olá **novo projeto** caixa de diálogo e expanda **Visual c#**.
3. Selecione **aplicação de consola** e introduza *sqltest* para o nome do projeto Olá.
4. Clique em **OK** toocreate e novo projeto de Olá abrir no Visual Studio
4. No Explorador de Soluções, clique com o botão direito do rato em **sqltest** e clique em **Gerir Pacotes NuGet**. 
5. No Olá **procurar**, procure ```System.Data.SqlClient``` e, quando encontrar, selecione-o.
6. No Olá **SqlClient** página, clique em **instalar**.
7. Quando concluída a instalação de Olá, reveja as alterações de Olá e, em seguida, clique em **OK** tooclose Olá **pré-visualização** janela. 
8. Se for apresentada uma janela **Aceitação de Licença**, clique em **Aceito**.

## <a name="insert-code-tooquery-sql-database"></a>Inserir código tooquery SQL da base de dados
1. Comutador demasiado (ou abrir se necessário) **Program.cs**

2. Substituir conteúdo Olá **Program.cs** com Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.

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

## <a name="run-hello-code"></a>Executar código Olá

1. Prima **F5** aplicação de Olá toorun.
2. Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.

## <a name="next-steps"></a>Passos seguintes

- Saiba como demasiado[ligar e consultar uma base de dados SQL do Azure utilizando o .NET core](sql-database-connect-query-dotnet-core.md) no Linux/Windows/macOS.  
- Saiba mais sobre [introdução ao .NET Core em Windows/Linux/macOS utilizando a linha de comandos Olá](/dotnet/core/tutorials/using-with-xplat-cli).
- Saiba como demasiado[conceber a sua primeira SQL database do Azure com o SSMS](sql-database-design-first-database.md) ou [conceber a sua primeira SQL database do Azure através do .NET](sql-database-design-first-database-csharp.md).
- Para obter mais informações sobre o .NET, veja a [Documentação .NET](https://docs.microsoft.com/dotnet/).
