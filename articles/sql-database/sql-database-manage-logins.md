---
title: "aaaAzure SQL inícios de sessão e os utilizadores | Microsoft Docs"
description: "Saiba mais sobre a gestão de segurança da base de dados SQL, especificamente como toomanage da base de dados segurança de início de sessão e acesso através de conta do principal de Olá ao nível do servidor."
keywords: "segurança de base de dados sql,gestão de segurança da base de dados,segurança de início de sessão,segurança de base de dados,acesso de base de dados"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Controlar e conceder acesso à base de dados

Quando as regras de firewall foram configuradas, pessoas podem ligar tooa base de dados do SQL Server como uma das contas de administrador Olá, como proprietário da base de dados de Olá ou um utilizador de base de dados na base de dados de Olá.  

>  [!NOTE]  
>  Este tópico aplica-se tooAzure SQL server e tooboth base de dados SQL e SQL Data Warehouse bases de dados que são criados no servidor de SQL do Azure Olá. De simplicidade, a base de dados SQL é utilizado ao fazer referência tooboth base de dados SQL e do armazém de dados do SQL Server. 
>

> [!TIP]
> Para um tutorial, consulte [proteger a base de dados do SQL do Azure](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Contas administrativas sem restrições
Existem duas contas administrativas (**Administrador de servidor** e **Administrador do Active Directory**) que atuam como administradores. tooidentify estas contas de administrador para o SQL server, abra Olá portal do Azure e navegue até toohello propriedades do servidor SQL.

![Administradores do SQL Server](./media/sql-database-manage-logins/sql-admins.png)

- **Administrador de servidor**   
Quando cria um servidor SQL do Azure, tem de designar um **Início de sessão de administrador do servidor**. Servidor de SQL cria essa conta como um início de sessão na base de dados mestra Olá. Liga-se através da autenticação do SQL Server (nome de utilizador e palavra-passe). Só pode existir uma destas contas.   
- **Administrador do Azure Active Directory**   
Também é possível configurar uma conta do Azure Active Directory, seja esta individual ou de grupo de segurança, como administrador. É opcional tooconfigure um administrador do Azure AD, mas um administrador do Azure AD tem de ser configurado se quiser toouse do Azure AD contas tooconnect tooSQL da base de dados. Para obter mais informações sobre como configurar o acesso ao Azure Active Directory, consulte [tooSQL de ligação da base de dados ou SQL dados do armazém por utilizar o Azure autenticação do Active Directory](sql-database-aad-authentication.md) e [SSMS suporte para o MFA do Azure AD com o SQL Server Base de dados e do armazém de dados do SQL Server](sql-database-ssms-mfa-authentication.md).
 

Olá **administração de servidor** e **do Azure AD admin** contas tem Olá seguintes características:
- Estas são apenas contas do Olá que poderão ligar automaticamente tooany base de dados SQL no servidor de Olá. (base de dados do utilizador do tooa de tooconnect, outras contas têm de estar proprietário Olá Olá da base de dados ou ter uma conta de utilizador na base de dados de utilizador de Olá.)
- Estas contas introduza bases de dados de utilizador como Olá `dbo` utilizador e ter todas as permissões de Olá nas bases de dados de utilizador de Olá. (proprietário Olá de uma base de dados do utilizador também introduz a base de dados de Olá como Olá `dbo` utilizador.) 
- Estas contas não introduza Olá `master` base de dados como Olá `dbo` utilizador e limitada permissões no mestre. 
- Estas contas não são membros de Olá standard do SQL Server `sysadmin` função de servidor fixa, que não está disponível na base de dados do SQL Server.  
- Estas contas podem criar, alterar e remover bases de dados, inícios de sessão, utilizadores na base de dados mestra e regras de firewall ao nível do servidor.
- Estas contas podem adicionar e remover membros toohello `dbmanager` e `loginmanager` funções.
- Estas contas podem ver Olá `sys.sql_logins` tabela do sistema.

### <a name="configuring-hello-firewall"></a>Configurar a firewall do Olá
Quando firewall ao nível do servidor de Olá está configurado para um endereço IP ou intervalo individuais, Olá **administrador do servidor SQL** e Olá **administração do Azure Active Directory** pode ligar a base de dados mestra toohello e todos os Olá bases de dados do utilizador. firewall do Olá inicial ao nível do servidor pode ser configurada através de Olá [portal do Azure](sql-database-get-started-portal.md)com [PowerShell](sql-database-get-started-powershell.md) ou utilizando Olá [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx). Depois de estabelecida uma ligação, também podem ser configuradas regras de firewall ao nível do servidor adicionais através do [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Caminho de acesso do administrador
Quando a firewall ao nível do servidor de Olá está corretamente configurada, Olá **administrador do servidor SQL** e Olá **administração do Azure Active Directory** podem estabelecer ligação utilizando ferramentas de cliente, como o SQL Server Management Studio ou o SQL Server Ferramentas de dados do servidor. Apenas Olá mais recentes ferramentas fornecem todas as funcionalidades de Olá e capacidades. Olá diagrama seguinte mostra uma configuração típica para Olá duas contas de administrador.

![Caminho de acesso do administrador](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Quando utilizar uma porta aberta na firewall ao nível do servidor de Olá, os administradores podem ligar tooany base de dados SQL.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Ligar a base de dados tooa utilizando o SQL Server Management Studio
Para uma passagem de criar um servidor, uma base de dados, as regras de firewall ao nível do servidor e utilizar o SQL Server Management Studio tooquery uma base de dados, consulte [começar com servidores de base de dados do Azure SQL, bases de dados e as regras de firewall utilizando Olá portal do Azure e SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> É recomendado que utilize sempre Olá versão mais recente do Management Studio tooremain sincronizada com atualizações tooMicrosoft Azure e a base de dados SQL. [Atualize o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Funções administrativas adicionais ao nível do servidor
Além disso toohello ao nível do servidor funções administrativas discutido anteriormente, base de dados do SQL Server fornece de duas funções administrativas restritas em contas de utilizador do Olá base de dados mestra toowhich podem ser adicionadas que conceda permissões tooeither criar bases de dados ou gerir inícios de sessão.

### <a name="database-creators"></a>Criadores de base de dados
Uma dessas funções administrativas é Olá **dbmanager** função. Os membros desta função podem criar novas bases de dados. toouse esta função, criar um utilizador no Olá `master` da base de dados e, em seguida, adicione Olá utilizador toohello **dbmanager** função de base de dados. toocreate uma base de dados, o utilizador Olá tem de ser um utilizador com base num início de sessão do SQL Server na base de dados mestra Olá ou continha utilizador de base de dados com base num utilizador do Azure Active Directory.

1. Utilizar uma conta de administrador, ligar a base de dados mestra toohello.
2. Passo opcional: criar um SQL Server authentication início de sessão com Olá [criar o início de sessão](https://msdn.microsoft.com/library/ms189751.aspx) instrução. Instrução de exemplo:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Utilize uma palavra-passe forte ao criar um utilizador de base de dados contido ou de início de sessão. Para obter mais informações, veja [Strong Passwords (Palavras-passe Fortes)](https://msdn.microsoft.com/library/ms161962.aspx).
    
   desempenho de tooimprove, inícios de sessão (nível de servidor principais) são temporariamente armazenados em cache ao nível da base de dados de Olá. cache de autenticação do toorefresh Olá, consulte [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. Base de dados mestra de Olá, criar um utilizador com Olá [criar utilizador](https://msdn.microsoft.com/library/ms173463.aspx) instrução. utilizador Olá pode ser um Azure Active Directory authentication contido da base de dados (se tiver configurado o seu ambiente para a autenticação do Azure AD), ou um utilizador de base de dados do SQL Server authentication contida ou um utilizador de autenticação do SQL Server com base no SQL Início de sessão do autenticação de servidor (criado no passo anterior Olá). Instruções de exemplo:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Adicionar Olá novo utilizador, toohello **dbmanager** função de base de dados utilizando Olá [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) instrução. Instruções de exemplo:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > Olá dbmanager é uma função de base de dados na base de dados mestra, pelo que só é possível adicionar uma função de dbmanager de toohello de utilizador de base de dados. Não é possível adicionar uma função de nível de toodatabase de início de sessão ao nível do servidor.
    
5. Se necessário, configure tooconnect uma firewall regra tooallow Olá novo utilizador. (o utilizador novo Olá poderá ser abrangido por uma regra de firewall existente).

Agora, utilizador de Olá pode ligar-se a base de dados mestra toohello e pode criar novas bases de dados. conta de Olá criar base de dados de Olá torna-se o proprietário de Olá da base de dados de Olá.

### <a name="login-managers"></a>Gestores de início de sessão
Olá outra administrativa função é função de Gestor de início de sessão de Olá. Os membros desta função podem criar novos inícios de sessão na base de dados mestra Olá. Se assim o desejar, pode concluir Olá mesmos passos (criar um início de sessão e o utilizador e adicionar um utilizador toohello **loginmanager** função) tooenable um utilizador toocreate novos inícios de sessão do mestre de Olá. Normalmente, os inícios de sessão não são necessários como a Microsoft recomenda a utilização de utilizadores de base de dados contida, o qual autenticar em Olá nível base de dados-em vez de utilizar os utilizadores com base em inícios de sessão. Para obter mais informações, veja [Contained Database Users - Making Your Database Portable (Utilizadores de Base de Dados Contidos - Tornar a Sua Base de Dados Portátil)](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Utilizadores não administradores
Geralmente, as contas de administrador não não precisa de aceder à base de dados mestra toohello. Criar utilizadores de base de dados contida no nível de base de dados de Olá utilizando Olá [criar utilizador (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) instrução. utilizador Olá pode ser um Azure Active Directory authentication contido da base de dados (se tiver configurado o seu ambiente para a autenticação do Azure AD), ou um utilizador de base de dados do SQL Server authentication contida ou um utilizador de autenticação do SQL Server com base no SQL Início de sessão do autenticação de servidor (criado no passo anterior Olá). Para obter mais informações, veja [Contained Database Users - Making Your Database Portable (Utilizadores de Base de Dados Contidos - Tornar a Sua Base de Dados Portátil)](https://msdn.microsoft.com/library/ff929188.aspx). 

utilizadores toocreate, ligar toohello base de dados e executar toohello semelhante as instruções seguintes exemplos:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Inicialmente, apenas um dos administradores de Olá ou proprietário Olá da base de dados de Olá pode criar utilizadores. tooauthorize utilizadores adicionais toocreate novos utilizadores, conceder Olá esse utilizador selecionado `ALTER ANY USER` permissão, utilizando uma instrução como:

```
GRANT ALTER ANY USER tooMary;
```

controlo total de utilizadores adicionais toogive da base de dados de Olá, tornar membro de Olá **db_owner** função de base de dados fixa utilizando Olá `ALTER ROLE` instrução.

> [!NOTE]
> Hello mais comuns razão toocreate da base de dados de utilizadores com base nos inícios de sessão, é se tiver utilizadores de autenticação do SQL Server que precisam de aceder toomultiple bases de dados. Os utilizadores com base em inícios de sessão são associadas toohello início de sessão e apenas uma palavra-passe que é mantida para início de sessão desse. Os utilizadores da base de dados contidos nas bases de dados individuais são entidades individuais e cada uma mantém a sua própria palavra-passe. Isto pode baralhar os utilizadores de base de dados contidos, se estes não mantiverem as palavras-passe idênticas.

### <a name="configuring-hello-database-level-firewall"></a>Configurar a firewall do nível de base de dados Olá
Como melhor prática, os utilizadores de não administrador só devem ter acesso através de Olá firewall toohello bases de dados que utilizam. Em vez de autorizar os respetivos IP endereços através de Olá nível do servidor de firewall e concedendo-lhes acesso tooall bases de dados, utilize Olá [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) firewall de nível de base de dados do instrução tooconfigure Olá. firewall de nível de base de dados de Olá não pode ser configurado através do portal Olá.

### <a name="non-administrator-access-path"></a>Caminho de acesso para não administradores
Quando a firewall do nível de base de dados de Olá está corretamente configurada, os utilizadores de base de dados de Olá podem estabelecer ligação utilizando ferramentas de cliente, como o SQL Server Management Studio ou o SQL Server Data Tools. Apenas Olá mais recentes ferramentas fornecem todas as funcionalidades de Olá e capacidades. Olá diagrama a seguir mostra um caminho de acesso comum de não administrador.

![Caminho de acesso para não administradores](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Grupos e funções
Gestão de acesso eficiente utiliza permissões atribuídas toogroups e funções em vez de utilizadores individuais. 

- Quando utilizar a autenticação do Azure Active Directory, coloque os utilizadores do Azure Active Directory num grupo do Azure Active Directory. Crie um utilizador de base de dados contida para o grupo de Olá. Colocar um ou mais utilizadores de base de dados para um [função de base de dados](https://msdn.microsoft.com/library/ms189121) e, em seguida, atribuir [permissões](https://msdn.microsoft.com/library/ms191291.aspx) toohello função de base de dados.

- Quando utilizar a autenticação do SQL Server, crie utilizadores de base de dados contida na base de dados de Olá. Colocar um ou mais utilizadores de base de dados para um [função de base de dados](https://msdn.microsoft.com/library/ms189121) e, em seguida, atribuir [permissões](https://msdn.microsoft.com/library/ms191291.aspx) toohello função de base de dados.

funções de base de dados de Olá podem ser como funções incorporadas Olá **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, e **db_denydatareader**. **db_owner** é frequentemente utilizadas toogrant permissão total tooonly alguns utilizadores. Olá outras funções de base de dados fixa são úteis para obter rapidamente uma base de dados simple de desenvolvimento, mas não são recomendadas para a maioria das bases de dados de produção. Por exemplo, Olá **db_datareader** função de base de dados fixa concede acesso de leitura tooevery tabela na base de dados Olá, que é normalmente mais do que é estritamente necessária. É melhor até que ponto toouse Olá [criar função](https://msdn.microsoft.com/library/ms187936.aspx) instrução toocreate os seus próprios definido pelo utilizador funções de base de dados e conceder cuidadosamente Olá cada função, pelo menos, permissões necessárias para a necessidade empresarial de Olá. Quando um utilizador é um membro de várias funções, estes agregar permissões Olá de todos eles.

## <a name="permissions"></a>Permissões
Existem mais de 100 permissões que podem ser individualmente concedidas ou negadas na Base de Dados SQL. Muitas destas permissões são aninhadas. Por exemplo, Olá `UPDATE` permissão num esquema inclui Olá `UPDATE` permissão em cada tabela dentro desse esquema. Como a maioria dos sistemas de permissão, Olá denial-of-uma permissão sobrepõe-se uma concessão. Devido à natureza Olá aninhado e número de Olá de permissões, pode demorar cuidado prático toodesign um tooproperly de sistema de permissões adequadas proteger a base de dados. Começar com uma lista de Olá de permissões em [permissões (motor de base de dados)](https://msdn.microsoft.com/library/ms191291.aspx) e rever Olá [gráfico de tamanho de cartaz](http://go.microsoft.com/fwlink/?LinkId=229142) de permissões de Olá.


### <a name="considerations-and-restrictions"></a>Considerações e restrições
Quando gerir inícios de sessão e os utilizadores na base de dados do SQL Server, considere o seguinte Olá:

* Tem de ser ligado toohello **mestre** da base de dados ao executar Olá `CREATE/ALTER/DROP DATABASE` instruções.   
* Olá correspondente de utilizador da base de dados toohello **administração de servidor** início de sessão não pode ser alterado ou removido. 
* Inglês dos Estados Unidos é o idioma predefinido Olá Olá **administração de servidor** início de sessão.
* Olá apenas os administradores (**administração de servidor** início de sessão ou o administrador do Azure AD) e os membros Olá Olá **dbmanager** função de base de dados no Olá **principal** tem de base de dados Olá tooexecute de permissão `CREATE DATABASE` e `DROP DATABASE` instruções.
* Tem de ser base de dados mestra toohello ligado ao executar Olá `CREATE/ALTER/DROP LOGIN` instruções. No entanto, não é aconselhável utilizar inícios de sessão. Utilize os utilizadores de base de dados contida.
* base de dados do utilizador do tooa de tooconnect, tem de fornecer o nome de Olá da base de dados de Olá na cadeia de ligação de Olá.
* Olá apenas ao nível do servidor principais início de sessão e Olá membros Olá **loginmanager** função de base de dados no Olá **mestre** base de dados ter Olá tooexecute de permissão `CREATE LOGIN`, `ALTER LOGIN`, e `DROP LOGIN` instruções.
* Ao executar Olá `CREATE/ALTER/DROP LOGIN` e `CREATE/ALTER/DROP DATABASE` declarações numa aplicação ADO.NET, utilizar os comandos parametrizados não é permitida. Para obter mais informações, consulte [Comandos e Parâmetros](https://msdn.microsoft.com/library/ms254953.aspx).
* Ao executar Olá `CREATE/ALTER/DROP DATABASE` e `CREATE/ALTER/DROP LOGIN` declarações, cada uma destas instruções tem de ser Olá apenas instrução num batch Transact-SQL. Caso contrário, ocorrerá um erro. Por exemplo, Olá que seguinte Transact-SQL verifica a existência de base de dados de Olá. Se existir, um `DROP DATABASE` instrução chama tooremove Olá da base de dados. Porque Olá `DROP DATABASE` instrução não é única instrução de Olá no lote de Olá, ao executar seguinte Olá instrução Transact-SQL resulta num erro.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Ao executar Olá `CREATE USER` instrução com Olá `FOR/FROM LOGIN` opção, tem de ser Olá apenas instrução num batch Transact-SQL.
* Ao executar Olá `ALTER USER` instrução com Olá `WITH LOGIN` opção, tem de ser Olá apenas instrução num batch Transact-SQL.
* demasiado`CREATE/ALTER/DROP` necessita de um utilizador Olá `ALTER ANY USER` permissão na base de dados de Olá.
* Quando tenta proprietário Olá de uma função de base de dados tooadd ou remova outro tooor de utilizador de base de dados da função de base de dados, pode ocorrer Olá seguinte erro: **utilizador ou função 'Name' não existe nesta base de dados.** Este erro ocorre porque o utilizador Olá não é proprietário de toohello visível. tooresolve este problema, conceda Olá função proprietário Olá `VIEW DEFINITION` permissão de utilizador de Olá. 


## <a name="next-steps"></a>Passos seguintes

- toolearn mais informações sobre regras de firewall, consulte [Firewall de base de dados SQL do Azure](sql-database-firewall-configure.md).
- Para obter uma descrição geral de todas as funcionalidades de segurança de base de dados SQL Olá, consulte [descrição geral de segurança do SQL Server](sql-database-security-overview.md).
- Para um tutorial, consulte [proteger a base de dados do SQL do Azure](sql-database-security-tutorial.md).
- Para obter informações sobre vistas e procedimentos armazenados, veja [Creating views and stored procedures (Criar vistas e procedimentos armazenados)](https://msdn.microsoft.com/library/ms365311.aspx)
- Para obter informações sobre o objeto de base de dados de tooa de acesso de concessão de permissões, consulte [conceder acesso tooa objeto de base de dados](https://msdn.microsoft.com/library/ms365327.aspx)
