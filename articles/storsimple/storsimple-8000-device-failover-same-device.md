---
title: "aaaStorSimple a ativação pós-falha, recuperação após desastre para os dispositivos de 8000 série | Microsoft Docs"
description: Saiba como toofail ao longo do seu toohello do dispositivo StorSimple mesmo dispositivo.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="77748-103">Efetuar a ativação pós-falha do dispositivo toosame dispositivo físico StorSimple</span><span class="sxs-lookup"><span data-stu-id="77748-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="77748-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="77748-104">Overview</span></span>

<span data-ttu-id="77748-105">Este tutorial descreve Olá passos necessários toofail através de um tooitself de dispositivo físico de série 8000 do StorSimple se ocorrer um desastre.</span><span class="sxs-lookup"><span data-stu-id="77748-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="77748-106">StorSimple utiliza Olá os dados de toomigrate da funcionalidade de ativação pós-falha de dispositivo de um dispositivo físico de origem no dispositivo físico do Olá datacenter tooanother.</span><span class="sxs-lookup"><span data-stu-id="77748-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="77748-107">orientações de Olá neste tutorial aplica-se tooStorSimple 8000 físico dispositivos das séries com versões do software Update 3 e posterior.</span><span class="sxs-lookup"><span data-stu-id="77748-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="77748-108">toolearn mais informações sobre a ativação pós-falha do dispositivo e como é utilizado toorecover de desastres, aceda demasiado[ativação pós-falha e recuperação após desastre para os dispositivos de série 8000 do StorSimple](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="77748-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="77748-109">toofail através de um dispositivo físico tooanother dispositivo físico, aceda demasiado[falhar toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="77748-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="77748-110">toofail através de um tooa do dispositivo físico StorSimple dispositivo de nuvem do StorSimple, aceda demasiado[falhar tooa dispositivo de nuvem do StorSimple](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="77748-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="77748-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77748-111">Prerequisites</span></span>

- <span data-ttu-id="77748-112">Certifique-se de que reviu Olá as considerações para ativação pós-falha do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77748-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="77748-113">Para mais informações, visite demasiado[considerações comuns para ativação pós-falha do dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="77748-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="77748-114">Passos toofail através de toohello mesmo dispositivo</span><span class="sxs-lookup"><span data-stu-id="77748-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="77748-115">Efetuar Olá os passos seguintes se precisar de toofail sobre toohello mesmo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77748-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="77748-116">Criar instantâneos de nuvem de todos os volumes de Olá no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77748-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="77748-117">Para mais informações, visite demasiado[cópias de segurança do Gestor de dispositivos do StorSimple utilize serviço toocreate](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="77748-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="77748-118">Repor as predefinições de toofactory de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77748-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="77748-119">Siga instruções de detalhado Olá [como predefinições tooreset um toofactory do dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="77748-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="77748-120">Aceda toohello do serviço StorSimple Manager de dispositivo e, em seguida, selecione **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="77748-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="77748-121">No Olá **dispositivos** painel, o dispositivo antigo Olá deve mostrar como **Offline**.</span><span class="sxs-lookup"><span data-stu-id="77748-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Dispositivo de origem offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="77748-123">Configurar o dispositivo e registá-lo com o serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77748-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="77748-124">Olá dispositivo recentemente registado deve mostrar como **pronto tooset segurança**.</span><span class="sxs-lookup"><span data-stu-id="77748-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="77748-125">nome de dispositivo Olá para novo dispositivo de Olá é Olá igual ao dispositivo antigo Olá, mas tem anexado um tooindicate numeral desse dispositivo Olá foi reposição toofactory predefinido e registado novamente.</span><span class="sxs-lookup"><span data-stu-id="77748-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Dispositivo recentemente registado tooset pronto cópias de segurança](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="77748-127">Para o novo dispositivo Olá, conclua a configuração de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="77748-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="77748-128">Para mais informações, visite demasiado[passo 4: concluir a configuração mínima do dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="77748-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="77748-129">No Olá **dispositivos** painel, Olá estado do dispositivo Olá é alterado demasiado**Online**.</span><span class="sxs-lookup"><span data-stu-id="77748-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="77748-130">**Concluir a configuração mínima Olá pela primeira vez, ou a DR poderão falhar.**</span><span class="sxs-lookup"><span data-stu-id="77748-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo recentemente registado online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="77748-132">Selecione o dispositivo de antigo Olá (estado offline) e a partir da barra de comando Olá, clique em **falhar**.</span><span class="sxs-lookup"><span data-stu-id="77748-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="77748-133">No Olá **falhar** painel, selecione o dispositivo antigo como origem de Olá e especifique o dispositivo de destino Olá como Olá recentemente registado o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77748-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Resumo de ativação pós-falha](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="77748-135">Para obter instruções detalhadas, consulte demasiado[efetuar a ativação pós-falha do dispositivo físico tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="77748-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="77748-136">É criada uma tarefa de restauro do dispositivo, que pode monitorizar a partir da Olá **tarefas** painel.</span><span class="sxs-lookup"><span data-stu-id="77748-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="77748-137">Depois da tarefa de Olá foi concluída com êxito, aceder ao dispositivo novo Olá e navegue toohello **contentores de Volume** painel.</span><span class="sxs-lookup"><span data-stu-id="77748-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="77748-138">Certifique-se de que todos os contentores de volume de Olá de dispositivo antigo Olá foram migradas toohello novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77748-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Os contentores de volume migrado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="77748-140">Após a conclusão da ativação pós-falha de Olá, pode desativar e eliminar dispositivo antigo Olá a partir do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="77748-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="77748-141">Selecione Olá antigo dispositivo (offline), botão direito e, em seguida, selecione **desativar**.</span><span class="sxs-lookup"><span data-stu-id="77748-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="77748-142">Depois do dispositivo de Olá está desativado, o estado de Olá do dispositivo Olá é atualizado.</span><span class="sxs-lookup"><span data-stu-id="77748-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Dispositivo de origem desativado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="77748-144">Selecione Olá desativou o dispositivo, rato e, em seguida, selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="77748-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="77748-145">Isto elimina dispositivo Olá da lista de Olá de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="77748-145">This deletes hello device from hello list of devices.</span></span>

    ![Dispositivo de origem eliminado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="77748-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="77748-147">Next steps</span></span>

* <span data-ttu-id="77748-148">Depois de ter de efetuar uma ativação pós-falha, poderá ser necessário demasiado[desative ou elimine o dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="77748-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="77748-149">Para obter informações sobre como toouse Olá StorSimple Manager de dispositivo de serviço, visite demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="77748-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

