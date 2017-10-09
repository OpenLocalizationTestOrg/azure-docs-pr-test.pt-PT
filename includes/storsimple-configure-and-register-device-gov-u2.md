<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="ad5db-101">dispositivo de Olá tooconfigure e registar</span><span class="sxs-lookup"><span data-stu-id="ad5db-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="ad5db-102">Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ad5db-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="ad5db-103">Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="ad5db-103">See [Use PuTTY tooconnect toohello device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="ad5db-104">**Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**</span><span class="sxs-lookup"><span data-stu-id="ad5db-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="ad5db-105">Na sessão de Olá que se abre, prima Enter uma vez tooget numa linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="ad5db-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span>
3. <span data-ttu-id="ad5db-106">Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad5db-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="ad5db-107">Especifique idiomas Olá e, em seguida, prima Enter.</span><span class="sxs-lookup"><span data-stu-id="ad5db-107">Specify hello language, and then press Enter.</span></span>
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="ad5db-109">No menu da consola de série de Olá que é apresentado, escolha a opção 1 toolog com acesso total.</span><span class="sxs-lookup"><span data-stu-id="ad5db-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span>
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="ad5db-111">Efetue Olá os seguintes passos tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad5db-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ad5db-112">Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="ad5db-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="ad5db-113">menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação.</span><span class="sxs-lookup"><span data-stu-id="ad5db-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="ad5db-114">Se não são ligar toohello de controlador ativo, desligue e, em seguida, ligar o controlador de Active Directory toohello.</span><span class="sxs-lookup"><span data-stu-id="ad5db-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="ad5db-115">Na linha de comandos Olá, escreva a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="ad5db-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="ad5db-116">palavra-passe de dispositivo do Olá predefinida é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="ad5db-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="ad5db-117">Escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ad5db-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="ad5db-118">Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="ad5db-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="ad5db-119">Fornecer Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="ad5db-119">Supply hello following information:</span></span>
      
      * <span data-ttu-id="ad5db-120">Endereço de IP da interface rede DATA 0</span><span class="sxs-lookup"><span data-stu-id="ad5db-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="ad5db-121">Máscara de sub-rede</span><span class="sxs-lookup"><span data-stu-id="ad5db-121">Subnet mask</span></span>
      * <span data-ttu-id="ad5db-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="ad5db-122">Gateway</span></span>
      * <span data-ttu-id="ad5db-123">Endereço IP do servidor DNS Primário</span><span class="sxs-lookup"><span data-stu-id="ad5db-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="ad5db-124">Endereço IP do servidor NTP Primário</span><span class="sxs-lookup"><span data-stu-id="ad5db-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ad5db-125">Poderá ter toowait alguns minutos para máscara de sub-rede Olá e toobe de definições de DNS aplicada.</span><span class="sxs-lookup"><span data-stu-id="ad5db-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="ad5db-126">Opcionalmente, configure o servidor proxy web.</span><span class="sxs-lookup"><span data-stu-id="ad5db-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="ad5db-127">Apesar da configuração de proxy web é opcional, lembre-se de que se utilizar um proxy web, só pode configurá-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="ad5db-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="ad5db-128">Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="ad5db-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="ad5db-129">Prima Ctrl + C Assistente de configuração de Olá tooexit.</span><span class="sxs-lookup"><span data-stu-id="ad5db-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="ad5db-130">Instale atualizações de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ad5db-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="ad5db-131">Utilize Olá os seguintes cmdlet tooset IPs em ambos os controladores de Olá:</span><span class="sxs-lookup"><span data-stu-id="ad5db-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="ad5db-132">Na linha de comandos Olá, execute `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="ad5db-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="ad5db-133">Devem ser notificados que atualizações estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ad5db-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="ad5db-134">Execute `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="ad5db-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="ad5db-135">Pode executar este comando em qualquer nó.</span><span class="sxs-lookup"><span data-stu-id="ad5db-135">You can run this command on any node.</span></span> <span data-ttu-id="ad5db-136">Actualizações serão aplicadas no primeiro controlador de Olá, controlador Olá irá efetuar a ativação pós-falha e, em seguida, Olá actualizações serão aplicadas no Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="ad5db-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="ad5db-137">Poderá monitorizar Olá progresso da atualização de Olá executando `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="ad5db-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="ad5db-138">Olá saída de exemplo seguinte mostra Olá atualização em curso.</span><span class="sxs-lookup"><span data-stu-id="ad5db-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="ad5db-139">Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="ad5db-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="ad5db-140">Esta operação pode demorar horas too11 tooapply Olá todas as atualizações, incluindo Olá atualizações do Windows.</span><span class="sxs-lookup"><span data-stu-id="ad5db-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>
