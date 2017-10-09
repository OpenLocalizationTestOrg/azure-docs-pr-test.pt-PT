---
title: "Portal do Azure: georreplicação de base de dados SQL | Microsoft Docs"
description: "Configurar georreplicação para a SQL Database do Azure em Olá portal do Azure e de iniciação de ativação pós-falha"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Configurar georreplicação ativa para a SQL Database do Azure em Olá portal do Azure e de iniciação de ativação pós-falha

Este artigo mostra como tooconfigure georreplicação ativa para a base de dados SQL no Olá [portal do Azure](http://portal.azure.com) e tooinitiate de ativação pós-falha.

ativação pós-falha de tooinitiate com Olá portal do Azure, consulte [inicie uma ativação pós-falha planeada ou não planeada para a SQL Database do Azure com o portal do Azure de Olá](sql-database-geo-replication-portal.md).

tooconfigure replicação geográfica activa utilizando Olá portal do Azure, terá de Olá os seguintes recursos:

* Uma base de dados SQL do Azure: Olá principal base de dados que pretende que a região geográfica do tooreplicate tooa diferente.

> [!Note]
Replicação geográfica activa tem de estar entre bases de dados no Olá mesma subscrição.

## <a name="add-a-secondary-database"></a>Adicionar uma base de dados secundária
Olá passos seguintes criar uma nova base de dados secundária numa parceria de georreplicação.  

tooadd uma base de dados secundária, tem de ser proprietário da subscrição Olá ou coproprietário.

base de dados secundária Olá tem Olá mesmo nome como base de dados primária Olá e tiver, por predefinição, Olá mesmo nível de serviço. base de dados secundária Olá pode ser uma base de dados ou uma base de dados num agrupamento elástico. Para obter mais informações, consulte [escalões de serviço](sql-database-service-tiers.md).
Depois de Olá secundário é criado e pré-propagadas, dados começa a replicar do Olá base de dados primária toohello nova base de dados secundária.

> [!NOTE]
> Se a base de dados de parceiro de Olá já existe (por exemplo, como resultado da terminação uma relação de replicação geográfica anterior) comando Olá falha.
> 

1. No Olá [portal do Azure](http://portal.azure.com), procurar toohello base de dados que pretende que o tooset para georreplicação.
2. Na página de base de dados SQL Olá, selecione **georreplicação**e, em seguida, selecione Olá região toocreate Olá secundária da base de dados. Pode selecionar qualquer região diferente da região de Olá que aloja a base de dados primária Olá, mas recomendamos Olá [região emparelhado](../best-practices-availability-paired-regions.md).
   
    ![Configurar georreplicação](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Selecione ou configure o servidor de Olá e escalão de preço da base de dados secundária Olá.
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/create-secondary.png)
4. Opcionalmente, pode adicionar um conjunto elástico de tooan de base de dados secundária. toocreate Olá base de dados secundária de um conjunto, clique em **conjunto elástico** e selecione um agrupamento de servidor de destino Olá. Um agrupamento tem de existir no servidor de destino Olá. Este fluxo de trabalho não crie um conjunto.
5. Clique em **criar** tooadd Olá secundário.
6. base de dados secundária Olá é criado e começa a Olá seeding processo.
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/seeding0.png)
7. Quando Olá seeding o processo estiver concluído, a base de dados secundária Olá apresenta o estado dele.
   
    ![O seeding concluída](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Inicie uma ativação pós-falha

base de dados secundária Olá pode ser desativados toobecome Olá primário.  

1. No Olá [portal do Azure](http://portal.azure.com), procurar toohello principal da base de dados na parceria de georreplicação Olá.
2. No painel da base de dados SQL de Olá, selecione **todas as definições** > **georreplicação**.
3. No Olá **secundárias** lista, selecione de Olá base de dados toobecome Olá nova principal e clique em **ativação pós-falha**.
   
    ![ativação pós-falha](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Clique em **Sim** toobegin ativação pós-falha de Olá.

comando Olá comutadores imediatamente base de dados secundária Olá na função primária Olá. 

Não há um curto período de tempo durante os quais não ambas as bases de dados estão disponíveis (na ordem de Olá de 0 too25 segundos) enquanto funções Olá são mudadas. Se a base de dados primária Olá tem várias bases de dados secundárias, o comando de Olá automaticamente reconfigura Olá outra bases de dados secundárias tooconnect toohello nova principal. operação todo Olá deve demorar menos de um minuto toocomplete em circunstâncias normais. 

> [!NOTE]
> Este comando foi concebido para recuperação rápida da base de dados de Olá em caso de indisponibilidade. Aciona a ativação pós-falha sem sincronização de dados (forçado a ativação pós-falha).  Se Olá primário está online e ao consolidar transações quando o comando de Olá é emitido alguma perda de dados poderão ocorrer. 
> 
> 

## <a name="remove-secondary-database"></a>Remover a base de dados secundária
Esta operação termina permanentemente Olá replicação toohello base de dados secundária e alterações Olá função de Olá tooa secundário regular leitura / escrita da base de dados. Se Olá conectividade toohello base de dados secundária for interrompida, o comando de Olá é concluída com êxito mas Olá does secundário deixam de ser de leitura / escrita até após o restauro de conectividade.  

1. No Olá [portal do Azure](http://portal.azure.com), procurar toohello principal da base de dados na parceria de georreplicação Olá.
2. Na página de base de dados SQL Olá, selecione **georreplicação**.
3. No Olá **secundárias** lista, selecione Olá base de dados tooremove da parceria de georreplicação Olá.
4. Clique em **pare a replicação**.
   
    ![Remover secundário](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Será apresentada uma janela de confirmação. Clique em **Sim** base de dados do tooremove Olá da parceria de georreplicação Olá. (Defina-o base de dados de leitura e escrita tooa não faz parte de qualquer replicação.)

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre a replicação geográfica activa, consulte [georreplicação ativa](sql-database-geo-replication-overview.md).
* Para cenários e uma descrição geral de continuidade de negócio, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).

