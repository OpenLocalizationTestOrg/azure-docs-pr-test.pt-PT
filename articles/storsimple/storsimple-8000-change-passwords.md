---
title: aaaChange as palavras-passe do StorSimple | Microsoft Docs
description: "Descreve como toouse Olá toochange de serviço do Gestor de dispositivos do StorSimple os Snapshot Manager do StorSimple e dispositivo administrador palavras-passe."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="02ae3-103">Utilizar toochange de serviço do Gestor de dispositivos do StorSimple Olá as palavras-passe do StorSimple</span><span class="sxs-lookup"><span data-stu-id="02ae3-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="02ae3-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="02ae3-104">Overview</span></span>
<span data-ttu-id="02ae3-105">portal do Azure de Olá **definições do dispositivo** opção contém todos os parâmetros de dispositivo Olá pode reconfigurar num dispositivo StorSimple que é gerido por um serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="02ae3-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="02ae3-106">Este tutorial explica como pode utilizar Olá **segurança** opção em **definições do dispositivo** toochange o administrador do dispositivo ou a palavra-passe do Snapshot Manager do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="02ae3-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="02ae3-107">Palavra-passe de administrador do dispositivo de Olá de alteração</span><span class="sxs-lookup"><span data-stu-id="02ae3-107">Change hello device administrator password</span></span>
<span data-ttu-id="02ae3-108">Quando utilizar o dispositivo do Windows PowerShell interface tooaccess Olá StorSimple, são necessário tooenter uma palavra-passe de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="02ae3-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="02ae3-109">Quando o dispositivo StorSimple primeiro Olá é registado com um serviço, a palavra-passe do Olá predefinida para esta interface é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="02ae3-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="02ae3-110">Para segurança Olá dos seus dados, é necessário toochange esta palavra-passe no fim de Olá do processo de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="02ae3-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="02ae3-111">Não pode sair do processo de registo Olá sem alterar esta palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="02ae3-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="02ae3-112">Para obter mais informações, consulte [passo 3: configurar e registar o dispositivo de Olá através do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="02ae3-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="02ae3-113">palavra-passe de Olá que primeiro foi definido através da interface do Windows PowerShell Olá durante o registo pode ser alterado posteriormente através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="02ae3-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="02ae3-114">Efetue Olá os seguintes passos toochange Olá dispositivo palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="02ae3-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="02ae3-115">palavra-passe de administrador de dispositivo de Olá toochange</span><span class="sxs-lookup"><span data-stu-id="02ae3-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="02ae3-116">Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="02ae3-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="02ae3-117">Na lista tabela Olá, dos dispositivos, selecione e clique em dispositivo Olá cuja palavras-passe que tenciona toochange.</span><span class="sxs-lookup"><span data-stu-id="02ae3-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="02ae3-118">No Olá **definições** painel, vá demasiado**definições do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="02ae3-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="02ae3-119">No Olá **definições de segurança** painel, clique em **palavra-passe** palavra-passe de administrador de dispositivo de Olá toochange.</span><span class="sxs-lookup"><span data-stu-id="02ae3-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="02ae3-120">No Olá **palavra-passe** painel, forneça uma palavra-passe de administrador que contém 8 too15 carateres.</span><span class="sxs-lookup"><span data-stu-id="02ae3-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="02ae3-121">palavra-passe de Olá tem de ser uma combinação de 3 ou mais carateres em maiúsculas, minúsculas, numérico e especiais.</span><span class="sxs-lookup"><span data-stu-id="02ae3-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="02ae3-122">Confirme a palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ae3-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="02ae3-123">Clique em **guardar** e quando for pedida a confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="02ae3-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="02ae3-124">palavra-passe de administrador de dispositivo Olá agora deve ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="02ae3-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="02ae3-125">Pode utilizar esta palavra-passe modificado tooaccess Olá do Windows PowerShell interface.</span><span class="sxs-lookup"><span data-stu-id="02ae3-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="02ae3-126">Palavra-passe do conjunto Olá Snapshot Manager do StorSimple</span><span class="sxs-lookup"><span data-stu-id="02ae3-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="02ae3-127">Software Snapshot Manager do StorSimple reside no anfitrião do Windows e permite aos administradores toomanage cópias de segurança do dispositivo StorSimple no formulário de Olá de locais e instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="02ae3-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="02ae3-128">Quando configurar um dispositivo no Snapshot Manager do StorSimple, será solicitado tooprovide Olá tooauthenticate de palavra-passe e endereço IP do dispositivo, o dispositivo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="02ae3-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="02ae3-129">Pode definir ou alterar a palavra-passe de Olá para Snapshot Manager do StorSimple através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="02ae3-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="02ae3-130">Efetuar Olá tooset passos a seguir e alterar palavra-passe do Olá Snapshot Manager do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="02ae3-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="02ae3-131">palavra-passe do tooset Olá Snapshot Manager do StorSimple</span><span class="sxs-lookup"><span data-stu-id="02ae3-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="02ae3-132">Aceda tooyour do serviço StorSimple Manager de dispositivo e clique em **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="02ae3-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="02ae3-133">Na lista tabela Olá, dos dispositivos, selecione e clique em dispositivo Olá cuja palavras-passe do Snapshot Manager do StorSimple que tenciona tooset ou altere.</span><span class="sxs-lookup"><span data-stu-id="02ae3-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="02ae3-134">No Olá **definições** painel, vá demasiado**definições do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="02ae3-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="02ae3-135">No Olá **definições de segurança** painel, clique em **palavra-passe** tooset alteração Olá Snapshot Manager do StorSimple da palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="02ae3-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="02ae3-136">No Olá **palavra-passe** painel, introduza uma palavra-passe 14 ou 15 carateres.</span><span class="sxs-lookup"><span data-stu-id="02ae3-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="02ae3-137">Certifique-se de que essa palavra-passe de Olá contém uma combinação de 3 ou mais carateres em maiúsculas, minúsculas, numérico e especiais.</span><span class="sxs-lookup"><span data-stu-id="02ae3-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="02ae3-138">Confirme a palavra-passe de Olá.</span><span class="sxs-lookup"><span data-stu-id="02ae3-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="02ae3-139">Clique em **guardar** e quando for pedida a confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="02ae3-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="02ae3-140">agora deve ser atualizado a palavra-passe do Olá Snapshot Manager do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="02ae3-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02ae3-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="02ae3-141">Next steps</span></span>
* <span data-ttu-id="02ae3-142">Saiba mais sobre [segurança do StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="02ae3-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="02ae3-143">Saiba mais sobre [modificar a configuração do dispositivo](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="02ae3-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="02ae3-144">Saiba mais sobre [utilizando Olá tooadminister de serviço do Gestor de dispositivos do StorSimple com o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="02ae3-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