8. <span data-ttu-id="ad5db-141">Execute Olá seguir o portal do Microsoft Azure Government de cmdlet toopoint Olá dispositivos toohello (porque aponta portal clássico do Azure público toohello por predefinição).</span><span class="sxs-lookup"><span data-stu-id="ad5db-141">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="ad5db-142">Esta ação irá reiniciar tanto os controladores.</span><span class="sxs-lookup"><span data-stu-id="ad5db-142">This will restart both controllers.</span></span> <span data-ttu-id="ad5db-143">Recomendamos que utilize sessões PuTTY dois toosimultaneously ligar tooboth controladores para que possa ver quando cada controlador é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="ad5db-143">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="ad5db-144">Verá uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="ad5db-144">You will see a confirmation message.</span></span> <span data-ttu-id="ad5db-145">Aceite a predefinição de Olá (**Y**).</span><span class="sxs-lookup"><span data-stu-id="ad5db-145">Accept hello default (**Y**).</span></span>
9. <span data-ttu-id="ad5db-146">Execute Olá cmdlet tooresume configuração os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ad5db-146">Run hello following cmdlet tooresume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Assistente de configuração de retomar](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="ad5db-148">Quando retomar a configuração, o Assistente de Olá será versão Olá Update 2.</span><span class="sxs-lookup"><span data-stu-id="ad5db-148">When you resume setup, hello wizard will be hello Update 2 version.</span></span>
10. <span data-ttu-id="ad5db-149">Aceite as definições de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="ad5db-149">Accept hello network settings.</span></span> <span data-ttu-id="ad5db-150">Verá uma mensagem de validação após a aceitação de cada definição.</span><span class="sxs-lookup"><span data-stu-id="ad5db-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="ad5db-151">Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora.</span><span class="sxs-lookup"><span data-stu-id="ad5db-151">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="ad5db-152">Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad5db-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="ad5db-153">Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres.</span><span class="sxs-lookup"><span data-stu-id="ad5db-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="ad5db-154">Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.</span><span class="sxs-lookup"><span data-stu-id="ad5db-154">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Registar o dispositivo 5 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="ad5db-156">passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="ad5db-156">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="ad5db-157">Para tal, será necessário Olá, chave de registo do serviço que obteve no [passo 2: chave de registo do serviço de Olá Get](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="ad5db-157">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="ad5db-158">Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.</span><span class="sxs-lookup"><span data-stu-id="ad5db-158">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ad5db-159">Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá.</span><span class="sxs-lookup"><span data-stu-id="ad5db-159">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="ad5db-160">Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="ad5db-160">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progresso de registo do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="ad5db-162">Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço.</span><span class="sxs-lookup"><span data-stu-id="ad5db-162">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="ad5db-163">Copie esta chave e guarde-a numa localização segura.</span><span class="sxs-lookup"><span data-stu-id="ad5db-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="ad5db-164">**Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="ad5db-164">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="ad5db-165">Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.</span><span class="sxs-lookup"><span data-stu-id="ad5db-165">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="ad5db-167">texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá.</span><span class="sxs-lookup"><span data-stu-id="ad5db-167">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="ad5db-168">Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="ad5db-168">You should then be able toopaste it in hello clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="ad5db-169">Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C.</span><span class="sxs-lookup"><span data-stu-id="ad5db-169">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="ad5db-170">Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração.</span><span class="sxs-lookup"><span data-stu-id="ad5db-170">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="ad5db-171">Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.</span><span class="sxs-lookup"><span data-stu-id="ad5db-171">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
14. <span data-ttu-id="ad5db-172">Consola de série de Olá saída.</span><span class="sxs-lookup"><span data-stu-id="ad5db-172">Exit hello serial console.</span></span>
15. <span data-ttu-id="ad5db-173">Devolver toohello Portal do Azure Government e concluir Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ad5db-173">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="ad5db-174">Faça duplo clique em seu Olá de tooaccess do serviço StorSimple Manager **início rápido** página.</span><span class="sxs-lookup"><span data-stu-id="ad5db-174">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="ad5db-175">Clique em **Ver dispositivos ligados**.</span><span class="sxs-lookup"><span data-stu-id="ad5db-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="ad5db-176">No Olá **dispositivos** página, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá.</span><span class="sxs-lookup"><span data-stu-id="ad5db-176">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="ad5db-177">Estado do dispositivo Olá deve ser **Online**.</span><span class="sxs-lookup"><span data-stu-id="ad5db-177">hello device status should be **Online**.</span></span>
       
        ![Página Dispositivos do StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="ad5db-179">Se o estado do dispositivo Olá for **Offline**, aguarde alguns minutos para Olá toocome de dispositivo online.</span><span class="sxs-lookup"><span data-stu-id="ad5db-179">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span>
       
        <span data-ttu-id="ad5db-180">Se o dispositivo de Olá é continuar offline mesmo após alguns minutos, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ad5db-180">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="ad5db-181">Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação do StorSimple Manager serviço para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad5db-181">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager Service-to-device communication.</span></span>

