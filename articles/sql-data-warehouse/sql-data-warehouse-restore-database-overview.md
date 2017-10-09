---
title: "aaaRestore um armazém de dados do Azure - local e georredundante | Microsoft Docs"
description: "Descrição geral das opções de restauro de base de dados de Olá para recuperar uma base de dados no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="0bd44-103">Restauro do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0bd44-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0bd44-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="0bd44-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="0bd44-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="0bd44-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="0bd44-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="0bd44-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="0bd44-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="0bd44-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="0bd44-108">SQL Data Warehouse oferece restauros geográficas tanto locais como parte do respetivo após desastre do armazém de dados capacidades de recuperação.</span><span class="sxs-lookup"><span data-stu-id="0bd44-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="0bd44-109">Utilize toorestore de cópias de segurança para do armazém de dados o restauro de tooa do armazém de dados do ponto na região primária Olá ou utilize cópias de segurança georredundante toorestore tooa diferentes região geográfica.</span><span class="sxs-lookup"><span data-stu-id="0bd44-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="0bd44-110">Este artigo explica especificações Olá restaurar um armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="0bd44-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="0bd44-111">O que é um restauro do armazém de dados?</span><span class="sxs-lookup"><span data-stu-id="0bd44-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="0bd44-112">Um restauro do armazém de dados é um novo armazém de dados que é criado a partir de uma cópia de segurança existente ou do armazém de dados eliminada.</span><span class="sxs-lookup"><span data-stu-id="0bd44-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="0bd44-113">armazém de dados restaurada do Olá recria o armazém de dados de cópia de segurança de Olá num momento específico.</span><span class="sxs-lookup"><span data-stu-id="0bd44-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="0bd44-114">Uma vez que o SQL Data Warehouse é um sistema distribuído, um restauro do armazém de dados é criado a partir de muitos ficheiros de cópia de segurança que são armazenados em blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd44-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="0bd44-115">Restauro da base de dados é uma parte essencial de qualquer estratégia de recuperação de continuidade e desastre negócio porque cria novamente os dados depois de danos acidentais ou eliminação.</span><span class="sxs-lookup"><span data-stu-id="0bd44-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="0bd44-116">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="0bd44-116">For more information, see:</span></span>

