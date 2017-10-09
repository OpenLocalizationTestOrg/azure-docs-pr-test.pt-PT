---
title: "aaaStore SQL Database do Azure cópias de segurança para cópia de segurança too10 anos | Microsoft Docs"
description: "Saiba como o SQL Database do Azure suporta armazenar cópias de segurança para cópia de segurança too10 anos."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="36cb3-103">Armazenar a base de dados do Azure SQL cópias de segurança para cópia de segurança too10 anos</span><span class="sxs-lookup"><span data-stu-id="36cb3-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="36cb3-104">Muitas aplicações terem regulamentação, conformidade ou de outras empresas fins que necessitam que tooretain cópias de segurança de base de dados para além de Olá dias 7-35 fornecidos pelo SQL Database do Azure [cópias de segurança automáticas](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="36cb3-105">Ao utilizar a funcionalidade de cópia de segurança de retenção de longo prazo Olá, pode armazenar as cópias de segurança de base de dados do SQL Server num cofre dos serviços de recuperação do Azure para cópia de segurança too10 anos.</span><span class="sxs-lookup"><span data-stu-id="36cb3-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="36cb3-106">Pode armazenar cópias de segurança too1, 000 bases de dados por cofre.</span><span class="sxs-lookup"><span data-stu-id="36cb3-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="36cb3-107">Em seguida, pode selecionar qualquer cópia de segurança na Olá cofre toorestore-o como uma nova base de dados.</span><span class="sxs-lookup"><span data-stu-id="36cb3-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36cb3-108">Retenção de cópias de segurança de longa duração está atualmente em pré-visualização e está disponível no Olá seguintes regiões: Leste da Austrália, Sudeste da Austrália, sul do Brasil, EUA Central, Ásia Oriental, EUA leste, EUA Leste 2, Índia Central, Sul da Índia, leste do Japão, oeste do Japão, Norte Central dos EUA, Norte Europa, EUA Centro-Sul, Sudeste asiático, Europa Ocidental e EUA oeste.</span><span class="sxs-lookup"><span data-stu-id="36cb3-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="36cb3-109">Pode ativar a cópia de segurança too200 bases de dados por cofre durante um período de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="36cb3-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="36cb3-110">Recomendamos que utilize um cofre separado para cada servidor toominimize Olá impacto este limite.</span><span class="sxs-lookup"><span data-stu-id="36cb3-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="36cb3-111">Como funciona a retenção de cópias de segurança de longa duração de base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="36cb3-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="36cb3-112">Com retenção de cópias de segurança de longo prazo, pode associar um servidor de base de dados SQL com um cofre dos serviços de recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="36cb3-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="36cb3-113">Tem de criar cofre Olá no Olá mesma subscrição do Azure que criar do SQL Server de Olá e no Olá mesmo grupo de recursos e a região geográfico.</span><span class="sxs-lookup"><span data-stu-id="36cb3-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="36cb3-114">Em seguida, configure uma política de retenção para uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="36cb3-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="36cb3-115">Olá política causas Olá semanal completa da base de dados cópias de segurança toobe copiado toohello Cofre de serviços de recuperação e retidos por período de retenção especificado Olá (cópia de segurança too10 anos).</span><span class="sxs-lookup"><span data-stu-id="36cb3-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="36cb3-116">Em seguida, pode restaurar a base de dados de Olá de qualquer um destas cópias de segurança tooa nova base de dados em qualquer servidor na subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="36cb3-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="36cb3-117">Armazenamento do Azure cria uma cópia de cópias de segurança existentes e cópia de Olá não tem nenhum impacto no desempenho na base de dados existente Olá.</span><span class="sxs-lookup"><span data-stu-id="36cb3-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="36cb3-118">Para um tooguide como, consulte [configurar e restauro a partir da retenção de cópias de segurança de longa duração de base de dados do Azure SQL](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="36cb3-119">Ativar a retenção de cópias de segurança de longa duração</span><span class="sxs-lookup"><span data-stu-id="36cb3-119">Enable long-term backup retention</span></span>

