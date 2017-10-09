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
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Utilizar tooquery Ruby uma base de dados SQL do Azure

Este tutorial de início rápido demonstra como toouse [Ruby](https://www.ruby-lang.org) toocreate tooan de tooconnect um programa Azure SQL da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápida neste tutorial de início, certifique-se de que tem os seguintes pré-requisitos de Olá:

- Uma base de dados SQL do Azure. Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos: 

   - [Criar BD - Portal](sql-database-get-started-portal.md)
   - [Criar BD - CLI](sql-database-get-started-cli.md)
   - [Criar BD - PowerShell](sql-database-get-started-powershell.md)

- A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.
- Ter instalado o Ruby e software relacionado para o seu sistema operativo.
    - **MacOS**: instale o Homebrew, instale o rbenv e o ruby-build, instale o Ruby e, em seguida, instale o FreeTDS. Veja os [Passos 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: instale os pré-requisitos para Ruby, instale o rbenv e o ruby-build, instale o Ruby e, em seguida, instale o FreeTDS. Veja os [Passos 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Informações de ligação do servidor SQL

Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure. Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página. 
3. No Olá **descrição geral** da base de dados, reveja o nome de servidor completamente qualificado Olá. Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção, conforme mostrado no Olá seguinte imagem:

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se tenha esquecido informações de início de sessão de Olá para o servidor da SQL Database do Azure, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.

> [!IMPORTANT]
> Tem de ter uma regra de firewall no local para o endereço IP público de Olá do computador Olá em que executar este tutorial. Se estiver num computador diferente ou ter um endereço IP público diferentes, crie um [através de regra de firewall ao nível do servidor Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Inserir código tooquery SQL da base de dados

1. No seu editor de texto favorito, crie um ficheiro novo, **sqltest.py**.

2. Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.

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

## <a name="run-hello-code"></a>Executar código Olá

1. Na linha de comandos Olá, execute Olá os seguintes comandos:

   ```bash
   ruby sqltest.rb
   ```

2. Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.


## <a name="next-steps"></a>Passos Seguintes
- [Criar a sua primeira base de dados SQL do Azure](sql-database-design-first-database.md)
- [Repositório do GitHub para TinyTDS](https://github.com/rails-sqlserver/tiny_tds)
- [Report issues or ask questions about TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues) (Comunicar problemas ou fazer perguntas sobre o TinyTDS)
- [Controladores Ruby para SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
