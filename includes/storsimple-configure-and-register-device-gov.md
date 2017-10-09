<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="7c51e-101">dispositivo de Olá tooconfigure e registar</span><span class="sxs-lookup"><span data-stu-id="7c51e-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="7c51e-102">Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7c51e-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="7c51e-103">Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="7c51e-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="7c51e-104">**Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**</span><span class="sxs-lookup"><span data-stu-id="7c51e-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="7c51e-105">Na sessão de Olá que se abre, prima Enter uma vez tooget numa linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7c51e-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span> 
3. <span data-ttu-id="7c51e-106">Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c51e-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="7c51e-107">Especifique idiomas Olá e, em seguida, prima Enter.</span><span class="sxs-lookup"><span data-stu-id="7c51e-107">Specify hello language, and then press Enter.</span></span> 
   
    ![Configurar e registar o dispositivo 1 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="7c51e-109">No menu da consola de série de Olá que é apresentado, escolha a opção 1 toolog com acesso total.</span><span class="sxs-lookup"><span data-stu-id="7c51e-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span> 
   
    ![Registar o dispositivo 2 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="7c51e-111">Efetue Olá os seguintes passos tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c51e-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7c51e-112">Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="7c51e-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="7c51e-113">menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c51e-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="7c51e-114">Se não são ligar toohello de controlador ativo, desligue e, em seguida, ligar o controlador de Active Directory toohello.</span><span class="sxs-lookup"><span data-stu-id="7c51e-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="7c51e-115">Na linha de comandos Olá, escreva a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="7c51e-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="7c51e-116">palavra-passe de dispositivo do Olá predefinida é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="7c51e-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="7c51e-117">Escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7c51e-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="7c51e-118">Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="7c51e-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="7c51e-119">Fornecer Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="7c51e-119">Supply hello following information:</span></span> 
      
      * <span data-ttu-id="7c51e-120">Endereço de IP da interface rede DATA 0</span><span class="sxs-lookup"><span data-stu-id="7c51e-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="7c51e-121">Máscara de sub-rede</span><span class="sxs-lookup"><span data-stu-id="7c51e-121">Subnet mask</span></span>
      * <span data-ttu-id="7c51e-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="7c51e-122">Gateway</span></span>
      * <span data-ttu-id="7c51e-123">Endereço IP do servidor DNS Primário</span><span class="sxs-lookup"><span data-stu-id="7c51e-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="7c51e-124">Endereço IP do servidor NTP Primário</span><span class="sxs-lookup"><span data-stu-id="7c51e-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7c51e-125">Poderá ter toowait alguns minutos para máscara de sub-rede Olá e toobe de definições de DNS aplicada.</span><span class="sxs-lookup"><span data-stu-id="7c51e-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="7c51e-126">Opcionalmente, configure o servidor proxy web.</span><span class="sxs-lookup"><span data-stu-id="7c51e-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="7c51e-127">Apesar da configuração de proxy web é opcional, lembre-se de que se utilizar um proxy web, só pode configurá-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="7c51e-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="7c51e-128">Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="7c51e-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="7c51e-129">Prima Ctrl + C Assistente de configuração de Olá tooexit.</span><span class="sxs-lookup"><span data-stu-id="7c51e-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="7c51e-130">Instale atualizações de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7c51e-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="7c51e-131">Utilize Olá os seguintes cmdlet tooset IPs em ambos os controladores de Olá:</span><span class="sxs-lookup"><span data-stu-id="7c51e-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="7c51e-132">Na linha de comandos Olá, execute `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="7c51e-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="7c51e-133">Devem ser notificados que atualizações estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7c51e-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="7c51e-134">Execute `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="7c51e-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="7c51e-135">Pode executar este comando em qualquer nó.</span><span class="sxs-lookup"><span data-stu-id="7c51e-135">You can run this command on any node.</span></span> <span data-ttu-id="7c51e-136">Actualizações serão aplicadas no primeiro controlador de Olá, controlador Olá irá efetuar a ativação pós-falha e, em seguida, Olá actualizações serão aplicadas no Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="7c51e-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="7c51e-137">Poderá monitorizar Olá progresso da atualização de Olá executando `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="7c51e-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="7c51e-138">Olá saída de exemplo seguinte mostra Olá atualização em curso.</span><span class="sxs-lookup"><span data-stu-id="7c51e-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="7c51e-139">Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="7c51e-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="7c51e-140">Esta operação pode demorar horas too11 tooapply Olá todas as atualizações, incluindo Olá atualizações do Windows.</span><span class="sxs-lookup"><span data-stu-id="7c51e-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>

8. <span data-ttu-id="7c51e-141">Após todos os hello atualizações são instaladas com êxito, hello execute seguintes cmdlet tooconfirm que Olá foram corretamente aplicadas as atualizações de software:</span><span class="sxs-lookup"><span data-stu-id="7c51e-141">After all hello updates are successfully installed, run hello following cmdlet tooconfirm that hello software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="7c51e-142">Deverá ver Olá seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="7c51e-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="7c51e-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="7c51e-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="7c51e-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="7c51e-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="7c51e-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="7c51e-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="7c51e-146">Olá execute os seguintes cmdlet tooconfirm que Olá atualização de firmware foi aplicado corretamente:</span><span class="sxs-lookup"><span data-stu-id="7c51e-146">Run hello following cmdlet tooconfirm that hello firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="7c51e-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="7c51e-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="7c51e-148">Estado do firmware Olá deve ser **UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="7c51e-148">hello firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="7c51e-149">Execute Olá seguir o portal do Microsoft Azure Government de cmdlet toopoint Olá dispositivos toohello (porque aponta portal clássico do Azure público toohello por predefinição).</span><span class="sxs-lookup"><span data-stu-id="7c51e-149">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="7c51e-150">Esta ação irá reiniciar tanto os controladores.</span><span class="sxs-lookup"><span data-stu-id="7c51e-150">This will restart both controllers.</span></span> <span data-ttu-id="7c51e-151">Recomendamos que utilize sessões PuTTY dois toosimultaneously ligar tooboth controladores para que possa ver quando cada controlador é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="7c51e-151">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="7c51e-152">Verá uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="7c51e-152">You will see a confirmation message.</span></span> <span data-ttu-id="7c51e-153">Aceite a predefinição de Olá (**Y**).</span><span class="sxs-lookup"><span data-stu-id="7c51e-153">Accept hello default (**Y**).</span></span>
11. <span data-ttu-id="7c51e-154">Execute Olá cmdlet tooresume configuração os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7c51e-154">Run hello following cmdlet tooresume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Assistente de configuração de retomar](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="7c51e-156">Quando retomar a configuração, o Assistente de Olá será versão Olá atualização 1 (o que corresponde tooversion 17469).</span><span class="sxs-lookup"><span data-stu-id="7c51e-156">When you resume setup, hello wizard will be hello Update 1 version (which corresponds tooversion 17469).</span></span> 
12. <span data-ttu-id="7c51e-157">Aceite as definições de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7c51e-157">Accept hello network settings.</span></span> <span data-ttu-id="7c51e-158">Verá uma mensagem de validação após a aceitação de cada definição.</span><span class="sxs-lookup"><span data-stu-id="7c51e-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="7c51e-159">Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora.</span><span class="sxs-lookup"><span data-stu-id="7c51e-159">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="7c51e-160">Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c51e-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="7c51e-161">Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres.</span><span class="sxs-lookup"><span data-stu-id="7c51e-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="7c51e-162">Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.</span><span class="sxs-lookup"><span data-stu-id="7c51e-162">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Registar o dispositivo 5 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="7c51e-164">passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7c51e-164">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="7c51e-165">Para tal, será necessário Olá, chave de registo do serviço que obteve no [passo 2: chave de registo do serviço de Olá Get](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="7c51e-165">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="7c51e-166">Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.</span><span class="sxs-lookup"><span data-stu-id="7c51e-166">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7c51e-167">Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá.</span><span class="sxs-lookup"><span data-stu-id="7c51e-167">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="7c51e-168">Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="7c51e-168">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progresso de registo do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="7c51e-170">Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço.</span><span class="sxs-lookup"><span data-stu-id="7c51e-170">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="7c51e-171">Copie esta chave e guarde-a numa localização segura.</span><span class="sxs-lookup"><span data-stu-id="7c51e-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="7c51e-172">**Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="7c51e-172">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="7c51e-173">Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.</span><span class="sxs-lookup"><span data-stu-id="7c51e-173">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="7c51e-175">texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá.</span><span class="sxs-lookup"><span data-stu-id="7c51e-175">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="7c51e-176">Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7c51e-176">You should then be able toopaste it in hello clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="7c51e-177">Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C.</span><span class="sxs-lookup"><span data-stu-id="7c51e-177">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="7c51e-178">Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração.</span><span class="sxs-lookup"><span data-stu-id="7c51e-178">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="7c51e-179">Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.</span><span class="sxs-lookup"><span data-stu-id="7c51e-179">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
16. <span data-ttu-id="7c51e-180">Consola de série de Olá saída.</span><span class="sxs-lookup"><span data-stu-id="7c51e-180">Exit hello serial console.</span></span>
17. <span data-ttu-id="7c51e-181">Devolver toohello Portal do Azure Government e concluir Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7c51e-181">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="7c51e-182">Faça duplo clique em seu Olá de tooaccess do serviço StorSimple Manager **início rápido** página.</span><span class="sxs-lookup"><span data-stu-id="7c51e-182">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="7c51e-183">Clique em **Ver dispositivos ligados**.</span><span class="sxs-lookup"><span data-stu-id="7c51e-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="7c51e-184">No Olá **dispositivos** página, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c51e-184">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="7c51e-185">Estado do dispositivo Olá deve ser **Online**.</span><span class="sxs-lookup"><span data-stu-id="7c51e-185">hello device status should be **Online**.</span></span>
       
        ![Página Dispositivos do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="7c51e-187">Se o estado do dispositivo Olá for **Offline**, aguarde alguns minutos para Olá toocome de dispositivo online.</span><span class="sxs-lookup"><span data-stu-id="7c51e-187">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span> 
       
        <span data-ttu-id="7c51e-188">Se o dispositivo de Olá é continuar offline mesmo após alguns minutos, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7c51e-188">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="7c51e-189">Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação de serviço para o dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7c51e-189">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager service-to-device communication.</span></span>

