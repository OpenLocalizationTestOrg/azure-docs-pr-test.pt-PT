---
title: "aaaMigrate armazenamento toopremium do armazém de dados existentes do Azure | Microsoft Docs"
description: "Instruções para migrar um armazenamento toopremium do armazém de dados existente"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="faea6-103">Migrar o armazenamento de toopremium do armazém de dados</span><span class="sxs-lookup"><span data-stu-id="faea6-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="faea6-104">O Azure SQL Data Warehouse recentemente adicionadas [armazenamento premium para previsão de desempenho superior][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="faea6-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="faea6-105">Os dados existentes armazéns atualmente no armazenamento standard podem agora ser migradas toopremium armazenamento.</span><span class="sxs-lookup"><span data-stu-id="faea6-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="faea6-106">Pode tirar partido da migração automática, ou se preferir toocontrol quando toomigrate (que envolvem algum período de indisponibilidade), pode fazê-lo Olá migração por si.</span><span class="sxs-lookup"><span data-stu-id="faea6-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="faea6-107">Se tiver mais do que um armazém de dados, utilize Olá [agenda migração automática] [ automatic migration schedule] toodetermine quando também será migrada.</span><span class="sxs-lookup"><span data-stu-id="faea6-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="faea6-108">Determinar o tipo de armazenamento</span><span class="sxs-lookup"><span data-stu-id="faea6-108">Determine storage type</span></span>
<span data-ttu-id="faea6-109">Se tiver criado um armazém de dados antes de Olá seguir datas, está atualmente a utilizar armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="faea6-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="faea6-110">**Região**</span><span class="sxs-lookup"><span data-stu-id="faea6-110">**Region**</span></span> | <span data-ttu-id="faea6-111">**Armazém de dados criado antes desta data**</span><span class="sxs-lookup"><span data-stu-id="faea6-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="faea6-112">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="faea6-112">Australia East</span></span> |<span data-ttu-id="faea6-113">Armazenamento Premium ainda não está disponível</span><span class="sxs-lookup"><span data-stu-id="faea6-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="faea6-114">Leste da China</span><span class="sxs-lookup"><span data-stu-id="faea6-114">China East</span></span> |<span data-ttu-id="faea6-115">1 de Novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="faea6-115">November 1, 2016</span></span> |
| <span data-ttu-id="faea6-116">China Norte</span><span class="sxs-lookup"><span data-stu-id="faea6-116">China North</span></span> |<span data-ttu-id="faea6-117">1 de Novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="faea6-117">November 1, 2016</span></span> |
| <span data-ttu-id="faea6-118">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="faea6-118">Germany Central</span></span> |<span data-ttu-id="faea6-119">1 de Novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="faea6-119">November 1, 2016</span></span> |
| <span data-ttu-id="faea6-120">Alemanha Nordeste</span><span class="sxs-lookup"><span data-stu-id="faea6-120">Germany Northeast</span></span> |<span data-ttu-id="faea6-121">1 de Novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="faea6-121">November 1, 2016</span></span> |
| <span data-ttu-id="faea6-122">Índia Ocidental</span><span class="sxs-lookup"><span data-stu-id="faea6-122">India West</span></span> |<span data-ttu-id="faea6-123">Armazenamento Premium ainda não está disponível</span><span class="sxs-lookup"><span data-stu-id="faea6-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="faea6-124">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="faea6-124">Japan West</span></span> |<span data-ttu-id="faea6-125">Armazenamento Premium ainda não está disponível</span><span class="sxs-lookup"><span data-stu-id="faea6-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="faea6-126">EUA Centro-Norte</span><span class="sxs-lookup"><span data-stu-id="faea6-126">North Central US</span></span> |<span data-ttu-id="faea6-127">10 de Novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="faea6-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="faea6-128">Detalhes de migração automática</span><span class="sxs-lookup"><span data-stu-id="faea6-128">Automatic migration details</span></span>
<span data-ttu-id="faea6-129">Por predefinição, iremos migrar a base de dados para si entre as 18:00:00 e 6:00:00 na sua região local durante Olá [agenda migração automática][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="faea6-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="faea6-130">O armazém de dados existente ficará inutilizável durante a migração de Olá.</span><span class="sxs-lookup"><span data-stu-id="faea6-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="faea6-131">migração de Olá irá demorar, aproximadamente, uma hora por com vários terabytes de armazenamento do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="faea6-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="faea6-132">Não será cobrada durante qualquer parte da migração automática Olá.</span><span class="sxs-lookup"><span data-stu-id="faea6-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="faea6-133">Quando Olá migração estiver concluída, o armazém de dados será novamente online e utilizável.</span><span class="sxs-lookup"><span data-stu-id="faea6-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="faea6-134">Microsoft está a demorar Olá os seguintes passos toocomplete Olá, a migração (estes não requerem qualquer envolvimento da sua parte).</span><span class="sxs-lookup"><span data-stu-id="faea6-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="faea6-135">Neste exemplo, imagine que o armazém de dados existente no armazenamento standard atualmente com o nome "MyDW."</span><span class="sxs-lookup"><span data-stu-id="faea6-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="faea6-136">Microsoft muda o nome "MyDW" demasiado "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="faea6-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="faea6-137">Microsoft interrompe "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="faea6-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="faea6-138">Durante este período, foi efetuada uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="faea6-138">During this time, a backup is taken.</span></span> <span data-ttu-id="faea6-139">Poderá ver várias coloca em pausa e retoma se podemos encontre quaisquer problemas durante este processo.</span><span class="sxs-lookup"><span data-stu-id="faea6-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="faea6-140">Microsoft cria um novo armazém de dados com o nome "MyDW" no armazenamento premium da cópia de segurança de Olá executada no passo 2.</span><span class="sxs-lookup"><span data-stu-id="faea6-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="faea6-141">"MyDW" não será apresentado até após a conclusão do restauro Olá.</span><span class="sxs-lookup"><span data-stu-id="faea6-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="faea6-142">Após a conclusão do restauro Olá, "MyDW" devolve toohello mesmos dados do armazém de unidades e de estado (em pausa ou Active Directory) que se encontravam antes da migração de Olá.</span><span class="sxs-lookup"><span data-stu-id="faea6-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="faea6-143">Depois de concluída a migração de Olá, a Microsoft elimina "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="faea6-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="faea6-144">Olá seguintes definições não passa como parte da migração de Olá:</span><span class="sxs-lookup"><span data-stu-id="faea6-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="faea6-145">Auditoria ao nível da base de dados de Olá tem toobe reativada.</span><span class="sxs-lookup"><span data-stu-id="faea6-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="faea6-146">Regras de firewall ao nível da base de dados de Olá necessário toobe adicionado novamente.</span><span class="sxs-lookup"><span data-stu-id="faea6-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="faea6-147">Regras de firewall ao nível do servidor de Olá não são afetadas.</span><span class="sxs-lookup"><span data-stu-id="faea6-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="faea6-148">Agenda de migração automática</span><span class="sxs-lookup"><span data-stu-id="faea6-148">Automatic migration schedule</span></span>
<span data-ttu-id="faea6-149">Migrações automáticas ocorrerem entre as 18:00:00 e 6:00:00 (hora local por região) durante Olá seguinte agenda de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="faea6-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="faea6-150">**Região**</span><span class="sxs-lookup"><span data-stu-id="faea6-150">**Region**</span></span> | <span data-ttu-id="faea6-151">**Data de início estimado**</span><span class="sxs-lookup"><span data-stu-id="faea6-151">**Estimated start date**</span></span> | <span data-ttu-id="faea6-152">**Data de fim estimado**</span><span class="sxs-lookup"><span data-stu-id="faea6-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="faea6-153">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="faea6-153">Australia East</span></span> |<span data-ttu-id="faea6-154">Não determinar ainda</span><span class="sxs-lookup"><span data-stu-id="faea6-154">Not determined yet</span></span> |<span data-ttu-id="faea6-155">Não determinar ainda</span><span class="sxs-lookup"><span data-stu-id="faea6-155">Not determined yet</span></span> |
| <span data-ttu-id="faea6-156">Leste da China</span><span class="sxs-lookup"><span data-stu-id="faea6-156">China East</span></span> |<span data-ttu-id="faea6-157">9 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-157">January 9, 2017</span></span> |<span data-ttu-id="faea6-158">13 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-158">January 13, 2017</span></span> |
| <span data-ttu-id="faea6-159">China Norte</span><span class="sxs-lookup"><span data-stu-id="faea6-159">China North</span></span> |<span data-ttu-id="faea6-160">9 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-160">January 9, 2017</span></span> |<span data-ttu-id="faea6-161">13 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-161">January 13, 2017</span></span> |
| <span data-ttu-id="faea6-162">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="faea6-162">Germany Central</span></span> |<span data-ttu-id="faea6-163">9 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-163">January 9, 2017</span></span> |<span data-ttu-id="faea6-164">13 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-164">January 13, 2017</span></span> |
| <span data-ttu-id="faea6-165">Alemanha Nordeste</span><span class="sxs-lookup"><span data-stu-id="faea6-165">Germany Northeast</span></span> |<span data-ttu-id="faea6-166">9 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-166">January 9, 2017</span></span> |<span data-ttu-id="faea6-167">13 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-167">January 13, 2017</span></span> |
| <span data-ttu-id="faea6-168">Índia Ocidental</span><span class="sxs-lookup"><span data-stu-id="faea6-168">India West</span></span> |<span data-ttu-id="faea6-169">Não determinar ainda</span><span class="sxs-lookup"><span data-stu-id="faea6-169">Not determined yet</span></span> |<span data-ttu-id="faea6-170">Não determinar ainda</span><span class="sxs-lookup"><span data-stu-id="faea6-170">Not determined yet</span></span> |
| <span data-ttu-id="faea6-171">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="faea6-171">Japan West</span></span> |<span data-ttu-id="faea6-172">Não determinar ainda</span><span class="sxs-lookup"><span data-stu-id="faea6-172">Not determined yet</span></span> |<span data-ttu-id="faea6-173">Não determinar ainda</span><span class="sxs-lookup"><span data-stu-id="faea6-173">Not determined yet</span></span> |
| <span data-ttu-id="faea6-174">EUA Centro-Norte</span><span class="sxs-lookup"><span data-stu-id="faea6-174">North Central US</span></span> |<span data-ttu-id="faea6-175">9 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-175">January 9, 2017</span></span> |<span data-ttu-id="faea6-176">13 de Janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="faea6-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="faea6-177">Armazenamento de toopremium migração automática</span><span class="sxs-lookup"><span data-stu-id="faea6-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="faea6-178">Se pretender toocontrol quando o período de indisponibilidade irá ocorrer, pode utilizar Olá seguindo os passos toomigrate um armazém de dados existente do armazenamento de toopremium de armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="faea6-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="faea6-179">Se escolher esta opção, tem de Concluir migração automática Olá antes do início da migração automática Olá nessa região.</span><span class="sxs-lookup"><span data-stu-id="faea6-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="faea6-180">Isto garante que evitar quaisquer risco da migração automática Olá provocando um conflito (consulte toohello [agenda migração automática][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="faea6-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="faea6-181">Instruções de migração automática</span><span class="sxs-lookup"><span data-stu-id="faea6-181">Self-migration instructions</span></span>
<span data-ttu-id="faea6-182">toomigrate os dados do armazém de si próprio, utilizam Olá cópia de segurança e restaurar as funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="faea6-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="faea6-183">Olá restauro parte migração Olá é esperado tootake aproximadamente uma hora por com vários terabytes de armazenamento do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="faea6-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="faea6-184">Se quiser Olá tookeep mesmo nome após a conclusão da migração, siga Olá [toorename passos durante a migração][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="faea6-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="faea6-185">[Colocar em pausa] [ Pause] o armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="faea6-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="faea6-186">Isto leva uma cópia de segurança automática.</span><span class="sxs-lookup"><span data-stu-id="faea6-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="faea6-187">[Restaurar] [ Restore] do seu instantâneo mais recente.</span><span class="sxs-lookup"><span data-stu-id="faea6-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="faea6-188">Elimine o armazém de dados existente no armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="faea6-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="faea6-189">**Se falharem toodo neste passo, será cobrada para ambos os armazéns de dados.**</span><span class="sxs-lookup"><span data-stu-id="faea6-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="faea6-190">Olá seguintes definições não passa como parte da migração de Olá:</span><span class="sxs-lookup"><span data-stu-id="faea6-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="faea6-191">Auditoria ao nível da base de dados de Olá tem toobe reativada.</span><span class="sxs-lookup"><span data-stu-id="faea6-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="faea6-192">Regras de firewall ao nível da base de dados de Olá necessário toobe adicionado novamente.</span><span class="sxs-lookup"><span data-stu-id="faea6-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="faea6-193">Regras de firewall ao nível do servidor de Olá não são afetadas.</span><span class="sxs-lookup"><span data-stu-id="faea6-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="faea6-194">Mudar o nome do armazém de dados durante a migração (opcional)</span><span class="sxs-lookup"><span data-stu-id="faea6-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="faea6-195">Duas bases de dados no mesmo servidor lógico não pode ter de Olá Olá o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="faea6-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="faea6-196">Armazém de dados do SQL Server suporta agora Olá capacidade toorename um armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="faea6-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="faea6-197">Neste exemplo, imagine que o armazém de dados existente no armazenamento standard atualmente com o nome "MyDW."</span><span class="sxs-lookup"><span data-stu-id="faea6-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="faea6-198">Mudar o nome "MyDW" utilizando Olá seguir o comando ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="faea6-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="faea6-199">(Neste exemplo, iremos irá mude o nome "MyDW_BeforeMigration.")  Este comando para todas as transações existentes e tem de ser efetuado no Olá toosucceed de base de dados mestra.</span><span class="sxs-lookup"><span data-stu-id="faea6-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="faea6-200">[Colocar em pausa] [ Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="faea6-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="faea6-201">Isto leva uma cópia de segurança automática.</span><span class="sxs-lookup"><span data-stu-id="faea6-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="faea6-202">[Restaurar] [ Restore] do seu instantâneo mais recente uma nova base de dados com o nome de Olá que utilizado toobe (por exemplo, "MyDW").</span><span class="sxs-lookup"><span data-stu-id="faea6-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="faea6-203">Eliminar "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="faea6-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="faea6-204">**Se falharem toodo neste passo, será cobrada para ambos os armazéns de dados.**</span><span class="sxs-lookup"><span data-stu-id="faea6-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="faea6-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="faea6-205">Next steps</span></span>
<span data-ttu-id="faea6-206">Com Olá alterar toopremium armazenamento, tem também um aumento do número de ficheiros de blob de base de dados na arquitetura subjacente do Olá do seu armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="faea6-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="faea6-207">benefícios de desempenho de Olá toomaximize desta alteração, reconstruir os índices columnstore em cluster utilizando Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="faea6-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="faea6-208">script de Olá funciona forçando alguns dos seus existente blobs adicionais de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="faea6-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="faea6-209">Se não efetuar qualquer ação, dados de Olá naturalmente redistribuir ao longo do tempo como carregados mais dados para as tabelas.</span><span class="sxs-lookup"><span data-stu-id="faea6-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="faea6-210">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="faea6-210">**Prerequisites:**</span></span>

- <span data-ttu-id="faea6-211">Hello do armazém de dados deve ser executada com unidades de armazém de 1000 dados ou superior (consulte [poder de computação de escala][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="faea6-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="faea6-212">Olá utilizador a executar o script de Olá deve estar no Olá [mediumrc função] [ mediumrc role] ou superior.</span><span class="sxs-lookup"><span data-stu-id="faea6-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="faea6-213">tooadd uma função de utilizador de toothis, execute o seguinte Olá:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="faea6-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="faea6-214">Se tiver quaisquer problemas com o armazém de dados, [criar um pedido de suporte] [ create a support ticket] e de referência "armazenamento de toopremium de migração" como uma causa possível Olá.</span><span class="sxs-lookup"><span data-stu-id="faea6-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
