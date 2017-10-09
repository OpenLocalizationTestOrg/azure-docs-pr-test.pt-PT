<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="3f457-101">correções toodownload</span><span class="sxs-lookup"><span data-stu-id="3f457-101">toodownload hotfixes</span></span>
<span data-ttu-id="3f457-102">Efetue Olá os seguintes passos toodownload Olá atualização de software.</span><span class="sxs-lookup"><span data-stu-id="3f457-102">Perform hello following steps toodownload hello software update.</span></span>

1. <span data-ttu-id="3f457-103">Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3f457-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="3f457-104">Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="3f457-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="3f457-105">![Instalar o catálogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="3f457-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="3f457-106">Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload, por exemplo **3063418**e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="3f457-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="3f457-107">Verá Olá **StorSimple atualização 1.2 aplicação atualização** pacote.</span><span class="sxs-lookup"><span data-stu-id="3f457-107">You will see hello **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="3f457-108">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3f457-108">Click **Add**.</span></span> <span data-ttu-id="3f457-109">atualização de Olá será adicionada toohello cesto.</span><span class="sxs-lookup"><span data-stu-id="3f457-109">hello update will be added toohello basket.</span></span>
5. <span data-ttu-id="3f457-110">Procure as correções adicionais listados na tabela de Olá acima (**3043005** e **3063416**) e adicione cada cesto Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-110">Search for any additional hotfixes listed in hello table above (**3043005** and **3063416**), and add each hello basket.</span></span>
6. <span data-ttu-id="3f457-111">Clique em **Ver Cesto**.</span><span class="sxs-lookup"><span data-stu-id="3f457-111">Click **View Basket**.</span></span>
   
    ![Ver cesto](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="3f457-113">Clique em **Transferir**.</span><span class="sxs-lookup"><span data-stu-id="3f457-113">Click **Download**.</span></span> <span data-ttu-id="3f457-114">Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear.</span><span class="sxs-lookup"><span data-stu-id="3f457-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="3f457-115">Olá as atualizações são transferidas toohello especificada a localização e colocada numa subpasta com o mesmo nome como atualização Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="3f457-116">pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="3f457-117">Correções de Olá devem ser acessíveis a ambos os toodetect controladores mensagens de quaisquer potenciais erros de controlador de ponto a ponto Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="3f457-118">tooinstall e certifique-se correções modo normal</span><span class="sxs-lookup"><span data-stu-id="3f457-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="3f457-119">Efetuar Olá tooinstall passos a seguir e certifique-se Olá regular modo correções.</span><span class="sxs-lookup"><span data-stu-id="3f457-119">Perform hello following steps tooinstall and verify hello regular-mode hotfixes.</span></span> <span data-ttu-id="3f457-120">Se já instalou utilizando Olá Portal do Azure, avançar diretamente demasiado[instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="3f457-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="3f457-121">tooinstall Olá de atualização de software, interface do Windows PowerShell de Olá de acesso na consola de série do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3f457-121">tooinstall hello software update, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="3f457-122">Siga instruções de detalhado Olá [consola de série utilizar o PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="3f457-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="3f457-123">Na linha de comandos Olá, prima **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3f457-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="3f457-124">Selecione **opção 1** toolog no dispositivo toohello com acesso total.</span><span class="sxs-lookup"><span data-stu-id="3f457-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="3f457-125">tooinstall Olá pacote de atualização, na linha de comandos Olá, tipo:</span><span class="sxs-lookup"><span data-stu-id="3f457-125">tooinstall hello update package, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="3f457-126">Utilize o IP, em vez de DNS no caminho de partilha no Olá acima comando.</span><span class="sxs-lookup"><span data-stu-id="3f457-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="3f457-127">parâmetro de credencial de Olá só é utilizado se aceder a uma partilha autenticada.</span><span class="sxs-lookup"><span data-stu-id="3f457-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="3f457-128">Recomendamos que utilize partilhas de tooaccess de parâmetro de credencial de Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="3f457-129">Mesmo partilhas que estão abertas demasiado "todos os utilizadores" são, normalmente, não abrir toounauthenticated utilizadores.</span><span class="sxs-lookup"><span data-stu-id="3f457-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="3f457-130">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3f457-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="3f457-131">Tipo **Y** quando o pedido tooconfirm Olá instalação de correção.</span><span class="sxs-lookup"><span data-stu-id="3f457-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="3f457-132">Monitorizar Olá update utilizando Olá `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f457-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="3f457-133">Olá saída de exemplo seguinte mostra Olá atualização em curso.</span><span class="sxs-lookup"><span data-stu-id="3f457-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="3f457-134">Olá `RunInprogress` será `True` quando Olá atualização se encontra em curso.</span><span class="sxs-lookup"><span data-stu-id="3f457-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="3f457-135">Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="3f457-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="3f457-136">Olá `RunInProgress` será `False` quando a atualização de Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="3f457-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="3f457-137">Ocasionalmente, Olá cmdlet relatórios `False` quando atualização Olá ainda está em curso.</span><span class="sxs-lookup"><span data-stu-id="3f457-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="3f457-138">tooensure Olá correção está concluída, aguarde alguns minutos, execute novamente este comando e certifique-se de que Olá `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="3f457-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="3f457-139">Se estiver, Olá correção foi concluída.</span><span class="sxs-lookup"><span data-stu-id="3f457-139">If it is, then hello hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="3f457-140">Após a conclusão da atualização de software Olá, verifique as versões de software do sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-140">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="3f457-141">Escreva Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3f457-141">Type hello following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="3f457-142">Deverá ver Olá seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="3f457-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="3f457-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="3f457-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="3f457-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="3f457-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="3f457-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="3f457-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="3f457-146">Se os números de versão de Olá não alterar depois de aplicar a atualização de Olá, indica que correção Olá tooapply falhou.</span><span class="sxs-lookup"><span data-stu-id="3f457-146">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="3f457-147">Se tal acontecer, entre em contacto com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter assistência.</span><span class="sxs-lookup"><span data-stu-id="3f457-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="3f457-148">Repita os passos 3 a 5 tooinstall Olá restantes correção de modo de regular (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="3f457-148">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="3f457-149">tooinstall e certifique-se correções do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="3f457-149">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="3f457-150">Utilize as atualizações de firmware do KB3063416 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="3f457-150">Use KB3063416 tooinstall disk firmware updates.</span></span> <span data-ttu-id="3f457-151">Estas atualizações acontece e tome em torno toocomplete 30 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="3f457-151">These are disruptive updates and take around 30-45 minutes toocomplete.</span></span> <span data-ttu-id="3f457-152">Pode escolher tooinstall estes numa janela de manutenção planeada por consola ligação de série do dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="3f457-152">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="3f457-153">atualizações de firmware do tooinstall Olá disco, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="3f457-153">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="3f457-154">Colocar o dispositivo Olá no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3f457-154">Place hello device in Maintenance mode.</span></span> <span data-ttu-id="3f457-155">Tenha em atenção que não deve utilizar a comunicação remota do Windows PowerShell ao ligar o dispositivo de tooa no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3f457-155">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="3f457-156">Terá de toorun este cmdlet no controlador de dispositivo Olá quando estiver ligado através da consola de série do dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-156">You will need toorun this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="3f457-157">Escreva:</span><span class="sxs-lookup"><span data-stu-id="3f457-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="3f457-158">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3f457-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="3f457-159">Em seguida, reinicie os dois controladores de Olá no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3f457-159">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="3f457-160">atualização de firmware de disco por Olá tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="3f457-160">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="3f457-161">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3f457-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="3f457-162">Monitor Olá instalar progresso com `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="3f457-162">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="3f457-163">Olá atualização estiver concluída quando hello `RunInProgress` alterações demasiado`False`.</span><span class="sxs-lookup"><span data-stu-id="3f457-163">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="3f457-164">Depois de concluída a instalação de Olá, será reiniciada controlador Olá em que a correção de modo de manutenção de Olá foi instalada.</span><span class="sxs-lookup"><span data-stu-id="3f457-164">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="3f457-165">Inicie sessão como opção 1 com acesso total e verificar a versão de firmware do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="3f457-165">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="3f457-166">Escreva:</span><span class="sxs-lookup"><span data-stu-id="3f457-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="3f457-167">Olá esperado versões de firmware do disco são:</span><span class="sxs-lookup"><span data-stu-id="3f457-167">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="3f457-168">Executar Olá `Get-HcsFirmwareVersion` comando em tooverify controlador segundo Olá que Olá versão do software foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="3f457-168">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="3f457-169">Modo de manutenção de Olá, em seguida, pode sair.</span><span class="sxs-lookup"><span data-stu-id="3f457-169">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="3f457-170">Escreva o seguinte comando para cada controlador de dispositivo de Olá:</span><span class="sxs-lookup"><span data-stu-id="3f457-170">Type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="3f457-171">os controladores de Olá reinicie quando sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3f457-171">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="3f457-172">Depois de firmware de disco Olá atualizações são aplicadas com êxito e o dispositivo de Olá saiu do modo de manutenção, toohello retorno portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f457-172">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="3f457-173">Tenha em atenção que portal Olá poderá não mostrar que instalou as atualizações de modo de manutenção Olá durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="3f457-173">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

