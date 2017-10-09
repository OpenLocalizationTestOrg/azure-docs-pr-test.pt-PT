---
title: "segurança de SQL Database do Azure para recuperação após desastre de aaaConfigure | Microsoft Docs"
description: "Este tópico explica as considerações de segurança para configurar e gerir a segurança depois de restaurar uma base de dados ou um servidor secundário de tooa de ativação pós-falha no evento Olá de uma falha do Centro de dados ou outro desastre"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="89a94-103">Configurar e gerir a segurança de SQL Database do Azure para georrestauro ou de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="89a94-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="89a94-104">[Replicação geográfica activa](sql-database-geo-replication-overview.md) está agora disponível para todas as bases de dados em todos os escalões de serviço.</span><span class="sxs-lookup"><span data-stu-id="89a94-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="89a94-105">Descrição geral dos requisitos de autenticação para a recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="89a94-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="89a94-106">Este tópico descreve tooconfigure de requisitos de autenticação de Olá e controlo [georreplicação ativa](sql-database-geo-replication-overview.md) e Olá os passos necessário tooset cópias de segurança utilizador acesso toohello base de dados secundária.</span><span class="sxs-lookup"><span data-stu-id="89a94-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="89a94-107">Também descreve como ativar a base de dados recuperada acesso toohello depois de utilizar [georrestauro](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="89a94-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="89a94-108">Para obter mais informações sobre as opções de recuperação, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="89a94-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="89a94-109">Recuperação após desastre com utilizadores contidos</span><span class="sxs-lookup"><span data-stu-id="89a94-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="89a94-110">Ao contrário dos utilizadores tradicionais, que tem de ser mapeado toologins na base de dados mestra Olá, um utilizador contido é completamente gerido pelo Olá própria base de dados.</span><span class="sxs-lookup"><span data-stu-id="89a94-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="89a94-111">Isto tem duas vantagens.</span><span class="sxs-lookup"><span data-stu-id="89a94-111">This has two benefits.</span></span> <span data-ttu-id="89a94-112">Num cenário de recuperação de desastre Olá, os utilizadores de Olá podem continuar tooconnect toohello nova base de dados primária ou base de dados de Olá recuperada utilizando georrestauro sem qualquer configuração adicional, porque a base de dados de Olá Gere utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="89a94-113">Também existem potencial escalabilidade e os benefícios de desempenho desta configuração de uma perspetiva de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="89a94-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="89a94-114">Para obter mais informações, veja [Contained Database Users - Making Your Database Portable (Utilizadores de Base de Dados Contidos - Tornar a Sua Base de Dados Portátil)](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="89a94-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="89a94-115">compromisso principal Olá é que é mais difícil gerir o processo de recuperação de desastres Olá à escala.</span><span class="sxs-lookup"><span data-stu-id="89a94-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="89a94-116">Quando tiver várias bases de dados que Olá utilize contido de início de sessão mesmo, mantendo as credenciais de Olá utilizando utilizadores em várias bases de dados poderão negate vantagens Olá de utilizadores contidos.</span><span class="sxs-lookup"><span data-stu-id="89a94-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="89a94-117">Por exemplo, a política de rotação de palavra-passe Olá requer que efetuadas alterações a ser consistentemente várias bases de dados em vez de alteração Olá palavra-passe para início de sessão Olá uma vez na base de dados mestra Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="89a94-118">Por este motivo, se tiver várias bases de dados que utilize Olá mesmo nome de utilizador e palavra-passe, a utilização de utilizadores contidos não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="89a94-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="89a94-119">Como tooconfigure inícios de sessão e os utilizadores</span><span class="sxs-lookup"><span data-stu-id="89a94-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="89a94-120">Se estiver a utilizar inícios de sessão e os utilizadores (em vez de utilizadores contidos), tem de efetuar passos adicionais tooinsure esse Olá inícios de sessão mesmos existem na base de dados mestra Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="89a94-121">Olá secções seguinte descrevem as considerações Olá passos envolvidos e adicionais.</span><span class="sxs-lookup"><span data-stu-id="89a94-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="89a94-122">Configurar utilizador acesso tooa secundário ou recuperado base de dados</span><span class="sxs-lookup"><span data-stu-id="89a94-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="89a94-123">Para que toobe de base de dados secundária Olá utilizável como uma base de dados secundária só de leitura e tooensure acesso adequado toohello nova base de dados ou Olá base de dados primária recuperado utilizando georrestauro, Olá principal base de dados do servidor de destino Olá tem de ter Olá configuração de segurança adequadas no local antes da recuperação de Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="89a94-124">permissões específicas de Olá para cada passo são descritas mais à frente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="89a94-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="89a94-125">A preparar tooa de acesso de utilizador georreplicação secundário deve ser efetuado como parte de configurar a georreplicação.</span><span class="sxs-lookup"><span data-stu-id="89a94-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="89a94-126">A preparar o acesso de utilizador bases de dados de georreplicação-restaurada toohello deve ser efetuada em qualquer altura quando o servidor original Olá está online (por exemplo, como parte de desagregação Olá DR).</span><span class="sxs-lookup"><span data-stu-id="89a94-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="89a94-127">Se, efetuar uma ativação pós-falha ou georrestauro servidor tooa que não tenha inícios de sessão está corretamente configurados, acesso tooit será a conta de administrador de servidor toohello limitado.</span><span class="sxs-lookup"><span data-stu-id="89a94-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="89a94-128">Configurar os inícios de sessão no servidor de destino Olá envolve três passos descritos abaixo:</span><span class="sxs-lookup"><span data-stu-id="89a94-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="89a94-129">1. Determine os inícios de sessão com acesso toohello principal da base de dados:</span><span class="sxs-lookup"><span data-stu-id="89a94-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="89a94-130">Olá primeiro passo do processo de Olá é toodetermine os inícios de sessão tem de estar duplicados no servidor de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="89a94-131">Isto é conseguido com um par de instruções SELECT, na Olá lógica principal da base de dados no servidor de origem Olá e um no Olá primário própria base de dados.</span><span class="sxs-lookup"><span data-stu-id="89a94-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="89a94-132">Olá apenas o administrador do servidor ou membro de Olá **LoginManager** função de servidor pode determinar Olá os inícios de sessão no servidor de origem Olá com Olá a seguinte instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="89a94-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="89a94-133">Apenas um membro da função de base de dados de db_owner Olá, um utilizador de dbo de Olá ou administrador de servidor, pode determinar todos os principais de utilizador de base de dados de Olá na base de dados primária Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="89a94-134">2. Localize Olá SID para inícios de sessão Olá identificados no passo 1:</span><span class="sxs-lookup"><span data-stu-id="89a94-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="89a94-135">Comparando saída Olá de consultas de Olá da secção anterior Olá e Olá correspondente SIDs, pode mapear o utilizador de toodatabase de início de sessão de servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="89a94-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="89a94-136">Inícios de sessão com um utilizador de base de dados com um SID correspondente tem base de dados de toothat de acesso de utilizador do utilizador da base de dados principal.</span><span class="sxs-lookup"><span data-stu-id="89a94-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="89a94-137">Olá seguinte consulta pode ser utilizado toosee todos os principais de utilizador Olá e os respetivos SIDs numa base de dados.</span><span class="sxs-lookup"><span data-stu-id="89a94-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="89a94-138">Apenas um membro de Olá db_owner da base de dados função de administrador ou de servidor pode executar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="89a94-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="89a94-139">Olá **INFORMATION_SCHEMA** e **sys** os utilizadores têm *nulo* SIDs e Olá **convidado** SID é **0x00**.</span><span class="sxs-lookup"><span data-stu-id="89a94-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="89a94-140">Olá **dbo** SID pode começar a utilizar *0x01060000000001648000000000048454*, se o criador de base de dados de Olá foi Olá, admin servidor em vez de um membro do **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="89a94-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="89a94-141">3. Crie inícios de sessão Olá no servidor de destino Olá:</span><span class="sxs-lookup"><span data-stu-id="89a94-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="89a94-142">Olá último passo é o servidor de destino toogo toohello ou servidores e gerar Olá os inícios de sessão com Olá adequado SIDs.</span><span class="sxs-lookup"><span data-stu-id="89a94-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="89a94-143">sintaxe básico Olá é a seguinte.</span><span class="sxs-lookup"><span data-stu-id="89a94-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="89a94-144">Se quiser toohello de acesso de utilizador toogrant secundário, mas não toohello primário, pode fazê-lo alterando o início de sessão de utilizador de Olá no servidor primário Olá utilizando Olá sintaxe.</span><span class="sxs-lookup"><span data-stu-id="89a94-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="89a94-145">INÍCIO DE SESSÃO DE ALTER <login name> DESATIVAR</span><span class="sxs-lookup"><span data-stu-id="89a94-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="89a94-146">DESATIVAR não irá alterar palavra-passe de Olá, pelo que pode sempre ativar-se necessário.</span><span class="sxs-lookup"><span data-stu-id="89a94-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="89a94-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="89a94-147">Next steps</span></span>
* <span data-ttu-id="89a94-148">Para obter mais informações sobre a gestão de acesso de base de dados e inícios de sessão, consulte [segurança da base de dados SQL: Gerir a segurança da base de dados de início de sessão e acesso](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="89a94-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="89a94-149">Para obter mais informações sobre os utilizadores de base de dados contida, consulte [contidos base de dados de utilizadores - tornar a base de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="89a94-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="89a94-150">Para obter informações sobre como utilizar e configurar a replicação geográfica activa, consulte [georreplicação ativa](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="89a94-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="89a94-151">Para obter informações sobre como utilizar georrestauro, consulte [georrestauro](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="89a94-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

