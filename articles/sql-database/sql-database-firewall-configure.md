---
title: regras de firewall de base de dados SQL aaaAzure | Microsoft Docs
description: "Saiba como tooconfigure SQL da base de dados firewall com acesso de toomanage de regras de firewall ao nível do servidor e o nível de base de dados."
keywords: firewall de base de dados
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Regras de firewall ao nível do servidor e o nível de base de dados de base de dados SQL do Azure 

A Base de Dados SQL do Microsoft Azure disponibiliza um serviço de bases de dados relacionais para o Azure e outras aplicações baseadas na Internet. toohelp proteger os seus dados, as firewalls para impedir que todos os acesso tooyour da base de dados servidor até especificar quais os computadores que tem permissão. firewall de Olá concede toodatabases de acesso com base no Olá provenientes de endereços IP de cada pedido.

## <a name="overview"></a>Descrição geral

Inicialmente, todos os Transact-SQL acesso tooyour Azure SQL server está bloqueada pela firewall Olá. toobegin através do Azure SQL server, tem de especificar uma ou mais regras de firewall ao nível do servidor que permitem acesso tooyour servidor SQL Azure. Utilize as regras de firewall do Olá toospecify qual o endereço IP, intervalos de Olá Internet são permitidos e aplicações do Azure se tentar tooconnect tooyour servidor SQL Azure.

tooselectively conceder acesso toojust uma Olá bases de dados no seu servidor SQL do Azure, tem de criar uma regra de nível de base de dados para a base de dados necessária Olá. Especifique um intervalo de endereços IP para a regra de firewall de base de dados de Olá ultrapassa Olá intervalo especificado na regra de firewall ao nível do servidor de Olá de endereço IP e certifique-se de que o endereço IP de hello do cliente de Olá estiver no intervalo de Olá especificado na regra de nível de base de dados de Olá.

Olá, as tentativas de ligação de Internet e o Azure tem primeiro de passar através da firewall Olá antes de pode atingirem o servidor SQL do Azure ou a base de dados do SQL Server, conforme mostrado no Olá diagrama a seguir:

   ![Diagrama com descrição da configuração da firewall.][1]

