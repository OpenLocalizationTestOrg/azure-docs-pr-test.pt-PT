---
title: aaaRestore Azure SQL Data Warehouse (portal do Azure) | Microsoft Docs
description: Tarefas do portais do Azure para restaurar o Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="357b5-103">Restaurar o Azure SQL Data Warehouse (portal)</span><span class="sxs-lookup"><span data-stu-id="357b5-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="357b5-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="357b5-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="357b5-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="357b5-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="357b5-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="357b5-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="357b5-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="357b5-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="357b5-108">Neste artigo, ficará a saber como toorestore Azure SQL Data Warehouse, utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="357b5-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="357b5-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="357b5-109">Before you begin</span></span>
<span data-ttu-id="357b5-110">**Certifique-se a capacidade DTU.**</span><span class="sxs-lookup"><span data-stu-id="357b5-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="357b5-111">Cada instância do SQL Data Warehouse está hospedada num servidor de SQL Server (por exemplo, myserver.database.windows.net) que tem uma quota de (DTU) de unidade de débito de dados predefinida.</span><span class="sxs-lookup"><span data-stu-id="357b5-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="357b5-112">Antes, pode restaurar o SQL Data Warehouse, certifique-se de que o servidor SQL tem suficiente restante quota de DTU de base de dados Olá que está a restaurar.</span><span class="sxs-lookup"><span data-stu-id="357b5-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="357b5-113">toolearn como quota de DTU toocalculate ou toorequest mais DTUs, consulte [pedir uma alteração de quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="357b5-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="357b5-114">Restaurar uma base de dados do Active Directory ou em pausa</span><span class="sxs-lookup"><span data-stu-id="357b5-114">Restore an active or paused database</span></span>
<span data-ttu-id="357b5-115">toorestore uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="357b5-115">toorestore a database:</span></span>

1. <span data-ttu-id="357b5-116">Inicie sessão no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="357b5-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="357b5-117">No painel esquerdo Olá, selecione **procurar**e, em seguida, selecione **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="357b5-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="357b5-119">Localizar o servidor e, em seguida, selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="357b5-119">Find your server, and then select it.</span></span>

    ![Selecione o seu servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="357b5-121">Localize a instância de Olá do armazém de dados do SQL Server que pretende toorestore do e, em seguida, selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="357b5-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Selecione Olá instância do SQL Data Warehouse toorestore](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="357b5-123">Olá parte superior do painel de armazém de dados de Olá, selecione **restaurar**.</span><span class="sxs-lookup"><span data-stu-id="357b5-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Selecione o restauro](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="357b5-125">Especifique um novo **nome de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="357b5-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="357b5-126">Selecione Olá mais recente **ponto de restauro**.</span><span class="sxs-lookup"><span data-stu-id="357b5-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="357b5-127">Certifique-se de que escolhe o último ponto de restauro Olá.</span><span class="sxs-lookup"><span data-stu-id="357b5-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="357b5-128">Porque os pontos de restauro são apresentados na hora Universal Coordenada (UTC), opção predefinida de Olá poderá não ser o ponto de restauro mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="357b5-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Selecione um ponto de restauro](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="357b5-130">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="357b5-130">Select **OK**.</span></span>
9. <span data-ttu-id="357b5-131">processo de restauro de base de dados de Olá começará e pode utilizar **notificações** processo de Olá toomonitor.</span><span class="sxs-lookup"><span data-stu-id="357b5-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="357b5-132">Depois de terminar o restauro de Olá, pode configurar a base de dados recuperada, seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="357b5-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="357b5-133">Restaurar uma base de dados eliminada</span><span class="sxs-lookup"><span data-stu-id="357b5-133">Restore a deleted database</span></span>
<span data-ttu-id="357b5-134">toorestore uma base de dados eliminada:</span><span class="sxs-lookup"><span data-stu-id="357b5-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="357b5-135">Inicie sessão no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="357b5-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="357b5-136">No painel esquerdo Olá, selecione **procurar**e, em seguida, selecione **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="357b5-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="357b5-138">Localizar o servidor e, em seguida, selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="357b5-138">Find your server, and then select it.</span></span>

    ![Selecione o seu servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="357b5-140">Desloque para baixo toohello **operações** secção no painel do seu servidor.</span><span class="sxs-lookup"><span data-stu-id="357b5-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="357b5-141">Selecione Olá **eliminou bases de dados** mosaico.</span><span class="sxs-lookup"><span data-stu-id="357b5-141">Select hello **Deleted databases** tile.</span></span>

    ![Selecione o mosaico de bases de dados do Olá eliminado](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="357b5-143">Selecione Olá eliminado da base de dados que pretende que o toorestore.</span><span class="sxs-lookup"><span data-stu-id="357b5-143">Select hello deleted database that you want toorestore.</span></span>

    ![Selecione um toorestore de base de dados](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="357b5-145">Especifique um novo **nome de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="357b5-145">Specify a new **Database name**.</span></span>

    ![Adicionar um nome de base de dados de Olá](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="357b5-147">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="357b5-147">Select **OK**.</span></span>
9. <span data-ttu-id="357b5-148">processo de restauro de base de dados de Olá começará e pode utilizar **notificações** processo de Olá toomonitor.</span><span class="sxs-lookup"><span data-stu-id="357b5-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="357b5-149">tooconfigure a base de dados depois de terminar o restauro de Olá, consulte [configurar a base de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="357b5-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="357b5-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="357b5-150">Next steps</span></span>
<span data-ttu-id="357b5-151">toolearn sobre as funcionalidades de continuidade de negócio Olá das edições do SQL Database do Azure, leia Olá [descrição geral da continuidade de negócio da linha de base de dados do Azure SQL][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="357b5-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
