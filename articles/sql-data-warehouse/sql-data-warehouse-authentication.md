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
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="bc45f-103">Autenticação tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bc45f-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc45f-104">Descrição geral de segurança</span><span class="sxs-lookup"><span data-stu-id="bc45f-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="bc45f-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="bc45f-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="bc45f-106">Encriptação (Portal)</span><span class="sxs-lookup"><span data-stu-id="bc45f-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="bc45f-107">Encriptação (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="bc45f-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="bc45f-108">tooconnect tooSQL do armazém de dados, tem de transmitir as credenciais de segurança para efeitos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="bc45f-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="bc45f-109">Depois de estabelecer uma ligação, determinadas definições de ligação estão configuradas como parte de estabelecer a sessão de consulta.</span><span class="sxs-lookup"><span data-stu-id="bc45f-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="bc45f-110">Para mais informações sobre segurança e como tooenable ligações tooyour do armazém de dados, consulte [proteger uma base de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="bc45f-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="bc45f-111">Autenticação do SQL</span><span class="sxs-lookup"><span data-stu-id="bc45f-111">SQL authentication</span></span>
<span data-ttu-id="bc45f-112">tooconnect tooSQL do armazém de dados, tem de fornecer Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="bc45f-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="bc45f-113">Servername completamente qualificado</span><span class="sxs-lookup"><span data-stu-id="bc45f-113">Fully qualified servername</span></span>
* <span data-ttu-id="bc45f-114">Especifique a autenticação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="bc45f-114">Specify SQL authentication</span></span>
* <span data-ttu-id="bc45f-115">Nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="bc45f-115">Username</span></span>
* <span data-ttu-id="bc45f-116">Palavra-passe</span><span class="sxs-lookup"><span data-stu-id="bc45f-116">Password</span></span>
* <span data-ttu-id="bc45f-117">Base de dados predefinida (opcional)</span><span class="sxs-lookup"><span data-stu-id="bc45f-117">Default database (optional)</span></span>

<span data-ttu-id="bc45f-118">Por predefinição, a ligação liga toohello *mestre* base de dados e não a base de dados do utilizador.</span><span class="sxs-lookup"><span data-stu-id="bc45f-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="bc45f-119">base de dados do utilizador do tooyour de tooconnect, pode escolher toodo uma das duas coisas:</span><span class="sxs-lookup"><span data-stu-id="bc45f-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="bc45f-120">Especificar Olá predefinido da base de dados ao registar o seu servidor com Olá SQL Server Object Explorer no SSDT, SSMS, ou na sua cadeia de ligação da aplicação.</span><span class="sxs-lookup"><span data-stu-id="bc45f-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="bc45f-121">Por exemplo, a incluir o parâmetro de InitialCatalog Olá para uma ligação de ODBC.</span><span class="sxs-lookup"><span data-stu-id="bc45f-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="bc45f-122">Realce Olá utilizador da base de dados antes de criar uma sessão no SSDT.</span><span class="sxs-lookup"><span data-stu-id="bc45f-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="bc45f-123">instrução Transact-SQL de Olá **utilize MyDatabase;** não é suportada para alterar a base de dados de Olá para uma ligação.</span><span class="sxs-lookup"><span data-stu-id="bc45f-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="bc45f-124">Para obter orientações sobre a ligação tooSQL do armazém de dados com SSDT, consulte toohello [consulta com o Visual Studio] [ Query with Visual Studio] artigo.</span><span class="sxs-lookup"><span data-stu-id="bc45f-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="bc45f-125">Autenticação do Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="bc45f-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="bc45f-126">[Azure Active Directory] [ What is Azure Active Directory] a autenticação é um mecanismo de ligar tooMicrosoft Azure SQL Data Warehouse, utilizando as identidades no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc45f-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bc45f-127">Com a autenticação do Azure Active Directory, pode gerir centralmente identidades Olá de utilizadores de base de dados e outros serviços Microsoft numa localização central.</span><span class="sxs-lookup"><span data-stu-id="bc45f-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="bc45f-128">Gestão de ID central fornece um único local toomanage utilizadores de armazém de dados do SQL Server e simplifica a gestão de permissão.</span><span class="sxs-lookup"><span data-stu-id="bc45f-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="bc45f-129">Benefícios</span><span class="sxs-lookup"><span data-stu-id="bc45f-129">Benefits</span></span>
<span data-ttu-id="bc45f-130">Vantagens do Azure Active Directory incluem:</span><span class="sxs-lookup"><span data-stu-id="bc45f-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="bc45f-131">Fornece uma autenticação de servidor tooSQL alternativo.</span><span class="sxs-lookup"><span data-stu-id="bc45f-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="bc45f-132">Ajuda a parar a proliferação de Olá das identidades de utilizador em servidores de base de dados.</span><span class="sxs-lookup"><span data-stu-id="bc45f-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="bc45f-133">Permite a rotação de palavra-passe num único local</span><span class="sxs-lookup"><span data-stu-id="bc45f-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="bc45f-134">Gerir permissões de base de dados através de grupos do externos (AAD).</span><span class="sxs-lookup"><span data-stu-id="bc45f-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="bc45f-135">Elimina armazenar palavras-passe através da autenticação integrada do Windows e outras formas de autenticação suportados pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc45f-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="bc45f-136">Utiliza continha identidades tooauthenticate de utilizadores de base de dados ao nível da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc45f-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="bc45f-137">Suporta a autenticação baseada em tokens para ligar tooSQL do armazém de dados de aplicações.</span><span class="sxs-lookup"><span data-stu-id="bc45f-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="bc45f-138">Suporta autenticação Multifator através da autenticação de Universal do Active Directory para SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="bc45f-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="bc45f-139">Para obter uma descrição do multi-factor Authentication, consulte [SSMS suporte para o MFA do Azure AD com base de dados SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bc45f-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bc45f-140">Azure Active Directory é ainda relativamente novo e tem algumas limitações.</span><span class="sxs-lookup"><span data-stu-id="bc45f-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="bc45f-141">tooensure que o Azure Active Directory é uma boa opção para o seu ambiente, consulte [funcionalidades do Azure AD e limitações][Azure AD features and limitations], especificamente Olá considerações adicionais.</span><span class="sxs-lookup"><span data-stu-id="bc45f-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="bc45f-142">Passos de configuração</span><span class="sxs-lookup"><span data-stu-id="bc45f-142">Configuration steps</span></span>
<span data-ttu-id="bc45f-143">Siga a autenticação do Azure Active Directory estes passos tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="bc45f-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="bc45f-144">Criar e preencher um Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc45f-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="bc45f-145">Opcional: Associar ou alterar Olá active directory está atualmente associado a sua subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="bc45f-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="bc45f-146">Crie um administrador do Azure Active Directory para o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bc45f-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="bc45f-147">Configurar os computadores cliente</span><span class="sxs-lookup"><span data-stu-id="bc45f-147">Configure your client computers</span></span>
5. <span data-ttu-id="bc45f-148">Criar utilizadores de base de dados contida na sua base de dados mapeado tooAzure identidades do AD</span><span class="sxs-lookup"><span data-stu-id="bc45f-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="bc45f-149">Ligar tooyour do armazém de dados através da utilização de identidades do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc45f-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="bc45f-150">Atualmente, os utilizadores do Azure Active Directory não são apresentados no SSDT Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="bc45f-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="bc45f-151">Como solução, ver os utilizadores Olá [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc45f-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="bc45f-152">Encontrar os detalhes da Olá</span><span class="sxs-lookup"><span data-stu-id="bc45f-152">Find hello details</span></span>
* <span data-ttu-id="bc45f-153">Olá passos tooconfigure e a utilização do Azure Active Directory authentication sejam praticamente idênticos para a SQL Database do Azure e Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bc45f-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bc45f-154">Siga Olá detalhadas passos Olá tópico [tooSQL de ligação da base de dados ou SQL dados do armazém por utilizar o Azure autenticação do Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bc45f-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="bc45f-155">Criar funções de base de dados personalizada e adicionar utilizadores toohello funções.</span><span class="sxs-lookup"><span data-stu-id="bc45f-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="bc45f-156">Em seguida, conceda permissões granulares toohello funções.</span><span class="sxs-lookup"><span data-stu-id="bc45f-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="bc45f-157">Para obter mais informações, consulte [introdução de permissões do motor de base de dados](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc45f-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc45f-158">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bc45f-158">Next steps</span></span>
<span data-ttu-id="bc45f-159">toostart consultar o armazém de dados com o Visual Studio e outras aplicações, consulte [consulta com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="bc45f-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
