---
title: aaaDeactivate e eliminar uma matriz Virtual do Microsoft Azure StorSimple | Microsoft Docs
description: "Descreve como o dispositivo StorSimple tooremove do serviço ao desativar-o primeiro e, em seguida, eliminá-lo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="ca172-103">Desativar e eliminar uma matriz de Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="ca172-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ca172-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="ca172-104">Overview</span></span>

<span data-ttu-id="ca172-105">Ao desativar uma matriz de Virtual StorSimple, interromper a ligação de Olá entre dispositivos de Olá e Olá correspondente o serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ca172-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="ca172-106">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="ca172-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="ca172-107">Desativar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="ca172-107">Deactivate a device</span></span> 
* <span data-ttu-id="ca172-108">Eliminar um dispositivo desativado</span><span class="sxs-lookup"><span data-stu-id="ca172-108">Delete a deactivated device</span></span>

<span data-ttu-id="ca172-109">informações de Olá neste artigo aplicam-se apenas tooStorSimple matrizes Virtual.</span><span class="sxs-lookup"><span data-stu-id="ca172-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="ca172-110">Para informações sobre 8000 série, visite toohow demasiado[desativar ou eliminar um dispositivo](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="ca172-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="ca172-111">Quando toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="ca172-111">When toodeactivate?</span></span>

<span data-ttu-id="ca172-112">A desativação de uma operação permanente e não pode ser anulada.</span><span class="sxs-lookup"><span data-stu-id="ca172-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="ca172-113">Não é possível registar um dispositivo desativado com Olá serviço StorSimple Manager de dispositivo novamente.</span><span class="sxs-lookup"><span data-stu-id="ca172-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="ca172-114">Poderá ter toodeactivate e eliminar uma matriz de Virtual StorSimple no Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="ca172-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="ca172-115">**A ativação pós-falha planeada** : O dispositivo está online e se planear toofail ao longo do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca172-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="ca172-116">Se estiver a planear tooupgrade tooa maior dispositivo, poderá ser necessário toofail ao longo do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca172-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="ca172-117">Depois de propriedade de dados de Olá é transferida e Olá ativação estiver concluída, o dispositivo de origem Olá é eliminado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ca172-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="ca172-118">**Ativação pós-falha não planeada** : O dispositivo estiver offline e precisar de toofail sobre dispositivos Olá.</span><span class="sxs-lookup"><span data-stu-id="ca172-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="ca172-119">Este cenário poderá ocorrer durante um desastre quando houver uma falha no datacenter de Olá e o dispositivo primário está inativo.</span><span class="sxs-lookup"><span data-stu-id="ca172-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="ca172-120">Planear toofail através de dispositivo do Olá dispositivo tooa secundário.</span><span class="sxs-lookup"><span data-stu-id="ca172-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="ca172-121">Depois de propriedade de dados de Olá é transferida e Olá ativação estiver concluída, o dispositivo de origem Olá é eliminado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ca172-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="ca172-122">**Desativar** : pretende que o dispositivo de Olá toodecommission.</span><span class="sxs-lookup"><span data-stu-id="ca172-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="ca172-123">Isto requer toofirst desativar Olá dispositivo e, em seguida, eliminá-lo.</span><span class="sxs-lookup"><span data-stu-id="ca172-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="ca172-124">Quando desativar um dispositivo, já não pode aceder a todos os dados que esteja armazenados localmente.</span><span class="sxs-lookup"><span data-stu-id="ca172-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="ca172-125">Pode apenas acesso e recuperar Olá os dados armazenados na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca172-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="ca172-126">Se planear os dados de dispositivos de Olá tookeep após a desativação, deve ter um instantâneo de nuvem de todos os seus dados antes de desativar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca172-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="ca172-127">Este instantâneo na nuvem permite-lhe toorecover Olá todos os dados, uma fase posterior.</span><span class="sxs-lookup"><span data-stu-id="ca172-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="ca172-128">Desativar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="ca172-128">Deactivate a device</span></span>

<span data-ttu-id="ca172-129">toodeactivate seu dispositivo, efetuar Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="ca172-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="ca172-130">dispositivo de Olá toodeactivate</span><span class="sxs-lookup"><span data-stu-id="ca172-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="ca172-131">No seu serviço, visite demasiado**gestão > dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ca172-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="ca172-132">No Olá **dispositivos** painel, clique e dispositivo Olá Selecione se pretende toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="ca172-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Selecione o dispositivo toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="ca172-134">No seu **dashboard dispositivo** painel, clique em **... Mais** e na lista de Olá, selecione **desativar**.</span><span class="sxs-lookup"><span data-stu-id="ca172-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Clique em Desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="ca172-136">No Olá **desativar** painel, nome de dispositivo do tipo Olá e, em seguida, clique em **desativar**.</span><span class="sxs-lookup"><span data-stu-id="ca172-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Confirmar a desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="ca172-138">Olá desativar processo inicia e demora alguns minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ca172-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Desativar em curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="ca172-140">Após a desativação, atualiza a lista de Olá dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ca172-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Desativar concluída](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="ca172-142">Pode agora eliminar este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca172-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="ca172-143">Eliminar Olá dispositivo</span><span class="sxs-lookup"><span data-stu-id="ca172-143">Delete hello device</span></span>

<span data-ttu-id="ca172-144">Um dispositivo tem toodelete de desativado primeiro toobe-lo.</span><span class="sxs-lookup"><span data-stu-id="ca172-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="ca172-145">Eliminar um dispositivo remove-o da lista de Olá de serviço ligado toohello de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ca172-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="ca172-146">serviço de Olá, em seguida, pode deixará de gerir dispositivos Olá eliminado.</span><span class="sxs-lookup"><span data-stu-id="ca172-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="ca172-147">No entanto permanecem dados Olá associados ao dispositivo Olá na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca172-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="ca172-148">Estes dados accrues, em seguida, os encargos.</span><span class="sxs-lookup"><span data-stu-id="ca172-148">This data then accrues charges.</span></span>

<span data-ttu-id="ca172-149">dispositivo de Olá toodelete, efetuar Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="ca172-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="ca172-150">dispositivo de Olá toodelete</span><span class="sxs-lookup"><span data-stu-id="ca172-150">toodelete hello device</span></span>

1. <span data-ttu-id="ca172-151">No Gestor de dispositivos do StorSimple, aceda demasiado**gestão > dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ca172-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="ca172-152">No Olá **dispositivos** painel, selecione um dispositivo desativado que pretende toodelete.</span><span class="sxs-lookup"><span data-stu-id="ca172-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="ca172-153">No Olá **dashboard dispositivo** painel, clique em **... Mais** e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ca172-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Selecione o dispositivo toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="ca172-155">No Olá **eliminar** painel, o nome do tipo Olá da sua eliminação do dispositivo tooconfirm Olá e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ca172-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="ca172-156">Eliminar dispositivos de Olá não elimina dados de nuvem Olá associados Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca172-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Confirmar eliminação](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="ca172-158">eliminação de Olá é iniciado e demora alguns minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ca172-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Eliminar em curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="ca172-160">Depois do dispositivo Olá é eliminado, pode ver lista Olá atualizado de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ca172-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca172-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ca172-161">Next steps</span></span>

* <span data-ttu-id="ca172-162">Para obter informações sobre como toofail, aceda demasiado[ativação pós-falha e recuperação após desastre da sua matriz de Virtual StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="ca172-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="ca172-163">mais informações sobre como toolearn como toouse Olá serviço Gestor de dispositivos do StorSimple, aceda demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple a matriz de Virtual StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ca172-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