* [<span data-ttu-id="0bd44-117">Cópias de segurança do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0bd44-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="0bd44-118">Descrição geral da continuidade de negócio</span><span class="sxs-lookup"><span data-stu-id="0bd44-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="0bd44-119">Pontos de restauro do armazém de dados</span><span class="sxs-lookup"><span data-stu-id="0bd44-119">Data warehouse restore points</span></span>
<span data-ttu-id="0bd44-120">Como uma vantagem de utilizar o Premium Storage do Azure, o SQL Data Warehouse utiliza o Blob de armazenamento do Azure instantâneos toobackup Olá principal do armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="0bd44-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="0bd44-121">Cada instantâneo tiver um ponto de restauro que representa o tempo de Olá instantâneo Olá foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="0bd44-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="0bd44-122">toorestore um armazém de dados, escolha um ponto de restauro e emitir um comando de restauro.</span><span class="sxs-lookup"><span data-stu-id="0bd44-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="0bd44-123">O SQL Data Warehouse sempre restaura Olá tooa cópia de segurança novo armazém de dados.</span><span class="sxs-lookup"><span data-stu-id="0bd44-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="0bd44-124">Pode manter o armazém de dados restaurada do Olá e Olá atual ou elimine um deles.</span><span class="sxs-lookup"><span data-stu-id="0bd44-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="0bd44-125">Se quiser tooreplace Olá atual do armazém de dados com Olá restaurada do armazém de dados, pode alterá-lo.</span><span class="sxs-lookup"><span data-stu-id="0bd44-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="0bd44-126">Se precisar de toorestore um armazém de dados eliminada ou em pausa, pode [criar um pedido de suporte](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="0bd44-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="0bd44-127">Georredundante restauro</span><span class="sxs-lookup"><span data-stu-id="0bd44-127">Geo-redundant restore</span></span>
<span data-ttu-id="0bd44-128">Pode restaurar a sua região tooany do armazém de dados que suportam o Azure SQL Data Warehouse ao seu nível de desempenho que escolheu.</span><span class="sxs-lookup"><span data-stu-id="0bd44-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="0bd44-129">Tenha em atenção que DWU 9000 e 18000 não são suportados em todas as regiões durante a pré-visualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd44-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="0bd44-130">restauro de um georredundante tooperform que tem não optou por fora esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="0bd44-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="0bd44-131">Restaurar a linha cronológica</span><span class="sxs-lookup"><span data-stu-id="0bd44-131">Restore timeline</span></span>
<span data-ttu-id="0bd44-132">Pode restaurar um ponto de restauro disponíveis de tooany de base de dados dentro de Olá últimos sete dias.</span><span class="sxs-lookup"><span data-stu-id="0bd44-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="0bd44-133">Instantâneos de iniciar a cada quatro horas tooeight e estão disponíveis para sete dias.</span><span class="sxs-lookup"><span data-stu-id="0bd44-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="0bd44-134">Quando um instantâneo com mais de sete dias, expirar e o respetivo ponto de restauro já não está disponível.</span><span class="sxs-lookup"><span data-stu-id="0bd44-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="0bd44-135">Restaurar os custos</span><span class="sxs-lookup"><span data-stu-id="0bd44-135">Restore costs</span></span>
<span data-ttu-id="0bd44-136">encargos de armazenamento Olá Olá restaurada do armazém de dados é faturado a taxa de Premium Storage do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd44-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="0bd44-137">Se colocar em pausa de um armazém de dados restaurada, são-lhe cobrados para armazenamento a taxa de Premium Storage do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="0bd44-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="0bd44-138">Olá vantagem colocar em pausa não é que lhe serem cobrados para recursos de informática Olá DWU.</span><span class="sxs-lookup"><span data-stu-id="0bd44-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="0bd44-139">Para obter mais informações sobre preços do SQL Data Warehouse, consulte [preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="0bd44-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="0bd44-140">Utilizações de restauro</span><span class="sxs-lookup"><span data-stu-id="0bd44-140">Uses for restore</span></span>
<span data-ttu-id="0bd44-141">a utilização de primário Olá do restauro do armazém de dados está toorecover dados após a perda acidental de dados ou danos.</span><span class="sxs-lookup"><span data-stu-id="0bd44-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="0bd44-142">Também pode utilizar tooretain de restauro do armazém de dados uma cópia de segurança para mais de sete dias.</span><span class="sxs-lookup"><span data-stu-id="0bd44-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="0bd44-143">Depois de o restauro da cópia de segurança de Olá, que tem o armazém de dados de Olá online e pode colocar em pausa-indefinidamente toosave custos de computação.</span><span class="sxs-lookup"><span data-stu-id="0bd44-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="0bd44-144">base de dados em pausa Olá implica a taxa de Premium Storage do Azure Olá, os encargos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0bd44-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="0bd44-145">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="0bd44-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="0bd44-146">Cenários</span><span class="sxs-lookup"><span data-stu-id="0bd44-146">Scenarios</span></span>
* <span data-ttu-id="0bd44-147">Para obter uma descrição de continuidade do negócio, consulte [descrição geral da continuidade de negócio](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="0bd44-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="0bd44-148">tooperform um armazém de dados restaurar, o restauro utilizando:</span><span class="sxs-lookup"><span data-stu-id="0bd44-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="0bd44-149">Consulte portal, do Azure [restaurar um armazém de dados utilizando Olá portal do Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0bd44-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="0bd44-150">Cmdlets do PowerShell, consulte [restaurar um armazém de dados utilizando cmdlets do PowerShell](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="0bd44-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="0bd44-151">APIs de REST, consulte [restaurar um armazém de dados utilizando Olá REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="0bd44-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
