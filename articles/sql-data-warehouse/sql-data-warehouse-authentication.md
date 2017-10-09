---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: Azure Active Directory (AAD) e o SQL Server authentication tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Autenticação tooAzure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Descrição geral de segurança](sql-data-warehouse-overview-manage-security.md)
> * [Autenticação](sql-data-warehouse-authentication.md)
> * [Encriptação (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Encriptação (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL do armazém de dados, tem de transmitir as credenciais de segurança para efeitos de autenticação. Depois de estabelecer uma ligação, determinadas definições de ligação estão configuradas como parte de estabelecer a sessão de consulta.  

Para mais informações sobre segurança e como tooenable ligações tooyour do armazém de dados, consulte [proteger uma base de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Autenticação do SQL
tooconnect tooSQL do armazém de dados, tem de fornecer Olá seguintes informações:

* Servername completamente qualificado
* Especifique a autenticação do SQL Server
* Nome de utilizador
* Palavra-passe
* Base de dados predefinida (opcional)

Por predefinição, a ligação liga toohello *mestre* base de dados e não a base de dados do utilizador. base de dados do utilizador do tooyour de tooconnect, pode escolher toodo uma das duas coisas:

* Especificar Olá predefinido da base de dados ao registar o seu servidor com Olá SQL Server Object Explorer no SSDT, SSMS, ou na sua cadeia de ligação da aplicação. Por exemplo, a incluir o parâmetro de InitialCatalog Olá para uma ligação de ODBC.
* Realce Olá utilizador da base de dados antes de criar uma sessão no SSDT.

> [!NOTE]
> instrução Transact-SQL de Olá **utilize MyDatabase;** não é suportada para alterar a base de dados de Olá para uma ligação. Para obter orientações sobre a ligação tooSQL do armazém de dados com SSDT, consulte toohello [consulta com o Visual Studio] [ Query with Visual Studio] artigo.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Autenticação do Azure Active Directory (AAD)
[Azure Active Directory] [ What is Azure Active Directory] a autenticação é um mecanismo de ligar tooMicrosoft Azure SQL Data Warehouse, utilizando as identidades no Azure Active Directory (Azure AD). Com a autenticação do Azure Active Directory, pode gerir centralmente identidades Olá de utilizadores de base de dados e outros serviços Microsoft numa localização central. Gestão de ID central fornece um único local toomanage utilizadores de armazém de dados do SQL Server e simplifica a gestão de permissão. 

### <a name="benefits"></a>Benefícios
Vantagens do Azure Active Directory incluem:

* Fornece uma autenticação de servidor tooSQL alternativo.
* Ajuda a parar a proliferação de Olá das identidades de utilizador em servidores de base de dados.
* Permite a rotação de palavra-passe num único local
* Gerir permissões de base de dados através de grupos do externos (AAD).
* Elimina armazenar palavras-passe através da autenticação integrada do Windows e outras formas de autenticação suportados pelo Azure Active Directory.
* Utiliza continha identidades tooauthenticate de utilizadores de base de dados ao nível da base de dados de Olá.
* Suporta a autenticação baseada em tokens para ligar tooSQL do armazém de dados de aplicações.
* Suporta autenticação Multifator através da autenticação de Universal do Active Directory para SQL Server Management Studio. Para obter uma descrição do multi-factor Authentication, consulte [SSMS suporte para o MFA do Azure AD com base de dados SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory é ainda relativamente novo e tem algumas limitações. tooensure que o Azure Active Directory é uma boa opção para o seu ambiente, consulte [funcionalidades do Azure AD e limitações][Azure AD features and limitations], especificamente Olá considerações adicionais.
> 
> 

### <a name="configuration-steps"></a>Passos de configuração
Siga a autenticação do Azure Active Directory estes passos tooconfigure.

1. Criar e preencher um Azure Active Directory
2. Opcional: Associar ou alterar Olá active directory está atualmente associado a sua subscrição do Azure
3. Crie um administrador do Azure Active Directory para o Azure SQL Data Warehouse.
4. Configurar os computadores cliente
5. Criar utilizadores de base de dados contida na sua base de dados mapeado tooAzure identidades do AD
6. Ligar tooyour do armazém de dados através da utilização de identidades do Azure AD

Atualmente, os utilizadores do Azure Active Directory não são apresentados no SSDT Object Explorer. Como solução, ver os utilizadores Olá [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Encontrar os detalhes da Olá
* Olá passos tooconfigure e a utilização do Azure Active Directory authentication sejam praticamente idênticos para a SQL Database do Azure e Azure SQL Data Warehouse. Siga Olá detalhadas passos Olá tópico [tooSQL de ligação da base de dados ou SQL dados do armazém por utilizar o Azure autenticação do Active Directory](../sql-database/sql-database-aad-authentication.md).
* Criar funções de base de dados personalizada e adicionar utilizadores toohello funções. Em seguida, conceda permissões granulares toohello funções. Para obter mais informações, consulte [introdução de permissões do motor de base de dados](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Passos seguintes
toostart consultar o armazém de dados com o Visual Studio e outras aplicações, consulte [consulta com o Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
