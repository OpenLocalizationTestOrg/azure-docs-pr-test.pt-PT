<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="3dba2-101">correções toodownload</span><span class="sxs-lookup"><span data-stu-id="3dba2-101">toodownload hotfixes</span></span>

<span data-ttu-id="3dba2-102">Efetue Olá seguintes passos toodownload Olá atualização de software de Olá catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="3dba2-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="3dba2-103">Inicie o Internet Explorer e navegue demasiado[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3dba2-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="3dba2-104">Se esta for a primeira vez utilizando Olá catálogo Microsoft Update neste computador, clique em **instalar** quando pedido tooinstall hello do suplemento do catálogo Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="3dba2-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="3dba2-106">Na caixa de pesquisa de Olá de Olá catálogo Microsoft Update, introduza o número de Base de dados de conhecimento (KB) Olá de correção de Olá que pretende toodownload, por exemplo **4037264**e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="3dba2-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="3dba2-107">Olá listagem de correção é apresentado, por exemplo, **cumulativa 5.0 atualização do pacote de Software para a série de 8000 do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="3dba2-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Catálogo de pesquisa](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="3dba2-109">Clique em **Transferir**.</span><span class="sxs-lookup"><span data-stu-id="3dba2-109">Click **Download**.</span></span> <span data-ttu-id="3dba2-110">Especifique ou **procurar** tooa localização local onde pretende Olá transfere tooappear.</span><span class="sxs-lookup"><span data-stu-id="3dba2-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="3dba2-111">Clique em ficheiros Olá toodownload toohello especificada a localização e a pasta.</span><span class="sxs-lookup"><span data-stu-id="3dba2-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="3dba2-112">pasta de Olá também pode ser copiado tooa partilha de rede que seja acessível a partir do dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="3dba2-113">Procure as correções adicionais listados na tabela de Olá acima (**4037266**), e transferência Olá correspondente ficheiros pastas específicas toohello conforme indicado em Olá anterior a tabela.</span><span class="sxs-lookup"><span data-stu-id="3dba2-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="3dba2-114">Correções de Olá devem ser acessíveis a ambos os toodetect controladores mensagens de quaisquer potenciais erros de controlador de ponto a ponto Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="3dba2-115">Olá correções têm de ser copiadas em 3 pastas separadas.</span><span class="sxs-lookup"><span data-stu-id="3dba2-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="3dba2-116">Por exemplo, a atualização de agente Cis/software/MDS Olá dispositivo pode ser copiada no _FirstOrderUpdate_ Olá, pasta, todas as outras atualizações não acontece foi possível copiar no Olá _SecondOrderUpdate_ pasta, e as atualizações de modo de manutenção copiadas no _ThirdOrderUpdate_ pasta.</span><span class="sxs-lookup"><span data-stu-id="3dba2-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="3dba2-117">tooinstall e certifique-se correções modo normal</span><span class="sxs-lookup"><span data-stu-id="3dba2-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="3dba2-118">Efetuar Olá tooinstall passos a seguir e certifique-se correções modo normal.</span><span class="sxs-lookup"><span data-stu-id="3dba2-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="3dba2-119">Se já instalou utilizando Olá portal do Azure, avançar diretamente demasiado[instalar e certifique-se correções do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="3dba2-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="3dba2-120">tooinstall Olá correções, interface do Windows PowerShell de Olá de acesso na consola de série do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dba2-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="3dba2-121">Siga instruções de detalhado Olá [consola de série utilizar o PuTTy tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="3dba2-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="3dba2-122">Na linha de comandos Olá, prima **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3dba2-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="3dba2-123">Selecione **opção 1** toolog no dispositivo toohello com acesso total.</span><span class="sxs-lookup"><span data-stu-id="3dba2-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="3dba2-124">Recomendamos que instale a correção de Olá no controlador passivo Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="3dba2-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="3dba2-125">correção de Olá tooinstall, na linha de comandos Olá, tipo:</span><span class="sxs-lookup"><span data-stu-id="3dba2-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="3dba2-126">Utilize o IP, em vez de DNS no caminho de partilha no Olá acima comando.</span><span class="sxs-lookup"><span data-stu-id="3dba2-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="3dba2-127">parâmetro de credencial de Olá só é utilizado se aceder a uma partilha autenticada.</span><span class="sxs-lookup"><span data-stu-id="3dba2-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="3dba2-128">Recomendamos que utilize partilhas de tooaccess de parâmetro de credencial de Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="3dba2-129">Mesmo partilhas que estão abertas demasiado "todos os utilizadores" são, normalmente, não abrir toounauthenticated utilizadores.</span><span class="sxs-lookup"><span data-stu-id="3dba2-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="3dba2-130">Forneça a palavra-passe Olá quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="3dba2-130">Supply hello password when prompted.</span></span> <span data-ttu-id="3dba2-131">Uma saída de exemplo para instalar atualizações de ordem primeiro Olá é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="3dba2-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="3dba2-132">Para a atualização de ordem primeiro Olá, terá de ficheiro específico do toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="3dba2-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="3dba2-133">Deverá instalar Olá _HcsSoftwareUpdate.exe_ primeiro.</span><span class="sxs-lookup"><span data-stu-id="3dba2-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="3dba2-134">Depois de concluir esta instalação, em seguida, instale _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="3dba2-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="3dba2-135">Tipo **Y** quando o pedido tooconfirm Olá instalação de correção.</span><span class="sxs-lookup"><span data-stu-id="3dba2-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="3dba2-136">Monitorizar Olá update utilizando Olá `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3dba2-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="3dba2-137">atualização Olá primeiro irá concluir num controlador de Olá passiva.</span><span class="sxs-lookup"><span data-stu-id="3dba2-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="3dba2-138">Depois do controlador passivo Olá é atualizada, existirá uma ativação pós-falha e atualização Olá, em seguida, irão ser aplicada em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="3dba2-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="3dba2-139">atualização de Olá está concluída quando ambos os controladores de Olá são atualizados.</span><span class="sxs-lookup"><span data-stu-id="3dba2-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="3dba2-140">Olá saída de exemplo seguinte mostra Olá atualização em curso.</span><span class="sxs-lookup"><span data-stu-id="3dba2-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="3dba2-141">Olá `RunInprogress` é `True` quando Olá atualização se encontra em curso.</span><span class="sxs-lookup"><span data-stu-id="3dba2-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="3dba2-142">Olá saída de exemplo a seguir indica que a atualização Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="3dba2-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="3dba2-143">Olá `RunInProgress` é `False` quando a atualização de Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="3dba2-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="3dba2-144">Ocasionalmente, Olá cmdlet relatórios `False` quando atualização Olá ainda está em curso.</span><span class="sxs-lookup"><span data-stu-id="3dba2-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="3dba2-145">tooensure Olá correção está concluída, aguarde alguns minutos, execute novamente este comando e certifique-se de que Olá `RunInProgress` é `False`.</span><span class="sxs-lookup"><span data-stu-id="3dba2-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="3dba2-146">Se estiver, Olá correção foi concluída.</span><span class="sxs-lookup"><span data-stu-id="3dba2-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="3dba2-147">Após a conclusão da atualização de software Olá, verifique as versões de software do sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="3dba2-148">Escreva:</span><span class="sxs-lookup"><span data-stu-id="3dba2-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="3dba2-149">Deverá ver Olá seguintes versões:</span><span class="sxs-lookup"><span data-stu-id="3dba2-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="3dba2-150">Se o número de versão Olá não alterar depois de aplicar a atualização de Olá, indica que correção Olá tooapply falhou.</span><span class="sxs-lookup"><span data-stu-id="3dba2-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="3dba2-151">Se tal acontecer, entre em contacto com o [Suporte da Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) para obter assistência.</span><span class="sxs-lookup"><span data-stu-id="3dba2-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="3dba2-152">Tem de reiniciar o controlador de Active Directory Olá através de Olá `Restart-HcsController` cmdlet antes de aplicar Olá próxima atualização.</span><span class="sxs-lookup"><span data-stu-id="3dba2-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="3dba2-153">Repita os passos 3 a 6 tooinstall Olá _CisMDSAgentupdate.exe_ agente transferido tooyour _FirstOrderUpdate_ pasta.</span><span class="sxs-lookup"><span data-stu-id="3dba2-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="3dba2-154">Repita os passos 3 a 6 tooinstall Olá segundo ordem das atualizações.</span><span class="sxs-lookup"><span data-stu-id="3dba2-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="3dba2-155">Para atualizações de ordem segundo, várias atualizações podem ser instaladas através da execução apenas Olá `Start-HcsHotfix cmdlet` e pasta toohello onde estão localizadas as atualizações de ordem segundo a apontar.</span><span class="sxs-lookup"><span data-stu-id="3dba2-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="3dba2-156">cmdlet de Olá executará todas as atualizações de Olá disponíveis na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="3dba2-157">Se já estiver instalada uma atualização, a lógica de atualização de Olá irá detetar que e não aplicar essa atualização.</span><span class="sxs-lookup"><span data-stu-id="3dba2-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="3dba2-158">Depois de instalar todas as correções Olá, utilize Olá `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3dba2-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="3dba2-159">versões de Olá devem ser:</span><span class="sxs-lookup"><span data-stu-id="3dba2-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="3dba2-160">tooinstall e certifique-se correções do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="3dba2-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="3dba2-161">Utilize as atualizações de firmware do KB4037263 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="3dba2-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="3dba2-162">Estas atualizações acontece e tomar toocomplete cerca de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="3dba2-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="3dba2-163">Pode escolher tooinstall estes numa janela de manutenção planeada por consola ligação de série do dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="3dba2-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="3dba2-164">Se o firmware do disco já se encontra atualizado, não terá de tooinstall estas atualizações.</span><span class="sxs-lookup"><span data-stu-id="3dba2-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="3dba2-165">Executar Olá `Get-HcsUpdateAvailability` cmdlet a partir da consola de série de dispositivo do Olá toocheck se as atualizações estão disponíveis e se Olá atualiza tem acontece (modo de manutenção) ou não acontece (modo normal) atualizações.</span><span class="sxs-lookup"><span data-stu-id="3dba2-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="3dba2-166">atualizações de firmware do tooinstall Olá disco, siga as instruções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="3dba2-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="3dba2-167">Colocar o dispositivo de Olá em modo de manutenção de Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="3dba2-168">Não utilize a comunicação remota do Windows PowerShell, quando ligar tooa dispositivo em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3dba2-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="3dba2-169">Em vez disso, execute este cmdlet no controlador de dispositivo Olá quando estiver ligado através da consola de série do dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="3dba2-170">controlador de Olá tooplace no modo de manutenção, escreva:</span><span class="sxs-lookup"><span data-stu-id="3dba2-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="3dba2-171">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3dba2-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="3dba2-172">Em seguida, reinicie os dois controladores de Olá no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3dba2-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="3dba2-173">atualização de firmware de disco por Olá tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="3dba2-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="3dba2-174">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3dba2-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="3dba2-175">Monitor Olá instalar progresso com `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="3dba2-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="3dba2-176">Olá atualização estiver concluída quando hello `RunInProgress` alterações demasiado`False`.</span><span class="sxs-lookup"><span data-stu-id="3dba2-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="3dba2-177">Depois de concluída a instalação de Olá, reinicia o controlador de Olá no qual Olá foi instalada a correção de modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3dba2-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="3dba2-178">Inicie sessão como opção 1 com acesso total e verificar a versão de firmware do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="3dba2-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="3dba2-179">Escreva:</span><span class="sxs-lookup"><span data-stu-id="3dba2-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="3dba2-180">Olá esperado versões de firmware do disco são:</span><span class="sxs-lookup"><span data-stu-id="3dba2-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="3dba2-181">É apresentada abaixo uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3dba2-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="3dba2-182">Executar Olá `Get-HcsFirmwareVersion` comando em tooverify controlador segundo Olá que Olá versão do software foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="3dba2-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="3dba2-183">Modo de manutenção de Olá, em seguida, pode sair.</span><span class="sxs-lookup"><span data-stu-id="3dba2-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="3dba2-184">toodo por isso, escreva Olá seguinte comando para cada controlador de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3dba2-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="3dba2-185">os controladores de Olá reinicie quando sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3dba2-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="3dba2-186">Depois de firmware de disco Olá atualizações são aplicadas com êxito e o dispositivo de Olá saiu do modo de manutenção, toohello retorno portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dba2-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="3dba2-187">Tenha em atenção que portal Olá poderá não mostrar que instalou as atualizações de modo de manutenção Olá durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="3dba2-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

