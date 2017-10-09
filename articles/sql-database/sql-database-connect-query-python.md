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
# <a name="use-python-tooquery-an-azure-sql-database"></a>Utilizar o Python tooquery uma base de dados SQL do Azure

 Este guia de introdução demonstra como toouse [Python](https://python.org) tooconnect tooan SQL do Azure da base de dados e utilizar os dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápida neste tutorial de início, certifique-se de que tem o seguinte Olá:

- Uma base de dados SQL do Azure. Este guia de introdução utiliza recursos de Olá criados destes inícios rápidos: 

   - [Criar BD - Portal](sql-database-get-started-portal.md)
   - [Criar BD - CLI](sql-database-get-started-cli.md)
   - [Criar BD - PowerShell](sql-database-get-started-powershell.md)

- A [regra de firewall ao nível do servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de Olá do computador Olá utilizar para este tutorial de início rápido.

- Ter instalado o Python e software relacionado para o seu sistema operativo.

    - **MacOS**: Homebrew instalar o Python, instalar o controlador ODBC Olá e SQLCMD e, em seguida, instalar Olá controlador do Python para o SQL Server. Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).
    - **Ubuntu**: instalar o Python e outros necessário pacotes e, em seguida, instalar Olá controlador do Python para o SQL Server. Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).
    - **Windows**: instalar a versão mais recente do Olá do Python (variável de ambiente está agora configurada por si), instale o controlador ODBC Olá e SQLCMD e, em seguida, instalar Olá Python controlador para o SQL Server. Veja os [Passos 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/). 

## <a name="sql-server-connection-information"></a>Informações de ligação do servidor SQL

Obter Olá ligação informações necessárias tooconnect toohello SQL database do Azure. Precisa de nome de servidor completamente qualificado de Olá, nome de base de dados e informações de início de sessão nos procedimentos seguintes Olá.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página. 
3. No Olá **descrição geral** página para a base de dados, consulte Olá nome completamente qualificado servidor conforme mostrado no Olá seguinte imagem. Pode colocar o cursor sobre Olá toobring de nome de servidor se Olá **clique toocopy** opção.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se se esquecer da sua informações de início de sessão do servidor, navegue toohello base de dados do SQL server página tooview Olá admin nome do servidor e, se necessário, de reposição de palavra-passe de Olá.     
    
## <a name="insert-code-tooquery-sql-database"></a>Inserir código tooquery SQL da base de dados 

1. No seu editor de texto favorito, crie um novo ficheiro, **sqltest.py**.  

2. Substitua o conteúdo de Olá Olá seguinte código e adicione os valores apropriados Olá para o seu servidor, base de dados, utilizador e palavra-passe.

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

## <a name="run-hello-code"></a>Executar código Olá

1. Na linha de comandos Olá, execute Olá os seguintes comandos:

   ```Python
   python sqltest.py
   ```

2. Certifique-se de que as linhas de 20 superior Olá são devolvidas e, em seguida, feche a janela de aplicação Olá.

## <a name="next-steps"></a>Passos seguintes

- [Criar a sua primeira base de dados SQL do Azure](sql-database-design-first-database.md)
- [Controladores Python da Microsoft para SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [Centro para Programadores do Python](https://azure.microsoft.com/develop/python/?v=17.23h)

