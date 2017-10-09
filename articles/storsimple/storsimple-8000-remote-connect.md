---
title: aaaConnect tooyour remotamente o dispositivo StorSimple | Microsoft Docs
description: "Explica como tooconfigure o dispositivo para a gestão remota e como tooconnect tooWindows do PowerShell para StorSimple através de HTTP ou HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="c33cc-103">Ligar remotamente o dispositivo de série de tooyour 8000 do StorSimple</span><span class="sxs-lookup"><span data-stu-id="c33cc-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="c33cc-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="c33cc-104">Overview</span></span>

<span data-ttu-id="c33cc-105">Pode ligar remotamente tooyour dispositivo através do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c33cc-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="c33cc-106">Quando se liga desta forma, não verá um menu.</span><span class="sxs-lookup"><span data-stu-id="c33cc-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="c33cc-107">(Pode ver um menu apenas se utilizar a consola de série de Olá no Olá dispositivo tooconnect.) Com comunicação remota do Windows PowerShell, ligar específico tooa de espaço de execução.</span><span class="sxs-lookup"><span data-stu-id="c33cc-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="c33cc-108">Também pode especificar o idioma de apresentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c33cc-108">You can also specify hello display language.</span></span>

<span data-ttu-id="c33cc-109">Para mais informações sobre como utilizar o seu dispositivo toomanage de comunicação remota do Windows PowerShell, visite demasiado[utilize o Windows PowerShell para StorSimple tooadminister o dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c33cc-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="c33cc-110">Este tutorial explica como tooconfigure o dispositivo para a gestão remota e, em seguida, tooconnect tooWindows do PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c33cc-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="c33cc-111">Pode utilizar HTTP ou HTTPS tooremotely estabelecerem ligação através do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c33cc-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="c33cc-112">No entanto, quando decidir como tooconnect tooWindows do PowerShell para StorSimple, considere Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c33cc-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="c33cc-113">Ligar diretamente toohello a consola de série do dispositivo é segura, mas a ligação consola de série de toohello através de comutadores de rede não está.</span><span class="sxs-lookup"><span data-stu-id="c33cc-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="c33cc-114">Tenha cuidado Olá riscos de segurança ao ligar a consola de série do dispositivo de toohello através de comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="c33cc-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="c33cc-115">Ligar através de uma sessão HTTP poderá oferecem mais segurança ao ligar através da consola de série de Olá rede Olá.</span><span class="sxs-lookup"><span data-stu-id="c33cc-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="c33cc-116">Embora não seja método mais seguro Olá, é aceitável em redes fidedignas.</span><span class="sxs-lookup"><span data-stu-id="c33cc-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="c33cc-117">Ligar através de uma sessão HTTPS com um certificado auto-assinado é Olá mais segura e Olá opção recomendada.</span><span class="sxs-lookup"><span data-stu-id="c33cc-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="c33cc-118">Pode ligar remotamente interface do Windows PowerShell toohello.</span><span class="sxs-lookup"><span data-stu-id="c33cc-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="c33cc-119">No entanto, o dispositivo StorSimple de tooyour de acesso remoto através da interface do Windows PowerShell Olá não está ativado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="c33cc-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="c33cc-120">Tem de ativar a gestão remota no dispositivo Olá primeiro e, em seguida, no Olá cliente que é utilizado tooaccess o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="c33cc-121">passos de Olá descritos neste artigo foram executados num sistema anfitrião com o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c33cc-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="c33cc-122">Ligar através de HTTP</span><span class="sxs-lookup"><span data-stu-id="c33cc-122">Connect through HTTP</span></span>

<span data-ttu-id="c33cc-123">Ligar tooWindows do PowerShell para StorSimple através de uma sessão HTTP oferece mais segurança a que se ligam através da consola de série de Olá do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c33cc-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="c33cc-124">Embora não seja método mais seguro Olá, é aceitável em redes fidedignas.</span><span class="sxs-lookup"><span data-stu-id="c33cc-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="c33cc-125">Pode utilizar qualquer um dos Olá portal ou Olá consola de série tooconfigure gestão remota do Azure.</span><span class="sxs-lookup"><span data-stu-id="c33cc-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="c33cc-126">Selecione uma das Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="c33cc-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="c33cc-127">Utilize a gestão remota do Olá tooenable portal do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="c33cc-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="c33cc-128">Utilize a gestão remota do Olá consola de série tooenable através de HTTP</span><span class="sxs-lookup"><span data-stu-id="c33cc-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="c33cc-129">Depois de ativar a gestão remota, utilize Olá seguir o cliente de Olá tooprepare procedimento para uma ligação remota.</span><span class="sxs-lookup"><span data-stu-id="c33cc-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="c33cc-130">Preparar o cliente Olá de ligação remota</span><span class="sxs-lookup"><span data-stu-id="c33cc-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="c33cc-131">Utilize a gestão remota do Olá tooenable portal do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="c33cc-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="c33cc-132">Efetue Olá seguindo os passos na gestão remota do Olá tooenable portal do Azure através de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c33cc-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="c33cc-133">gestão remota do tooenable através do Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c33cc-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="c33cc-134">Aceda tooyour do serviço StorSimple Manager de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="c33cc-135">Selecione **dispositivos** e, em seguida, selecione e clique em dispositivo Olá tooconfigure que pretende para a gestão remota.</span><span class="sxs-lookup"><span data-stu-id="c33cc-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="c33cc-136">Aceda demasiado**definições do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="c33cc-137">No Olá **definições de segurança** painel, clique em **gestão remota**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="c33cc-138">No Olá **gestão remota** painel, defina **ativar a gestão remota** demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="c33cc-139">Agora, pode escolher tooconnect através de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c33cc-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="c33cc-140">(a predefinição de Olá é tooconnect através de HTTPS.) Certifique-se de que o HTTP está selecionado.</span><span class="sxs-lookup"><span data-stu-id="c33cc-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c33cc-141">A ligação através de HTTP é aceitável apenas em redes fidedignas.</span><span class="sxs-lookup"><span data-stu-id="c33cc-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="c33cc-142">Clique em **guardar** e quando for pedida a confirmação, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="c33cc-143">Utilize a gestão remota do Olá consola de série tooenable através de HTTP</span><span class="sxs-lookup"><span data-stu-id="c33cc-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="c33cc-144">Efetue Olá os seguintes passos Olá gestão de dispositivos consola de série tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="c33cc-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="c33cc-145">gestão remota do tooenable através da consola de série do dispositivo de Olá</span><span class="sxs-lookup"><span data-stu-id="c33cc-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="c33cc-146">No menu da consola de série de Olá, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="c33cc-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="c33cc-147">Para mais informações sobre como utilizar a consola de série de Olá no dispositivo Olá, visite demasiado[ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c33cc-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="c33cc-148">Na linha de Olá, escreva:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="c33cc-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="c33cc-149">Será notificado sobre vulnerabilidades de segurança de Olá de utilizar HTTP tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="c33cc-150">Quando lhe for solicitado, confirme escrevendo **Y**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="c33cc-151">Certifique-se de que está ativado HTTP escrevendo:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="c33cc-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="c33cc-152">Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsAndHttpEnabled**.hello seguinte ilustração mostra estas definições no PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c33cc-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Série HTTPS e HTTP ativada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="c33cc-154">Preparar o cliente Olá de ligação remota</span><span class="sxs-lookup"><span data-stu-id="c33cc-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="c33cc-155">Efetue Olá seguindo os passos na gestão remota do Olá cliente tooenable.</span><span class="sxs-lookup"><span data-stu-id="c33cc-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="c33cc-156">cliente de Olá tooprepare para ligação remota</span><span class="sxs-lookup"><span data-stu-id="c33cc-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="c33cc-157">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="c33cc-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="c33cc-158">Escreva Olá seguinte endereço IP do comando tooadd Olá da lista de anfitriões fidedignos Olá StorSimple dispositivo toohello do cliente:</span><span class="sxs-lookup"><span data-stu-id="c33cc-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="c33cc-159">Substitua <*device_ip*> com o endereço IP Olá do seu dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c33cc-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="c33cc-160">Escreva Olá credenciais de dispositivo do comando toosave Olá numa variável os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c33cc-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="c33cc-161">Na caixa de diálogo de Olá que é apresentado:</span><span class="sxs-lookup"><span data-stu-id="c33cc-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="c33cc-162">Nome de utilizador do tipo Olá neste formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="c33cc-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="c33cc-163">Escrever Olá dispositivo administrador palavra-passe que foi definido quando o dispositivo de Olá foi configurado com o Assistente de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="c33cc-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="c33cc-164">palavra-passe predefinida de Olá é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="c33cc-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="c33cc-165">Inicie uma sessão do Windows PowerShell no dispositivo Olá escrevendo este comando:</span><span class="sxs-lookup"><span data-stu-id="c33cc-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="c33cc-166">toocreate uma sessão do Windows PowerShell para utilização com Olá do dispositivo virtual StorSimple, acrescentar Olá `–Port` parâmetro e especifique a porta pública Olá configurada no sistema de interação remota para o dispositivo Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c33cc-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="c33cc-167">Nesta fase, deve ter uma Active Directory remota do Windows PowerShell sessão toohello do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![Comunicação remota do PowerShell através de HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="c33cc-169">Ligar através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="c33cc-169">Connect through HTTPS</span></span>

<span data-ttu-id="c33cc-170">Ligar tooWindows do PowerShell para StorSimple através de uma sessão HTTPS é Olá mais segura e recomendada método do dispositivo de Microsoft Azure StorSimple tooyour remotamente ao ligar.</span><span class="sxs-lookup"><span data-stu-id="c33cc-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="c33cc-171">Olá procedimentos a seguir explica como tooset segurança Olá série consola e dos computadores cliente para que possa utilizar HTTPS tooconnect tooWindows do PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c33cc-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="c33cc-172">Pode utilizar qualquer um dos Olá portal ou Olá consola de série tooconfigure gestão remota do Azure.</span><span class="sxs-lookup"><span data-stu-id="c33cc-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="c33cc-173">Selecione uma das Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="c33cc-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="c33cc-174">Utilize a gestão remota do Olá tooenable portal do Azure através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="c33cc-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="c33cc-175">Utilize a gestão remota do Olá consola de série tooenable através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="c33cc-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="c33cc-176">Depois de ativar a gestão remota, utilize Olá seguir o anfitrião de Olá tooprepare procedimentos para um gestão remota e ligar o dispositivo de toohello de anfitrião remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="c33cc-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="c33cc-177">Preparar o anfitrião de Olá para a gestão remota</span><span class="sxs-lookup"><span data-stu-id="c33cc-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="c33cc-178">Ligar dispositivo toohello de anfitrião remoto Olá</span><span class="sxs-lookup"><span data-stu-id="c33cc-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="c33cc-179">Utilize a gestão remota do Olá tooenable portal do Azure através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="c33cc-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="c33cc-180">Efetue Olá seguindo os passos na gestão remota do Olá tooenable portal do Azure através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c33cc-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="c33cc-181">gestão remota tooenable através de HTTPS de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c33cc-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="c33cc-182">Aceda tooyour do serviço StorSimple Manager de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="c33cc-183">Selecione **dispositivos** e, em seguida, selecione e clique em dispositivo Olá tooconfigure que pretende para a gestão remota.</span><span class="sxs-lookup"><span data-stu-id="c33cc-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="c33cc-184">Aceda demasiado**definições do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="c33cc-185">No Olá **definições de segurança** painel, clique em **gestão remota**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="c33cc-186">Definir **ativar a gestão remota** demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="c33cc-187">Agora, pode escolher tooconnect através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c33cc-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="c33cc-188">(a predefinição de Olá é tooconnect através de HTTPS.) Certifique-se de que o HTTPS é selecionado.</span><span class="sxs-lookup"><span data-stu-id="c33cc-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="c33cc-189">Clique em... e, em seguida, clique em **Transferir certificado de gestão remoto**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="c33cc-190">Especifique uma localização toosave este ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c33cc-190">Specify a location toosave this file.</span></span> <span data-ttu-id="c33cc-191">É necessário tooinstall este certificado no computador de cliente ou anfitrião Olá que irá utilizar tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="c33cc-192">Clique em **guardar** e, em seguida, clique em **Sim** quando um pedido de confirmação.</span><span class="sxs-lookup"><span data-stu-id="c33cc-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="c33cc-193">Utilize a gestão remota do Olá consola de série tooenable através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="c33cc-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="c33cc-194">Efetue Olá os seguintes passos Olá gestão de dispositivos consola de série tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="c33cc-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="c33cc-195">gestão remota do tooenable através da consola de série do dispositivo de Olá</span><span class="sxs-lookup"><span data-stu-id="c33cc-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="c33cc-196">No menu da consola de série de Olá, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="c33cc-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="c33cc-197">Para mais informações sobre como utilizar a consola de série de Olá no dispositivo Olá, visite demasiado[ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c33cc-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="c33cc-198">Na linha de Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="c33cc-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="c33cc-199">Isto deve ativar HTTPS no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="c33cc-200">Certifique-se de que foi ativado HTTPS, escrevendo:</span><span class="sxs-lookup"><span data-stu-id="c33cc-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="c33cc-201">Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsEnabled**.hello seguinte ilustração mostra estas definições no PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c33cc-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Série ativadas por HTTPS](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="c33cc-203">Da saída de Olá de `Get-HcsSystem`, copie Olá o número de série do dispositivo Olá e guardá-lo para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="c33cc-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c33cc-204">número de série de Olá mapeia o nome CN de toohello no certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="c33cc-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="c33cc-205">Obter um certificado de gestão remota, escrevendo:</span><span class="sxs-lookup"><span data-stu-id="c33cc-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="c33cc-206">Será apresentada a seguinte de toohello semelhante um certificado.</span><span class="sxs-lookup"><span data-stu-id="c33cc-206">A certificate similar toohello following will appear.</span></span>
   
    ![Obter o certificado de gestão remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="c33cc-208">Copiar as informações de Olá certificado Olá **---BEGIN CERTIFICATE---** demasiado**---fim certificado---** num editor de texto, como o bloco de notas e guarde-como um ficheiro. cer.</span><span class="sxs-lookup"><span data-stu-id="c33cc-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="c33cc-209">(Vai copiar este anfitrião remoto da tooyour de ficheiro ao preparar o anfitrião de Olá.)</span><span class="sxs-lookup"><span data-stu-id="c33cc-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c33cc-210">toogenerate um novo certificado, utilize Olá `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c33cc-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="c33cc-211">Preparar o anfitrião de Olá para a gestão remota</span><span class="sxs-lookup"><span data-stu-id="c33cc-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="c33cc-212">computador de anfitrião de Olá tooprepare para uma ligação remota que utiliza uma sessão HTTPS, execute Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="c33cc-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="c33cc-213">[Ficheiro. cer de Olá de importação para arquivo de raiz de hello do cliente Olá ou anfitrião remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="c33cc-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="c33cc-214">[Adicionar ficheiro hosts toohello de números de série de dispositivos de Olá no seu anfitrião remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="c33cc-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="c33cc-215">Cada um dos Olá precedente procedimentos, é descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="c33cc-216">certificado de Olá tooimport no anfitrião remoto Olá</span><span class="sxs-lookup"><span data-stu-id="c33cc-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="c33cc-217">Clique no ficheiro. cer de Olá e selecione **instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="c33cc-218">Esta ação inicia Olá Assistente para importar certificados.</span><span class="sxs-lookup"><span data-stu-id="c33cc-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![Assistente de importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="c33cc-220">Para **localização do arquivo**, selecione **máquina Local**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="c33cc-221">Selecione **colocar todos os certificados no Olá seguir arquivo**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="c33cc-222">Navegue toohello o arquivo de raiz do seu anfitrião remoto e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistente de importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="c33cc-224">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-224">Click **Finish**.</span></span> <span data-ttu-id="c33cc-225">É apresentada uma mensagem que indica que a importação de Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="c33cc-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![Assistente de importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="c33cc-227">anfitrião remoto de toohello números de série de dispositivo tooadd</span><span class="sxs-lookup"><span data-stu-id="c33cc-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="c33cc-228">Inicie o bloco de notas como administrador e, em seguida, abra o ficheiro de anfitriões de Olá localizado em \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="c33cc-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="c33cc-229">Adicionar Olá seguintes três ficheiro de anfitriões de tooyour entradas: **endereço IP de dados 0**, **endereço de IP fixo do controlador 0**, e **endereço IP fixo do controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="c33cc-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="c33cc-230">Introduza o número de série do dispositivo Olá que guardou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c33cc-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="c33cc-231">Mapear este endereço IP toohello conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="c33cc-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="c33cc-232">Para o controlador 0 e 1 de controlador, acrescentar **Controller0** e **Controller1** no fim de Olá do número de série de Olá (nome CN).</span><span class="sxs-lookup"><span data-stu-id="c33cc-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Adicionar nome CN toohosts ficheiro](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="c33cc-234">Ficheiro de anfitriões de Olá guardado.</span><span class="sxs-lookup"><span data-stu-id="c33cc-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="c33cc-235">Ligar dispositivo toohello de anfitrião remoto Olá</span><span class="sxs-lookup"><span data-stu-id="c33cc-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="c33cc-236">Utilizar o Windows PowerShell e do SSL tooenter uma sessão de SSAdmin no seu dispositivo a partir de um anfitrião remoto ou o cliente.</span><span class="sxs-lookup"><span data-stu-id="c33cc-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="c33cc-237">sessão de SSAdmin Olá mapeia toooption 1 na Olá [consola de série](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="c33cc-238">Efetue Olá seguir o procedimento no computador de Olá partir do qual pretende que a ligação do toomake Olá remota do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c33cc-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="c33cc-239">tooenter uma sessão de SSAdmin no dispositivo de Olá através do Windows PowerShell e do SSL</span><span class="sxs-lookup"><span data-stu-id="c33cc-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="c33cc-240">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="c33cc-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="c33cc-241">Adicione anfitriões fidedignos Olá dispositivo IP endereço toohello do cliente, escrevendo:</span><span class="sxs-lookup"><span data-stu-id="c33cc-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="c33cc-242">Onde <*device_ip*> é o endereço IP Olá do seu dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c33cc-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="c33cc-243">toocreate uma credencial nova, escreva:</span><span class="sxs-lookup"><span data-stu-id="c33cc-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="c33cc-244">Onde <*IP do dispositivo-alvo*> é o endereço IP Olá de dados 0 para o seu dispositivo; por exemplo, **10.126.173.90** conforme mostrado no Olá anterior a imagem do ficheiro de anfitriões de Olá.</span><span class="sxs-lookup"><span data-stu-id="c33cc-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="c33cc-245">Além disso, forneça a palavra-passe de administrador de Olá para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="c33cc-246">Crie uma sessão introduzindo:</span><span class="sxs-lookup"><span data-stu-id="c33cc-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="c33cc-247">Para o parâmetro - ComputerName de Olá no cmdlet Olá, fornecer Olá <*número de série do dispositivo-alvo*>.</span><span class="sxs-lookup"><span data-stu-id="c33cc-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="c33cc-248">Este número de série foi mapeado toohello endereço IP de dados 0 no ficheiro de anfitriões de Olá no seu anfitrião remoto; Por exemplo, **SHX0991003G44MT** conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="c33cc-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="c33cc-249">Escreva:</span><span class="sxs-lookup"><span data-stu-id="c33cc-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="c33cc-250">Terá de toowait uns minutos e, em seguida, será dispositivo tooyour ligado através de HTTPS através de SSL.</span><span class="sxs-lookup"><span data-stu-id="c33cc-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="c33cc-251">Verá uma mensagem que indica que está ligado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c33cc-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![Comunicação remota do PowerShell através de HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="c33cc-253">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c33cc-253">Next steps</span></span>

* <span data-ttu-id="c33cc-254">Saiba mais sobre [através do Windows PowerShell tooadminister o dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c33cc-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="c33cc-255">Saiba mais sobre [utilizando Olá tooadminister de serviço do Gestor de dispositivos do StorSimple com o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c33cc-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

