---
title: aaaConnect tooyour remotamente o dispositivo StorSimple | Microsoft Docs
description: "Explica como tooconfigure o dispositivo para a gestão remota e como tooconnect tooWindows do PowerShell para StorSimple através de HTTP ou HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="31f9b-103">Ligar remotamente o dispositivo de série de tooyour 8000 do StorSimple</span><span class="sxs-lookup"><span data-stu-id="31f9b-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="31f9b-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="31f9b-104">Overview</span></span>
<span data-ttu-id="31f9b-105">Pode utilizar o dispositivo do Windows PowerShell remota tooconnect tooyour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="31f9b-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="31f9b-106">Quando se liga desta forma, não verá um menu.</span><span class="sxs-lookup"><span data-stu-id="31f9b-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="31f9b-107">(Pode ver um menu apenas se utilizar a consola de série de Olá no Olá dispositivo tooconnect.) Com comunicação remota do Windows PowerShell, ligar específico tooa de espaço de execução.</span><span class="sxs-lookup"><span data-stu-id="31f9b-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="31f9b-108">Também pode especificar o idioma de apresentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="31f9b-109">Para mais informações sobre como utilizar o seu dispositivo toomanage de comunicação remota do Windows PowerShell, visite demasiado[utilize o Windows PowerShell para StorSimple tooadminister o dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="31f9b-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="31f9b-110">Este tutorial explica como tooconfigure o dispositivo para a gestão remota e, em seguida, tooconnect tooWindows do PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="31f9b-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="31f9b-111">Pode utilizar HTTP ou HTTPS tooconnect através de comunicação remota do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31f9b-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="31f9b-112">No entanto, quando decidir como tooconnect tooWindows do PowerShell para StorSimple, considere o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="31f9b-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="31f9b-113">Ligar diretamente toohello a consola de série do dispositivo é segura, mas a ligação consola de série de toohello através de comutadores de rede não está.</span><span class="sxs-lookup"><span data-stu-id="31f9b-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="31f9b-114">Tenha cuidado Olá riscos de segurança ao ligar a consola de série do dispositivo de toohello através de comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="31f9b-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="31f9b-115">Ligar através de uma sessão HTTP poderá oferecem mais segurança ao ligar através da consola de série de Olá rede Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="31f9b-116">Embora não seja método mais seguro Olá, é aceitável em redes fidedignas.</span><span class="sxs-lookup"><span data-stu-id="31f9b-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="31f9b-117">Ligar através de uma sessão HTTPS com um certificado auto-assinado é Olá mais segura e Olá opção recomendada.</span><span class="sxs-lookup"><span data-stu-id="31f9b-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="31f9b-118">Pode ligar remotamente interface do Windows PowerShell toohello.</span><span class="sxs-lookup"><span data-stu-id="31f9b-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="31f9b-119">No entanto, o dispositivo StorSimple de tooyour de acesso remoto através da interface do Windows PowerShell Olá não está ativado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="31f9b-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="31f9b-120">Precisar tooenable gestão remota no dispositivo Olá primeiro e, em seguida, no Olá cliente que é utilizado tooaccess seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="31f9b-121">passos de Olá descritos neste artigo foram executados num sistema anfitrião com o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="31f9b-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="31f9b-122">Ligar através de HTTP</span><span class="sxs-lookup"><span data-stu-id="31f9b-122">Connect through HTTP</span></span>
<span data-ttu-id="31f9b-123">Ligar tooWindows do PowerShell para StorSimple através de uma sessão HTTP oferece mais segurança a que se ligam através da consola de série de Olá do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="31f9b-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="31f9b-124">Embora não seja método mais seguro Olá, é aceitável em redes fidedignas.</span><span class="sxs-lookup"><span data-stu-id="31f9b-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="31f9b-125">Pode utilizar o Olá portal clássico do Azure ou a gestão remota do Olá consola de série tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="31f9b-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="31f9b-126">Selecione uma das Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="31f9b-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="31f9b-127">Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="31f9b-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="31f9b-128">Utilize a gestão remota do Olá consola de série tooenable através de HTTP</span><span class="sxs-lookup"><span data-stu-id="31f9b-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="31f9b-129">Depois de ativar a gestão remota, utilize Olá seguir o cliente de Olá tooprepare procedimento para uma ligação remota.</span><span class="sxs-lookup"><span data-stu-id="31f9b-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="31f9b-130">Preparar o cliente Olá de ligação remota</span><span class="sxs-lookup"><span data-stu-id="31f9b-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="31f9b-131">Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTP</span><span class="sxs-lookup"><span data-stu-id="31f9b-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="31f9b-132">Efetue Olá seguindo os passos na gestão remota do Olá tooenable de portal clássico do Azure através de HTTP.</span><span class="sxs-lookup"><span data-stu-id="31f9b-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="31f9b-133">gestão remota do tooenable através do Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="31f9b-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="31f9b-134">Acesso **dispositivos** > **configurar** para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="31f9b-135">Desloque para baixo toohello **gestão remota** secção.</span><span class="sxs-lookup"><span data-stu-id="31f9b-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="31f9b-136">Definir **ativar a gestão remota** demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="31f9b-137">Agora, pode escolher tooconnect através de HTTP.</span><span class="sxs-lookup"><span data-stu-id="31f9b-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="31f9b-138">(a predefinição de Olá é tooconnect através de HTTPS.) Certifique-se de que o HTTP está selecionado.</span><span class="sxs-lookup"><span data-stu-id="31f9b-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31f9b-139">A ligação através de HTTP é aceitável apenas em redes fidedignas.</span><span class="sxs-lookup"><span data-stu-id="31f9b-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="31f9b-140">Clique em **guardar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="31f9b-141">Utilize a gestão remota do Olá consola de série tooenable através de HTTP</span><span class="sxs-lookup"><span data-stu-id="31f9b-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="31f9b-142">Efetue Olá os seguintes passos Olá gestão de dispositivos consola de série tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="31f9b-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="31f9b-143">gestão remota do tooenable através da consola de série do dispositivo de Olá</span><span class="sxs-lookup"><span data-stu-id="31f9b-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="31f9b-144">No menu da consola de série de Olá, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="31f9b-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="31f9b-145">Para mais informações sobre como utilizar a consola de série de Olá no dispositivo Olá, visite demasiado[ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="31f9b-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="31f9b-146">Na linha de Olá, escreva:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="31f9b-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="31f9b-147">Será notificado sobre vulnerabilidades de segurança de Olá de utilizar HTTP tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="31f9b-148">Quando lhe for solicitado, confirme escrevendo **Y**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="31f9b-149">Certifique-se de que está ativado HTTP escrevendo:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="31f9b-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="31f9b-150">Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsAndHttpEnabled**.hello seguinte ilustração mostra estas definições no PuTTY.</span><span class="sxs-lookup"><span data-stu-id="31f9b-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Série HTTPS e HTTP ativada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="31f9b-152">Preparar o cliente Olá de ligação remota</span><span class="sxs-lookup"><span data-stu-id="31f9b-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="31f9b-153">Efetue Olá seguindo os passos na gestão remota do Olá cliente tooenable.</span><span class="sxs-lookup"><span data-stu-id="31f9b-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="31f9b-154">cliente de Olá tooprepare para ligação remota</span><span class="sxs-lookup"><span data-stu-id="31f9b-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="31f9b-155">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="31f9b-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="31f9b-156">Escreva Olá seguinte endereço IP do comando tooadd Olá da lista de anfitriões fidedignos Olá StorSimple dispositivo toohello do cliente:</span><span class="sxs-lookup"><span data-stu-id="31f9b-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="31f9b-157">Substitua <*device_ip*> com o endereço IP Olá do seu dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="31f9b-158">Escreva Olá credenciais de dispositivo do comando toosave Olá numa variável os seguintes:</span><span class="sxs-lookup"><span data-stu-id="31f9b-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="31f9b-159">Na caixa de diálogo de Olá que é apresentado:</span><span class="sxs-lookup"><span data-stu-id="31f9b-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="31f9b-160">Nome de utilizador do tipo Olá neste formato: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="31f9b-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="31f9b-161">Escrever Olá dispositivo administrador palavra-passe que foi definido quando o dispositivo de Olá foi configurado com o Assistente de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="31f9b-162">palavra-passe predefinida de Olá é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="31f9b-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="31f9b-163">Inicie uma sessão do Windows PowerShell no dispositivo Olá escrevendo este comando:</span><span class="sxs-lookup"><span data-stu-id="31f9b-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="31f9b-164">toocreate uma sessão do Windows PowerShell para utilização com Olá do dispositivo virtual StorSimple, acrescentar Olá `–Port` parâmetro e especifique a porta pública Olá configurada no sistema de interação remota para o dispositivo Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="31f9b-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="31f9b-165">Nesta fase, deve ter uma Active Directory remota do Windows PowerShell sessão toohello do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Comunicação remota do PowerShell através de HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="31f9b-167">Ligar através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="31f9b-167">Connect through HTTPS</span></span>
<span data-ttu-id="31f9b-168">Ligar tooWindows do PowerShell para StorSimple através de uma sessão HTTPS é Olá mais segura e recomendada método do dispositivo de Microsoft Azure StorSimple tooyour remotamente ao ligar.</span><span class="sxs-lookup"><span data-stu-id="31f9b-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="31f9b-169">Olá procedimentos a seguir explica como tooset segurança Olá série consola e dos computadores cliente para que possa utilizar HTTPS tooconnect tooWindows do PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="31f9b-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="31f9b-170">Pode utilizar o Olá portal clássico do Azure ou a gestão remota do Olá consola de série tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="31f9b-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="31f9b-171">Selecione uma das Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="31f9b-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="31f9b-172">Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="31f9b-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="31f9b-173">Utilize a gestão remota do Olá consola de série tooenable através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="31f9b-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="31f9b-174">Depois de ativar a gestão remota, utilize Olá seguir o anfitrião de Olá tooprepare procedimentos para um gestão remota e ligar o dispositivo de toohello de anfitrião remoto Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="31f9b-175">Preparar o anfitrião de Olá para a gestão remota</span><span class="sxs-lookup"><span data-stu-id="31f9b-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="31f9b-176">Ligar dispositivo toohello de anfitrião remoto Olá</span><span class="sxs-lookup"><span data-stu-id="31f9b-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="31f9b-177">Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="31f9b-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="31f9b-178">Efetue Olá seguindo os passos na gestão remota do Olá tooenable de portal clássico do Azure através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31f9b-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="31f9b-179">gestão remota tooenable através de HTTPS de Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="31f9b-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="31f9b-180">Acesso **dispositivos** > **configurar** para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="31f9b-181">Desloque para baixo toohello **gestão remota** secção.</span><span class="sxs-lookup"><span data-stu-id="31f9b-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="31f9b-182">Definir **ativar a gestão remota** demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="31f9b-183">Agora, pode escolher tooconnect através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31f9b-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="31f9b-184">(a predefinição de Olá é tooconnect através de HTTPS.) Certifique-se de que o HTTPS é selecionado.</span><span class="sxs-lookup"><span data-stu-id="31f9b-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="31f9b-185">Clique em **Transferir certificado de gestão remota**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="31f9b-186">Especifique uma localização toosave este ficheiro.</span><span class="sxs-lookup"><span data-stu-id="31f9b-186">Specify a location toosave this file.</span></span> <span data-ttu-id="31f9b-187">Terá de tooinstall este certificado no computador de cliente ou anfitrião Olá que irá utilizar tooconnect toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="31f9b-188">Clique em **guardar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="31f9b-189">Utilize a gestão remota do Olá consola de série tooenable através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="31f9b-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="31f9b-190">Efetue Olá os seguintes passos Olá gestão de dispositivos consola de série tooenable remoto.</span><span class="sxs-lookup"><span data-stu-id="31f9b-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="31f9b-191">gestão remota do tooenable através da consola de série do dispositivo de Olá</span><span class="sxs-lookup"><span data-stu-id="31f9b-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="31f9b-192">No menu da consola de série de Olá, selecione a opção 1.</span><span class="sxs-lookup"><span data-stu-id="31f9b-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="31f9b-193">Para mais informações sobre como utilizar a consola de série de Olá no dispositivo Olá, visite demasiado[ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="31f9b-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="31f9b-194">Na linha de Olá, escreva:</span><span class="sxs-lookup"><span data-stu-id="31f9b-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="31f9b-195">Isto deve ativar HTTPS no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="31f9b-196">Certifique-se de que foi ativado HTTPS, escrevendo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="31f9b-197">Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsEnabled**.hello seguinte ilustração mostra estas definições no PuTTY.</span><span class="sxs-lookup"><span data-stu-id="31f9b-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Série ativadas por HTTPS](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="31f9b-199">Da saída de Olá de `Get-HcsSystem`, copie Olá o número de série do dispositivo Olá e guardá-lo para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="31f9b-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31f9b-200">número de série de Olá mapeia o nome CN de toohello no certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="31f9b-201">Obter um certificado de gestão remota, escrevendo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="31f9b-202">Será apresentada a seguinte de toohello semelhante um certificado.</span><span class="sxs-lookup"><span data-stu-id="31f9b-202">A certificate similar toohello following will appear.</span></span>
   
    ![Obter o certificado de gestão remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="31f9b-204">Copiar as informações de Olá certificado Olá **---BEGIN CERTIFICATE---** demasiado**---fim certificado---** num editor de texto, como o bloco de notas e guarde-como um ficheiro. cer.</span><span class="sxs-lookup"><span data-stu-id="31f9b-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="31f9b-205">(Vai copiar este anfitrião remoto da tooyour de ficheiro ao preparar o anfitrião de Olá.)</span><span class="sxs-lookup"><span data-stu-id="31f9b-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31f9b-206">toogenerate um novo certificado, utilize Olá `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31f9b-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="31f9b-207">Preparar o anfitrião de Olá para a gestão remota</span><span class="sxs-lookup"><span data-stu-id="31f9b-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="31f9b-208">computador de anfitrião de Olá tooprepare para uma ligação remota que utiliza uma sessão HTTPS, execute Olá os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="31f9b-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="31f9b-209">[Ficheiro. cer de Olá de importação para arquivo de raiz de hello do cliente Olá ou anfitrião remoto](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="31f9b-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="31f9b-210">[Adicionar ficheiro hosts toohello de números de série de dispositivos de Olá no seu anfitrião remoto](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="31f9b-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="31f9b-211">Cada um destes procedimentos é descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="31f9b-212">certificado de Olá tooimport no anfitrião remoto Olá</span><span class="sxs-lookup"><span data-stu-id="31f9b-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="31f9b-213">Clique no ficheiro. cer de Olá e selecione **instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="31f9b-214">Esta ação iniciará Olá Assistente para importar certificados.</span><span class="sxs-lookup"><span data-stu-id="31f9b-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Assistente de importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="31f9b-216">Para **localização do arquivo**, selecione **máquina Local**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="31f9b-217">Selecione **colocar todos os certificados no Olá seguir arquivo**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="31f9b-218">Navegue toohello o arquivo de raiz do seu anfitrião remoto e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistente de importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="31f9b-220">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-220">Click **Finish**.</span></span> <span data-ttu-id="31f9b-221">É apresentada uma mensagem que indica que a importação de Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="31f9b-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Assistente de importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="31f9b-223">anfitrião remoto de toohello números de série de dispositivo tooadd</span><span class="sxs-lookup"><span data-stu-id="31f9b-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="31f9b-224">Inicie o bloco de notas como administrador e, em seguida, abra o ficheiro de anfitriões de Olá localizado em \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="31f9b-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="31f9b-225">Adicionar Olá seguintes três ficheiro de anfitriões de tooyour entradas: **endereço IP de dados 0**, **endereço de IP fixo do controlador 0**, e **endereço IP fixo do controlador 1**.</span><span class="sxs-lookup"><span data-stu-id="31f9b-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="31f9b-226">Introduza o número de série do dispositivo Olá que guardou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31f9b-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="31f9b-227">Mapear este endereço IP toohello conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="31f9b-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="31f9b-228">Para o controlador 0 e 1 de controlador, acrescentar **Controller0** e **Controller1** no fim de Olá do número de série de Olá (nome CN).</span><span class="sxs-lookup"><span data-stu-id="31f9b-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Adicionar nome CN toohosts ficheiro](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="31f9b-230">Ficheiro de anfitriões de Olá guardado.</span><span class="sxs-lookup"><span data-stu-id="31f9b-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="31f9b-231">Ligar dispositivo toohello de anfitrião remoto Olá</span><span class="sxs-lookup"><span data-stu-id="31f9b-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="31f9b-232">Utilizar o Windows PowerShell e do SSL tooenter uma sessão de SSAdmin no seu dispositivo a partir de um anfitrião remoto ou o cliente.</span><span class="sxs-lookup"><span data-stu-id="31f9b-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="31f9b-233">sessão de SSAdmin Olá mapeia toooption 1 na Olá [consola de série](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="31f9b-234">Efetue Olá seguir o procedimento no computador de Olá partir do qual pretende que a ligação do toomake Olá remota do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31f9b-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="31f9b-235">tooenter uma sessão de SSAdmin no dispositivo de Olá através do Windows PowerShell e do SSL</span><span class="sxs-lookup"><span data-stu-id="31f9b-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="31f9b-236">Inicie uma sessão do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="31f9b-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="31f9b-237">Adicione anfitriões fidedignos Olá dispositivo IP endereço toohello do cliente, escrevendo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="31f9b-238">Onde <*device_ip*> é o endereço IP Olá do seu dispositivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="31f9b-239">Crie uma credencial nova escrevendo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="31f9b-240">Onde <*IP do dispositivo-alvo*> é o endereço IP Olá de dados 0 para o seu dispositivo; por exemplo, **10.126.173.90** conforme mostrado no Olá anterior a imagem do ficheiro de anfitriões de Olá.</span><span class="sxs-lookup"><span data-stu-id="31f9b-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="31f9b-241">Além disso, forneça a palavra-passe de administrador de Olá para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="31f9b-242">Crie uma sessão introduzindo:</span><span class="sxs-lookup"><span data-stu-id="31f9b-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="31f9b-243">Para o parâmetro - ComputerName de Olá no cmdlet Olá, fornecer Olá <*número de série do dispositivo-alvo*>.</span><span class="sxs-lookup"><span data-stu-id="31f9b-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="31f9b-244">Este número de série foi mapeado toohello endereço IP de dados 0 no ficheiro de anfitriões de Olá no seu anfitrião remoto; Por exemplo, **SHX0991003G44MT** conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="31f9b-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="31f9b-245">Escreva:</span><span class="sxs-lookup"><span data-stu-id="31f9b-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="31f9b-246">Terá de toowait uns minutos e, em seguida, será dispositivo tooyour ligado através de HTTPS através de SSL.</span><span class="sxs-lookup"><span data-stu-id="31f9b-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="31f9b-247">Verá uma mensagem que indica que está ligado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="31f9b-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![Comunicação remota do PowerShell através de HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="31f9b-249">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="31f9b-249">Next steps</span></span>
* <span data-ttu-id="31f9b-250">Saiba mais sobre [através do Windows PowerShell tooadminister o dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="31f9b-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="31f9b-251">Saiba mais sobre [utilizando Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="31f9b-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

