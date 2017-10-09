---
title: "aaaManage computação power no Azure SQL Data Warehouse (portal do Azure) | Microsoft Docs"
description: "Capacidade de computação de toomanage tarefas portal do Azure. Dimensionar os recursos de computação ao ajustar as DWUs. Ou, colocar em pausa e retomar os custos de toosave de recursos de computação."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="19293-105">Gerir a capacidade de computação no Azure SQL Data Warehouse (portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="19293-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19293-106">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="19293-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="19293-107">Portal</span><span class="sxs-lookup"><span data-stu-id="19293-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="19293-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19293-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="19293-109">REST</span><span class="sxs-lookup"><span data-stu-id="19293-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="19293-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="19293-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="19293-111">Capacidade de computação de escala</span><span class="sxs-lookup"><span data-stu-id="19293-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="19293-112">recursos de computação toochange:</span><span class="sxs-lookup"><span data-stu-id="19293-112">toochange compute resources:</span></span>

1. <span data-ttu-id="19293-113">Abra Olá [portal do Azure][Azure portal], abra a sua base de dados e clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="19293-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Clique em escala][1]
2. <span data-ttu-id="19293-115">No painel de escala Olá, mova o controlo de deslize de Olá à esquerda ou definição de DWU toochange Olá botão direito do rato.</span><span class="sxs-lookup"><span data-stu-id="19293-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Mover o controlo de deslize][2]
3. <span data-ttu-id="19293-117">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="19293-117">Click **Save**.</span></span> <span data-ttu-id="19293-118">É apresentada uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="19293-118">A confirmation message appears.</span></span> <span data-ttu-id="19293-119">Clique em **Sim** tooconfirm ou **não** toocancel.</span><span class="sxs-lookup"><span data-stu-id="19293-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Clicar em Guardar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="19293-121">Computação pausa</span><span class="sxs-lookup"><span data-stu-id="19293-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="19293-122">toopause uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="19293-122">toopause a database:</span></span>

1. <span data-ttu-id="19293-123">Abra Olá [portal do Azure] [ Azure portal] e abrir a base de dados.</span><span class="sxs-lookup"><span data-stu-id="19293-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="19293-124">Tenha em atenção que Olá estado é **Online**.</span><span class="sxs-lookup"><span data-stu-id="19293-124">Notice that hello Status is **Online**.</span></span>

    ![Estado online][6]
2. <span data-ttu-id="19293-126">recursos de computação e memória toosuspend, clique em **pausa**, e, em seguida, é apresentada uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="19293-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="19293-127">Clique em **Sim** tooconfirm ou **não** toocancel.</span><span class="sxs-lookup"><span data-stu-id="19293-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirme a colocar em pausa][7]
3. <span data-ttu-id="19293-129">Enquanto o armazém de dados do SQL Server está a iniciar a base de dados de Olá, o estado de Olá é **Pausing**.</span><span class="sxs-lookup"><span data-stu-id="19293-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="19293-130">Quando o estado de Olá é **em pausa**, operação de colocação em pausa Olá é efetuada e já não estão a ser-lhe cobrados dwus.</span><span class="sxs-lookup"><span data-stu-id="19293-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Estado de pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="19293-132">Retomar de computação</span><span class="sxs-lookup"><span data-stu-id="19293-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="19293-133">tooresume uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="19293-133">tooresume a database:</span></span>

1. <span data-ttu-id="19293-134">Abra Olá [portal do Azure] [ Azure portal] e abrir a base de dados.</span><span class="sxs-lookup"><span data-stu-id="19293-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="19293-135">Tenha em atenção que Olá estado é **em pausa**.</span><span class="sxs-lookup"><span data-stu-id="19293-135">Notice that hello Status is **Paused**.</span></span>

    ![Base de dados de pausa][4]
2. <span data-ttu-id="19293-137">Clique em base de dados de Olá tooresume **iniciar**, e, em seguida, é apresentada uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="19293-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="19293-138">Clique em **Sim** tooconfirm ou **não** toocancel.</span><span class="sxs-lookup"><span data-stu-id="19293-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirmar retomar][5]
3. <span data-ttu-id="19293-140">Enquanto o armazém de dados do SQL Server está a iniciar a base de dados de Olá, o estado de Olá é "A retomar".</span><span class="sxs-lookup"><span data-stu-id="19293-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="19293-141">Quando o estado de Olá é **online**, base de dados de Olá está pronto.</span><span class="sxs-lookup"><span data-stu-id="19293-141">When hello status is **online**, hello database is ready.</span></span>

    ![Estado online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="19293-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="19293-143">Next steps</span></span>
<span data-ttu-id="19293-144">Para obter mais informações, consulte [descrição geral da gestão][Management overview].</span><span class="sxs-lookup"><span data-stu-id="19293-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
