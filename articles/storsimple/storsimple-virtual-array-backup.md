---
title: "tutorial de cópia de segurança de matriz Virtual do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Descreve como partilha tooback segurança matriz Virtual StorSimple e volumes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="efd72-103">Criar cópias de segurança partilhas ou volumes na sua matriz de Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="efd72-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="efd72-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="efd72-104">Overview</span></span>

<span data-ttu-id="efd72-105">Olá matriz Virtual StorSimple é um híbridos na nuvem no local virtual dispositivo de armazenamento que podem ser configurados como um servidor de ficheiros ou um servidor de iSCSI.</span><span class="sxs-lookup"><span data-stu-id="efd72-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="efd72-106">matriz virtual Olá permite cópias de segurança agendadas e manuais de todos os volumes ou partilhas de Olá Olá toocreate de utilizador no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="efd72-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="efd72-107">Quando configurado como um servidor de ficheiros, também permite a recuperação ao nível do item.</span><span class="sxs-lookup"><span data-stu-id="efd72-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="efd72-108">Este tutorial descreve como toocreate agendada e cópias de segurança manuais e efetuar a recuperação ao nível do item toorestore um ficheiro na sua matriz virtual eliminado.</span><span class="sxs-lookup"><span data-stu-id="efd72-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="efd72-109">Este tutorial aplica-se toohello StorSimple Virtual matrizes só.</span><span class="sxs-lookup"><span data-stu-id="efd72-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="efd72-110">Para informações sobre 8000 série, visite demasiado[criar uma cópia de segurança para o dispositivo da 8000 série](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="efd72-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="efd72-111">Cópia de segurança de partilhas e os volumes</span><span class="sxs-lookup"><span data-stu-id="efd72-111">Back up shares and volumes</span></span>

