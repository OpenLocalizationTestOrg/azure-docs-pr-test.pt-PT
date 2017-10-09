---
title: aaaRestore um Azure SQL Data Warehouse (REST API) | Microsoft Docs
description: Tarefas da REST API para restaurar um Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="ddaff-103">Restaurar um armazém de dados SQL do Azure (REST API)</span><span class="sxs-lookup"><span data-stu-id="ddaff-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ddaff-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="ddaff-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="ddaff-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="ddaff-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="ddaff-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ddaff-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="ddaff-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="ddaff-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="ddaff-108">Neste artigo, ficará a saber como toorestore um Azure SQL Data Warehouse, utilizando Olá REST API.</span><span class="sxs-lookup"><span data-stu-id="ddaff-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ddaff-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ddaff-109">Before you begin</span></span>
<span data-ttu-id="ddaff-110">**Certifique-se a capacidade DTU.**</span><span class="sxs-lookup"><span data-stu-id="ddaff-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="ddaff-111">Cada SQL Data Warehouse for alojado por um servidor de SQL Server (por exemplo, myserver.database.windows.net) tem uma quota DTU predefinido.</span><span class="sxs-lookup"><span data-stu-id="ddaff-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="ddaff-112">Antes de pode restaurar um SQL Data Warehouse, certifique-se que Olá que do SQL server tem suficiente restante quota de DTU para base de dados de Olá seja restaurado.</span><span class="sxs-lookup"><span data-stu-id="ddaff-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="ddaff-113">toolearn como toocalculate DTU necessário ou toorequest DTU mais, consulte [pedir uma alteração de quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="ddaff-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="ddaff-114">Restaurar uma base de dados do Active Directory ou em pausa</span><span class="sxs-lookup"><span data-stu-id="ddaff-114">Restore an active or paused database</span></span>
<span data-ttu-id="ddaff-115">toorestore uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="ddaff-115">toorestore a database:</span></span>

1. <span data-ttu-id="ddaff-116">Obter a lista de Olá de pontos de restauro de base de dados utilizando a operação de pontos de restauro de base de dados de Get Olá.</span><span class="sxs-lookup"><span data-stu-id="ddaff-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="ddaff-117">Iniciar o restauro utilizando Olá [criar pedido de restauro de base de dados] [ Create database restore request] operação.</span><span class="sxs-lookup"><span data-stu-id="ddaff-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="ddaff-118">Controlar o estado de Olá do seu restauro utilizando Olá [base de dados de estado da operação] [ Database operation status] operação.</span><span class="sxs-lookup"><span data-stu-id="ddaff-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="ddaff-119">Depois de concluir o restauro de Olá, pode configurar a base de dados recuperada seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="ddaff-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="ddaff-120">Restaurar uma base de dados eliminada</span><span class="sxs-lookup"><span data-stu-id="ddaff-120">Restore a deleted database</span></span>
<span data-ttu-id="ddaff-121">toorestore uma base de dados eliminada:</span><span class="sxs-lookup"><span data-stu-id="ddaff-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="ddaff-122">Lista todas as bases de dados eliminadas que possam ser restauradas utilizando Olá [lista que possam ser restaurada remover bases de dados] [ List restorable dropped databases] operação.</span><span class="sxs-lookup"><span data-stu-id="ddaff-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="ddaff-123">Detalhes do obter Olá para Olá eliminar base de dados toorestore utilizando Olá [Get que possam ser restaurada removido da base de dados] [ Get restorable dropped database] operação.</span><span class="sxs-lookup"><span data-stu-id="ddaff-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="ddaff-124">Iniciar o restauro utilizando Olá [criar pedido de restauro de base de dados] [ Create database restore request] operação.</span><span class="sxs-lookup"><span data-stu-id="ddaff-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="ddaff-125">Controlar o estado de Olá do seu restauro utilizando Olá [base de dados de estado da operação] [ Database operation status] operação.</span><span class="sxs-lookup"><span data-stu-id="ddaff-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="ddaff-126">tooconfigure a base de dados depois de concluir o restauro de Olá, consulte [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="ddaff-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ddaff-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ddaff-127">Next steps</span></span>
<span data-ttu-id="ddaff-128">toolearn sobre as funcionalidades de continuidade de negócio Olá das edições do SQL Database do Azure, leia Olá [descrição geral da continuidade de negócio da linha de base de dados do Azure SQL][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="ddaff-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