<span data-ttu-id="36cb3-120">tooconfigure cópia de segurança retenção de longo prazo para uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="36cb3-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="36cb3-121">Criar um cofre dos serviços de recuperação do Azure no Olá mesmo grupo de recurso, de subscrição e região que o servidor de base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="36cb3-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="36cb3-122">Registe o Cofre de toohello Olá servidor.</span><span class="sxs-lookup"><span data-stu-id="36cb3-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="36cb3-123">Crie uma política de proteção do Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="36cb3-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="36cb3-124">Aplica Olá proteção política toohello bases de dados que necessitam de retenção de cópias de segurança de longa duração.</span><span class="sxs-lookup"><span data-stu-id="36cb3-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="36cb3-125">tooconfigure, gerir e restaurar uma base de dados de retenção de cópias de segurança de longa duração das cópias de segurança automatizadas num cofre dos serviços de recuperação do Azure, efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="36cb3-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="36cb3-126">Olá, utilizando o portal do Azure: clique em **retenção de cópias de segurança de longa duração**, selecione uma base de dados e, em seguida, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="36cb3-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selecione uma base de dados para a retenção de cópias de segurança de longa duração](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="36cb3-128">Através do PowerShell: Aceda demasiado[configurar e restauro a partir da retenção de cópias de segurança de longa duração de base de dados do Azure SQL](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="36cb3-129">Restaurar uma base de dados que é armazenado com funcionalidade de cópia de segurança de retenção de longo prazo Olá</span><span class="sxs-lookup"><span data-stu-id="36cb3-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="36cb3-130">toorecover de uma cópia de segurança de retenção de cópias de segurança longo prazo:</span><span class="sxs-lookup"><span data-stu-id="36cb3-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="36cb3-131">Cofre do Olá de lista onde está armazenada a cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="36cb3-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="36cb3-132">Lista Olá contentor servidor lógico tooyour mapeada.</span><span class="sxs-lookup"><span data-stu-id="36cb3-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="36cb3-133">Origem de dados de Olá de lista no Cofre de Olá que é mapeado tooyour base de dados.</span><span class="sxs-lookup"><span data-stu-id="36cb3-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="36cb3-134">Lista Olá pontos de recuperação que estão disponível toorestore.</span><span class="sxs-lookup"><span data-stu-id="36cb3-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="36cb3-135">Restaure a base de dados de Olá Olá recuperação ponto toohello do servidor de destino na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="36cb3-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="36cb3-136">tooconfigure, gerir e restaurar uma base de dados de retenção de cópias de segurança de longa duração das cópias de segurança automatizadas num cofre dos serviços de recuperação do Azure, efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="36cb3-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="36cb3-137">Olá, utilizando o portal do Azure: aceda demasiado[gerir longo prazo retenção de cópias de segurança utilizando Olá portal do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="36cb3-138">Através do PowerShell: Aceda demasiado[gerir retenção de cópias de segurança de longo prazo com o PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="36cb3-139">Obter o preço da retenção de cópias de segurança de longa duração</span><span class="sxs-lookup"><span data-stu-id="36cb3-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="36cb3-140">Retenção de cópias de segurança de longa duração de uma base de dados do SQL Server é cobrada de acordo com toohello [serviços de cópia de segurança do Azure, taxas de preços](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="36cb3-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="36cb3-141">Depois do servidor de base de dados do SQL Server Olá toohello registado cofre, são-lhe cobrados para armazenamento total Olá que é utilizado pelo Olá semanal cópias de segurança armazenadas no Cofre de Olá.</span><span class="sxs-lookup"><span data-stu-id="36cb3-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="36cb3-142">Vista disponíveis cópias de segurança que são armazenadas na retenção de cópias de segurança de longa duração</span><span class="sxs-lookup"><span data-stu-id="36cb3-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="36cb3-143">tooconfigure, gerir e restaurar uma base de dados de retenção de cópias de segurança de longa duração das cópias de segurança automatizadas num cofre do Azure Recovery Services utilizando Olá portal do Azure, efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="36cb3-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="36cb3-144">Olá, utilizando o portal do Azure: aceda demasiado[gerir longo prazo retenção de cópias de segurança utilizando Olá portal do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="36cb3-145">Através do PowerShell: Aceda demasiado[gerir retenção de cópias de segurança de longo prazo com o PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="36cb3-146">Desativar a retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="36cb3-146">Disable long-term retention</span></span>

<span data-ttu-id="36cb3-147">serviço de recuperação Olá automaticamente processa limpeza Olá de cópias de segurança com base no Olá fornecido a política de retenção.</span><span class="sxs-lookup"><span data-stu-id="36cb3-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="36cb3-148">toostop envio Olá cópias de segurança para um cofre de toohello de base de dados específica, remova a política de retenção de Olá para essa base de dados.</span><span class="sxs-lookup"><span data-stu-id="36cb3-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="36cb3-149">as cópias de segurança de Olá que já estão num cofre Olá não são afetadas.</span><span class="sxs-lookup"><span data-stu-id="36cb3-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="36cb3-150">Estes são eliminados automaticamente pelo serviço de recuperação Olá quando o respetivo período de retenção expira.</span><span class="sxs-lookup"><span data-stu-id="36cb3-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="36cb3-151">Retenção de cópias de segurança de longa duração FAQ</span><span class="sxs-lookup"><span data-stu-id="36cb3-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="36cb3-152">**Posso manualmente a eliminar as cópias de segurança específicas no Cofre de Olá?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="36cb3-153">Atualmente não.</span><span class="sxs-lookup"><span data-stu-id="36cb3-153">Not currently.</span></span> <span data-ttu-id="36cb3-154">cofre Olá limpa automaticamente cópias de segurança quando o período de retenção de Olá expirou.</span><span class="sxs-lookup"><span data-stu-id="36cb3-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="36cb3-155">**Pode registar os meus toomore de cópias de segurança do servidor toostore que um cofre?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="36cb3-156">Não, atualmente, pode armazenar um cofre de cópias de segurança tooonly cada vez.</span><span class="sxs-lookup"><span data-stu-id="36cb3-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="36cb3-157">**Posso ter um cofre e o servidor em diferentes subscrições?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="36cb3-158">Não, atualmente Olá cofre e o servidor tem de constar Olá mesmo grupo de recursos e de subscrição.</span><span class="sxs-lookup"><span data-stu-id="36cb3-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="36cb3-159">**Pode utilizar um cofre que criar numa região diferente da região do meu servidor?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="36cb3-160">Não, Olá cofre e o servidor tem de ser Olá mesma região toominimize copiar tempo e evitar custos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="36cb3-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="36cb3-161">**Como muitas bases de dados pode armazenar um cofre?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="36cb3-162">Atualmente, fornecemos suporte cópias de segurança too1, 000 bases de dados por cofre.</span><span class="sxs-lookup"><span data-stu-id="36cb3-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="36cb3-163">**Quantos cofres pode criar por subscrição**</span><span class="sxs-lookup"><span data-stu-id="36cb3-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="36cb3-164">Pode criar cópias de segurança too25 cofres por subscrição.</span><span class="sxs-lookup"><span data-stu-id="36cb3-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="36cb3-165">**Como muitas bases de dados pode configurar por dia por Cofre?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="36cb3-166">Pode configurar 200 bases de dados por dia por cofre.</span><span class="sxs-lookup"><span data-stu-id="36cb3-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="36cb3-167">**Retenção de cópias de segurança de longa duração funciona com conjuntos elásticos?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="36cb3-168">Sim.</span><span class="sxs-lookup"><span data-stu-id="36cb3-168">Yes.</span></span> <span data-ttu-id="36cb3-169">Qualquer base de dados no agrupamento de Olá pode ser configurado com a política de retenção de Olá.</span><span class="sxs-lookup"><span data-stu-id="36cb3-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="36cb3-170">**Pode escolher em que é criada a cópia de segurança de Olá de tempo de Olá?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="36cb3-171">Não, a base de dados SQL controla Olá agenda de cópia de segurança toominimize Olá impacto no desempenho nas suas bases de dados.</span><span class="sxs-lookup"><span data-stu-id="36cb3-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="36cb3-172">**Tenho a encriptação transparente de dados ativada para a minha base de dados. Posso utilizá-lo com o Cofre de Olá?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="36cb3-173">Sim, a encriptação transparente de dados é suportada.</span><span class="sxs-lookup"><span data-stu-id="36cb3-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="36cb3-174">Pode restaurar a base de dados de Olá do Cofre de Olá, mesmo se a base de dados original Olá já não existe.</span><span class="sxs-lookup"><span data-stu-id="36cb3-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="36cb3-175">**O que acontece com as cópias de segurança de Olá no Cofre de Olá minha subscrição está suspensa?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="36cb3-176">Se a sua subscrição está suspensa, vamos manter bases de dados existente do Olá e cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="36cb3-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="36cb3-177">Novas cópias de segurança não são copiados toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="36cb3-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="36cb3-178">Após reativar subscrição Olá, o serviço Olá retoma de cópias de segurança toohello Cofre de cópia.</span><span class="sxs-lookup"><span data-stu-id="36cb3-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="36cb3-179">O Cofre torna-se operações de restauro toohello acessível através da utilização de cópias de segurança de Olá que foram copiadas existe antes de subscrição de Olá foi suspenso.</span><span class="sxs-lookup"><span data-stu-id="36cb3-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="36cb3-180">**Posso obter acesso ficheiros de cópia de segurança de base de dados do toohello SQL para que posso pode transferir ou restaurá-las do SQL Server de toohello?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="36cb3-181">Não, atualmente não.</span><span class="sxs-lookup"><span data-stu-id="36cb3-181">No, not currently.</span></span>

<span data-ttu-id="36cb3-182">**É possível toohave várias agendas (diariamente, semanalmente, mensalmente, anualmente) dentro de uma política de retenção do SQL Server.**</span><span class="sxs-lookup"><span data-stu-id="36cb3-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="36cb3-183">Não, vários agendamentos atualmente só estão disponíveis para cópias de segurança da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="36cb3-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="36cb3-184">**E se configuramos retenção de cópias de segurança de longa duração numa base de dados que é uma base de dados secundária georreplicação ativa?**</span><span class="sxs-lookup"><span data-stu-id="36cb3-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="36cb3-185">Uma vez que não fazer cópias de segurança em réplicas, atualmente não é efectuada nenhuma opção para a retenção de cópias de segurança de longa duração em bases de dados secundárias.</span><span class="sxs-lookup"><span data-stu-id="36cb3-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="36cb3-186">No entanto, é importante para os utilizadores tooset segurança de retenção de cópias de segurança de longa duração numa base de dados secundária georreplicação ativa para estes motivos:</span><span class="sxs-lookup"><span data-stu-id="36cb3-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="36cb3-187">Quando ocorre uma ativação pós-falha e a base de dados de Olá torna-se uma base de dados primária, iremos efetuar um completo cópia de segurança, que é carregado toovault.</span><span class="sxs-lookup"><span data-stu-id="36cb3-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="36cb3-188">Não há nenhum extra de cliente de toohello custo para configurar a retenção de cópias de segurança de longa duração numa base de dados secundária.</span><span class="sxs-lookup"><span data-stu-id="36cb3-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36cb3-189">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="36cb3-189">Next steps</span></span>
<span data-ttu-id="36cb3-190">Porque as cópias de segurança da base de dados proteger os dados de danos acidentais ou eliminação, se estiver a uma parte essencial dos quaisquer continuidade do negócio e a estratégia de recuperação após desastre.</span><span class="sxs-lookup"><span data-stu-id="36cb3-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="36cb3-191">toolearn sobre Olá outras soluções de continuidade do negócio da base de dados SQL, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="36cb3-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
