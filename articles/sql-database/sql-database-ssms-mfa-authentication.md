---
title: "autenticação de fator aaaMulti - SQL do Azure | Microsoft Docs"
description: "Utilize a autenticação Factored de várias com o SSMS para a base de dados SQL e do armazém de dados do SQL Server."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Autenticação universal com a base de dados SQL e SQL Data Warehouse (SSMS suporte para a MFA)
SQL Database do Azure e o Azure SQL Data Warehouse suportam ligações da utilização do SQL Server Management Studio (SSMS) *autenticação de Universal do Active Directory*. 
**Transferir Olá SSMS mais recente** - no computador de cliente Olá, transfira a versão mais recente do Olá do SSMS, de [transferir SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Para todas as funcionalidades de Olá neste tópico, utilize, pelo menos, Julho de 2017, versão 17.2.  caixa de diálogo de ligação mais recente do Olá, se parece com isto: ![1mfa universal ligar](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "caixa de nome de utilizador de Olá Completes.")  

## <a name="hello-five-authentication-options"></a>Opções de autenticação de Olá cinco  
- Autenticação de Universal do Active Directory suporta dois métodos de autenticação não interativa Olá (`Active Directory - Password` autenticação e `Active Directory - Integrated` autenticação). Não interativo `Active Directory - Password` e `Active Directory - Integrated` métodos de autenticação podem ser utilizados em muitas aplicações diferentes (ADO.NET, JDBC, ODBC, etc.). Estes dois métodos nunca resultam nas caixas de diálogo de pop-up.

- `Active Directory - Universal with MFA`a autenticação é um método interativo que também suporta *Azure multi-factor Authentication* (MFA). MFA do Azure ajuda a salvaguardar acesso toodata e aplicações cumprindo o pedido do utilizador para um processo de início de sessão simple. Fornece autenticação forte com uma gama de opções de verificação fácil (chamada telefónica, mensagem de texto, os smart cards com pin ou a notificação da aplicação móvel) método de Olá toochoose permitir que os utilizadores que preferem. Interativo MFA com o Azure AD pode resultar numa caixa de diálogo de pop-up para validação.

Para obter uma descrição do multi-factor Authentication, consulte [multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).
Para obter passos de configuração, consulte [configurar a base de dados de SQL do Azure multi-factor authentication para SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Azure AD domínio nome ou o inquilino parâmetro ID   

Começando com [SSMS versão 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), os utilizadores que são importados para Olá atual do Active Directory de outros diretórios de Active Directory do Azure como os utilizadores convidados, pode fornecer o nome de domínio Olá do Azure AD ou ID de inquilino quando se ligam. Os utilizadores convidados incluem utilizadores convidados a partir de outros anúncios do Azure, as contas Microsoft, tais como outlook.com, hotmail.com, live.com ou outras contas como gmail.com. Estas informações, permite **Active Directory universais com autenticação de MFA** tooidentify Olá autenticar autoridade correta. Esta opção também é necessário toosupport contas da Microsoft (MSA), tais como o outlook.com, hotmail.com, live.com ou contas não MSA. Estes utilizadores que pretendem toobe autenticado utilizando a autenticação Universal deve introduzir o respetivo nome de domínio do Azure AD ou o inquilino ID. Este parâmetro representa Olá ID Olá atual do Azure AD domínio nome/inquilino do Azure servidor está ligado com. Por exemplo, se o servidor do Azure está associado ao domínio do Azure AD `contosotest.onmicrosoft.com` onde utilizador `joe@contosodev.onmicrosoft.com` está alojado como um utilizador de domínio do Azure AD importado `contosodev.onmicrosoft.com`, Olá tooauthenticate necessário o nome de domínio este utilizador é `contosotest.onmicrosoft.com`. Quando o utilizador Olá é um utilizador nativo do Olá do Azure AD ligado tooAzure servidor e não é uma conta MSA, nenhum ID de nome ou o inquilino do domínio é necessário. tooenter Olá parâmetro (início com o SSMS versão 17.2), Olá **ligar tooDatabase** caixa de diálogo, a caixa de diálogo Olá concluída, selecionar **do Active Directory - Universal com a MFA** autenticação, Clique em **opções**, Olá concluída **nome de utilizador** caixa e, em seguida, clique em Olá **propriedades de ligação** separador. Verifique Olá **ID de nome ou o inquilino de domínio do AD** caixa e fornecer a autoridade de autenticação, tais como o nome de domínio Olá (**contosotest.onmicrosoft.com**) ou Olá GUID do ID do inquilino Olá.  
   ![ssms de inquilino de mfa](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Suporta toobusiness de negócio do Azure AD   
Suportado para cenários B2B do Azure AD, como os utilizadores convidados os utilizadores do AD do Azure (consulte [o que é a colaboração B2B do Azure](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) pode ligar-se tooSQL da base de dados e do armazém de dados do SQL Server apenas como parte de membros de um grupo criado no Azure AD atual e mapeado manualmente utilizar Olá Transact-SQL `CREATE USER` declaração numa base de dados fornecido. Por exemplo, se `steve@gmail.com` é tooAzure convidado AD `contosotest` (com o domínio do Azure Ad de Olá `contosotest.onmicrosoft.com`), grupo de um Azure AD, tal como `usergroup` tem de ser criada no Olá do Azure AD que contém Olá `steve@gmail.com` membro. Em seguida, este grupo tem de ser criado numa base de dados específicos (ou seja, MyDatabase) pelo administrador de SQL do Azure AD ou Azure AD DBO executando Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` instrução. Após a criação de utilizador de base de dados de Olá, em seguida, Olá utilizador `steve@gmail.com` pode iniciar sessão demasiado`MyDatabase` utilizando a opção de autenticação do SSMS Olá `Active Directory – Universal with MFA support`. Olá grupo, por predefinição, tem apenas Olá ligar permissão e qualquer acesso a dados adicional que terá de toobe concedida na Olá forma normal. Tenha em atenção que o utilizador `steve@gmail.com` como um utilizador convidado tem Olá caixa de verificação e adicione o nome de domínio Olá AD `contosotest.onmicrosoft.com` no Olá SSMS **ligação propriedade** caixa de diálogo. Olá **ID de nome ou o inquilino de domínio do AD** opção só é suportada para Olá Universal com opções de ligação de MFA, caso contrário, se estiver a cinzento.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Limitações de autenticação universais para a base de dados SQL e do armazém de dados do SQL Server
* SSMS e SqlPackage.exe são Olá apenas as ferramentas atualmente ativadas para a MFA através da autenticação de Universal do Active Directory.
* SSMS versão 17.2, suporta acesso de vários utilizadores em simultâneo através da autenticação Universal com a MFA. Versão 17.0 e 17.1, restringido a um início de sessão para uma instância do SSMS utilizando a conta do Azure Active Directory único tooa autenticação Universal. toolog na como outra conta do Azure AD, tem de utilizar outra instância do SSMS. (Esta restrição é limitado tooActive autenticação Universal diretório; pode iniciar sessão nos servidores de toodifferent utilizando a autenticação de palavra-passe do Active Directory, a autenticação integrada do Active Directory ou autenticação do SQL Server).
* SSMS suporta a autenticação de Universal do Active Directory para visualização Object Explorer, o Editor de consultas e o arquivo de consultas.
* SSMS versão 17.2 fornece suporte de assistente DacFx da base de dados de dados de exportação/extrair/implementar. Depois de um utilizador específico é autenticado através de diálogo de autenticação inicial Olá através da autenticação Universal, hello funções DacFx assistente Olá mesma forma que realiza todos os outros métodos de autenticação.
* Olá SSMS Designer de tabela não suporta a autenticação Universal.
* Não existem não requisitos de software adicionais para autenticação de Universal do Active Directory, exceto que tem de utilizar uma versão suportada do SSMS.  
* versão do Active Directory Authentication Library (ADAL) Olá para autenticação Universal foi versão lançada ADAL.dll 3.13.9 disponível mais recente do tooits atualizado. Consulte [biblioteca de autenticação do Active Directory 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Passos seguintes

- Para obter passos de configuração, consulte [configurar a base de dados de SQL do Azure multi-factor authentication para SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Conceder a outros utilizadores aceder à base de dados tooyour: [autorização e autenticação de base de dados do SQL Server: conceder acesso](sql-database-manage-logins.md)  
- Certifique-se a outros utilizadores podem ligar através de firewall de Olá: [através da regra de firewall de configurar um SQL Database do Azure ao nível do servidor Olá portal do Azure](sql-database-configure-firewall-settings.md)  
- [Configurar e gerir a autenticação do Azure Active Directory com a base de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importar um tooa de ficheiro BACPAC nova SQL Database do Azure](../sql-database/sql-database-import.md)  
- [Exportar um ficheiro de BACPAC de tooa de base de dados SQL do Azure](../sql-database/sql-database-export.md)  
- Interface de c# [IUniversalAuthProvider Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
