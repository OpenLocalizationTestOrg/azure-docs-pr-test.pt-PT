---
title: "Inícios de sessão e utilizadores do SQL do Azure | Microsoft Docs"
description: "Saiba mais sobre a gestão da segurança da Base de Dados SQL, mais concretamente como gerir o acesso às bases de dados e a segurança dos inícios de sessão através da conta principal ao nível do servidor."
keywords: "segurança de base de dados sql,gestão de segurança da base de dados,segurança de início de sessão,segurança de base de dados,acesso de base de dados"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Active
ms.date: 01/23/2017
ms.author: carlrab
ms.openlocfilehash: 4963e67317f22140c318e29bcd03bce4b9f57ab6
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/11/2018
---
# <a name="controlling-and-granting-database-access"></a>Controlar e conceder acesso à base de dados

Depois de tem configuradas regras de firewall, as pessoas podem ligar a uma base de dados do SQL Server como uma das contas de administrador, como o proprietário da base de dados ou um utilizador de base de dados na base de dados.  

>  [!NOTE]  
>  Este tópico aplica-se ao servidor SQL do Azure, bem como às bases de dados da Base de Dados SQL e do SQL Data Warehouse que são criadas no servidor SQL do Azure. Para simplificar, a Base de Dados SQL é utilizada para referenciar a Base de Dados SQL e o SQL Data Warehouse. 
>