<span data-ttu-id="efd72-112">As cópias de segurança fornecem proteção de ponto no tempo, melhorar a capacidade de recuperação e minimizar os tempos de restauro de volumes e partilhas.</span><span class="sxs-lookup"><span data-stu-id="efd72-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="efd72-113">Pode efetuar cópias de segurança de uma partilha ou volume no dispositivo StorSimple de duas formas: **agendada** ou **Manual**.</span><span class="sxs-lookup"><span data-stu-id="efd72-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="efd72-114">Cada um dos métodos de Olá é abordada em Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="efd72-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="efd72-115">Hora de início de cópia de segurança de Olá de alteração</span><span class="sxs-lookup"><span data-stu-id="efd72-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="efd72-116">Nesta versão, as cópias de segurança agendadas são criadas por uma política predefinida que é executada diariamente a uma determinada hora e efetua cópias de segurança de todos os volumes ou partilhas de Olá no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="efd72-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="efd72-117">Não é possível toocreate políticas personalizadas para cópias de segurança agendadas neste momento.</span><span class="sxs-lookup"><span data-stu-id="efd72-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="efd72-118">A matriz de Virtual StorSimple tem uma política de cópia de segurança predefinida que inicia a uma determinada hora do dia (22:30) e efetua uma cópia de segurança de todos os volumes ou partilhas de Olá no dispositivo Olá uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="efd72-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="efd72-119">Pode alterar o tempo de Olá que começa de cópia de segurança Olá, mas frequência Olá e Olá retenção (que especifica o número de Olá de cópias de segurança tooretain) não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="efd72-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="efd72-120">Durante estas cópias de segurança, o dispositivo virtual completo de Olá é uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="efd72-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="efd72-121">Isto foi potencialmente afetar o desempenho de Olá do dispositivo Olá e afetam as cargas de trabalho de Olá implementadas no dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="efd72-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="efd72-122">Por conseguinte, recomendamos que agende estas cópias de segurança para as horas de ponta.</span><span class="sxs-lookup"><span data-stu-id="efd72-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="efd72-123">a cópia de segurança predefinida de Olá toochange hora de início, execute Olá os seguintes passos no Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="efd72-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="efd72-124">Olá toochange hora de início para política de cópia de segurança Olá predefinida</span><span class="sxs-lookup"><span data-stu-id="efd72-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="efd72-125">Aceda demasiado**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="efd72-125">Go too**Devices**.</span></span> <span data-ttu-id="efd72-126">lista de Olá de dispositivos registados com o serviço StorSimple Manager de dispositivo será apresentada.</span><span class="sxs-lookup"><span data-stu-id="efd72-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Navegue toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="efd72-128">Selecione e clique em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="efd72-128">Select and click your device.</span></span> <span data-ttu-id="efd72-129">Olá **definições** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="efd72-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="efd72-130">Aceda demasiado**gerir > políticas de cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="efd72-130">Go too**Manage > Backup policies**.</span></span>
   
    ![Selecione o seu dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="efd72-132">No Olá **políticas de cópia de segurança** painel, hora de início do Olá predefinido é 22:30.</span><span class="sxs-lookup"><span data-stu-id="efd72-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="efd72-133">Pode especificar Olá novo a hora de início para uma agenda diária Olá no fuso horário do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="efd72-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![Navegue toobackup políticas](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="efd72-135">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="efd72-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="efd72-136">Efetuar uma cópia de segurança manual</span><span class="sxs-lookup"><span data-stu-id="efd72-136">Take a manual backup</span></span>

<span data-ttu-id="efd72-137">Além disso tooscheduled cópias de segurança, que pode tomar uma cópia de segurança (a pedido) manual de dados de dispositivo em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="efd72-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="efd72-138">toocreate uma cópia de segurança manual</span><span class="sxs-lookup"><span data-stu-id="efd72-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="efd72-139">Aceda demasiado**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="efd72-139">Go too**Devices**.</span></span> <span data-ttu-id="efd72-140">Selecione o seu dispositivo e faça duplo clique **...**  na extremidade direita Olá na linha selecionada Olá.</span><span class="sxs-lookup"><span data-stu-id="efd72-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="efd72-141">No menu de contexto de Olá, selecione **efetuar cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="efd72-141">From hello context menu, select **Take backup**.</span></span>
   
    ![Navegue tootake cópia de segurança](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="efd72-143">No Olá **efetuar cópia de segurança** painel, clique em **efetuar cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="efd72-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="efd72-144">Isto irá criar cópias de segurança todas as partilhas de Olá no servidor de ficheiros de Olá ou todos os volumes de Olá no seu servidor de iSCSI.</span><span class="sxs-lookup"><span data-stu-id="efd72-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![a partir de cópia de segurança](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="efd72-146">Inicia uma cópia de segurança a pedido e verá que uma tarefa de cópia de segurança foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="efd72-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![a partir de cópia de segurança](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="efd72-148">Assim que a tarefa de Olá foi concluída com êxito, será notificado novamente.</span><span class="sxs-lookup"><span data-stu-id="efd72-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="efd72-149">em seguida, inicia o processo de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="efd72-149">hello backup process then starts.</span></span>
   
    ![tarefa de cópia de segurança criada](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="efd72-151">progresso de Olá tootrack de cópias de segurança de Olá e ver os detalhes da tarefa Olá, clique em notificação Olá.</span><span class="sxs-lookup"><span data-stu-id="efd72-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="efd72-152">Isto leva-o demasiado **detalhes da tarefa**.</span><span class="sxs-lookup"><span data-stu-id="efd72-152">This takes you too **Job details**.</span></span>
   
     ![Detalhes da tarefa de cópia de segurança](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="efd72-154">Depois de concluída a cópia de segurança de Olá, aceda demasiado**gestão > catálogo de cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="efd72-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="efd72-155">Verá um instantâneo de nuvem de todas as partilhas de Olá (ou volumes) no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="efd72-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Cópia de segurança concluída](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="efd72-157">Ver as cópias de segurança existentes</span><span class="sxs-lookup"><span data-stu-id="efd72-157">View existing backups</span></span>
<span data-ttu-id="efd72-158">tooview Olá cópias de segurança existentes, efetuar Olá os seguintes passos no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="efd72-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="efd72-159">tooview cópias de segurança existentes</span><span class="sxs-lookup"><span data-stu-id="efd72-159">tooview existing backups</span></span>

1. <span data-ttu-id="efd72-160">Aceda demasiado**dispositivos** painel.</span><span class="sxs-lookup"><span data-stu-id="efd72-160">Go too**Devices** blade.</span></span> <span data-ttu-id="efd72-161">Selecione e clique em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="efd72-161">Select and click your device.</span></span> <span data-ttu-id="efd72-162">No Olá **definições** painel, vá demasiado**gestão > catálogo de cópia de segurança**.</span><span class="sxs-lookup"><span data-stu-id="efd72-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Navegue toobackup catálogo](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="efd72-164">Especifique Olá toobe critérios utilizado para filtrar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="efd72-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="efd72-165">**Intervalo de tempo** – pode ser **última 1 hora**, **últimas 24 horas**, **nos últimos 7 dias**, **nos últimos 30 dias**, **passado ano**, e **data personalizada**.</span><span class="sxs-lookup"><span data-stu-id="efd72-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="efd72-166">**Dispositivos** – selecione na lista de Olá de servidores de ficheiros ou servidores iSCSI registados com o serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="efd72-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="efd72-167">**Iniciou** – pode ser automaticamente **agendada** (por uma política de cópia de segurança) ou **manualmente** iniciada (por si).</span><span class="sxs-lookup"><span data-stu-id="efd72-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtrar as cópias de segurança](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="efd72-169">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="efd72-169">Click **Apply**.</span></span> <span data-ttu-id="efd72-170">Olá lista filtrada de cópias de segurança é apresentada no Olá **catálogo de cópia de segurança** painel.</span><span class="sxs-lookup"><span data-stu-id="efd72-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="efd72-171">Elementos de cópia de segurança de nota 100 só podem ser apresentados num determinado momento.</span><span class="sxs-lookup"><span data-stu-id="efd72-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catálogo de cópias de segurança atualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="efd72-173">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="efd72-173">Next steps</span></span>

<span data-ttu-id="efd72-174">Saiba mais sobre [administrar a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="efd72-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

