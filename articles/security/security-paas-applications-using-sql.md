---
title: aaaSecuring PaaS bases de dados no Azure | Microsoft Docs
description: " Saiba mais sobre a segurança da SQL Database do Azure e o SQL Data Warehouse melhores práticas para proteger o seu web de PaaS e as aplicações móveis. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Proteger bases de dados PaaS no Azure

Neste artigo, discutimos a uma coleção de [SQL Database do Azure](https://azure.microsoft.com/services/sql-database/) e [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) melhores práticas de segurança para proteger o seu web de PaaS e as aplicações móveis. Estas melhores práticas são derivadas da nossa experiência com o Azure e experiências Olá dos clientes, como por si.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Base de dados SQL do Azure e do armazém de dados do SQL Server
[Base de dados SQL do Azure](../sql-database/sql-database-technical-overview.md) e [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) fornecer um serviço de base de dados relacional das suas aplicações baseado na Internet. Vamos ver serviços que ajudam a proteger as suas aplicações e dados ao utilizar a SQL Database do Azure e do armazém de dados do SQL Server numa implementação PaaS:

- Autenticação do Active Directory do Azure (em vez de autenticação do SQL Server)
- Firewall SQL do Azure
- Encriptação de dados transparente (TDE)

## <a name="best-practices"></a>Melhores práticas

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Utilizar um repositório de identidade centralizada para autenticação e autorização

Bases de dados SQL do Azure podem ser configurado toouse um dos dois tipos de autenticação:

- **Autenticação do SQL Server** utiliza um nome de utilizador e palavra-passe. Quando criou o servidor lógico de Olá da base de dados, que especificou um início de sessão do "administrador do servidor" com um nome de utilizador e palavra-passe. Estas credenciais podem autenticar tooany base de dados nesse servidor como proprietário da base de dados de Olá.

- **Azure autenticação do Active Directory** utiliza identidades geridas pelo Azure Active Directory e é suportada nos domínios geridos e integrados. toouse autenticação do Active Directory do Azure, tem de criar outro administrador de servidor chamado Olá "Do Azure AD admin," o que é permitido tooadminister do Azure AD utilizadores e grupos. Este administrador também pode fazer todas as operações que um administrador de servidor normal faz.

[Autenticação do Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md) é um mecanismo de ligar tooAzure base de dados SQL e SQL Data Warehouse, utilizando as identidades no Azure Active Directory (AD). O Azure AD fornece uma autenticação de servidor alternativo tooSQL, pelo que pode parar proliferação Olá das identidades de utilizador em servidores de base de dados. Azure AD authentication ativa toocentrally gerir identidades de Olá de utilizadores de base de dados e outros serviços Microsoft numa localização central. Gestão de ID central fornece um único local toomanage utilizadores de base de dados e simplifica a gestão de permissão.  

Vantagens da utilização da autenticação do Azure AD em vez de autenticação do SQL Server incluem:

- Permite a rotação de palavra-passe num único local.
- Gere as permissões de base de dados a utilizar o Azure externo grupos do Active Directory.
- Elimina armazenar palavras-passe através da autenticação integrada do Windows e outras formas de autenticação suportados pelo Azure AD.
- Utiliza continha identidades tooauthenticate de utilizadores de base de dados ao nível da base de dados de Olá.
- Suporta a autenticação baseada em tokens para ligar tooSQL da base de dados de aplicações.
- Suporta ADFS (Federação de domínio) ou autenticação de utilizador/palavra-passe nativo para um local do Azure AD sem sincronização de domínio.
- Suporta ligações a partir do SQL Server Management Studio que utilizam a autenticação do Active Directory Universal, que inclui [multi-factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md). MFA inclui autenticação forte com uma gama de opções de verificação fácil — chamada telefónica, mensagem de texto, os smart cards com pin ou a notificação da aplicação móvel. Para obter mais informações, consulte [SSMS suporte para o MFA do Azure AD com base de dados SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn mais informações sobre a autenticação do Azure AD, consulte:

- [Ligar tooSQL da base de dados ou SQL dados do armazém por utilizar o Azure autenticação do Active Directory](../sql-database/sql-database-aad-authentication.md)
- [Autenticação tooAzure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Suporte de autenticação baseada em tokens de BD SQL do Azure através da autenticação do Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> tooensure que o Azure Active Directory é uma boa opção para o seu ambiente, consulte [funcionalidades do Azure AD e limitações](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), especificamente Olá considerações adicionais.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Restringir o acesso com base no endereço IP
Pode criar regras de firewall que especifique os intervalos de endereços IP aceitáveis. Estas regras podem ser segmentadas no servidor de Olá e níveis de base de dados. Recomendamos que utilize regras de firewall ao nível da base de dados sempre que possível tooenhance segurança e toomake a base de dados mais portátil. Regras de firewall ao nível do servidor são melhor utilizadas para os administradores e quando tem muitas bases de dados que tenham Olá mesmos requisitos de acesso, mas não pretende tempo toospend configurar individualmente cada base de dados.

Restrições de endereço IP de origem predefinido da base de dados de SQL permitem o acesso a partir de qualquer endereço do Azure (incluindo outras subscrições e inquilinos). Pode restringir a este tooonly permitir que a instância de Olá de tooaccess de endereços IP. Mesmo com as restrições de endereço IP e firewall do SQL Server, a autenticação forte é ainda necessária. Ver as recomendações de Olá efetuadas anteriormente neste artigo.

toolearn mais informações sobre a Firewall do SQL do Azure e restrições de IP, consulte:

- [Controlo de acesso de base de dados SQL do Azure](../sql-database/sql-database-control-access.md)
- [Configurar regras de firewall da SQL Database do Azure - descrição geral](../sql-database/sql-database-firewall-configure.md)
- [Configurar uma regra de firewall ao nível do servidor da SQL Database do Azure utilizando Olá portal do Azure](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Encriptação de dados inativos
[Encriptação de dados transparente (TDE)](https://msdn.microsoft.com/library/azure/bb934049) está ativada por predefinição. TDE transparente encripta os ficheiros de registo e dados do SQL Server, SQL Database do Azure e Azure SQL Data Warehouse. TDE protege contra o comprometimento dos ficheiros de toohello acesso direto ou as respetivas cópias de segurança. Isto permite-lhe tooencrypt dados Inativos sem alterar as aplicações existentes. TDE sempre deve permanecer ativada; No entanto, isto não irá parar um atacante Olá normal de acesso caminho a utilizar. TDE fornece a capacidade de Olá toocomply com muitos leis, normas e diretrizes estabelecidas no indústrias vários.

SQL do Azure gere problemas relacionados com chave para TDE. Tal como com TDE, no local especial deve ter cuidado tooensure capacidade de recuperação e ao mover as bases de dados. Em cenários mais sofisticados, chaves de Olá explicitamente geridas no Cofre de chaves do Azure através de gestão de chaves extensível (consulte [TDE ativar no SQL Server utilizando EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Isto também permite para traga a sua própria chave (BYOK) através da capacidade de BYOK de cofres de chaves do Azure.

SQL do Azure fornece encriptação para colunas através de [sempre encriptados](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Isto permite o acesso apenas aplicações autorizadas toosensitive colunas. Utilizar este tipo de encriptação limita as consultas SQL para os valores com base em tooequality colunas encriptadas.

Encriptação de nível de aplicações também deve ser utilizada para dados seletivos. As questões de soberania dos dados, por vezes, podem ser mitigadas ao encriptar dados com uma chave que é mantida país correto Olá. Isto impede que a transferência de dados acidentais mesmo causar um problema, uma vez que é Olá toodecrypt impossível dados sem chave Olá, partindo do princípio de um algoritmo forte são utilizados (por exemplo, AES 256).

Pode utilizar as precauções adicionais toohelp Olá seguro da base de dados como conceber um sistema seguro, encriptação ativos confidenciais e criação de uma firewall em torno de servidores de base de dados de Olá.

## <a name="next-steps"></a>Passos seguintes
Este artigo introduzida tooa coleção da base de dados SQL e SQL Data Warehouse segurança melhores práticas para proteger o seu web de PaaS e as aplicações móveis. toolearn mais informações sobre a proteger as implementações PaaS, consulte:

- [Proteger implementações PaaS](security-paas-deployments.md)
- [Proteger o PaaS web e aplicações móveis com o serviços de aplicações do Azure](security-paas-applications-using-app-services.md)