> [!TIP]
> Para um tutorial, consulte [proteger a base de dados do SQL do Azure](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Contas administrativas sem restrições
Existem duas contas administrativas (**Administrador de servidor** e **Administrador do Active Directory**) que atuam como administradores. Para identificar estas contas de administrador para o seu servidor SQL, abra o portal do Azure e navegue para as propriedades do servidor SQL.

![Administradores do SQL Server](./media/sql-database-manage-logins/sql-admins.png)

- **Administrador de servidor**   
Quando cria um servidor SQL do Azure, tem de designar um **Início de sessão de administrador do servidor**. O servidor SQL cria essa conta como um início de sessão na base de dados mestra. Liga-se através da autenticação do SQL Server (nome de utilizador e palavra-passe). Só pode existir uma destas contas.   
- **Administrador do Azure Active Directory**   
Também é possível configurar uma conta do Azure Active Directory, seja esta individual ou de grupo de segurança, como administrador. Configurar um administrador do Azure AD é opcional. Contudo, este tem de ser configurado se quiser utilizar contas do Azure AD para ligar à Base de Dados SQL. Para obter mais informações sobre a configuração do acesso do Azure Active Directory, veja [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication (Ligar à Base de Dados SQL ou ao SQL Data Warehouse Com a Autenticação do Azure Active Directory)](sql-database-aad-authentication.md) e [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication (Suporte do SSMS para Azure AD MFA com Base de Dados SQL e SQL Data Warehouse)](sql-database-ssms-mfa-authentication.md).
 

As contas de **Administrador de servidor** e de **Administrador do Azure AD** têm as seguintes características:
- São as únicas contas que podem ligar automaticamente a qualquer Base de Dados SQL no servidor. (Para ligar a uma base de dados de utilizador, as outras contas têm de ser o proprietário da base de dados ou ter uma conta de utilizador na base de dados de utilizador.)
- Estas contas introduzem bases de dados de utilizador como o utilizador `dbo` e têm todas as permissões nas bases de dados de utilizador. (O proprietário de uma base de dados de utilizador também introduz a base de dados como o utilizador `dbo`.) 
- Estas contas não introduzem a base de dados `master` como o utilizador `dbo` e têm permissões limitadas na base de dados mestra. 
- Estas contas não são membros da função de servidor fixa `sysadmin` standard do SQL Server, a qual não está disponível na base de dados SQL.  
- Estas contas podem criar, alterar e remover bases de dados, inícios de sessão, utilizadores na base de dados mestra e regras de firewall ao nível do servidor.
- Estas contas podem adicionar e remover membros das funções `dbmanager` e `loginmanager`.
- Estas contas podem ver a tabela de sistema `sys.sql_logins`.

### <a name="configuring-the-firewall"></a>Configurar a firewall
Quando a firewall ao nível do servidor está configurada para um endereço IP individual ou intervalo de IP, o **administrador de servidor SQL** e o **administrador do Azure Active Directory** podem ligar-se à base de dados mestra e a todas as bases de dados de utilizador. A firewall ao nível do servidor inicial pode ser configurada através do [portal do Azure](sql-database-get-started-portal.md), com o [PowerShell](sql-database-get-started-powershell.md) ou com a [API REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Depois de estabelecida uma ligação, também podem ser configuradas regras de firewall ao nível do servidor adicionais através do [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Caminho de acesso do administrador
Quando a firewall ao nível do servidor está configurada corretamente, o **administrador de servidor SQL** e o **administrador do Azure Active Directory** podem ligar-se com ferramentas de cliente como o SQL Server Management Studio ou os SQL Server Data Tools. Só as ferramentas mais recentes proporcionam todas as funcionalidades e capacidades. O diagrama seguinte mostra uma configuração típica para as duas contas de administrador.

![Caminho de acesso do administrador](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Quando utilizar uma porta aberta na firewall ao nível do servidor, os administradores podem ligar-se a qualquer Base de Dados SQL.

### <a name="connecting-to-a-database-by-using-sql-server-management-studio"></a>Ligar a uma base de dados com o SQL Server Management Studio
Para ver uma introdução à criação de um servidor, uma base de dados, regras de firewall ao nível do servidor e à utilização do SQL Server Management Studio para consultar uma base de dados, veja [Introdução aos servidores, bases de dados e regras de firewall da Base de Dados SQL do Azure através do portal do Azure e do SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> É recomendado utilizar sempre a versão mais recente do Management Studio, para permanecer sincronizado com as atualizações do Microsoft Azure e da Base de Dados SQL. [Atualize o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Funções administrativas adicionais ao nível do servidor
Para além das funções administrativas ao nível do servidor abordadas anteriormente, a Base de Dados SQL fornece duas funções administrativas restritas na base de dados mestra às quais podem ser adicionadas contas de utilizador que concedam permissões para criar bases de dados ou gerir inícios de sessão.

### <a name="database-creators"></a>Criadores de base de dados
Uma destas funções administrativas é a função **dbmanager**. Os membros desta função podem criar novas bases de dados. Para utilizar esta função, crie um utilizador na base de dados `master` e, em seguida, adicione o utilizador à função de base de dados **dbmanager**. Para criar uma base de dados, o utilizador tem de ser um utilizador baseado num início de sessão do SQL Server na base de dados mestra ou um utilizador de base de dados contida baseado num utilizador do Azure Active Directory.

1. Ao utilizar uma conta de administrador, ligue à base de dados mestra.
2. Passo opcional: crie um início de sessão da autenticação do SQL Server, utilizando a instrução [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx). Instrução de exemplo:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Utilize uma palavra-passe forte ao criar um utilizador de base de dados contido ou de início de sessão. Para obter mais informações, veja [Strong Passwords (Palavras-passe Fortes)](https://msdn.microsoft.com/library/ms161962.aspx).
    
   Para melhorar o desempenho, os início de sessão (principais ao nível do servidor) são temporariamente colocados em cache ao nível da base de dados. Para atualizar a cache de autenticação, veja [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. Na base de dados mestra, crie um utilizador com a instrução [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx). O utilizador pode ser um utilizador de base de dados contido do Azure Active Directory (se tiver configurado o ambiente para autenticação do Azure AD), um utilizador de base de dados contido de autenticação do SQL Server ou um utilizador de autenticação do SQL Server com base num início de sessão de autenticação do SQL Server (criado no passo anterior). Instruções de exemplo:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Adicione o utilizador novo à função de base de dados **dbmanager** com a instrução [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx). Instruções de exemplo:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > O dbmanager é uma função de base de dados na base de dados mestra, pelo que só pode adicionar um utilizador de base de dados à função dbmanager. Não pode adicionar um início de sessão ao nível do servidor à função de nível de base de dados.
    
5. Se for necessário, configure uma regra de firewall para permitir que o novo utilizador se ligue. (O novo utilizador poderá ser abrangido por uma regra de firewall existente.)

Agora, o utilizador pode ligar à base de dados mestra e criar bases de dados novas. A conta que cria a base de dados torna-se na proprietária da base de dados.

### <a name="login-managers"></a>Gestores de início de sessão
A outra função administrativa é a função de gestor de início de sessão. Os membros desta função podem criar novos inícios de sessão na base de dados mestra. Se pretender, pode seguir os mesmos passos (criar um início de sessão e um utilizador e adicionar um utilizador à função **loginmanager**) para permitir que um utilizador crie novos inícios de sessão na base de dados mestra. Normalmente, os inícios de sessão não são necessários, uma vez que a Microsoft recomenda a utilização de utilizadores de base de dados contidos, o que autentica ao nível da base de dados em vez de utilizar os utilizadores com base em inícios de sessão. Para obter mais informações, veja [Contained Database Users - Making Your Database Portable (Utilizadores de Base de Dados Contidos - Tornar a Sua Base de Dados Portátil)](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Utilizadores não administradores
Geralmente, as contas de não administrador não precisam de acesso à base de dados mestra. Utilize a instrução [CREATE USER (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) para criar os utilizadores de base de dados contidos na base de dados ao nível da base de dados. O utilizador pode ser um utilizador de base de dados contido do Azure Active Directory (se tiver configurado o ambiente para autenticação do Azure AD), um utilizador de base de dados contido de autenticação do SQL Server ou um utilizador de autenticação do SQL Server com base num início de sessão de autenticação do SQL Server (criado no passo anterior). Para obter mais informações, veja [Contained Database Users - Making Your Database Portable (Utilizadores de Base de Dados Contidos - Tornar a Sua Base de Dados Portátil)](https://msdn.microsoft.com/library/ff929188.aspx). 

Para criar utilizadores, ligue à base de dados e execute instruções semelhantes aos exemplos seguintes:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Inicialmente, apenas um dos administradores ou o proprietário da base de dados pode criar utilizadores. Para permitir que outros utilizadores criem utilizadores novos, conceda-lhes a permissão `ALTER ANY USER`, mediante uma instrução como:

```
GRANT ALTER ANY USER TO Mary;
```

Para conceder aos utilizadores adicionais controlo total da base de dados, torne-os membros da função de base de dados fixa **db_owner** com a instrução `ALTER ROLE`.

> [!NOTE]
> O motivo mais comum para criar utilizadores de base de dados baseados em inícios de sessão é ter utilizadores de autenticação do SQL Server que precisam de aceder a várias bases de dados. Os utilizadores com base em inícios de sessão são associados ao início de sessão e é mantida apenas uma palavra-passe para esse início de sessão. Os utilizadores da base de dados contidos nas bases de dados individuais são entidades individuais e cada uma mantém a sua própria palavra-passe. Isto pode baralhar os utilizadores de base de dados contidos, se estes não mantiverem as palavras-passe idênticas.

### <a name="configuring-the-database-level-firewall"></a>Configurar a firewall ao nível da base de dados
Como melhor prática, os utilizadores não administradores só devem ter acesso às bases de dados que utilizam através da firewall. Em vez de autorizar os endereços IP deles através da firewall ao nível do servidor e conceder acesso a todas as bases de dados, utilize a instrução [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) para configurar a firewall ao nível da base de dados. Não é possível configurar a firewall ao nível da base de dados no portal.

### <a name="non-administrator-access-path"></a>Caminho de acesso para não administradores
Quando a firewall ao nível da base de dados está devidamente configurada, os utilizadores da base de dados podem ligar através de ferramentas de cliente, como o SQL Server Management Studio ou o SQL Server Data Tools. Só as ferramentas mais recentes proporcionam todas as funcionalidades e capacidades. O diagrama seguinte mostra um caminho típico de acesso para não administradores.

![Caminho de acesso para não administradores](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Grupos e funções
A gestão de acessos eficaz utiliza permissões atribuídas a grupos e funções em vez de utilizadores individuais. 

- Quando utilizar a autenticação do Azure Active Directory, coloque os utilizadores do Azure Active Directory num grupo do Azure Active Directory. Crie um utilizador de base de dados contido para o grupo. Coloque um ou mais utilizadores de base de dados numa [função de base de dados](https://msdn.microsoft.com/library/ms189121) e, em seguida, atribua [permissões](https://msdn.microsoft.com/library/ms191291.aspx) à função de base de dados.

- Ao utilizar a autenticação do SQL Server, crie utilizadores de base de dados contida na base de dados. Coloque um ou mais utilizadores de base de dados numa [função de base de dados](https://msdn.microsoft.com/library/ms189121) e, em seguida, atribua [permissões](https://msdn.microsoft.com/library/ms191291.aspx) à função de base de dados.

As funções de base de dados podem ser as funções incorporadas, tais como **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter** e **db_denydatareader**. **db_owner** é, geralmente, utilizada para conceder permissão total apenas a alguns utilizadores. As outras funções de base de dados fixas são úteis para colocar bases de dados simples em desenvolvimento rapidamente, mas não são recomendadas para a maioria das bases de dados de produção. Por exemplo, a função de base de dados fixa **db_datareader** concede acesso de leitura a todas as tabelas na base de dados, o que, regra geral, é mais do que o estritamente necessário. É muito melhor utilizar a instrução [CREATE ROLE](https://msdn.microsoft.com/library/ms187936.aspx) para criar as suas próprias funções de base de dados definidas pelo utilizador e conceder, cuidadosamente, a cada função o menor número de permissões necessárias para a atividade em causa. Quando um utilizador é membro de várias funções, agrega as permissões de todas essas funções.

## <a name="permissions"></a>Permissões
Existem mais de 100 permissões que podem ser individualmente concedidas ou negadas na Base de Dados SQL. Muitas destas permissões são aninhadas. Por exemplo, a permissão `UPDATE` num esquema inclui a permissão `UPDATE` em cada tabela dentro desse esquema. Tal como na maioria dos sistemas de permissões, a recusa de uma permissão sobrepõe-se a uma atribuição. Devido à natureza aninhada e ao número de permissões, desenhar um sistema de permissões que proteja as bases de dados adequadamente pode envolver um cuidadoso estudo. Comece com a lista de permissões em [Permissions (Database Engine) (Permissões [Motor de Base de Dados])](https://msdn.microsoft.com/library/ms191291.aspx) e reveja o [gráfico em tamanho de cartaz](http://go.microsoft.com/fwlink/?LinkId=229142) das permissões.


### <a name="considerations-and-restrictions"></a>Considerações e restrições
Ao gerir inícios de sessão e utilizadores na Base de Dados SQL, considere o seguinte:

* Tem de estar ligado à base de dados **mestra** ao executar as instruções `CREATE/ALTER/DROP DATABASE`.   
* O utilizador da base de dados que corresponde ao início de sessão do **Administrador de servidor** não pode ser alterado ou removido. 
* O inglês dos E.U.A. é o idioma predefinido do início de sessão do **Administrador de servidor**.
* Só os administradores (início de sessão do **Administrador de servidor** ou administrador do Azure AD) e os membros da função de base de dados **dbmanager**ba base de dados **mestra** têm permissão para executar as declarações `CREATE DATABASE` e `DROP DATABASE`.
* Tem de estar ligado à base de dados mestra ao executar as instruções `CREATE/ALTER/DROP LOGIN`. No entanto, não é aconselhável utilizar inícios de sessão. Utilize os utilizadores de base de dados contida.
* Para ligar a uma base de dados do utilizador, tem de fornecer o nome da base de dados na cadeia de ligação.
* Apenas o início de sessão principal ao nível do servidor e os membros da função de base de dados **loginmanager** na base de dados **mestra** têm permissão para executar as instruções `CREATE LOGIN`, `ALTER LOGIN`, e `DROP LOGIN`.
* Ao executar as instruções `CREATE/ALTER/DROP LOGIN` e `CREATE/ALTER/DROP DATABASE` numa aplicação ADO.NET, não deve utilizar comandos parametrizados. Para obter mais informações, consulte [Comandos e Parâmetros](https://msdn.microsoft.com/library/ms254953.aspx).
* Ao executar as instruções `CREATE/ALTER/DROP DATABASE` e `CREATE/ALTER/DROP LOGIN`, cada uma das seguintes declarações tem de ser a única instrução num batch do Transact-SQL. Caso contrário, ocorrerá um erro. Por exemplo, o Transact-SQL seguinte verifica se a base de dados existe. Se existir, é chamada uma instrução `DROP DATABASE` para remover a base de dados. Uma vez que a instrução `DROP DATABASE` não é a única instrução no batch, executar a seguinte instrução do Transact-SQL ocorre um erro.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Ao executar a `CREATE USER` com a opção `FOR/FROM LOGIN`, tem de ser a única instrução num batch do Transact-SQL.
* Ao executar a `ALTER USER` com a opção `WITH LOGIN`, tem de ser a única instrução num batch do Transact-SQL.
* Para `CREATE/ALTER/DROP`, um utilizador necessita da permissão `ALTER ANY USER` na base de dados.
* Quando o proprietário de uma função de base de dados tenta adicionar ou remover outro utilizador de base de dados de ou para essa função de base de dados, pode ocorrer o seguinte erro: **o utilizador ou a função "Nome" não existe nesta base de dados.** Este erro ocorre porque o utilizador não está visível para o proprietário. Para resolver este problema, conceda uma permissão de `VIEW DEFINITION` ao proprietário da função. 


## <a name="next-steps"></a>Passos Seguintes

- Para saber mais sobre regras de firewall, veja [Firewall da Base de Dados SQL do Azure](sql-database-firewall-configure.md).
- Para obter uma descrição geral de todas as funcionalidades de segurança da Base de Dados SQL, veja a [Descrição geral da segurança de SQL](sql-database-security-overview.md).
- Para um tutorial, consulte [proteger a base de dados do SQL do Azure](sql-database-security-tutorial.md).
- Para obter informações sobre vistas e procedimentos armazenados, veja [Creating views and stored procedures (Criar vistas e procedimentos armazenados)](https://msdn.microsoft.com/library/ms365311.aspx)
- Para obter informações sobre como conceder acesso a um objeto de base de dados, veja [Granting Access to a Database Object (Conceder Acesso a um Objeto de Base de Dados)](https://msdn.microsoft.com/library/ms365327.aspx)
