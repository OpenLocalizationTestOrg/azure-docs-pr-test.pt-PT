<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="956b2-101">correções toodownload</span><span class="sxs-lookup"><span data-stu-id="956b2-101">toodownload hotfixes</span></span>
<span data-ttu-id="956b2-102">Efetue Olá seguintes passos toodownload Olá atualização de software de Olá catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="956b2-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="956b2-103">Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="956b2-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="956b2-104">Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="956b2-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="956b2-105">![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="956b2-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="956b2-106">Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload, por exemplo **3186843**e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="956b2-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3186843**, and then click **Search**.</span></span>
   
    <span data-ttu-id="956b2-107">Olá listagem de correção é apresentado, por exemplo, **cumulativa 3.0 de atualização de pacote de Software para a série de 8000 do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="956b2-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**.</span></span>
   
    ![Catálogo de pesquisa](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="956b2-109">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="956b2-109">Click **Add**.</span></span> <span data-ttu-id="956b2-110">atualização de Olá está adicionada toohello cesto.</span><span class="sxs-lookup"><span data-stu-id="956b2-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="956b2-111">Procure as correções adicionais listados na tabela de Olá acima (**3186859**) e adicione cada cesto toohello.</span><span class="sxs-lookup"><span data-stu-id="956b2-111">Search for any additional hotfixes listed in hello table above (**3186859**), and add each toohello basket.</span></span>
6. <span data-ttu-id="956b2-112">Clique em **Ver Cesto**.</span><span class="sxs-lookup"><span data-stu-id="956b2-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="956b2-113">Clique em **Transferir**.</span><span class="sxs-lookup"><span data-stu-id="956b2-113">Click **Download**.</span></span> <span data-ttu-id="956b2-114">Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear.</span><span class="sxs-lookup"><span data-stu-id="956b2-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="956b2-115">Olá as atualizações são transferidas toohello especificada a localização e colocada numa pasta com o mesmo nome como atualização Olá de Olá secundárias.</span><span class="sxs-lookup"><span data-stu-id="956b2-115">hello updates are downloaded toohello specified location and placed in a sub-folder with hello same name as hello update.</span></span> <span data-ttu-id="956b2-116">pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="956b2-117">Correções de Olá devem ser acessíveis a ambos os toodetect controladores mensagens de quaisquer potenciais erros de controlador de ponto a ponto Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="956b2-118">tooinstall e certifique-se correções modo normal</span><span class="sxs-lookup"><span data-stu-id="956b2-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="956b2-119">Efetuar Olá tooinstall passos a seguir e certifique-se correções modo normal.</span><span class="sxs-lookup"><span data-stu-id="956b2-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="956b2-120">Se já instalou utilizando Olá Portal do Azure, avançar diretamente demasiado[instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="956b2-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="956b2-121">tooinstall Olá correções, interface do Windows PowerShell de Olá de acesso na consola de série do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="956b2-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="956b2-122">Siga instruções de detalhado Olá [consola de série utilizar o PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="956b2-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="956b2-123">Na linha de comandos Olá, prima **Enter**.</span><span class="sxs-lookup"><span data-stu-id="956b2-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="956b2-124">Selecione **opção 1** toolog no dispositivo toohello com acesso total.</span><span class="sxs-lookup"><span data-stu-id="956b2-124">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="956b2-125">Recomendamos que instale a correção de Olá no controlador passivo Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="956b2-125">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="956b2-126">correção de Olá tooinstall, na linha de comandos Olá, tipo:</span><span class="sxs-lookup"><span data-stu-id="956b2-126">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="956b2-127">Utilize o IP, em vez de DNS no caminho de partilha no Olá acima comando.</span><span class="sxs-lookup"><span data-stu-id="956b2-127">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="956b2-128">parâmetro de credencial de Olá só é utilizado se aceder a uma partilha autenticada.</span><span class="sxs-lookup"><span data-stu-id="956b2-128">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="956b2-129">Recomendamos que utilize partilhas de tooaccess de parâmetro de credencial de Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-129">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="956b2-130">Mesmo partilhas que estão abertas demasiado "todos os utilizadores" são, normalmente, não abrir toounauthenticated utilizadores.</span><span class="sxs-lookup"><span data-stu-id="956b2-130">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="956b2-131">Forneça a palavra-passe Olá quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="956b2-131">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="956b2-132">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="956b2-132">A sample output is shown below.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="956b2-133">Tipo **Y** quando o pedido tooconfirm Olá instalação de correção.</span><span class="sxs-lookup"><span data-stu-id="956b2-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="956b2-134">Monitorizar Olá update utilizando Olá `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="956b2-134">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="956b2-135">atualização Olá primeiro irá concluir num controlador de Olá passiva.</span><span class="sxs-lookup"><span data-stu-id="956b2-135">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="956b2-136">Depois do controlador passivo Olá é atualizada, existirá uma ativação pós-falha e atualização Olá, em seguida, irão ser aplicada em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="956b2-136">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="956b2-137">atualização de Olá está concluída quando ambos os controladores de Olá são atualizados.</span><span class="sxs-lookup"><span data-stu-id="956b2-137">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="956b2-138">Olá saída de exemplo seguinte mostra Olá atualização em curso.</span><span class="sxs-lookup"><span data-stu-id="956b2-138">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="956b2-139">Olá `RunInprogress` será `True` quando Olá atualização se encontra em curso.</span><span class="sxs-lookup"><span data-stu-id="956b2-139">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="956b2-140">Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="956b2-140">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="956b2-141">Olá `RunInProgress` será `False` quando a atualização de Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="956b2-141">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="956b2-142">Ocasionalmente, Olá cmdlet relatórios `False` quando atualização Olá ainda está em curso.</span><span class="sxs-lookup"><span data-stu-id="956b2-142">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="956b2-143">tooensure Olá correção está concluída, aguarde alguns minutos, execute novamente este comando e certifique-se de que Olá `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="956b2-143">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="956b2-144">Se estiver, Olá correção foi concluída.</span><span class="sxs-lookup"><span data-stu-id="956b2-144">If it is, then hello hotfix has completed.</span></span>

1. <span data-ttu-id="956b2-145">Após a conclusão da atualização de software Olá, verifique as versões de software do sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-145">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="956b2-146">Escreva:</span><span class="sxs-lookup"><span data-stu-id="956b2-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="956b2-147">Deverá ver Olá seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="956b2-147">You should see hello following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     <span data-ttu-id="956b2-148">Se os números de versão de Olá não alterar depois de aplicar a atualização de Olá, indica que correção Olá tooapply falhou.</span><span class="sxs-lookup"><span data-stu-id="956b2-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="956b2-149">Se tal acontecer, entre em contacto com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter assistência.</span><span class="sxs-lookup"><span data-stu-id="956b2-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="956b2-150">Tem de reiniciar o controlador de Active Directory Olá através de Olá `Restart-HcsController` cmdlet antes de aplicar Olá restantes atualizações.</span><span class="sxs-lookup"><span data-stu-id="956b2-150">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="956b2-151">Repita os passos 3 a 5 controladores de Olá LSI tooinstall e correção de firmware **KB3186859**.</span><span class="sxs-lookup"><span data-stu-id="956b2-151">Repeat steps 3-5 tooinstall hello LSI driver and firmware hotfix **KB3186859**.</span></span> <span data-ttu-id="956b2-152">Após a correção de Olá estiver instalada, utilize Olá `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="956b2-152">After hello hotfix is installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="956b2-153">versão de Olá LSI deve ser:</span><span class="sxs-lookup"><span data-stu-id="956b2-153">hello LSI version should be:</span></span>
   
   * `Lsisas2Version: 2.0.78.00`
3. <span data-ttu-id="956b2-154">Repita os passos 3 a 5 tooinstall Olá Storport e atualização Spaceport **KB3121261**.</span><span class="sxs-lookup"><span data-stu-id="956b2-154">Repeat steps 3-5 tooinstall hello Storport and Spaceport update **KB3121261**.</span></span>
4. <span data-ttu-id="956b2-155">Se estão a atualizar a partir da atualização 2 ou versão anterior, também terá toodownload:</span><span class="sxs-lookup"><span data-stu-id="956b2-155">If you are updating from Update 2 or earlier version, you will also need toodownload:</span></span>
   
   * <span data-ttu-id="956b2-156">correção de iSCSI utilizando KB3146621</span><span class="sxs-lookup"><span data-stu-id="956b2-156">iSCSI fix using KB3146621</span></span>
   * <span data-ttu-id="956b2-157">Correção WMI utilizando KB3103616</span><span class="sxs-lookup"><span data-stu-id="956b2-157">WMI fix using KB3103616</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="956b2-158">tooinstall e certifique-se correções do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="956b2-158">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="956b2-159">Utilize as atualizações de firmware do KB3121899 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="956b2-159">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="956b2-160">Estas atualizações acontece e tomar toocomplete cerca de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="956b2-160">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="956b2-161">Pode escolher tooinstall estes numa janela de manutenção planeada por consola ligação de série do dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="956b2-161">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="956b2-162">Tenha em atenção que se o firmware do disco já se encontra atualizado, não terá de tooinstall estas atualizações.</span><span class="sxs-lookup"><span data-stu-id="956b2-162">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="956b2-163">Executar Olá `Get-HcsUpdateAvailability` cmdlet a partir da consola de série de dispositivo do Olá toocheck se as atualizações estão disponíveis e se Olá atualiza tem acontece (modo de manutenção) ou não acontece (modo normal) atualizações.</span><span class="sxs-lookup"><span data-stu-id="956b2-163">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="956b2-164">atualizações de firmware do tooinstall Olá disco, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="956b2-164">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="956b2-165">Colocar o dispositivo de Olá em modo de manutenção de Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-165">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="956b2-166">Tenha em atenção que não deve utilizar a comunicação remota do Windows PowerShell ao ligar o dispositivo de tooa no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="956b2-166">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="956b2-167">Em vez disso, execute este cmdlet no controlador de dispositivo Olá quando estiver ligado através da consola de série do dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-167">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="956b2-168">Escreva:</span><span class="sxs-lookup"><span data-stu-id="956b2-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="956b2-169">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="956b2-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="956b2-170">Em seguida, reinicie os dois controladores de Olá no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="956b2-170">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="956b2-171">atualização de firmware de disco por Olá tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="956b2-171">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="956b2-172">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="956b2-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="956b2-173">Monitor Olá instalar progresso com `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="956b2-173">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="956b2-174">Olá atualização estiver concluída quando hello `RunInProgress` alterações demasiado`False`.</span><span class="sxs-lookup"><span data-stu-id="956b2-174">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="956b2-175">Depois de concluída a instalação de Olá, reinicia o controlador de Olá no qual Olá foi instalada a correção de modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="956b2-175">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="956b2-176">Inicie sessão como opção 1 com acesso total e verificar a versão de firmware do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="956b2-176">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="956b2-177">Escreva:</span><span class="sxs-lookup"><span data-stu-id="956b2-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="956b2-178">Olá esperado versões de firmware do disco são:</span><span class="sxs-lookup"><span data-stu-id="956b2-178">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="956b2-179">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="956b2-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="956b2-180">Executar Olá `Get-HcsFirmwareVersion` comando em tooverify controlador segundo Olá que Olá versão do software foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="956b2-180">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="956b2-181">Modo de manutenção de Olá, em seguida, pode sair.</span><span class="sxs-lookup"><span data-stu-id="956b2-181">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="956b2-182">toodo por isso, escreva Olá seguinte comando para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="956b2-182">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="956b2-183">os controladores de Olá reinicie quando sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="956b2-183">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="956b2-184">Depois de firmware de disco Olá atualizações são aplicadas com êxito e o dispositivo de Olá saiu do modo de manutenção, toohello retorno portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="956b2-184">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="956b2-185">Tenha em atenção que portal Olá poderá não mostrar que instalou as atualizações de modo de manutenção Olá durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="956b2-185">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

