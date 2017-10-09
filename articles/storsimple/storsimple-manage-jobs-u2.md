---
title: aaaView e gerir tarefas do StorSimple | Microsoft Docs
description: "Descreve a página de tarefas de serviço do Olá StorSimple Manager e como toouse, tarefas de cópia de segurança mais recente, atual e agendada tootrack."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="f5e3b-103">Utilize tooview de serviço do StorSimple Manager Olá e gerir tarefas do StorSimple (atualização 2)</span><span class="sxs-lookup"><span data-stu-id="f5e3b-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="f5e3b-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="f5e3b-104">Overview</span></span>
<span data-ttu-id="f5e3b-105">Olá **tarefas** página fornece um único portal central para visualização e gestão de tarefas que foram iniciadas em dispositivos ligados tooyour do serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="f5e3b-106">Pode ver as tarefas agendadas, em execução, concluídas, canceladas e falhadas para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="f5e3b-107">Os resultados são apresentados em formato tabular.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-107">Results are presented in a tabular format.</span></span> 

![Página das tarefas](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="f5e3b-109">Pode encontrar rapidamente tarefas Olá que estão interessadas nas filtrando campos, tais como:</span><span class="sxs-lookup"><span data-stu-id="f5e3b-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="f5e3b-110">**Estado** – tarefas podem estar em execução, concluída, cancelada, com falha, cancelamento ou foi concluída com erros.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="f5e3b-111">**A partir de e para** – tarefas podem ser o intervalo de filtrado Olá com base na data e hora.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="f5e3b-112">**Tipo** – o tipo de tarefa de Olá pode ser a cópia de segurança, restauro, cópia de segurança manual, a ativação pós-falha do dispositivo, e clone volume localmente afixado de criar, modificar o volume, atualizar, suporta pacote ou aprovisionamento do dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="f5e3b-113">**Dispositivos** – tarefas são iniciadas num serviço determinadas tooyour dispositivo ligado.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="f5e3b-114">Olá tarefas são, em seguida, apresentadas numa base de Olá de Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="f5e3b-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="f5e3b-115">**Tipo** – cópia de segurança, restauro, cópia de segurança manual, a ativação pós-falha do dispositivo, e clone volume localmente afixado de criar, modificar o volume, atualizar, suporta pacote ou aprovisionamento do dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="f5e3b-116">**Estado** – em execução, concluída, cancelada, com falha, cancelamento ou foi concluída com erros.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="f5e3b-117">**Entidade** – tarefas Olá podem ser associadas um volume, uma política de cópia de segurança ou um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="f5e3b-118">Por exemplo, uma tarefa de clone está associada um volume, enquanto uma tarefa de cópia de segurança agendada é associada a uma política de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="f5e3b-119">Como resultado de uma recuperação após desastre (DR) ou uma operação de restauro, é criada uma tarefa de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="f5e3b-120">**Dispositivo** – hello nome de dispositivo Olá no qual Olá a tarefa foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="f5e3b-121">**Iniciar** – tempo Olá quando a tarefa de Olá foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="f5e3b-122">**Progresso** – Olá percentagem de conclusão de uma tarefa em execução.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="f5e3b-123">Para uma tarefa concluída, isto deve ser sempre 100%.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="f5e3b-124">lista de Olá de tarefas é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="f5e3b-125">Pode efetuar Olá seguintes ações relacionadas com a tarefa nesta página:</span><span class="sxs-lookup"><span data-stu-id="f5e3b-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="f5e3b-126">Ver detalhes da tarefa</span><span class="sxs-lookup"><span data-stu-id="f5e3b-126">View job details</span></span>
* <span data-ttu-id="f5e3b-127">Cancelar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="f5e3b-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="f5e3b-128">Ver detalhes da tarefa</span><span class="sxs-lookup"><span data-stu-id="f5e3b-128">View job details</span></span>
<span data-ttu-id="f5e3b-129">Efetue Olá os passos tooview Olá detalhes de qualquer tarefa.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="f5e3b-130">Detalhes da tarefa tooview</span><span class="sxs-lookup"><span data-stu-id="f5e3b-130">tooview job details</span></span>
1. <span data-ttu-id="f5e3b-131">No Olá **tarefas** página, apresentar tarefas Olá estão interessadas ao executar uma consulta com filtros adequados.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="f5e3b-132">Pode pesquisar para concluir, em execução ou cancelar tarefas.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="f5e3b-133">Selecione uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-133">Select a job.</span></span>
3. <span data-ttu-id="f5e3b-134">Na Olá parte inferior da página Olá, clique em **detalhes**.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="f5e3b-135">No Olá **detalhes da tarefa de cópia de segurança** caixa de diálogo, pode ver o estado de Olá, detalhes, as estatísticas de tempo e estatísticas de dados.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Página de detalhes da tarefa](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="f5e3b-137">Cancelar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="f5e3b-137">Cancel a job</span></span>
<span data-ttu-id="f5e3b-138">Efetue Olá os seguintes passos toocancel uma tarefa em execução.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="f5e3b-139">Algumas tarefas, tais como modificar um tipo de volume do volume toochange Olá ou expandir um volume, não podem ser canceladas.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="f5e3b-140">toocancel uma tarefa</span><span class="sxs-lookup"><span data-stu-id="f5e3b-140">toocancel a job</span></span>
1. <span data-ttu-id="f5e3b-141">No Olá **tarefas** página, apresentar Olá de tarefas em execução que pretende que toocancel ao executar uma consulta com filtros adequados.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="f5e3b-142">Selecione a tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-142">Select hello job.</span></span>
3. <span data-ttu-id="f5e3b-143">Na Olá parte inferior da página Olá, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="f5e3b-144">Quando lhe for pedida a confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="f5e3b-145">Esta tarefa agora, será cancelada.</span><span class="sxs-lookup"><span data-stu-id="f5e3b-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5e3b-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f5e3b-146">Next steps</span></span>
* <span data-ttu-id="f5e3b-147">Saiba como demasiado[gerir as políticas de cópia de segurança do StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f5e3b-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="f5e3b-148">Saiba como demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f5e3b-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

