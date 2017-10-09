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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Configurar e gerir a segurança de SQL Database do Azure para georrestauro ou de ativação pós-falha 

> [!NOTE]
> [Replicação geográfica activa](sql-database-geo-replication-overview.md) está agora disponível para todas as bases de dados em todos os escalões de serviço.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Descrição geral dos requisitos de autenticação para a recuperação de desastre
Este tópico descreve tooconfigure de requisitos de autenticação de Olá e controlo [georreplicação ativa](sql-database-geo-replication-overview.md) e Olá os passos necessário tooset cópias de segurança utilizador acesso toohello base de dados secundária. Também descreve como ativar a base de dados recuperada acesso toohello depois de utilizar [georrestauro](sql-database-recovery-using-backups.md#geo-restore). Para obter mais informações sobre as opções de recuperação, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Recuperação após desastre com utilizadores contidos
Ao contrário dos utilizadores tradicionais, que tem de ser mapeado toologins na base de dados mestra Olá, um utilizador contido é completamente gerido pelo Olá própria base de dados. Isto tem duas vantagens. Num cenário de recuperação de desastre Olá, os utilizadores de Olá podem continuar tooconnect toohello nova base de dados primária ou base de dados de Olá recuperada utilizando georrestauro sem qualquer configuração adicional, porque a base de dados de Olá Gere utilizadores Olá. Também existem potencial escalabilidade e os benefícios de desempenho desta configuração de uma perspetiva de início de sessão. Para obter mais informações, veja [Contained Database Users - Making Your Database Portable (Utilizadores de Base de Dados Contidos - Tornar a Sua Base de Dados Portátil)](https://msdn.microsoft.com/library/ff929188.aspx). 

compromisso principal Olá é que é mais difícil gerir o processo de recuperação de desastres Olá à escala. Quando tiver várias bases de dados que Olá utilize contido de início de sessão mesmo, mantendo as credenciais de Olá utilizando utilizadores em várias bases de dados poderão negate vantagens Olá de utilizadores contidos. Por exemplo, a política de rotação de palavra-passe Olá requer que efetuadas alterações a ser consistentemente várias bases de dados em vez de alteração Olá palavra-passe para início de sessão Olá uma vez na base de dados mestra Olá. Por este motivo, se tiver várias bases de dados que utilize Olá mesmo nome de utilizador e palavra-passe, a utilização de utilizadores contidos não é recomendada. 

## <a name="how-tooconfigure-logins-and-users"></a>Como tooconfigure inícios de sessão e os utilizadores
Se estiver a utilizar inícios de sessão e os utilizadores (em vez de utilizadores contidos), tem de efetuar passos adicionais tooinsure esse Olá inícios de sessão mesmos existem na base de dados mestra Olá. Olá secções seguinte descrevem as considerações Olá passos envolvidos e adicionais.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Configurar utilizador acesso tooa secundário ou recuperado base de dados
Para que toobe de base de dados secundária Olá utilizável como uma base de dados secundária só de leitura e tooensure acesso adequado toohello nova base de dados ou Olá base de dados primária recuperado utilizando georrestauro, Olá principal base de dados do servidor de destino Olá tem de ter Olá configuração de segurança adequadas no local antes da recuperação de Olá.

permissões específicas de Olá para cada passo são descritas mais à frente neste tópico.

A preparar tooa de acesso de utilizador georreplicação secundário deve ser efetuado como parte de configurar a georreplicação. A preparar o acesso de utilizador bases de dados de georreplicação-restaurada toohello deve ser efetuada em qualquer altura quando o servidor original Olá está online (por exemplo, como parte de desagregação Olá DR).

> [!NOTE]
> Se, efetuar uma ativação pós-falha ou georrestauro servidor tooa que não tenha inícios de sessão está corretamente configurados, acesso tooit será a conta de administrador de servidor toohello limitado.
> 
> 

Configurar os inícios de sessão no servidor de destino Olá envolve três passos descritos abaixo:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Determine os inícios de sessão com acesso toohello principal da base de dados:
Olá primeiro passo do processo de Olá é toodetermine os inícios de sessão tem de estar duplicados no servidor de destino Olá. Isto é conseguido com um par de instruções SELECT, na Olá lógica principal da base de dados no servidor de origem Olá e um no Olá primário própria base de dados.

Olá apenas o administrador do servidor ou membro de Olá **LoginManager** função de servidor pode determinar Olá os inícios de sessão no servidor de origem Olá com Olá a seguinte instrução SELECT. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Apenas um membro da função de base de dados de db_owner Olá, um utilizador de dbo de Olá ou administrador de servidor, pode determinar todos os principais de utilizador de base de dados de Olá na base de dados primária Olá.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Localize Olá SID para inícios de sessão Olá identificados no passo 1:
Comparando saída Olá de consultas de Olá da secção anterior Olá e Olá correspondente SIDs, pode mapear o utilizador de toodatabase de início de sessão de servidor Olá. Inícios de sessão com um utilizador de base de dados com um SID correspondente tem base de dados de toothat de acesso de utilizador do utilizador da base de dados principal. 

Olá seguinte consulta pode ser utilizado toosee todos os principais de utilizador Olá e os respetivos SIDs numa base de dados. Apenas um membro de Olá db_owner da base de dados função de administrador ou de servidor pode executar esta consulta.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Olá **INFORMATION_SCHEMA** e **sys** os utilizadores têm *nulo* SIDs e Olá **convidado** SID é **0x00**. Olá **dbo** SID pode começar a utilizar *0x01060000000001648000000000048454*, se o criador de base de dados de Olá foi Olá, admin servidor em vez de um membro do **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Crie inícios de sessão Olá no servidor de destino Olá:
Olá último passo é o servidor de destino toogo toohello ou servidores e gerar Olá os inícios de sessão com Olá adequado SIDs. sintaxe básico Olá é a seguinte.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Se quiser toohello de acesso de utilizador toogrant secundário, mas não toohello primário, pode fazê-lo alterando o início de sessão de utilizador de Olá no servidor primário Olá utilizando Olá sintaxe.
> 
> INÍCIO DE SESSÃO DE ALTER <login name> DESATIVAR
> 
> DESATIVAR não irá alterar palavra-passe de Olá, pelo que pode sempre ativar-se necessário.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações sobre a gestão de acesso de base de dados e inícios de sessão, consulte [segurança da base de dados SQL: Gerir a segurança da base de dados de início de sessão e acesso](sql-database-manage-logins.md).
* Para obter mais informações sobre os utilizadores de base de dados contida, consulte [contidos base de dados de utilizadores - tornar a base de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).
* Para obter informações sobre como utilizar e configurar a replicação geográfica activa, consulte [georreplicação ativa](sql-database-geo-replication-overview.md)
* Para obter informações sobre como utilizar georrestauro, consulte [georrestauro](sql-database-recovery-using-backups.md#geo-restore)

