---
title: aaaUpdate o dispositivo StorSimple | Microsoft Docs
description: "Explica como toouse Olá StorSimple atualizar funcionalidade tooinstall regular e atualizações de modo de manutenção e as correções."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="cbb63-103">Atualizar o seu dispositivo de série de 8000 do StorSimple</span><span class="sxs-lookup"><span data-stu-id="cbb63-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="cbb63-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="cbb63-104">Overview</span></span>
<span data-ttu-id="cbb63-105">Olá StorSimple atualizações funcionalidades permitem-lhe tooeasily par o dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cbb63-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="cbb63-106">Dependendo do tipo de atualização de Olá, pode aplicar o dispositivo de toohello atualizações através de Olá portal clássico do Azure ou através da interface do Windows PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb63-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="cbb63-107">Este tutorial descreve os tipos de atualização de Olá e como tooinstall, cada um deles.</span><span class="sxs-lookup"><span data-stu-id="cbb63-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="cbb63-108">Pode aplicar dois tipos de atualizações de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="cbb63-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="cbb63-109">Regular (ou modo Normal) atualizações</span><span class="sxs-lookup"><span data-stu-id="cbb63-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="cbb63-110">Atualizações de modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="cbb63-110">Maintenance mode updates</span></span>

<span data-ttu-id="cbb63-111">Pode instalar atualizações regulares através de Olá portal clássico do Azure ou o Windows PowerShell; No entanto, tem de utilizar atualizações de modo de manutenção do Windows PowerShell tooinstall.</span><span class="sxs-lookup"><span data-stu-id="cbb63-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="cbb63-112">Cada tipo de atualização é descrito em separado, abaixo.</span><span class="sxs-lookup"><span data-stu-id="cbb63-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="cbb63-113">Atualizações regulares</span><span class="sxs-lookup"><span data-stu-id="cbb63-113">Regular updates</span></span>
<span data-ttu-id="cbb63-114">Atualizações regulares são não acontece atualizações que podem ser instaladas quando o dispositivo de Olá está no modo Normal.</span><span class="sxs-lookup"><span data-stu-id="cbb63-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="cbb63-115">Estas atualizações são aplicadas através do controlador de dispositivo de tooeach de Web site Microsoft Update Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb63-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cbb63-116">Um controlador ativação pós-falha pode ocorrer durante o processo de atualização de Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb63-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="cbb63-117">No entanto, isto não irá afetar a disponibilidade de sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="cbb63-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="cbb63-118">Para obter detalhes sobre como tooinstall regular atualizações através de Olá portal clássico do Azure, consulte [instalar atualizações regulares através do portal clássico do Azure de Olá](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="cbb63-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="cbb63-119">Também pode instalar atualizações regulares através do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cbb63-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="cbb63-120">Para obter mais informações, consulte [instalar atualizações regulares através do Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="cbb63-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="cbb63-121">Atualizações de modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="cbb63-121">Maintenance mode updates</span></span>
<span data-ttu-id="cbb63-122">As atualizações de modo de manutenção são atualizações acontece, tais como atualizações de firmware do disco.</span><span class="sxs-lookup"><span data-stu-id="cbb63-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="cbb63-123">Estas atualizações requerem Olá dispositivo toobe colocado em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="cbb63-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="cbb63-124">Para obter mais informações, consulte [passo 2: modo de manutenção introduza](#step2).</span><span class="sxs-lookup"><span data-stu-id="cbb63-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="cbb63-125">Não é possível utilizar atualizações de modo de manutenção do Olá tooinstall de portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb63-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="cbb63-126">Em vez disso, deve utilizar o Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cbb63-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="cbb63-127">Para obter detalhes sobre como o modo de manutenção tooinstall atualizações, consulte [atualizações de modo de manutenção instalar através do Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="cbb63-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb63-128">Modo de manutenção atualizações tem de ser aplicadas em separado tooeach controlador.</span><span class="sxs-lookup"><span data-stu-id="cbb63-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="cbb63-129">Instalar atualizações regulares através de Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="cbb63-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="cbb63-130">Pode utilizar o dispositivo do StorSimple tooyour Olá tooapply de portal clássico do Azure atualizações.</span><span class="sxs-lookup"><span data-stu-id="cbb63-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="cbb63-131">Instalar atualizações regulares através do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="cbb63-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="cbb63-132">Em alternativa, pode utilizar o Windows PowerShell para as atualizações do StorSimple tooapply regular (modo Normal).</span><span class="sxs-lookup"><span data-stu-id="cbb63-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb63-133">Apesar de poder instalar atualizações regulares através do Windows PowerShell para StorSimple, recomendamos vivamente que instala atualizações regulares através de Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb63-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="cbb63-134">A partir do Update 1, verificações prévias será efetuada tooinstalling anterior atualizações do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb63-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="cbb63-135">Estas verificações prévias serão alta impedem mais falhas e certifique-se de uma experiência smoother.</span><span class="sxs-lookup"><span data-stu-id="cbb63-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="cbb63-136">Instalar atualizações de modo de manutenção através do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="cbb63-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="cbb63-137">Utilizar o Windows PowerShell para StorSimple tooapply manutenção modo atualizações tooyour o dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cbb63-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="cbb63-138">Todos os pedidos de e/s são colocadas em pausa neste modo.</span><span class="sxs-lookup"><span data-stu-id="cbb63-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="cbb63-139">Serviços, tais como a memória de acesso aleatório não volátil (NVRAM) ou o serviço de cluster de Olá também estão parados.</span><span class="sxs-lookup"><span data-stu-id="cbb63-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="cbb63-140">Tanto os controladores são reiniciados, quando introduzir ou sair neste modo.</span><span class="sxs-lookup"><span data-stu-id="cbb63-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="cbb63-141">Quando sair deste modo, todos os serviços de Olá retomará e devem estar em bom estado.</span><span class="sxs-lookup"><span data-stu-id="cbb63-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="cbb63-142">(Isto pode demorar alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="cbb63-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="cbb63-143">Se precisar de atualizações de modo de manutenção tooapply, receberá um alerta através de Olá portal clássico do Azure que tem atualizações que devem ser instaladas.</span><span class="sxs-lookup"><span data-stu-id="cbb63-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="cbb63-144">Este alerta inclui instruções para utilizar o Windows PowerShell para as atualizações do StorSimple tooinstall Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb63-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="cbb63-145">Depois de atualizar o seu dispositivo, utilize Olá mesmo modo de tooRegular do procedimento toochange Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cbb63-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="cbb63-146">Para obter instruções passo a passo, consulte [passo 4: modo de manutenção de saída](#step4).</span><span class="sxs-lookup"><span data-stu-id="cbb63-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="cbb63-147">Antes de introduzir o modo de manutenção, certifique-se de que ambos os controladores de dispositivo estão em bom Estados, verificando Olá **estado do Hardware** no Olá **manutenção** página Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb63-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="cbb63-148">Se o controlador de Olá não está em bom estado, contacte Support da Microsoft para passos Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb63-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="cbb63-149">Para obter mais informações, visite tooContact Support da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cbb63-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="cbb63-150">Quando estiver no modo de manutenção, terá de tooapply Olá atualização pela primeira vez num controlador e, em seguida, no Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="cbb63-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="cbb63-151">Passo 1: Ligar a consola de série toohello<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="cbb63-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="cbb63-152">Em primeiro lugar, utilize uma aplicação, tais como o PuTTY tooaccess Olá consola de série.</span><span class="sxs-lookup"><span data-stu-id="cbb63-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="cbb63-153">Olá procedimento seguinte explica como consola de série do toohello toouse PuTTY tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cbb63-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="cbb63-154">Passo 2: Introduza o modo de manutenção<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="cbb63-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="cbb63-155">Depois de ligar a consola de toohello, determine se existem atualizações tooinstall e introduza tooinstall de modo de manutenção-los.</span><span class="sxs-lookup"><span data-stu-id="cbb63-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="cbb63-156">Passo 3: Instalar as atualizações<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="cbb63-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="cbb63-157">Em seguida, instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="cbb63-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="cbb63-158">Passo 4: Modo de manutenção de saída<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="cbb63-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="cbb63-159">Por fim, saia do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="cbb63-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="cbb63-160">Instalar correções através do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="cbb63-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="cbb63-161">Ao contrário das atualizações do Microsoft Azure StorSimple, correções estão instaladas a partir de uma pasta partilhada.</span><span class="sxs-lookup"><span data-stu-id="cbb63-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="cbb63-162">Tal como acontece com as atualizações, existem dois tipos de correções:</span><span class="sxs-lookup"><span data-stu-id="cbb63-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="cbb63-163">Correções regulares</span><span class="sxs-lookup"><span data-stu-id="cbb63-163">Regular hotfixes</span></span> 
* <span data-ttu-id="cbb63-164">Correções de modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="cbb63-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="cbb63-165">Olá procedimentos seguintes explicam como toouse do Windows PowerShell para StorSimple tooinstall regular e correções do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="cbb63-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="cbb63-166">O que acontece tooupdates se efetuar uma fábrica de reposição do dispositivo Olá?</span><span class="sxs-lookup"><span data-stu-id="cbb63-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="cbb63-167">Se um dispositivo reposição toofactory definições, todas as atualizações de Olá serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="cbb63-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="cbb63-168">Depois do dispositivo de reposição de fábrica Olá registado e configurado, terá de atualizações de instalação de toomanually através de Olá portal clássico do Azure e/ou do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cbb63-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="cbb63-169">Para obter mais informações sobre a reposição de fábrica, consulte [repor as predefinições do Olá dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="cbb63-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbb63-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cbb63-170">Next steps</span></span>
* <span data-ttu-id="cbb63-171">Saiba mais sobre [através do Windows PowerShell para StorSimple tooadminister o dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="cbb63-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="cbb63-172">Saiba mais sobre [utilizando Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="cbb63-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

