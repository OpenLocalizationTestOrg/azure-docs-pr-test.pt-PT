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
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="41f2a-103">Configurar georreplicação ativa para a SQL Database do Azure em Olá portal do Azure e de iniciação de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="41f2a-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="41f2a-104">Este artigo mostra como tooconfigure georreplicação ativa para a base de dados SQL no Olá [portal do Azure](http://portal.azure.com) e tooinitiate de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="41f2a-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="41f2a-105">ativação pós-falha de tooinitiate com Olá portal do Azure, consulte [inicie uma ativação pós-falha planeada ou não planeada para a SQL Database do Azure com o portal do Azure de Olá](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="41f2a-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="41f2a-106">tooconfigure replicação geográfica activa utilizando Olá portal do Azure, terá de Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="41f2a-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="41f2a-107">Uma base de dados SQL do Azure: Olá principal base de dados que pretende que a região geográfica do tooreplicate tooa diferente.</span><span class="sxs-lookup"><span data-stu-id="41f2a-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="41f2a-108">Replicação geográfica activa tem de estar entre bases de dados no Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="41f2a-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="41f2a-109">Adicionar uma base de dados secundária</span><span class="sxs-lookup"><span data-stu-id="41f2a-109">Add a secondary database</span></span>
<span data-ttu-id="41f2a-110">Olá passos seguintes criar uma nova base de dados secundária numa parceria de georreplicação.</span><span class="sxs-lookup"><span data-stu-id="41f2a-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="41f2a-111">tooadd uma base de dados secundária, tem de ser proprietário da subscrição Olá ou coproprietário.</span><span class="sxs-lookup"><span data-stu-id="41f2a-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="41f2a-112">base de dados secundária Olá tem Olá mesmo nome como base de dados primária Olá e tiver, por predefinição, Olá mesmo nível de serviço.</span><span class="sxs-lookup"><span data-stu-id="41f2a-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="41f2a-113">base de dados secundária Olá pode ser uma base de dados ou uma base de dados num agrupamento elástico.</span><span class="sxs-lookup"><span data-stu-id="41f2a-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="41f2a-114">Para obter mais informações, consulte [escalões de serviço](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="41f2a-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="41f2a-115">Depois de Olá secundário é criado e pré-propagadas, dados começa a replicar do Olá base de dados primária toohello nova base de dados secundária.</span><span class="sxs-lookup"><span data-stu-id="41f2a-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="41f2a-116">Se a base de dados de parceiro de Olá já existe (por exemplo, como resultado da terminação uma relação de replicação geográfica anterior) comando Olá falha.</span><span class="sxs-lookup"><span data-stu-id="41f2a-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="41f2a-117">No Olá [portal do Azure](http://portal.azure.com), procurar toohello base de dados que pretende que o tooset para georreplicação.</span><span class="sxs-lookup"><span data-stu-id="41f2a-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="41f2a-118">Na página de base de dados SQL Olá, selecione **georreplicação**e, em seguida, selecione Olá região toocreate Olá secundária da base de dados.</span><span class="sxs-lookup"><span data-stu-id="41f2a-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="41f2a-119">Pode selecionar qualquer região diferente da região de Olá que aloja a base de dados primária Olá, mas recomendamos Olá [região emparelhado](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="41f2a-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configurar georreplicação](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="41f2a-121">Selecione ou configure o servidor de Olá e escalão de preço da base de dados secundária Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="41f2a-123">Opcionalmente, pode adicionar um conjunto elástico de tooan de base de dados secundária.</span><span class="sxs-lookup"><span data-stu-id="41f2a-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="41f2a-124">toocreate Olá base de dados secundária de um conjunto, clique em **conjunto elástico** e selecione um agrupamento de servidor de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="41f2a-125">Um agrupamento tem de existir no servidor de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="41f2a-126">Este fluxo de trabalho não crie um conjunto.</span><span class="sxs-lookup"><span data-stu-id="41f2a-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="41f2a-127">Clique em **criar** tooadd Olá secundário.</span><span class="sxs-lookup"><span data-stu-id="41f2a-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="41f2a-128">base de dados secundária Olá é criado e começa a Olá seeding processo.</span><span class="sxs-lookup"><span data-stu-id="41f2a-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="41f2a-130">Quando Olá seeding o processo estiver concluído, a base de dados secundária Olá apresenta o estado dele.</span><span class="sxs-lookup"><span data-stu-id="41f2a-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![O seeding concluída](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="41f2a-132">Inicie uma ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="41f2a-132">Initiate a failover</span></span>

<span data-ttu-id="41f2a-133">base de dados secundária Olá pode ser desativados toobecome Olá primário.</span><span class="sxs-lookup"><span data-stu-id="41f2a-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="41f2a-134">No Olá [portal do Azure](http://portal.azure.com), procurar toohello principal da base de dados na parceria de georreplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="41f2a-135">No painel da base de dados SQL de Olá, selecione **todas as definições** > **georreplicação**.</span><span class="sxs-lookup"><span data-stu-id="41f2a-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="41f2a-136">No Olá **secundárias** lista, selecione de Olá base de dados toobecome Olá nova principal e clique em **ativação pós-falha**.</span><span class="sxs-lookup"><span data-stu-id="41f2a-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![ativação pós-falha](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="41f2a-138">Clique em **Sim** toobegin ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="41f2a-139">comando Olá comutadores imediatamente base de dados secundária Olá na função primária Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="41f2a-140">Não há um curto período de tempo durante os quais não ambas as bases de dados estão disponíveis (na ordem de Olá de 0 too25 segundos) enquanto funções Olá são mudadas.</span><span class="sxs-lookup"><span data-stu-id="41f2a-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="41f2a-141">Se a base de dados primária Olá tem várias bases de dados secundárias, o comando de Olá automaticamente reconfigura Olá outra bases de dados secundárias tooconnect toohello nova principal.</span><span class="sxs-lookup"><span data-stu-id="41f2a-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="41f2a-142">operação todo Olá deve demorar menos de um minuto toocomplete em circunstâncias normais.</span><span class="sxs-lookup"><span data-stu-id="41f2a-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="41f2a-143">Este comando foi concebido para recuperação rápida da base de dados de Olá em caso de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="41f2a-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="41f2a-144">Aciona a ativação pós-falha sem sincronização de dados (forçado a ativação pós-falha).</span><span class="sxs-lookup"><span data-stu-id="41f2a-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="41f2a-145">Se Olá primário está online e ao consolidar transações quando o comando de Olá é emitido alguma perda de dados poderão ocorrer.</span><span class="sxs-lookup"><span data-stu-id="41f2a-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="41f2a-146">Remover a base de dados secundária</span><span class="sxs-lookup"><span data-stu-id="41f2a-146">Remove secondary database</span></span>
<span data-ttu-id="41f2a-147">Esta operação termina permanentemente Olá replicação toohello base de dados secundária e alterações Olá função de Olá tooa secundário regular leitura / escrita da base de dados.</span><span class="sxs-lookup"><span data-stu-id="41f2a-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="41f2a-148">Se Olá conectividade toohello base de dados secundária for interrompida, o comando de Olá é concluída com êxito mas Olá does secundário deixam de ser de leitura / escrita até após o restauro de conectividade.</span><span class="sxs-lookup"><span data-stu-id="41f2a-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="41f2a-149">No Olá [portal do Azure](http://portal.azure.com), procurar toohello principal da base de dados na parceria de georreplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="41f2a-150">Na página de base de dados SQL Olá, selecione **georreplicação**.</span><span class="sxs-lookup"><span data-stu-id="41f2a-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="41f2a-151">No Olá **secundárias** lista, selecione Olá base de dados tooremove da parceria de georreplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="41f2a-152">Clique em **pare a replicação**.</span><span class="sxs-lookup"><span data-stu-id="41f2a-152">Click **Stop Replication**.</span></span>
   
    ![Remover secundário](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="41f2a-154">Será apresentada uma janela de confirmação.</span><span class="sxs-lookup"><span data-stu-id="41f2a-154">A confirmation window opens.</span></span> <span data-ttu-id="41f2a-155">Clique em **Sim** base de dados do tooremove Olá da parceria de georreplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="41f2a-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="41f2a-156">(Defina-o base de dados de leitura e escrita tooa não faz parte de qualquer replicação.)</span><span class="sxs-lookup"><span data-stu-id="41f2a-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="41f2a-157">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="41f2a-157">Next steps</span></span>
* <span data-ttu-id="41f2a-158">toolearn mais informações sobre a replicação geográfica activa, consulte [georreplicação ativa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41f2a-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="41f2a-159">Para cenários e uma descrição geral de continuidade de negócio, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="41f2a-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

