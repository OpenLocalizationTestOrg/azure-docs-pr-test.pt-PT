---
title: "autenticação do Active Directory de aaaAzure - SQL do Azure (descrição geral) | Microsoft Docs"
description: "Saiba mais sobre como toouse do Azure Active Directory para a autenticação com base de dados SQL e do armazém de dados do SQL Server"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Utilizar a autenticação do Active Directory do Azure para a autenticação com base de dados SQL ou SQL Data Warehouse
A autenticação do Active Directory do Azure é um mecanismo de ligar tooMicrosoft SQL Database do Azure e [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) utilizando as identidades no Azure Active Directory (Azure AD). Com a autenticação do Azure AD, pode gerir centralmente identidades Olá de utilizadores de base de dados e outros serviços Microsoft numa localização central. Gestão de ID central fornece um único local toomanage utilizadores de base de dados e simplifica a gestão de permissão. Benefícios incluem o seguinte Olá:

* Fornece uma autenticação de servidor tooSQL alternativo.
* Ajuda a parar a proliferação de Olá das identidades de utilizador em servidores de base de dados.
* Permite a rotação de palavra-passe num único local
* Os clientes podem gerir as permissões de base de dados através de grupos do externos (AAD).
* -Pode eliminar armazenar palavras-passe através da autenticação integrada do Windows e outras formas de autenticação suportados pelo Azure Active Directory.
* Autenticação do Azure AD utiliza as identidades de tooauthenticate de utilizadores de base de dados contida ao nível da base de dados de Olá.
* AD do Azure suporta a autenticação baseada em tokens para ligar tooSQL da base de dados de aplicações.
* Autenticação do AD do Azure suporta ADFS (Federação de domínio) ou autenticação de utilizador/palavra-passe nativo para um Azure Active Directory local sem sincronização de domínio.  
* Azure AD suporta ligações de SQL Server Management Studio que utilizam a autenticação do Active Directory Universal, que inclui o multi-factor Authentication (MFA).  MFA inclui autenticação forte com uma gama de opções de verificação fácil — chamada telefónica, mensagem de texto, os smart cards com pin ou a notificação da aplicação móvel. Para obter mais informações, consulte [SSMS suporte para o MFA do Azure AD com base de dados SQL e SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Ligar tooSQL servidor em execução numa VM do Azure não é suportado com uma conta do Azure Active Directory. Em alternativa, utilize um domínio de conta do Active Directory.  

passos de configuração de Olá incluem Olá tooconfigure procedimentos a seguir e utilizam a autenticação do Azure Active Directory.

1. Criar e preencher do Azure AD.
2. Opcional: Associar ou alterar Olá active directory está atualmente associado a sua subscrição do Azure.
3. Criar um administrador do Azure Active Directory para o Azure SQL server ou [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Configure os computadores cliente.
5. Crie utilizadores de base de dados contida na sua base de dados mapeado tooAzure identidades do AD.
6. Liga a base de dados de tooyour utilizando identidades do Azure AD.

> [!NOTE]
> toolearn como toocreate e preencher do Azure AD e, em seguida, configurar o Azure AD com o SQL Database do Azure e o SQL Data Warehouse, consulte [configurar do Azure AD com base de dados do Azure SQL](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Arquitetura de confiança
Olá alto nível diagrama a seguir resume a arquitetura de solução Olá de utilização da autenticação do Azure AD com a SQL Database do Azure. Olá mesmos conceitos se aplicam tooSQL do armazém de dados. é considerado toosupport do Azure AD utilizador nativo palavra-passe, apenas a parte da nuvem Olá e a base de dados do Azure AD/Azure SQL. toosupport Federated autenticação (ou utilizador/palavra-passe para as credenciais do Windows), não é necessária a comunicação Olá com bloqueio de ADFS. setas de Olá indicam caminhos de comunicação.

![Diagrama de autenticação do aad][1]

Olá diagrama a seguir indica Federação Olá, fidedignidade e alojar as relações que permitem que um cliente de base de dados do tooconnect tooa submetendo um token. token de Olá é autenticado por um Azure AD e é considerada fidedigna pela base de dados de Olá. Cliente 1 pode representar um Azure Active Directory com utilizadores nativos ou um Azure AD com utilizadores federados. Cliente 2 representa uma solução possíveis, incluindo os utilizadores importados. Neste exemplo provém de um federado do Azure Active Directory com AD FS que está a ser sincronizados com o Azure Active Directory. É importante toounderstand aceder tooa base de dados utilizando a autenticação do Azure AD requer que Olá alojamento subscrição é toohello associado do Azure AD. Olá mesma subscrição tem de ser Olá alojamento do toocreate utilizados Olá do SQL Server SQL Database do Azure ou SQL Data Warehouse.

![relação de subscrição][2]

## <a name="administrator-structure"></a>Estrutura de administrador
Quando utilizar a autenticação do Azure AD, existem duas contas de administrador para o servidor de base de dados SQL Olá; Olá original administrador do SQL Server e o administrador de Olá do Azure AD. Olá mesmos conceitos se aplicam tooSQL do armazém de dados. Apenas o administrador Olá com base numa conta do Azure AD pode criar o utilizador de base de dados do Olá primeiro Azure AD contido na base de dados do utilizador. o início de sessão do Olá do Azure AD administrador pode ser um utilizador do Azure AD ou um grupo do Azure AD. Quando o administrador de Olá for uma conta de grupo, pode ser utilizada por qualquer membro do grupo, permitindo que os administradores do Azure AD vários para a instância do SQL Server de Olá. Toocentrally utilizando a conta de grupo como um administrador melhora a capacidade de gestão, permitindo-lhe adicionar e remover membros do grupo no Azure AD sem alterar os utilizadores de Olá ou permissões na base de dados do SQL Server. Apenas um administrador do Azure AD (um utilizador ou grupo) pode ser configurado em qualquer altura.

![estrutura de Admin][3]

## <a name="permissions"></a>Permissões
os novos utilizadores toocreate, tem de ter Olá `ALTER ANY USER` permissão na base de dados de Olá. Olá `ALTER ANY USER` permissão pode ser concedida tooany utilizador de base de dados. Olá `ALTER ANY USER` permissão também está a ser retida pelas contas de administrador do servidor Olá e os utilizadores de base de dados com Olá `CONTROL ON DATABASE` ou `ALTER ON DATABASE` permissões para essa base de dados e por membros da Olá `db_owner` função de base de dados.

toocreate um utilizador de base de dados contida na SQL Database do Azure ou do armazém de dados do SQL Server, tem de ligar toohello base de dados com uma identidade do Azure AD. toocreate Olá primeira base de dados contida utilizador, tem de ligar toohello base de dados através da utilização de um administrador do Azure AD (que é proprietário de Olá da base de dados de Olá). Isto é demonstrado nos passos 4 e 5 abaixo. Qualquer autenticação do Azure AD só é possível se Olá, admin do Azure AD foi criada para o servidor da SQL Database do Azure ou SQL Data Warehouse. Se Olá, admin do Azure Active Directory foi removido do servidor de Olá, os utilizadores do Azure Active Directory existentes criados anteriormente no interior do SQL Server já não podem ligar toohello base de dados utilizando as credenciais do Azure Active Directory.

## <a name="azure-ad-features-and-limitations"></a>Funcionalidades do Azure AD e limitações
Olá seguintes membros do Azure AD pode ser aprovisionado no servidor SQL do Azure ou do armazém de dados do SQL Server:

* Membros nativos: membro criado no Azure AD no domínio gerido Olá ou num domínio cliente. Para obter mais informações, consulte [adicionar o seus próprios tooAzure de nome de domínio AD](../active-directory/active-directory-add-domain.md).
* Federado membros do domínio: membro criado no Azure AD com um domínio federado. Para obter mais informações, consulte [Microsoft Azure suporta agora a Federação com o Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Importados os membros de outro do Azure AD que são membros de domínio nativo ou federada.
* Grupos do Active Directory criados como grupos de segurança.

Contas Microsoft (por exemplo, outlook.com, hotmail.com, live.com) ou outras contas de convidado (por exemplo gmail.com, yahoo.com) não são suportadas. Se lhe pode iniciar sessão no demasiado[https://login.live.com](https://login.live.com) utilizando a conta de Olá e a palavra-passe, e estiver a utilizar uma conta Microsoft, que não é suportado para a autenticação do Azure AD para a SQL Database do Azure ou do Azure SQL Data Warehouse.

## <a name="connecting-using-azure-ad-identities"></a>Ligar utilizando as identidades do Azure AD

A autenticação do Active Directory do Azure suporta Olá seguintes métodos de ligação tooa da base de dados utilizando as identidades do Azure AD:

* Utilizando a autenticação integrada do Windows
* Utilizar um nome principal do Azure AD e uma palavra-passe
* Utilizar a autenticação de token de aplicação

### <a name="additional-considerations"></a>Considerações adicionais

* capacidade de gestão tooenhance, recomendamos aprovisionar um dedicado do Azure AD grupo como um administrador.   
* Apenas um administrador do Azure AD (um utilizador ou grupo) pode ser configurado para um servidor SQL do Azure ou o Azure SQL Data Warehouse em qualquer altura.   
* Apenas um administrador do Azure AD para o SQL Server inicialmente pode ligar toohello servidor SQL Azure ou do Azure SQL Data Warehouse, utilizando uma conta do Azure Active Directory. administrador do Active Directory Olá pode configurar subsequente do Azure AD os utilizadores de base de dados.   
* Recomendamos que a definição Olá ligação tempo limite too30 em segundos.   
* SQL Server 2016 Management Studio e SQL Server Data Tools para Visual Studio 2015 (versão 14.0.60311.1April 2016 ou posterior) suportam a autenticação do Azure Active Directory. (Autenticação do azure AD é suportada pelo Olá **.NET Framework Data Provider para SqlServer**; pelo menos, versão do .NET Framework 4.6). Olá, por conseguinte, as versões mais recentes destas ferramentas e aplicações de camada de dados (DAC e bacpac) podem utilizar a autenticação do Azure AD.   
* [ODBC versão 13.1](https://www.microsoft.com/download/details.aspx?id=53339) suporta a autenticação do Azure Active Directory no entanto `bcp.exe` não é possível ligar através da autenticação do Azure Active Directory porque utiliza um fornecedor ODBC mais antigo.   
* `sqlcmd`suporta o início de autenticação do Azure Active Directory com a versão disponível a partir do Olá 13.1 [Centro de transferências](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools para Visual Studio 2015 requer, pelo menos, versão de Abril de 2016 Olá do Olá Data Tools (versão 14.0.60311.1). Atualmente, os utilizadores do Azure AD não são apresentados no SSDT Object Explorer. Como solução, ver os utilizadores Olá [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [Microsoft JDBC controlador 6.0 para o SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) autenticação de suporte do Azure AD. Além disso, consulte [definir propriedades de ligação de Olá](https://msdn.microsoft.com/library/ms378988.aspx).   
* O PolyBase não pode autenticar utilizando a autenticação do Azure AD.   
* Autenticação do Azure AD é suportada para a base de dados SQL por Olá portal do Azure **importar base de dados** e **exportar a base de dados** painéis. Importação e exportação utilizando a autenticação do Azure AD também é suportada a partir Olá comando do PowerShell.   
* Autenticação do Azure AD é suportada para a base de dados SQL e do armazém de dados do SQL Server através da utilização CLI. Para obter mais informações, consulte [configurar e gerir a autenticação do Azure Active Directory com a base de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md) e [do SQL Server - servidor de sql az](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Passos seguintes
- toolearn como toocreate e preencher do Azure AD e, em seguida, configurar o Azure AD com o SQL Database do Azure ou o Azure SQL Data Warehouse, consulte [configurar e gerir a autenticação do Azure Active Directory com a base de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md).
- Para obter uma descrição geral do acesso e controlo na Base de Dados SQL, veja [Acesso e controlo da Base de Dados SQL](sql-database-control-access.md).
- Para obter uma descrição geral de inícios de sessão, utilizadores e funções de base de dados da Base de Dados SQL, veja [Inícios de sessão, utilizadores e funções de base de dados](sql-database-manage-logins.md).
- Para obter mais informações sobre os principais de bases de dados, veja [Principals (Principais)](https://msdn.microsoft.com/library/ms181127.aspx).
- Para obter mais informações sobre as funções de base de dados, veja [Database roles (Funções de base de dados)](https://msdn.microsoft.com/library/ms189121.aspx).
- Para obter mais informações sobre as regras de firewall na Base de Dados SQL, veja [Regras de firewall da Base de Dados SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

