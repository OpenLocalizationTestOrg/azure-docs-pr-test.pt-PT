---
title: "A ativação pós-falha TSQL:initiate SQL Database do Azure | Microsoft Docs"
description: "Inicie uma ativação pós-falha planeada ou não planeada para a base de dados do SQL do Azure com o Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Inicie uma ativação pós-falha planeada ou não planeada para a base de dados do Azure SQL com o Transact-SQL

Este artigo mostra como tooinitiate tooa de ativação pós-falha secundário base de dados SQL com o Transact-SQL. tooconfigure georreplicação, consulte [configurar georreplicação da base de dados do Azure SQL](sql-database-geo-replication-transact-sql.md).

tooinitiate de ativação pós-falha, é necessário o seguinte Olá:

* Um início de sessão que se encontra DBManager Olá primário
* Ter db_ownership de Olá local da base de dados que irá replicar georreplicação
* Ser DBManager no toowhich de servidor (es) de parceiro de Olá irá configurar georreplicação
* Versão mais recente do SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> É recomendado que utilize sempre Olá versão mais recente do Management Studio tooremain sincronizada com atualizações tooMicrosoft Azure e a base de dados SQL. [Atualize o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Inicie uma ativação pós-falha planeada promover um base de dados secundária toobecome Olá nova principal
Pode utilizar Olá **ALTER DATABASE** instrução toopromote um base de dados secundária toobecome Olá nova principal da base de dados de forma planeada, despromover toobecome de principal existente Olá uma secundária. Esta declaração de é executada na base de dados mestra Olá no servidor de lógica de Olá SQL Database do Azure na qual Olá georreplicação base de dados secundária que está a ser promovido reside. Esta funcionalidade foi concebida para ativação pós-falha planeada, tal como durante simulações de Olá DR e requer que essa base de dados primária Olá estar disponível.

comando Olá efetua Olá seguinte fluxo de trabalho:

1. Temporariamente o modo de toosynchronous de replicação de comutadores, fazendo com que todas as transações pendentes toobe descarregados toohello secundário e bloquear todas as transações do novo;
2. Comutadores Olá funções de Olá duas bases de dados na parceria de georreplicação Olá.  

Esta sequência garante que Olá duas bases de dados estão sincronizados antes de mudar de funções de Olá e, por conseguinte, não irá ocorrer nenhuma perda de dados. Não há um curto período de tempo durante os quais não ambas as bases de dados estão disponíveis (na ordem de Olá de 0 too25 segundos) enquanto funções Olá são mudadas. Se a base de dados primária Olá tem várias bases de dados secundárias, o comando de Olá será automaticamente reconfigure Olá outra bases de dados secundárias tooconnect toohello nova principal.  operação todo Olá deve demorar menos de um minuto toocomplete em circunstâncias normais. Para obter mais informações, consulte [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [escalões de serviço](sql-database-service-tiers.md).

Utilize Olá os seguintes passos tooinitiate uma ativação pós-falha planeada.

1. No Management Studio, ligue o servidor de lógica de SQL Database do Azure de toohello em que reside um georreplicação base de dados secundária.
2. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **mestre**e, em seguida, clique em **nova consulta**.
3. Utilize o seguinte Olá **ALTER DATABASE** instrução tooswitch Olá base de dados secundária toohello função primária.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Clique em **executar** consulta de Olá toorun.

> [!NOTE]
> Em casos raros, é possível que a operação de Olá não é possível concluir e pode aparecer bloqueada. Neste caso, o utilizador Olá pode executar o comando de ativação pós-falha de imposição de Olá e aceitar a perda de dados.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Inicie uma ativação pós-falha não planeada do Olá base de dados primária toohello base de dados secundária
Pode utilizar Olá **ALTER DATABASE** instrução toopromote um base de dados secundária toobecome Olá nova principal da base de dados de forma não planeada, forçar a despromoção Olá do toobecome de principal existente Olá uma secundária num momento quando Olá base de dados primária já não está disponível. Esta declaração de é executada na base de dados mestra Olá no servidor de lógica de Olá SQL Database do Azure na qual Olá georreplicação base de dados secundária que está a ser promovido reside.

Esta funcionalidade foi concebida para recuperação após desastre quando restaurar disponibilidade da base de dados de Olá é crítico e alguma perda de dados é aceitável. Quando a ativação pós-falha forçada é invocada, Olá especificado base de dados secundária torna-se a base de dados primária Olá imediatamente e começa a aceitação de transações de escrita. Assim que Olá original base de dados primária é capaz de tooreconnect com esta nova base de dados primária, cópia de segurança incremental é criada no Olá original base de dados primária e Olá antigo base de dados primária é efetuada numa base de dados secundária para Olá nova base de dados primária; posteriormente, é simplesmente uma réplica de sincronização de principal novo Olá.

No entanto, porque o ponto no tempo restaurar não é suportada em bases de dados secundária de Olá, se o utilizador de Olá pretende dados toorecover consolidados toohello antigo principal base de dados que não tinha sido replicados toohello nova principal da base de dados antes de ocorrer a ativação pós-falha de Olá forçado, Olá utilizador terá de tooengage suporte toorecover este caso de perda de dados.

Se a base de dados primária Olá tem várias bases de dados secundárias, o comando de Olá será automaticamente reconfigure Olá outra bases de dados secundárias tooconnect toohello nova principal.

Utilize Olá os seguintes passos tooinitiate uma ativação pós-falha não planeada.

1. No Management Studio, ligue o servidor de lógica de SQL Database do Azure de toohello em que reside um georreplicação base de dados secundária.
2. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **mestre**e, em seguida, clique em **nova consulta**.
3. Utilize o seguinte Olá **ALTER DATABASE** instrução tooswitch Olá base de dados secundária toohello função primária.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Clique em **executar** consulta de Olá toorun.

> [!NOTE]
> Se o comando de Olá é emitido quando principais e secundários estiverem online primário antigo Olá deixará de estar Olá novo secundário imediatamente sem sincronização de dados. Se tiver Olá primário podem ocorrer ao consolidar transações quando o comando de Olá é emitido alguma perda de dados.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Após a ativação pós-falha, certifique-se requisitos de autenticação de Olá para o servidor e base de dados estão configurados no principal Olá de novo. Para obter mais informações, consulte [segurança da base de dados do SQL Server após a recuperação de desastre](sql-database-geo-replication-security-config.md).
* toolearn recuperação após desastres utilizando a replicação geográfica activa, incluindo os passos de recuperação de pré-lançamento e pós-recuperação e realizar um exercício de recuperação após desastre, consulte [recuperação após desastre](sql-database-disaster-recovery.md)
* Para uma mensagem de blogue Sasha Nosov sobre replicação geográfica activa, consulte [Spotlight em novas capacidades de replicação geográfica](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Para obter informações sobre como criar nuvem aplicações toouse replicação geográfica activa, consulte [aplicações em nuvem de conceção para utilizar a georreplicação de continuidade do negócio](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Para obter informações sobre como utilizar a georreplicação ativa com conjuntos elásticos, consulte [estratégias de recuperação de desastre do conjunto elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Para obter uma descrição geral da continuidade do negócio, consulte [descrição geral da continuidade de negócio](sql-database-business-continuity.md)

