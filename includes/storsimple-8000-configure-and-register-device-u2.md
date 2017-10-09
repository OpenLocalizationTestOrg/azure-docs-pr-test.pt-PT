<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="dcb93-101">dispositivo de Olá tooconfigure e registar</span><span class="sxs-lookup"><span data-stu-id="dcb93-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="dcb93-102">Aceder à interface do Windows PowerShell Olá na consola de série do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dcb93-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="dcb93-103">Consulte [utilizar o PuTTY tooconnect toohello consola de série dispositivo](#use-putty-to-connect-to-the-device-serial-console) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="dcb93-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="dcb93-104">**Ser exatamente o procedimento de Olá toofollow se ou não será capaz de tooaccess consola de Olá.**</span><span class="sxs-lookup"><span data-stu-id="dcb93-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="dcb93-105">Na sessão de Olá que se abre, prima **Enter** um tempo tooget numa linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="dcb93-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="dcb93-106">Será pedido toochoose Olá idioma que pretende tooset para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="dcb93-107">Especifique o idioma Olá e, em seguida, prima **Enter**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="dcb93-108">No menu da consola de série de Olá que é apresentado, selecione a opção 1 demasiado**iniciar sessão com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="dcb93-109">Conclua os passos 5 a 12 tooconfigure Olá mínimo necessário as definições de rede para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="dcb93-110">**Estes passos de configuração necessário toobe efetuada em Olá controlador ativo do dispositivo Olá.**</span><span class="sxs-lookup"><span data-stu-id="dcb93-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="dcb93-111">menu da consola de série de Olá indica o estado do controlador Olá na mensagem de faixa de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcb93-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="dcb93-112">Se não estiver ligado toohello de controlador ativo, desligue e, em seguida, ligar o controlador toohello de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dcb93-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="dcb93-113">Na linha de comandos Olá, escreva a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="dcb93-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="dcb93-114">palavra-passe de dispositivo do Olá predefinida é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="dcb93-115">Olá tipo os seguintes comandos: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="dcb93-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="dcb93-116">Um Assistente de configuração irá aparecer toohelp configurar definições de rede Olá para dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="dcb93-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="dcb93-117">Fornecer Olá Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="dcb93-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="dcb93-118">Endereço IP para Olá interface rede DATA 0</span><span class="sxs-lookup"><span data-stu-id="dcb93-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="dcb93-119">Máscara de sub-rede</span><span class="sxs-lookup"><span data-stu-id="dcb93-119">Subnet mask</span></span>
   * <span data-ttu-id="dcb93-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="dcb93-120">Gateway</span></span>
   * <span data-ttu-id="dcb93-121">Endereço IP do servidor DNS Primário</span><span class="sxs-lookup"><span data-stu-id="dcb93-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="dcb93-122">É apresentada uma saída de exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="dcb93-123">Olá anterior a saída de exemplo, pode ver que o sistema Olá é validar as definições de rede após cada passo no processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcb93-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dcb93-124">Poderá ter toowait alguns minutos para máscara de sub-rede Olá e as definições de DNS do Olá toobe aplicada.</span><span class="sxs-lookup"><span data-stu-id="dcb93-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="dcb93-125">Se receber uma mensagem de erro de "Verificação Olá rede conectividade tooData 0", verifique a ligação de rede física Olá no Olá interface rede DATA 0 do controlador ativo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="dcb93-126">(Opcional) Configure o servidor proxy Web.</span><span class="sxs-lookup"><span data-stu-id="dcb93-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="dcb93-127">Apesar de a configuração do proxy Web ser opcional, **tenha em atenção que se utilizar um proxy Web, só pode configurá-lo aqui**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="dcb93-128">Para mais informações, visite demasiado[configurar o proxy web para o seu dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="dcb93-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="dcb93-129">Configure um servidor NTP Primário para o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="dcb93-130">Os servidores NTP são obrigatórios, uma vez que o seu dispositivo tem de sincronizar a hora para se poder autenticar junto dos fornecedores de serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="dcb93-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="dcb93-131">Certifique-se de que a sua rede permite toopass de tráfego NTP do seu centro de dados de toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="dcb93-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="dcb93-132">Se esta ação não for possível, especifique um servidor NTP interno.</span><span class="sxs-lookup"><span data-stu-id="dcb93-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="dcb93-133">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="dcb93-134">Por motivos de segurança, a palavra-passe de administrador de dispositivo Olá expira após Olá primeira sessão e terá de toochange it agora.</span><span class="sxs-lookup"><span data-stu-id="dcb93-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="dcb93-135">Quando lhe for solicitado, forneça uma palavra-passe de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="dcb93-136">Uma palavra-passe de administrador do dispositivo válida tem de ter entre 8 e 15 carateres.</span><span class="sxs-lookup"><span data-stu-id="dcb93-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="dcb93-137">Olá palavra-passe tem de conter três dos seguintes Olá: carateres em minúsculas, maiúsculas, numérico e especiais.</span><span class="sxs-lookup"><span data-stu-id="dcb93-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="dcb93-138">passo final do Olá no Assistente de configuração de Olá regista o dispositivo com Olá serviço StorSimple Manager do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="dcb93-139">Para tal, terá de chave de registo do serviço Olá que obteve no passo 2.</span><span class="sxs-lookup"><span data-stu-id="dcb93-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="dcb93-140">Depois de fornecer a chave de registo Olá, poderá ser necessário toowait para 2 a 3 minutos antes do dispositivo de Olá está registado.</span><span class="sxs-lookup"><span data-stu-id="dcb93-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="dcb93-141">Pode premir Ctrl + C em qualquer Assistente de configuração do tempo tooexit Olá.</span><span class="sxs-lookup"><span data-stu-id="dcb93-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="dcb93-142">Se tiver introduzido todas as definições de rede de Olá (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="dcb93-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="dcb93-143">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="dcb93-144">Depois do dispositivo de Olá estiver registado, será apresentada uma chave de encriptação de dados do serviço.</span><span class="sxs-lookup"><span data-stu-id="dcb93-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="dcb93-145">Copie esta chave e guarde-a numa localização segura.</span><span class="sxs-lookup"><span data-stu-id="dcb93-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="dcb93-146">**Esta chave será necessária com Olá serviço registo tooregister chave dispositivos adicionais com Olá serviço StorSimple Manager do dispositivo.**</span><span class="sxs-lookup"><span data-stu-id="dcb93-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="dcb93-147">Consulte demasiado[segurança do StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre esta chave.</span><span class="sxs-lookup"><span data-stu-id="dcb93-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Registar o dispositivo 7 do StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="dcb93-149">texto de Olá toocopy da janela de consola de série de Olá, basta selecionar texto Olá.</span><span class="sxs-lookup"><span data-stu-id="dcb93-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="dcb93-150">Em seguida, deve ser capaz de toopaste-la na área de transferência Olá ou qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="dcb93-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="dcb93-151">Não utilize Ctrl + chave de encriptação de dados de serviço Olá toocopy C.</span><span class="sxs-lookup"><span data-stu-id="dcb93-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="dcb93-152">Utilização de Ctrl + C fará com tooexit Olá Assistente de configuração.</span><span class="sxs-lookup"><span data-stu-id="dcb93-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="dcb93-153">Como resultado, não será possível alterar a palavra-passe de administrador de dispositivo Olá e dispositivo Olá irá reverter a palavra-passe do toohello predefinida.</span><span class="sxs-lookup"><span data-stu-id="dcb93-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="dcb93-154">Consola de série de Olá saída.</span><span class="sxs-lookup"><span data-stu-id="dcb93-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="dcb93-155">Devolver toohello portal do Azure e concluir Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="dcb93-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="dcb93-156">Aceda tooyour do serviço StorSimple Manager de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dcb93-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="dcb93-157">Clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="dcb93-158">Na tabela de lista de dispositivos de Olá, certifique-se de que o dispositivo Olá foi ligado com êxito toohello serviço ao procurar o estado de Olá.</span><span class="sxs-lookup"><span data-stu-id="dcb93-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="dcb93-159">Estado do dispositivo Olá deve ser **pronto tooset segurança**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Página Dispositivos do StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="dcb93-161">Poderá ser necessário toowait para alguns minutos para toochange de estado do dispositivo Olá**pronto tooset segurança**.</span><span class="sxs-lookup"><span data-stu-id="dcb93-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="dcb93-162">Se o dispositivo de Olá não for apresentada nesta lista, em seguida, tem de certificar-se de que a sua rede de firewall foi configurada conforme descrito em toomake [requisitos de rede para o dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="dcb93-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="dcb93-163">Certifique-se de que a porta 9354 está aberta para comunicação de saída como é utilizada pelo barramento de serviço Olá para comunicação de dispositivo de serviço do Gestor de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dcb93-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