* **Regras de firewall ao nível do servidor:** estas regras ativar clientes tooaccess o servidor de SQL do Azure completo, ou seja, todas as bases de dados de Olá dentro Olá mesmo servidor lógico. Estas regras são armazenadas no Olá **mestre** base de dados. Regras de firewall ao nível do servidor podem ser configuradas através do portal Olá ou através de instruções Transact-SQL. regras de firewall ao nível do servidor de toocreate utilizando Olá portal do Azure ou o PowerShell, tem de ser proprietário da subscrição Olá ou um contribuinte da subscrição. toocreate uma regra de firewall ao nível do servidor com o Transact-SQL, tem de ligar toohello instância de base de dados do SQL Server como início de sessão principal Olá ao nível do servidor ou o administrador do Azure Active Directory Olá (o que significa que uma regra de firewall ao nível do servidor tem primeiro de ser criada por um utilizador com permissões ao nível do Azure).
* **Regras de firewall de nível de base de dados:** estas regras ativar clientes tooaccess determinadas (seguro) bases de dados dentro de Olá mesmo servidor lógico. Pode criar estas regras para cada base de dados (incluindo Olá **mestre** database0) e são armazenados nas bases de dados individuais Olá. Regras de firewall ao nível da base de dados só podem ser configuradas através da utilização de instruções Transact-SQL e só depois de ter configurado Olá primeiro ao nível do servidor de firewall. Se especificar um intervalo de endereços IP na regra de firewall ao nível da base de dados de Olá que é o intervalo de Olá exteriores especificado na regra de firewall ao nível do servidor de Olá, apenas aos clientes com endereços IP no intervalo de nível de base de dados de Olá podem aceder a base de dados de Olá. Pode ter um máximo de 128 regras de firewall ao nível da base de dados para uma base de dados. Regras de firewall ao nível da base de dados para bases de dados mestra e utilizador só podem ser criadas e geridas através de Transact-SQL. Para obter mais informações sobre como configurar regras de firewall ao nível da base de dados, consulte o exemplo Olá posteriormente neste artigo e ver [sp_set_database_firewall_rule (bases de dados do Azure SQL)](https://msdn.microsoft.com/library/dn270010.aspx).

**Recomendação:** Microsoft recomenda a utilização de regras de firewall ao nível da base de dados sempre que possível tooenhance segurança e toomake a base de dados mais portátil. Utilize as regras de firewall ao nível do servidor para os administradores e quando tem muitas bases de dados que tenham Olá mesmos requisitos de acesso e não pretender que tempo toospend configurar individualmente cada base de dados.

> [!Note]
> Para informações sobre bases de dados portátil no contexto de Olá de continuidade do negócio, consulte [requisitos de autenticação para recuperação após desastre](sql-database-geo-replication-security-config.md).
>

### <a name="connecting-from-hello-internet"></a>Ligar a partir de Olá Internet

Quando um computador tenta tooconnect tooyour servidor de base de dados de Olá Internet, firewall Olá verifica primeiro Olá provenientes de endereço IP do pedido de Olá contra regras de firewall ao nível da base de dados de Olá, da base de dados de Olá que está a solicitar a ligação de Olá:

* Se o endereço IP Olá de pedido de Olá estiver dentro dos intervalos de Olá especificados nas regras de firewall ao nível da base de dados de Olá, Olá ligação é concedida pelo toohello base de dados do SQL Server que contém a regra de Olá.
* Se o endereço IP Olá de pedido de Olá não está dentro dos intervalos de Olá especificados na regra de firewall ao nível da base de dados de Olá, regras de firewall ao nível do servidor de Olá são verificadas. Se o endereço IP Olá de pedido de Olá estiver dentro dos intervalos de Olá especificados nas regras de firewall ao nível do servidor de Olá, ligação Olá é concedida. Regras de firewall ao nível do servidor aplicam-se tooall bases de dados do SQL no servidor de SQL do Azure Olá.  
* Se o endereço IP Olá de pedido de Olá não está dentro do intervalos Olá especificado em nenhum dos Olá ao nível da base de dados ou regras de firewall ao nível do servidor, Olá pedido de ligação falha.

> [!NOTE]
> tooaccess SQL Database do Azure do seu computador local, certifique-se de firewall de Olá na sua rede e o computador local permite a comunicação de saída na porta TCP 1433.
> 

### <a name="connecting-from-azure"></a>Ligar a partir do Azure
tem de estar ativadas tooallow aplicações do Azure tooconnect tooyour servidor SQL do Azure, as ligações do Azure. Quando o servidor de base de dados de tooyour tooconnect de tentativas de uma aplicação do Azure, a firewall Olá verifica que são permitidas ligações do Azure. Uma definição com inicial e final too0.0.0.0 igual do endereço de firewall indica que estas ligações são permitidas. Se não for permitida a tentativa de ligação de Olá, pedido Olá não atingiu o servidor de base de dados do Azure SQL Olá.

> [!IMPORTANT]
> Esta opção configura Olá firewall tooallow todas as ligações a partir do Azure ligações incluindo de subscrições de Olá de outros clientes. Quando a seleção desta opção, certifique-se de que o início de sessão e permissões de utilizador limitam acesso tooonly que os utilizadores autorizados.
> 

## <a name="creating-and-managing-firewall-rules"></a>Criar e gerir regras de firewall
definição de firewall ao nível do servidor primeiro Olá pode ser criada utilizando Olá [portal do Azure](https://portal.azure.com/) ou através de programação utilizando [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [CLI do Azure](/cli/azure/sql/server/firewall-rule#create), ou Olá [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx). As regras seguintes podem ser criadas e geridas com estes métodos e com o Transact-SQL. 

> [!IMPORTANT]
> Regras de firewall ao nível da base de dados só podem ser criadas e geridos através de Transact-SQL. 
>

desempenho de tooimprove, firewall ao nível do servidor regras temporariamente são colocadas em cache ao nível da base de dados de Olá. cache de Olá toorefresh, consulte [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx). 

> [!TIP]
> Pode utilizar [auditoria de base de dados SQL](sql-database-auditing.md) tooaudit alterações de firewall ao nível do servidor e o nível de base de dados.
>

### <a name="azure-portal"></a>Portal do Azure

tooset uma regra de firewall ao nível do servidor no portal do Azure de Olá, pode optar por voltar toohello página de descrição geral para a sua página de descrição geral de base de dados ou Olá SQL do Azure para o servidor lógico de base de dados do Azure.

> [!TIP]
> Para um tutorial, consulte [criar uma base de dados utilizando Olá portal do Azure](sql-database-get-started-portal.md).
>

**Na página de descrição geral da base de dados**

1. tooset uma regra de firewall ao nível do servidor da página de descrição geral da base de dados de Olá, clique em **definir a firewall do servidor** na barra de ferramentas de Olá conforme mostrado no Olá seguinte imagem: Olá **definições de Firewall** página Olá SQL É aberto o servidor de base de dados.

      ![regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. Clique em **Adicionar IP do cliente** no Olá barra de ferramentas tooadd Olá endereço IP do Olá computador estiver a utilizar e, em seguida, clique em **guardar**. É criada uma regra de firewall ao nível do servidor para o seu endereço IP atual.

      ![configurar regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**Na página de descrição geral do servidor**

Olá página de descrição geral para a sua abre-se do servidor, que mostra Olá completamente qualificado nome do servidor (tais como **mynewserver20170403.database.windows.net**) e fornece opções para continuar a configuração.

1. tooset uma regra de ao nível do servidor a partir da página de descrição geral do servidor, clique em **Firewall** no menu da esquerda do Olá em definições, conforme mostrado na Olá seguinte imagem: 

     ![Descrição geral do servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Clique em **Adicionar IP do cliente** no Olá barra de ferramentas tooadd Olá endereço IP do Olá computador estiver a utilizar e, em seguida, clique em **guardar**. É criada uma regra de firewall ao nível do servidor para o seu endereço IP atual.

     ![configurar regra de firewall do servidor](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| Vista de Catálogo ou Procedimento Armazenado | Nível | Descrição |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |Servidor |Apresenta as regras de firewall ao nível do servidor atual Olá |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |Servidor |Cria ou atualiza as regras de firewall ao nível do servidor |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |Servidor |Remove as regras de firewall ao nível do servidor |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |Base de Dados |Apresenta as regras de firewall ao nível da base de dados atuais Olá |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |Base de Dados |Cria ou atualiza as regras de firewall ao nível da base de dados de Olá |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |Bases de Dados |Remove as regras de firewall ao nível da base de dados |


Olá exemplos seguintes reveja as regras existentes de Olá, ativar a um intervalo de endereços IP no servidor de Olá Contoso e elimina uma regra de firewall:
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
Em seguida, adicione uma regra de firewall.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

toodelete uma regra de firewall ao nível do servidor, executar o procedimento de sp_delete_firewall_rule armazenados Olá. Olá exemplo seguinte elimina regra Olá denominada ContosoFirewallRule:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | Nível | Descrição |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |Servidor |Devolve as regras de firewall ao nível do servidor atual Olá |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |Servidor |Cria uma regra de firewall ao nível do servidor nova |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |Servidor |Atualizações Olá propriedades de uma regra de firewall ao nível do servidor existente |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |Servidor |Remove as regras de firewall ao nível do servidor |


Olá seguinte o exemplo define uma regra de firewall ao nível do servidor com o PowerShell:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> Para exemplos do PowerShell no contexto de Olá de um início rápido, consulte [criar DB - PowerShell](sql-database-get-started-powershell.md) e [criar uma base de dados e configurar uma regra de firewall com o PowerShell](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>CLI do Azure
| Cmdlet | Nível | Descrição |
| --- | --- | --- |
| [firewall do servidor de sql de AZ criar](/cli/azure/sql/server/firewall-rule#create) | Cria um tooall de acesso de tooallow de regra de firewall bases de dados SQL no servidor de Olá do intervalo de endereços IP Olá introduzido.|
| [eliminação de firewall AZ sql server](/cli/azure/sql/server/firewall-rule#delete)| Elimina uma regra de firewall.|
| [lista de firewall AZ sql server](/cli/azure/sql/server/firewall-rule#list)| Apresenta uma lista de regras de firewall de Olá.|
| [Mostrar a regra de firewall AZ sql server](/cli/azure/sql/server/firewall-rule#show)| Mostra detalhes de Olá de uma regra de firewall.|
| [AX atualização de regra de firewall do sql server](/cli/azure/sql/server/firewall-rule#update)| Atualiza uma regra de firewall.

Olá seguinte o exemplo define uma regra de firewall ao nível do servidor utilizando Olá CLI do Azure: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> Para obter um exemplo da CLI do Azure no contexto de Olá de um início rápido, consulte [criar DDB - CLI do Azure](sql-database-get-started-cli.md) e [criar uma base de dados e configurar uma regra de firewall utilizando Olá CLI do Azure](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>API REST
| API | Nível | Descrição |
| --- | --- | --- |
| [Listar Regras de Firewall](https://msdn.microsoft.com/library/azure/dn505715.aspx) |Servidor |Apresenta as regras de firewall ao nível do servidor atual Olá |
| [Criar Regra de Firewall](https://msdn.microsoft.com/library/azure/dn505712.aspx) |Servidor |Cria ou atualiza as regras de firewall ao nível do servidor |
| [Definir Regra de Firewall](https://msdn.microsoft.com/library/azure/dn505707.aspx) |Servidor |Atualizações Olá propriedades de uma regra de firewall ao nível do servidor existente |
| [Eliminar Regra de Firewall](https://msdn.microsoft.com/library/azure/dn505706.aspx) |Servidor |Remove as regras de firewall ao nível do servidor |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>Regra de firewall ao nível do servidor em comparação com uma regra de firewall ao nível da base de dados
Q. Os utilizadores de uma base de dados devem ser completamente isolados de outra base de dados?   
  Se Sim, conceda acesso através de regras de firewall ao nível da base de dados. Isto evita utilizando regras de firewall ao nível do servidor, que permitem acesso através da firewall Olá tooall bases de dados, reduzindo a profundidade de Olá do seu defesas.   
 
Q. Os utilizadores do endereço IP Olá precisa de aceder tooall bases de dados?   
  Utilize a firewall ao nível do servidor das regras tooreduce Olá o número de vezes que tem de configurar as regras de firewall.   

Q. A pessoa Olá ou equipa configurar regras de firewall de Olá apenas tem acesso através de Olá portal do Azure, PowerShell ou Olá REST API?   
  Tem de utilizar as regras de firewall ao nível do servidor. Regras de firewall ao nível da base de dados só podem ser configuradas com o Transact-SQL.  

Q. É pessoa Olá ou equipa configurar regras de firewall de Olá proibida de ter permissão de alto nível ao nível da base de dados de Olá?   
  Utilize as regras de firewall ao nível do servidor. Configurar regras de firewall ao nível da base de dados com o Transact-SQL, necessita de, pelo menos, `CONTROL DATABASE` permissão ao nível da base de dados de Olá.  

Q. É pessoa Olá ou equipa configurar ou auditoria de regras de firewall de Olá, gerir centralmente as regras de firewall para muitos (talvez 100) das bases de dados?   
  Esta seleção depende da sua necessidades e ambiente. Regras de firewall ao nível do servidor podem ser mais fácil tooconfigure, mas scripting pode configurar regras no Olá ao nível da base de dados. E, mesmo se utilizar regras de firewall ao nível do servidor, poderá ter de regras de firewall de base de dados de Olá tooaudit, toosee se os utilizadores com `CONTROL` permissão na base de dados de Olá criou regras de firewall ao nível da base de dados.   

Q. Pode utilizar uma combinação de ambas as regras de firewall ao nível do servidor e o nível de base de dados?   
  Sim. Alguns utilizadores, tal como os administradores poderão ter regras de firewall ao nível do servidor. Outros utilizadores, tais como utilizadores de uma aplicação de base de dados, poderão ter regras de firewall ao nível da base de dados.   

## <a name="troubleshooting-hello-database-firewall"></a>Resolução de problemas de firewall de base de dados de Olá
Considere Olá seguintes pontos ao acesso toohello serviço base de dados do Microsoft Azure SQL não se comporte como esperado:

* **Configuração da local firewall:** antes do computador pode aceder a SQL Database do Azure, poderá ser necessário toocreate uma exceção de firewall no seu computador para a porta TCP 1433. Se estiver a efetuar ligações dentro de limites de nuvem do Azure Olá, poderá ter tooopen de portas adicionais. Para obter mais informações, consulte Olá **base de dados SQL: fora vs dentro** secção [portas para além de 1433 para ADO.NET 4.5 e a SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).
* **Tradução de endereços (NAT) de rede:** atraso tooNAT, endereço IP de Olá utilizado pelo seu tooAzure tooconnect de computador base de dados SQL pode ser diferente do endereço IP Olá apresentado nas definições de configuração de IP do computador. endereço IP tooview Olá o computador está a utilizar tooconnect tooAzure, inicie sessão no portal de toohello e navegue toohello **configurar** separador no servidor de Olá que aloja a base de dados. Em Olá **endereços de IP permitido** secção, hello **endereço de IP de cliente atual** é apresentado. Clique em **adicionar** toohello **endereços de IP permitido** tooallow este servidor de Olá de tooaccess do computador.
* **Lista de permissões de alterações toohello não tenham sido ainda aplicadas:** poderão existir como sucederia com um atraso de cinco minutos para o efeito de tootake do toohello SQL Database do Azure firewall configuração é alterado.
* **início de sessão Olá não está autorizado ou foi utilizada uma palavra-passe incorreta:** se um início de sessão não tem permissões no servidor de base de dados do Azure SQL Olá ou palavra-passe de Olá utilizada está incorreta, o servidor de base de dados do Azure SQL Olá ligação toohello é negado. Apenas criando uma definição de firewall fornece aos clientes com um tooattempt oportunidade ligar tooyour servidor; cada cliente tem de fornecer credenciais de segurança necessários Olá. Para obter mais informações sobre a preparação dos inícios de sessão, veja Managing Databases, Logins, and Users in Azure SQL Database (Gerir Bases de Dados, Inícios de Sessão e Utilizadores na Base de Dados SQL do Azure).
* **Endereço IP dinâmico:** se tiver uma ligação à Internet com endereçamento de IP dinâmico e estiver a ter dificuldades em obter através da firewall Olá, foi experimente um dos Olá soluções a seguir:
  
  * Peça ao seu fornecedor de serviços de Internet (ISP) para o intervalo de endereços IP Olá atribuído computadores de cliente tooyour esse servidor do acesso Olá SQL Database do Azure e, em seguida, adicione o intervalo de endereços IP Olá como uma regra de firewall.
  * Obter estático endereçamento IP em vez disso, para os computadores cliente e, em seguida, adicionar endereços IP Olá como as regras de firewall.

## <a name="next-steps"></a>Passos seguintes

- Para uma introdução rápida sobre a criação de uma base de dados e uma regra de firewall ao nível do servidor, consulte [criar uma base de dados SQL do Azure](sql-database-get-started-portal.md).
- Para obter ajuda na ligação tooan SQL database do Azure de código aberto ou aplicações de terceiros, consulte [tooSQL da base de dados de exemplo de código de início rápido do cliente](https://msdn.microsoft.com/library/azure/ee336282.aspx).
- Para obter informações sobre portas adicionais que poderá ser necessário tooopen, consulte Olá **base de dados SQL: fora vs dentro** secção [portas para além de 1433 para ADO.NET 4.5 e a base de dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md)
- Para obter uma descrição geral de segurança da base de dados do Azure SQL, consulte [proteger a sua base de dados](sql-database-security-overview.md)

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
