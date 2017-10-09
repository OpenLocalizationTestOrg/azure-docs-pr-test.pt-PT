---
title: "aaaSQL simulações de recuperação de desastre de base de dados | Microsoft Docs"
description: "Saiba orientações e melhores práticas para utilizar a SQL Database do Azure tooperform desastre recuperação aprofunda toohelp a mantê o missão aplicações de negócio crítico toofailures resiliente e falhas."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="ff079-103">Efetuar exercício de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="ff079-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="ff079-104">Recomenda-se que a validação da preparação da aplicação para o fluxo de trabalho de recuperação é efetuada periodicamente.</span><span class="sxs-lookup"><span data-stu-id="ff079-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="ff079-105">Comportamento da aplicação Olá verificar e implicações de interrupção de perda de e/ou Olá dados envolve a que a ativação pós-falha é uma boa prática de engenharia.</span><span class="sxs-lookup"><span data-stu-id="ff079-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="ff079-106">Também é um requisito pela maioria das normas da indústria como parte da certificação de continuidade do negócio.</span><span class="sxs-lookup"><span data-stu-id="ff079-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="ff079-107">Efetuar um exercício de recuperação de desastre é composta por:</span><span class="sxs-lookup"><span data-stu-id="ff079-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="ff079-108">Falha de camada de dados simulando</span><span class="sxs-lookup"><span data-stu-id="ff079-108">Simulating data tier outage</span></span>
* <span data-ttu-id="ff079-109">Recuperar</span><span class="sxs-lookup"><span data-stu-id="ff079-109">Recovering</span></span>
* <span data-ttu-id="ff079-110">Validar a recuperação de post de integridade de aplicações</span><span class="sxs-lookup"><span data-stu-id="ff079-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="ff079-111">Dependendo de como pode [concebido a aplicação para a continuidade do negócio](sql-database-business-continuity.md), desagregação de Olá Olá fluxo de trabalho tooexecute pode variar.</span><span class="sxs-lookup"><span data-stu-id="ff079-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="ff079-112">Abaixo, iremos descrevem as melhores práticas de Olá realizar um exercício de recuperação após desastre no contexto de Olá da SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff079-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="ff079-113">Georrestauro</span><span class="sxs-lookup"><span data-stu-id="ff079-113">Geo-restore</span></span>
<span data-ttu-id="ff079-114">tooprevent Olá potencial perda de dados quando realizar um exercício de recuperação após desastre, recomendamos desagregação Olá utilizando um ambiente de teste ao criar uma cópia do ambiente de produção Olá e utilizá-lo a executar o fluxo de trabalho da aplicação Olá tooverify ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="ff079-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="ff079-115">Simulação de falha</span><span class="sxs-lookup"><span data-stu-id="ff079-115">Outage simulation</span></span>
<span data-ttu-id="ff079-116">toosimulate Olá falha, pode eliminar ou mudar o nome da base de dados de origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ff079-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="ff079-117">Isto faz com que as falhas de conectividade de aplicação.</span><span class="sxs-lookup"><span data-stu-id="ff079-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="ff079-118">Recuperação</span><span class="sxs-lookup"><span data-stu-id="ff079-118">Recovery</span></span>
* <span data-ttu-id="ff079-119">Efetuar georrestauro Olá da base de dados de Olá para um servidor diferente, tal como descrito [aqui](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="ff079-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="ff079-120">Alteração Olá aplicação configuração tooconnect toohello recuperado da base de dados e siga Olá [configurar uma base de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ff079-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="ff079-121">Validação</span><span class="sxs-lookup"><span data-stu-id="ff079-121">Validation</span></span>
* <span data-ttu-id="ff079-122">Exercício Olá concluída, verificando recuperação post Olá aplicação integridade (incluindo cadeias de ligação, inícios de sessão, testar a funcionalidade básica ou outro parte validações dos procedimentos de signoffs padrão de aplicação).</span><span class="sxs-lookup"><span data-stu-id="ff079-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="ff079-123">Georreplicação</span><span class="sxs-lookup"><span data-stu-id="ff079-123">Geo-replication</span></span>
<span data-ttu-id="ff079-124">Para uma base de dados que está protegida com desagregação de Olá georreplicação exercício envolve a base de dados secundária do toohello de ativação pós-falha planeada.</span><span class="sxs-lookup"><span data-stu-id="ff079-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="ff079-125">Olá ativação pós-falha planeada garante que Olá primário e as bases de dados secundária Olá permanecerem sincronizadas quando funções Olá são mudadas.</span><span class="sxs-lookup"><span data-stu-id="ff079-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="ff079-126">Ao contrário Olá ativação pós-falha não planeada, esta operação resulta numa perda de dados, modo de desagregação Olá pode ser executada no ambiente de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="ff079-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="ff079-127">Simulação de falha</span><span class="sxs-lookup"><span data-stu-id="ff079-127">Outage simulation</span></span>
<span data-ttu-id="ff079-128">Falha de Olá toosimulate, pode desativar aplicação web de Olá ou toohello base de dados de dados da máquina virtual ligada.</span><span class="sxs-lookup"><span data-stu-id="ff079-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="ff079-129">Isto resulta em falhas de conectividade Olá para clientes de web de Olá.</span><span class="sxs-lookup"><span data-stu-id="ff079-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="ff079-130">Recuperação</span><span class="sxs-lookup"><span data-stu-id="ff079-130">Recovery</span></span>
* <span data-ttu-id="ff079-131">Certifique-se de configuração da aplicação Olá no Olá DR região pontos toohello anterior secundário que fica Olá acessível completamente nova principal.</span><span class="sxs-lookup"><span data-stu-id="ff079-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="ff079-132">Efetuar [a ativação pós-falha planeada](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake Olá secundário base de dados de um novo site primário</span><span class="sxs-lookup"><span data-stu-id="ff079-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="ff079-133">Siga Olá [configurar uma base de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ff079-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="ff079-134">Validação</span><span class="sxs-lookup"><span data-stu-id="ff079-134">Validation</span></span>
* <span data-ttu-id="ff079-135">Exercício Olá concluída, verificando recuperação post Olá aplicação integridade (incluindo cadeias de ligação, inícios de sessão, testar a funcionalidade básica ou outro parte validações dos procedimentos de signoffs padrão de aplicação).</span><span class="sxs-lookup"><span data-stu-id="ff079-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff079-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ff079-136">Next steps</span></span>
* <span data-ttu-id="ff079-137">toolearn sobre cenários de continuidade do negócio, consulte [cenários de continuidade](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="ff079-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="ff079-138">toolearn sobre cópias de segurança automatizada de SQL Database do Azure, consulte [cópias de segurança automatizadas de base de dados SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="ff079-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="ff079-139">toolearn sobre a utilização de cópias de segurança automatizadas para recuperação, consulte [restaurar uma base de dados de cópias de segurança do Olá iniciou o serviço](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="ff079-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="ff079-140">toolearn sobre as opções de recuperação mais rápidas, consulte [georreplicação ativa](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ff079-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
