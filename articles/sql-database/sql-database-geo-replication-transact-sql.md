---
title: "replicação geográfica aaaConfigure para a base de dados do Azure SQL com o Transact-SQL | Microsoft Docs"
description: "Configurar a georreplicação da base de dados do SQL do Azure com o Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Configurar a georreplicação ativa para a base de dados do Azure SQL com o Transact-SQL

Este artigo mostra como tooconfigure georreplicação ativa para uma base de dados do SQL do Azure com o Transact-SQL.

ativação pós-falha de tooinitiate utilizando Transact-SQL, consulte [inicie uma ativação pós-falha planeada ou não planeada para a base de dados do Azure SQL com o Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Quando utilizar a georreplicação ativa (de dados secundárias legíveis) para a recuperação de desastre deve configurar um grupo de ativação pós-falha para todas as bases de dados dentro de uma aplicação tooenable automática e transparente ativação pós-falha. Esta funcionalidade está em pré-visualização. Para obter mais informações consulte [grupos de ativação de pós-falha automática e a georreplicação](sql-database-geo-replication-overview.md).
> 
> 

tooconfigure georreplicação ativa com Transact-SQL, terá de seguinte Olá:

* Uma subscrição do Azure.
* Um servidor lógico da SQL Database do Azure <MyLocalServer> e uma base de dados do SQL Server <MyDB> -Olá principal base de dados que pretende que o tooreplicate
* Um ou mais lógicos SQL Database do Azure servidores < MySecondaryServer(n) > - olá lógica servidores que serão servidores de parceiro de Olá nos quais irá criar bases de dados secundárias
* Um início de sessão que se encontra DBManager Olá primário
* Ter db_ownership de Olá local da base de dados que irá replicar georreplicação
* Ser DBManager no toowhich de servidor (es) de parceiro de Olá irá configurar georreplicação
* versão mais recente do Olá do SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> É recomendado que utilize sempre Olá versão mais recente do Management Studio tooremain sincronizada com atualizações tooMicrosoft Azure e a base de dados SQL. [Atualize o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Adicionar a base de dados secundária
Pode utilizar Olá **ALTER DATABASE** instrução toocreate um georreplicação base de dados secundária num servidor de parceiro. Executar esta instrução na base de dados mestra Olá de Olá servidor contentora Olá da base de dados toobe replicado. Olá georreplicação base de dados (hello "primário da base de dados") será ter Olá mesmo nome como base de dados de Olá a ser replicada e irá, por predefinição, tem Olá mesmo nível de serviço como base de dados primária Olá. Olá base de dados secundária pode ser legível ou não legível e pode ser uma base de dados ou num agrupamento elástico. Para obter mais informações, consulte [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [escalões de serviço](sql-database-service-tiers.md).
Depois de base de dados secundária Olá é criado e pré-propagadas, dados começará a replicar de forma assíncrona da base de dados primária Olá. Olá passos abaixo descrevem como tooconfigure georreplicação utilizando o Management Studio. Passos toocreate não legível e legíveis réplicas secundárias, como uma base de dados ou num agrupamento elástico, são fornecidas.

> [!NOTE]
> Se uma base de dados existe no servidor de parceiro especificado Olá com Olá mesmo nome como comando de Olá Olá base de dados primária irá falhar.
> 

### <a name="add-readable-secondary-single-database"></a>Adicionar secundário legível (base de dados individual)
Utilize Olá os seguintes passos toocreate uma secundária legível como uma base de dados.

1. No Management Studio, ligue o servidor lógico da SQL Database do Azure de tooyour.
2. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **mestre**e, em seguida, clique em **nova consulta**.
3. Utilize o seguinte Olá **ALTER DATABASE** instrução toomake uma base de dados local para um site primário georreplicação com uma base de dados secundária legível num servidor secundário.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Clique em **executar** consulta de Olá toorun.

### <a name="add-readable-secondary-elastic-pool"></a>Adicionar secundário legível (agrupamento elástico)
Utilize os seguintes passos toocreate uma secundária legível num agrupamento elástico de Olá.

1. No Management Studio, ligue o servidor lógico da SQL Database do Azure de tooyour.
2. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **mestre**e, em seguida, clique em **nova consulta**.
3. Utilize o seguinte Olá **ALTER DATABASE** instrução toomake uma base de dados local para um site primário georreplicação com uma base de dados secundária legível num servidor secundário num agrupamento elástico.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Clique em **executar** consulta de Olá toorun.

## <a name="remove-secondary-database"></a>Remover a base de dados secundária
Pode utilizar Olá **ALTER DATABASE** instrução toopermanently terminar parceria de replicação de Olá entre uma base de dados secundário e o respetivo principal. Esta declaração de é executada na Olá base de dados mestra no qual Olá reside base de dados primária. Após a terminação da relação de Olá, base de dados secundária Olá, torna-se uma base de dados de leitura e escrita regular. Se a base de dados do Olá conectividade toosecondary está quebrada é concluída com êxito do comando de Olá mas Olá secundário irá tornar-se leitura / escrita após o restauro de conectividade. Para obter mais informações, consulte [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [escalões de serviço](sql-database-service-tiers.md).

Utilize Olá seguintes georreplicação secundário do tooremove passos de uma parceria de georreplicação.

1. No Management Studio, ligue o servidor lógico da SQL Database do Azure de tooyour.
2. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **mestre**e, em seguida, clique em **nova consulta**.
3. Utilize o seguinte Olá **ALTER DATABASE** secundário tooremove um georreplicação de instrução.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Clique em **executar** consulta de Olá toorun.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Monitorizar o estado de funcionamento e configuração de replicação geográfica activa

Tarefas de monitorização incluem a monitorização da configuração de replicação geográfica Olá e monitorização de estado de funcionamento de replicação de dados.  Pode utilizar Olá **sys.dm_geo_replication_links** vista de gestão dinâmica no Olá base de dados mestra tooreturn obter informações sobre todas as ligações de replicação exiting para cada base de dados no servidor lógico da SQL Database do Azure de Olá. Esta vista contém uma linha para cada ligação de replicação de Olá entre bases de dados primários e secundários. Pode utilizar Olá **sys.dm_replication_link_status** gestão dinâmica ver tooreturn uma linha para cada base de dados de SQL do Azure que está atualmente parte da ligação de replicação de replicação. Isto inclui as bases de dados primários e secundários. Se existir mais do que uma ligação de replicação contínua para uma determinada base de dados primária, esta tabela contém uma linha para cada uma das relações de Olá. Vista de Olá é criada em todas as bases de dados, incluindo mestre lógico Olá. No entanto, a consultar esta vista no mestre lógico Olá devolve um conjunto vazio. Pode utilizar Olá **operation_status** gestão dinâmica Ver estado de Olá tooshow para todas as operações, incluindo o estado de Olá Olá das ligações de replicação de base de dados. Para obter mais informações, consulte [sys.geo_replication_links (SQL Database do Azure)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (SQL Database do Azure)](https://msdn.microsoft.com/library/mt575504.aspx), e [operation_status (Azure SQL Base de dados)](https://msdn.microsoft.com/library/dn270022.aspx).

Utilize Olá parceria de toomonitor uma georreplicação ativa passos a seguir.

1. No Management Studio, ligue o servidor lógico da SQL Database do Azure de tooyour.
2. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **mestre**e, em seguida, clique em **nova consulta**.
3. Utilize Olá seguinte declaração tooshow todas as bases de dados com ligações de georreplicação.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Clique em **executar** consulta de Olá toorun.
5. Abra a pasta de bases de dados de Olá, expanda Olá **bases de dados do sistema** pasta, o botão direito no **MyDB**e, em seguida, clique em **nova consulta**.
6. Olá de utilização seguintes replicação de Olá instrução tooshow lags e última hora de replicação do meu bases de dados secundárias de MyDB.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Clique em **executar** consulta de Olá toorun.
8. Utilize Olá instrução tooshow Olá mais recentes georreplicação operações associadas a base de dados MyDB a seguir.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Clique em **executar** consulta de Olá toorun.

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre grupos de ativação pós-falha e a georreplicação ativa, consulte - [grupos de ativação pós-falha](sql-database-geo-replication-overview.md)
* Para cenários e uma descrição geral de continuidade de negócio, consulte [descrição geral da continuidade de negócio](sql-database-business-continuity.md)

