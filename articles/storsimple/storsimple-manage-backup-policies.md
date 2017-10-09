---
title: "aaaManage as políticas de cópia de segurança do StorSimple | Microsoft Docs"
description: "Explica como pode utilizar toocreate de serviço do StorSimple Manager Olá e gerir cópias de segurança manuais, as agendas de cópia de segurança e retenção de cópias de segurança."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="d8910-103">Utilizar políticas de toomanage de serviço StorSimple Manager do Olá cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="d8910-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="d8910-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="d8910-104">Overview</span></span>
<span data-ttu-id="d8910-105">Este tutorial explica como toouse Olá serviço StorSimple Manager **políticas de cópia de segurança** página toocontrol processos de cópia de segurança e retenção de cópias de segurança para os volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8910-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="d8910-106">Descreve também como toocomplete uma cópia de segurança manual.</span><span class="sxs-lookup"><span data-stu-id="d8910-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="d8910-107">Olá **políticas de cópia de segurança** página permite-lhe políticas de cópia de segurança toomanage e agenda locais e instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d8910-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="d8910-108">(As políticas de cópia de segurança estão tooconfigure utilizados agendas de cópia de segurança e retenção de cópias de segurança para uma coleção de volumes). Políticas de cópia de segurança permitem-lhe tootake um instantâneo de vários volumes em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="d8910-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="d8910-109">Isto significa que as cópias de segurança de Olá criadas por uma política de cópia de segurança serão cópias consistentes com falhas.</span><span class="sxs-lookup"><span data-stu-id="d8910-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="d8910-110">Esta página apresenta uma lista de políticas de cópia de segurança de Olá, os respetivos tipos, volumes Olá associado, número Olá de retenção de cópias de segurança e Olá opção tooenable estas políticas.</span><span class="sxs-lookup"><span data-stu-id="d8910-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="d8910-111">Olá **políticas de cópia de segurança** página também permite-lhe toofilter Olá cópia de segurança políticas existentes por uma ou mais Olá seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="d8910-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="d8910-112">**Nome da política** – hello nome associado Olá política.</span><span class="sxs-lookup"><span data-stu-id="d8910-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="d8910-113">Olá os diferentes tipos de políticas incluem:</span><span class="sxs-lookup"><span data-stu-id="d8910-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="d8910-114">Políticas agendadas, explicitamente são criadas pelo utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="d8910-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="d8910-115">Políticas automáticas, que são criadas quando o momento de Olá de criação de volumes de cópia de segurança do Olá predefinida para esta opção de volume foi ativada.</span><span class="sxs-lookup"><span data-stu-id="d8910-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="d8910-116">Estas políticas são designadas como VolumeName_Default onde o nome do Volume refere-se nome toohello Olá volume StorSimple configurada pelo utilizador Olá Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8910-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="d8910-117">políticas automática Olá resultam em diária instantâneos de nuvem a partir do momento de dispositivo de 22:30.</span><span class="sxs-lookup"><span data-stu-id="d8910-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="d8910-118">Importar políticas, que foram criadas originalmente no Olá Snapshot Manager do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8910-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="d8910-119">Estes tem uma etiqueta que descreve o anfitrião do Olá Snapshot Manager do StorSimple que políticas Olá foram importadas a partir.</span><span class="sxs-lookup"><span data-stu-id="d8910-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="d8910-120">**Volumes** – Olá volumes associados Olá política.</span><span class="sxs-lookup"><span data-stu-id="d8910-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="d8910-121">Todos os volumes de Olá associados uma política de cópia de segurança são agrupados quando forem criadas cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="d8910-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="d8910-122">**Última cópia de segurança com êxito** – Olá data e hora do Olá última cópia de segurança que foi feita com esta política.</span><span class="sxs-lookup"><span data-stu-id="d8910-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="d8910-123">**Cópia de segurança seguinte** – Olá data e hora do Olá próxima cópia de segurança agendada que será iniciada por esta política.</span><span class="sxs-lookup"><span data-stu-id="d8910-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="d8910-124">**As agendas** – Olá diversas agendas associados a política de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8910-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="d8910-125">operações de Olá utilizada frequentemente que pode efetuar nesta página são:</span><span class="sxs-lookup"><span data-stu-id="d8910-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="d8910-126">Adicionar uma política de cópias de segurança</span><span class="sxs-lookup"><span data-stu-id="d8910-126">Add a backup policy</span></span> 
* <span data-ttu-id="d8910-127">Adicionar ou modificar uma agenda</span><span class="sxs-lookup"><span data-stu-id="d8910-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="d8910-128">Eliminar uma política de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="d8910-128">Delete a backup policy</span></span> 
* <span data-ttu-id="d8910-129">Efetuar uma cópia de segurança manual</span><span class="sxs-lookup"><span data-stu-id="d8910-129">Take a manual backup</span></span> 
* <span data-ttu-id="d8910-130">Criar uma política de cópia de segurança personalizada com vários volumes e agendas</span><span class="sxs-lookup"><span data-stu-id="d8910-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="d8910-131">Adicionar uma política de cópias de segurança</span><span class="sxs-lookup"><span data-stu-id="d8910-131">Add a backup policy</span></span>
<span data-ttu-id="d8910-132">Adicione uma agenda de tooautomatically de política de cópia de segurança as cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="d8910-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="d8910-133">Efetue Olá os seguintes passos no Olá tooadd portal clássico do Azure uma política de cópia de segurança para o dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8910-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="d8910-134">Depois de adicionar política Olá, pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="d8910-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="d8910-135">![Vídeo disponível](./media/storsimple-manage-backup-policies/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="d8910-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="d8910-136">toowatch um vídeo que demonstra como toocreate local ou na nuvem de cópia de segurança política, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="d8910-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="d8910-137">Adicionar ou modificar uma agenda</span><span class="sxs-lookup"><span data-stu-id="d8910-137">Add or modify a schedule</span></span>
<span data-ttu-id="d8910-138">Pode adicionar ou modificar uma agenda de cópia de segurança de política existente anexado tooan no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8910-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="d8910-139">Execute Olá os seguintes passos no Olá tooadd de portal clássico do Azure ou modificar uma agenda.</span><span class="sxs-lookup"><span data-stu-id="d8910-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="d8910-140">Eliminar uma política de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="d8910-140">Delete a backup policy</span></span>
<span data-ttu-id="d8910-141">Efetue Olá os seguintes passos no Olá toodelete portal clássico do Azure uma política de cópia de segurança no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8910-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="d8910-142">Efetuar uma cópia de segurança manual</span><span class="sxs-lookup"><span data-stu-id="d8910-142">Take a manual backup</span></span>
<span data-ttu-id="d8910-143">Efetue Olá os seguintes passos no Olá toocreate portal clássico do Azure uma pedido () cópia de segurança manual de um único volume.</span><span class="sxs-lookup"><span data-stu-id="d8910-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="d8910-144">Criar uma política de cópia de segurança personalizada com vários volumes e agendas</span><span class="sxs-lookup"><span data-stu-id="d8910-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="d8910-145">Execute os seguintes passos no Olá toocreate portal clássico do Azure uma política de cópia de segurança personalizada que tenha vários volumes e agendas de Olá.</span><span class="sxs-lookup"><span data-stu-id="d8910-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="d8910-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d8910-146">Next steps</span></span>
<span data-ttu-id="d8910-147">Saiba mais sobre [utilizando Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d8910-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

